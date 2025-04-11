---
{"dg-publish":true,"permalink":"/02-Area/Development/(Development) TCP 3 & 4 way handshake/","tags":["Area/Development"],"noteIcon":"","created":"2025-01-05T15:54:46.000+09:00","updated":"2025-04-07T23:13:20.165+09:00"}
---


# Summary

TCP(**Transmission Control Protocol**)이라는 핵심 프로토콜과 이 연결 설정 과정인 3-way 핸드셰이크를 알아보자.
# Contents
## TCP

TCP는 데이터 송신에 오류나 차질이 없도록 고안된 데이터 전송 프로토콜이다. TCP는 데이터를 세그먼트라는 단위로 나누어 전송하는데, 이는 *세그먼트 헤더*와 *데이터*의 두 섹션으로 구성된다. 이는 각종 정보에 대한 플래그를 포함한다.
## 3-way handshake

![https://i.imgur.com/eM5yexz.png](https://i.imgur.com/eM5yexz.png)

**3-way handshake**

는 TCP 프로토콜에서 데이터를 전송하기 전 연결을 설정하는 과정으로, 총 3번의 연결이 일어나기 때문에 3-way라고 불린다.
TCP는 송신자와 수신자를 확인하기 위해 다음과 같은 과정을 거친다.

1. 클라이언트가 서버에게 **SYN 패킷을 보냄** (sequence : x) - *SYN은 최초의 패킷에만 붙는 플래그*
2. 서버가 SYN(x)를 받고, 클라이언트로 받았다는 신호인 **ACK와 SYN 패킷을 보냄** (sequence : y, ACK : x + 1) - *ACK는 ’잘 받았다’라는 플래그*
3. 클라이언트는 서버의 응답 (sequence : y, ACK : x + 1)를 받고, ACK : y + 1을 서버로 보냄

이렇게 3번의 통신이 완료되면 연결이 성립된다.
## 4-way handshake

![https://i.imgur.com/Xoo4Abc.png](https://i.imgur.com/Xoo4Abc.png)

3-way와는 다르게 **4-way handshake**는 모든 통신이 끝난 후 연결을 해제하는 과정이다.

1. 클라이언트는 서버에게 연결을 종료한다는 FIN 플래그를 보낸다.
2. 서버는 FIN을 받고, 확인했다는 ACK 플래그를 클라이언트에게 보낸다. - *이 때 CLOSE_WAIT상태가 된다*
3. 데이터를 모두 보낸 후에는 연결이 종료되었다는 FIN 플래그를 클라이언트에게 보낸다.
4. 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보낸다. - *이 때 클라이언트는 TIME_WAIT으로 기다린다*
5. 서버는 ACK를 받은 이후 소켓을 닫는다.
6. TIME_WAIT 시간이 끝나면 클라이언트도 닫는다.
# Reference
- https://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1_%EC%A0%9C%EC%96%B4_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C
- https://www.geeksforgeeks.org/tcp-connection-termination/