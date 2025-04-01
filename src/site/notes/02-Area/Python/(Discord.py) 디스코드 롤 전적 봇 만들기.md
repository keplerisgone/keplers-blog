---
{"dg-publish":true,"permalink":"/02-Area/Python/(Discord.py) 디스코드 롤 전적 봇 만들기/","tags":["Area/Python"],"noteIcon":"","created":"2025-01-05T15:55:25.000+09:00","updated":"2025-04-01T22:53:50.586+09:00"}
---

# 디스코드 롤 전적 봇 만들기

# Cog로 명령어 분리하기

유의해야 할 점)

1. @bot.command 데코레이션이 @commands.command로 바뀜.
2. @bot.event 도 @command.Cog.listener 로 바뀜. 이 안에 이벤트를 정의해야함.
3. [discord.py](http://discord.py) 2.x 이후로는 Cog 세팅이 전부 비동기를 사용하도록 변경. 예전 예제와 헷갈리지 않도록 주의.

# 라이엇 API 뽑아오기

```jsx
load_dotenv()
API_KEY = os.getenv("RIOT_TOKEN")  # Riot API 키
REGION = "kr"  # 한국 서버
BASE_URL = f"https://{REGION}.api.riotgames.com"
MATCH_URL = f"https://asia.api.riotgames.com"
```

1. 게임 아이디 + 태그로 각종 id 뽑아오기.
    
    ```jsx
    url = f"{MATCH_URL}/riot/account/v1/accounts/by-riot-id/{encodedName}/{encodedTag}"
    ```
    
    response에서 `puuid` 뽑아오기. 이걸로 매치 데이터를 뽑아야 함.
    
2. 플레이어 데이터를 뽑아 플레이어 아이콘, 현재 시즌 티어 + 포인트, 승패 기록과 승률 표시.
3. 최근 10개 매치 데이터를 불러와 모스트 챔, 각 매치의 승패와 KDA 표시.
    1. 챔피언은 id로만 불러옴. 실제 이름을 불러오려면 data dragon 이용.

## 유의해야 할 점

1. **@bot.command** → **@commands.command**:
    - Discord.py의 Cog 구조에서는 @bot.command를 사용하지 않음.
    - 대신 Cog 클래스 내에서 @commands.command를 사용함.
2. **@bot.event** → **@commands.Cog.listener**:
    - Cog에서는 이벤트 핸들러를 정의할 때 @commands.Cog.listener를 사용해야 함.
3. Discord.py 2.x 이후로 Cog의 세팅이 비동기로 변경됨:
    - Cog를 로드하거나 초기화할 때 반드시 비동기 함수(async def)를 사용해야 함.
    - 예전 버전의 예제와 헷갈리지 않도록 주의.

---

## 라이엇 API 연동

더 자세한 연동 내용은 [공식 developer portal](https://developer.riotgames.com/apis) 참고.

### 기본 설정

```python
load_dotenv()
API_KEY = os.getenv("RIOT_TOKEN")  # Riot API 키
REGION = "kr"  # 한국 서버
BASE_URL = f"https://{REGION}.api.riotgames.com"
MATCH_URL = f"https://asia.api.riotgames.com"
```

### 주요 기능

1. **게임 아이디 + 태그로 각종 ID 뽑아오기**
    - URL: `/riot/account/v1/accounts/by-riot-id/{encodedName}/{encodedTag}`
    - Riot ID(GameName#TagLine)를 사용해 API 호출.
    - `response`에서 `puuid`를 추출함. `puuid`는 매치 데이터를 조회할 때 사용됨.
2. **플레이어 데이터 가져오기**
    - 플레이어 아이콘, 현재 시즌 티어와 포인트, 승패 기록 및 승률을 표시.
3. **최근 10개 매치 데이터 가져오기**
    - API를 호출하여 최근 10개의 매치 데이터를 불러옴.
    - 모스트 챔피언 계산: 매치 데이터를 순회하며 가장 많이 플레이한 챔피언 ID를 계산함.
    - 각 매치의 승패와 KDA를 표시.
    - 챔피언 ID를 실제 이름으로 변환하려면 Riot Data Dragon을 이용해야 함.

---

## 작업한 코드 내용 요약

### 1. **로그 기록**

- `on_message` 이벤트를 사용하여 채팅 메시지를 기록함.
- 로그 파일은 `Chats` 폴더에 저장되도록 수정됨.
- `save_messages` 명령어를 통해 최근 N개의 메시지를 저장 가능.
    - 메시지는 파일에 최신 순서대로 저장됨.
    - 저장된 파일은 `Chats` 폴더에 위치함.

### 2. **플레이어 정보**

- Riot ID(GameName#TagLine)를 받아 플레이어의 `puuid`를 추출함.
- `puuid`를 이용해 다음 데이터를 가져옴:
    - **현재 시즌 티어와 포인트**
    - **승/패 기록과 승률**
- Discord Embed를 사용하여 위 정보를 보기 좋게 출력.

### 3. **최근 매치 기록**

- `puuid`를 통해 최근 10개의 매치 데이터를 조회.
- 모스트 챔피언을 ID 기반으로 계산함.
- 각 매치의 승패를 이모지(O/X)로 표시하고 평균 KDA를 계산하여 출력.

---

## 알게 된 내용

1. **Discord.py 2.x의 Cog 세팅 변화**:
    - Cog는 비동기적으로 초기화해야 하며, @commands.Cog.listener와 @commands.command를 사용해야 함.
2. **명령어에서 띄어쓰기 처리**:
    - Discord 명령어에서 띄어쓰기가 포함된 인자를 받으려면 ``를 사용해야 함.
    - 예: `async def fetch_player_info(self, ctx, *, playerName: str)`
3. **Riot Data Dragon의 사용 여부**:
    - 챔피언 이름 변환을 위해 Data Dragon을 사용할 수 있음.
    - Data Dragon 사용이 비효율적일 경우 챔피언 ID를 그대로 출력하는 방식도 가능.
4. **디버깅 팁**:
    - Riot API 호출 결과를 디버깅하기 위해 `response.status_code`와 `response.text`를 출력해야 함.
    - `summoner` 객체의 유효성을 확인하고 기본값을 설정해야 오류를 방지할 수 있음.

---

## 전체 코드

```python
import discord
from discord.ext import commands
import json
from urllib import parse

from dotenv import load_dotenv
import os
import requests

load_dotenv()
API_KEY = os.getenv("RIOT_TOKEN")  # Riot API 키
REGION = "kr"  # 한국 서버
BASE_URL = f"https://{REGION}.api.riotgames.com"
MATCH_URL = f"https://asia.api.riotgames.com"

REQUEST_HEADERS = {
	"User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36",
	"Accept-Language": "en-US,en;q=0.9,ko;q=0.8",
	"Accept-Charset": "application/x-www-form-urlencoded; charset=UTF-8",
	"Origin": "https://developer.riotgames.com",
	"X-Riot-Token": API_KEY
}

# # 챔피언 데이터 로드 함수
# def load_champion_data():
# 	url = "http://ddragon.leagueoflegends.com/cdn/12.23.1/data/en_US/champion.json"  # 최신 패치 버전을 사용할 것
# 	response = requests.get(url)
# 	if response.status_code == 200:
# 		data = response.json()
# 		id_to_name = {int(champ["key"]): champ["id"] for champ in data["data"].values()}
# 		return id_to_name
# 	return {}

# # 챔피언 ID -> 이름 매핑 데이터 로드
# CHAMPION_MAP = load_champion_data()

class Lol(commands.Cog):
	def __init__(self, bot):
		self.bot = bot
  
	@commands.command(name="player")
	async def fetch_player_info(self, ctx, *, playerName: str):
		# 소환사 정보 가져오기
		playerID = get_playerID_by_name(playerName)
		if not playerID:
			await ctx.send(f"소환사를 찾을 수 없습니다: {playerName}")
			return

		puuid = playerID['puuid']
		summoner = get_summoner_by_puuid(puuid)
		if not summoner:
			await ctx.send("소환사를 가져오는 데 실패했습니다.")
			return

		# 소환사 ID를 사용하여 티어와 승/패 데이터 가져오기
		summoner_id = summoner['id']
		playerInfo = get_playerInfo_by_summonerid(summoner_id)
		if not playerInfo:
			await ctx.send("플레이어 정보를 가져올 수 없습니다.")
			return

		# 랭크 데이터 처리 (솔로랭크 정보 찾기)
		rank_data = next((entry for entry in playerInfo if entry['queueType'] == 'RANKED_SOLO_5x5'), None)
		if rank_data:
			tier = rank_data.get('tier', 'Unranked')
			rank = rank_data.get('rank', '')
			lp = rank_data.get('leaguePoints', 0)
			wins = rank_data.get('wins', 0)
			losses = rank_data.get('losses', 0)
			total_games = wins + losses
			win_rate = (wins / total_games) * 100 if total_games > 0 else 0
		else:
			tier = "Unranked"
			rank = ""
			lp = 0
			wins = 0
			losses = 0
			win_rate = 0

		profile_icon_id = summoner.get("profileIconId")
		profile_icon_url = f"http://ddragon.leagueoflegends.com/cdn/12.23.1/img/profileicon/{profile_icon_id}.png"

		# 최근 게임 정보 가져오기
		match_ids = get_recent_matches(puuid)
		if not match_ids:
			await ctx.send("최근 게임 정보를 가져올 수 없습니다.")
			return

		# 최근 10경기 승/패 및 KDA 계산
		total_kills, total_deaths, total_assists = 0, 0, 0
		recent_results = []

		for match_id in match_ids:
			match = get_match_details(match_id)
			if not match:
				continue
			participants = match.get("info", {}).get("participants", [])
			for participant in participants:
				if participant.get("puuid") == puuid:
					kills = participant.get("kills", 0)
					deaths = participant.get("deaths", 0)
					assists = participant.get("assists", 0)
					win = participant.get("win", False)
					champion_id = participant.get("championId")

					# 승/패 이모지 저장
					recent_results.append(":o: " if win else ":x: ")

					# KDA 계산
					total_kills += kills
					total_deaths += deaths
					total_assists += assists

					# 모스트 챔피언 계산
					# champion_usage[champion_id] = champion_usage.get(champion_id, 0) + 1

		# 평균 KDA 계산
		avg_kda = (
			f"{total_kills / len(match_ids):.1f}/"
			f"{total_deaths / len(match_ids):.1f}/"
			f"{total_assists / len(match_ids):.1f}"
		)

		# # 모스트 챔피언 계산
		# most_played_champion_id = max(champion_usage, key=champion_usage.get)
		# most_played_champion_name = CHAMPION_MAP.get(most_played_champion_id, "Unknown Champion")
		# most_played_count = champion_usage[most_played_champion_id]

		# Discord Embed 생성
		embed = discord.Embed(title=f"{playerID['gameName']} 정보", color=discord.Color.blue())
		print("embed 생성 완료")
		embed.set_thumbnail(url=profile_icon_url)
		embed.add_field(name="현재 티어", value=f"{tier} {rank} ({lp} LP)", inline=False)
		embed.add_field(name="승률", value=f"{win_rate:.2f}% ({wins}승 / {losses}패)", inline=False)
		embed.add_field(name="최근 10경기", value=" ".join(recent_results), inline=False)
		embed.add_field(name="평균 KDA", value=avg_kda, inline=False)
		# embed.add_field(name="모스트 챔피언", value=f"{most_played_champion_name} ({most_played_count}회)", inline=False)

		await ctx.send(embed=embed)
  
async def setup(bot):
	await bot.add_cog(Lol(bot))
 
# 소환사 정보 가져오기
def get_playerID_by_name(USERID):
	gameName, tagLine = slice_by_hash(USERID)
	print(f"gameName : {gameName}, tag : {tagLine}")
	encodedName = parse.quote(gameName)
	encodedTag = parse.quote(tagLine)
	url = f"{MATCH_URL}/riot/account/v1/accounts/by-riot-id/{encodedName}/{encodedTag}"
	response = requests.get(url, headers=REQUEST_HEADERS)
	print(f"Status Code: {response.status_code}, Response: {response.text}")  # 디버깅용 로그
	return response.json() if response.status_code == 200 else None

def get_summoner_by_puuid(puuid):
	url = f"{BASE_URL}/lol/summoner/v4/summoners/by-puuid/{puuid}"
	response = requests.get(url, headers=REQUEST_HEADERS)
	return response.json() if response.status_code == 200 else None

def get_playerInfo_by_summonerid(id):
	url = f"{BASE_URL}/lol/league/v4/entries/by-summoner/{id}"
	response = requests.get(url, headers=REQUEST_HEADERS)
	return response.json() if response.status_code == 200 else None

# 최근 게임 ID 가져오기
def get_recent_matches(puuid, count=20):
	url = f"{MATCH_URL}/lol/match/v5/matches/by-puuid/{puuid}/ids?start=0&count={count}"
	response = requests.get(url, headers=REQUEST_HEADERS)
	return response.json() if response.status_code == 200 else None

# 게임 상세 정보 가져오기
def get_match_details(match_id):
	url = f"{MATCH_URL}/lol/match/v5/matches/{match_id}"
	response = requests.get(url, headers=REQUEST_HEADERS)
	return response.json() if response.status_code == 200 else None
  
def slice_by_hash(input_string):
	parts = input_string.split('#', 1)  # '#'을 기준으로 최대 한 번만 나눔
	if len(parts) == 2:
		return parts[0], parts[1]  # 두 개로 나누어진 결과 반환
	return parts[0], None  # '#'이 없으면 두 번째 값은 None

```

## 추가 작업 가능성

1. **챔피언 이름 캐싱**:
    - Riot Data Dragon API를 호출하지 않고 로컬에서 챔피언 이름을 매핑하는 방식.
    - JSON 파일로 챔피언 데이터를 저장하고 이를 참조.
2. **로그 파일 관리**:
    - 오래된 로그 파일을 자동으로 삭제하거나 아카이브하는 기능 추가 가능.
3. **임베드 메시지 확장**:
    - Discord Embed에 추가적인 통계 정보(예: 평균 딜량, CS)를 포함하는 방식.
