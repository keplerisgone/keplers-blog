---
{"dg-publish":true,"permalink":"/02-Area/Python/(Discord.py) 연말 알림 봇 만들기/","tags":["Area/Python"],"noteIcon":"","created":"2025-01-05T15:55:25.000+09:00","updated":"2025-04-01T22:54:46.115+09:00"}
---

# 연말 알림 봇 만들기

### Discord 봇 알림 기능 구현

이 코드는 **Discord 봇**에 알림 기능을 추가하는 방법을 보여줍니다. 사용자가 특정 날짜와 시간에 맞춰 메시지를 예약하고, 해당 시간에 자동으로 메시지를 전송하는 기능을 구현합니다.

### 주요 구성 요소:

- `commands.Cog`: 봇의 커맨드를 정의하고 그룹화하는 데 사용됩니다.
- `apscheduler.schedulers.asyncio.AsyncIOScheduler`: 예약된 작업을 비동기적으로 처리하는 스케줄러.
- `apscheduler.triggers.date.DateTrigger`: 특정 날짜와 시간에 실행될 작업을 예약하는 트리거.

### 코드 설명:

```python
from discord.ext import commands
from apscheduler.schedulers.asyncio import AsyncIOScheduler
from apscheduler.triggers.date import DateTrigger
from datetime import datetime

class Alert(commands.Cog):
    def __init__(self, bot):
        self.bot = bot
        self.scheduler = AsyncIOScheduler()
        self.scheduler.start()

    @commands.command(name="schedule")
    async def schedule_message(self, ctx, date: str, time: str, *, message: str):
        """
        특정 날짜와 시간에 메시지 발송
        date: "YYYY-MM-DD" 형식으로 입력
        time: "HH:MM" 형식으로 입력
        message: 발송할 메시지
        """
        try:
            # 입력된 날짜와 시간 파싱
            target_datetime = datetime.strptime(f"{date} {time}", "%Y-%m-%d %H:%M")
            if target_datetime < datetime.now():
                await ctx.send("이미 지난 시간을 입력하셨습니다.")
                return

            # 작업 예약
            self.scheduler.add_job(
                self.send_message,
                DateTrigger(run_date=target_datetime),
                args=[ctx.channel.id, message]
            )
            await ctx.send(f"{target_datetime}에 메시지가 발송됩니다.")
        except ValueError:
            await ctx.send("날짜와 시간 형식이 잘못되었습니다. YYYY-MM-DD HH:MM 형식으로 입력해주세요.")

    async def send_message(self, channel_id, message):
        channel = self.bot.get_channel(channel_id)
        if channel:
            await channel.send(message)

async def setup(bot):
    await bot.add_cog(Alert(bot))

```

### 설명:

1. **Alert 클래스**: `commands.Cog`를 상속받아 봇에 알림 관련 명령어를 추가합니다.
2. **`__init__` 메소드**: 봇을 초기화하고 스케줄러를 시작합니다.
3. **`schedule_message` 명령어**: 사용자가 날짜와 시간, 메시지를 입력하여 예약할 수 있습니다.
    - 사용자가 입력한 `date`와 `time`을 파싱하여 예약된 시간이 현재 시간보다 미래일 때만 알림을 설정합니다.
    - 날짜와 시간 형식이 잘못되었을 경우 오류 메시지를 반환합니다.
4. **`send_message` 메소드**: 예약된 시간에 해당 채널에 메시지를 발송합니다.
5. **`setup` 함수**: 봇에 `Alert` cog를 추가합니다.

### 사용 방법:

- 봇에서 `!schedule 2025-01-01 10:00 메시지 내용` 형식으로 입력하면, 2025년 1월 1일 10시에 해당 메시지가 자동으로 발송됩니다.