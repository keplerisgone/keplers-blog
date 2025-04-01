---
{"dg-publish":true,"permalink":"/02-Area/RaspberryPi/(RaspberryPi) 라즈베리파이 개발환경 설정하기/","tags":["Area/RaspberryPi"],"noteIcon":"","created":"2025-01-05T21:00:40.000+09:00","updated":"2025-04-01T22:52:12.336+09:00"}
---

# 라즈베리파이 개발환경 설정하기

# 라즈베리 개발환경 설정

목적은 간단하다. 별다른 GUI 환경 없이 내부에서 GPIO 핀 상태를 보거나 프로그래밍만 할 수 있으면 된다. 설령 GUI 환경이 이것저것 관측하기는 편하더라도, CLI 환경에서 이를 보는 방법은 구글링만 하면 전부 나오니… 우선 [[라즈베리파이를 세팅해보자 (mac)\|라즈베리파이를 세팅해보자 (mac)]], [[02-Area/RaspberryPi/(RaspberryPi) 라즈베리파이에 Linux 설치하기\|(RaspberryPi) 라즈베리파이에 Linux 설치하기]] 문서를 통해 현재 라즈베리파이 4 에는 우분투 서버버전이 깔려있고, ssh를 통해 접속할 수 있게 세팅된 것을 알 수 있다.

![https://i.imgur.com/sYeOGNr.png|520](https://i.imgur.com/sYeOGNr.png)

*(잘 된당)*

VSCode 에서도 Remote-SSH 익스텐션을 설치, ssh를 이용해 터미널에서 하듯이 라즈베리파이에 접속해 주면 세팅이 끝난다.

![https://i.imgur.com/OiWUC1q.png|620](https://i.imgur.com/OiWUC1q.png)

![https://i.imgur.com/mAdbY9v.png|600](https://i.imgur.com/mAdbY9v.png)

사실 여기서 더 나아가 외부에 있을 때도 원격으로 라즈베리파이에 접속하고 싶지만.. 이를 위해서는 포트포워딩과 DMZ 세팅이 필요하다. 우선 포트포워딩.

## 포트포워딩

포트포워딩은 간단하게 말하면 *다른 사람들이 이 네트워크로 들어오려고 하는데, 좀 허락해주세요*~이다. 네트워크에 연결된 기기는 기기마다 고유의 ip를 할당받는다. 외부에서 이런 기기에 접속하기 위해서는 포트를 통해야 하는데, 이는 포트포워딩으로 열려있는 포트로만 접속할 수 있다.

우선 라즈베리파이의 고유 ip를 확인하자. 여기서 확인한 ip는 **내부 ip**이다.

```
$ ifconfig (sudo apt install net-tools 필요)
or
$ ip a
```

1. 내부 ip를 알아낸 뒤 공유기 설정에 들어가 포트를 연다.
2. **외부 ip**를 이용해 ssh로 접속. 명령어는 다음과 같다.

```
$ ssh [이름]@[외부 ip] -p [포트 번호]
```

이제 라즈베리파이가 집에 연결만 되어있어도 어디서든 접속할 수 있다! 그런데 권한이나 그런거는 어떻게 관리하지… 외부에서 무턱대고 접속하면 기록이 여기저기 남아버려 곤란하다.