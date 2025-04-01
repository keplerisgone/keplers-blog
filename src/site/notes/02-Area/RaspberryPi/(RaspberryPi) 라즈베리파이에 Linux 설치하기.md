---
{"dg-publish":true,"permalink":"/02-Area/RaspberryPi/(RaspberryPi) 라즈베리파이에 Linux 설치하기/","tags":["Area/RaspberryPi"],"noteIcon":"","created":"2025-01-05T15:55:32.000+09:00","updated":"2025-04-01T22:52:19.461+09:00"}
---

# 라즈베리파이에 Linux 설치하기

# Summary

라즈베리파이에 리눅스를 설치해보자.
# Contents

~~1. 라즈베리파이 Imager에서 일반적인 라즈베리파이 OS가 아닌 우분투를 다운받는다.
1. ~~32비트로 다운받을 경우에는 아래와 같이 따로 설정이 가능하다.~~
2. ~~부팅이 완료된 것 같으면 ssh 명령어를 이용해 터미널에서 라즈베리파이로 접속.~~
1. `~~sudo apt update`, `sudo apt upgrade`를 이용, 패키지를 인스톨한다.~~
2. `~~sudo apt install net-tools zip unzip tar curl wget git p7zip` 명령어로 네트워크 관리 패키지, 압축 관련 패키지를 다운받는다.~~
3. ~~우분투에서 `sudo apt-get install tigervnc-standalone-server tigervnc-xorg-extension` 명령어를 이용해 vnc 서버를 설치~~

다 때려치우고 서버용 리눅스를 다운받았다. 64bit버전으로 다운받을걸 그랬나

![https://i.imgur.com/hBD8lUI.png](https://i.imgur.com/hBD8lUI.png)

# Reference