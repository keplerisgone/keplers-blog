---
{"dg-publish":true,"permalink":"/02-area/raspberry-pi/raspberry-pi/","tags":["Area/RaspberryPi"],"noteIcon":"","created":"2025-01-05T15:55:32.000+09:00","updated":"2025-04-01T22:51:53.586+09:00"}
---

# 라즈베리파이를 로컬로 접속하고 싶다

# 라즈베리파이 로컬로 접속하기

결론은 망했어요.

나중에 나가서 라즈베리파이를 쓸 일이 생길지도 모르니 네트워크없이 유선 연결 하는 방법을 기록해놓자.

## 기본적인 방법

1. 라즈베리파이 Imager 설정

[라즈베리파이 OS Imger](https://www.raspberrypi.com/software/)를 이용해 SD 카드에 OS를 올린다. ssh 설정과 사용자 및 암호 설정을 한다.

1. config, cmdline 수정

SD 카드를 PC에 꽂고 에디터를 이용해 두 파일을 수정해야 한다.

`config.txt` 파일의 맨 끝에는 다음과 같은 내용을 추가한다.

```
dtoverlay=dwc2
```

`cmdline.txt`의 `rootwait` 바로 뒤에 다음과 같은 내용을 추가한다.

```
modules-load=dwc2,g_ether
```

1. PC와 연결

PC와 라즈베리파이를 USB-C로 연결한 뒤 `ssh`를 이용해 접속한다. 윈도우는 putty를 이용해야 한다고 한다. mac/linux는 다음과 같이 접속 가능하다.

```
# 접속 확인
ping <hostname>.local

# 접속
ssh <hostname>.local
```

접속이 잘 되면 성공이다. 그런데…

왜 난 안 될까?

## Troubleshooting

### USB 부팅

SD 카드를 꽂아 부팅을 시도했다. ACT LED인 초록색 LED는 잘 깜빡이지만 nmap이나 ping 명령어로 라즈베리파이의 존재를 확인할 수 없었다.
구글을 뒤져 보니 ACT LED의 점등이 부팅 오류를 알려준다는데… 다시 LED를 보니 꺼져 있었다. LED가 아예 꺼진 것은 SD 카드를 잘 읽지 못하고 있다는 뜻이라고 한다.

내 맥북이 SD 카드를 잘 읽고 쓰는 것으로 보아 SD 카드에는 문제가 없다. *라즈베리파이의 SD 카드 리더에 문제가 있을 수 있으니* USB 부팅을 시도해보고자 한다.

USB로 부팅을 하기 위해서는 USB에 OS를 담고(나는 SD 카드 리더기가 있어서 생략) config.txt에 다음을 추가해 USB 부팅으로 만들어야 한다고 한다.

```
echo program_usb_boot_mode=1 | sudo tee -a /boot/config.txt
```

전원을 켜고 살펴보니 *이번에는 ATC LED가 무한으로 켜지고 있었다!* 아마 USB 부팅은 안 되고 있고 SD 카드를 찾는 것 같은데, 이제 어쩌지??

### LAN 연결

확실하게 유선 연결을 이용해 인터넷에 접속하는 방법을 써보자. 문제 해결도 쉬워질 것이다. 잠자는 윈도우를 깨워 랜선을 연결해보자. 현재 WIFI 세팅에 들어가 인터넷 공유 설정을 한 후, 대상을 이더넷으로 설정한다.

그러면 이더넷이 인터넷에 연결되면서 IP 주소를 받아야하는데. 라즈베리가 인터넷에 연결되지 않는다!

### 모니터 연결

모든 문제는 모니터가 없어서 그렇다. 정확히는 micro HDMI가 없어 모니터에 연결하지 못했다. 모니터만 연결하면 문제가 뭔지 바로 알 수 있거나, 직접 속 시원하게 WIFI 접속을 할 수 있었을 것이다. 다급하게 3000원짜리 케이블을 구매했다.