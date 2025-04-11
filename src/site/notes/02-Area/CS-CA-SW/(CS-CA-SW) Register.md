---
{"dg-publish":true,"permalink":"/02-Area/CS-CA-SW/(CS-CA-SW) Register/","tags":["Area/CS-CA-SW"],"noteIcon":"","created":"2025-01-05T15:55:09.000+09:00","updated":"2025-04-07T22:55:09.011+09:00"}
---

# Register

## 레지스터

레지스터는 CPU 내부의 임시 저장소입니다.

### 반드시 알아야 할 레지스터

- 프로그램 카운터 (`PC, program counter`)
메모리에서 가져올 명령어의 주소를 저장합니다. 이를 명령어 포인터 (`IP, instruction pointer`)라고 부르기도 합니다.
- 명령어 레지스터 (`IR, instruction register`)
해석할 명령어를 저장하는 레지스터입니다. 제어장치는 여기에 담긴 명령어를 해석하고 제어신호를 내보냅니다.
- 메모리 주소 레지스터 (`MAR, memory address register`)
메모리의 주소를 저장하는 레지스터입니다. CPU가 읽어들이고자 하는 주소 값을 주소 버스로 보낼 때 메모리 주소 레지스터를 거치게 됩니다.
- 메모리 버퍼 레지스터 (`MBR, memory buffer register`)
메모리와 주고받을 값을 저장하는 레지스터입니다. 메모리에서 전달받은 값, 메모리로 전달받을 값 모두를 저장합니다.
- 범용 레지스터 (`general purpose register`)
다양한 종류의 값을 저장하는 레지스터입니다. CPU 내부에 여러 개가 존재하고, 주소와 데이터를 모두 받을 수 있습니다.
- 플래그 레지스터 (`flag register`)
각종 플래그 값들을 저장하는 레지스터입니다.

각 메모리에 어떤 데이터가 들어가는지 예시를 통해 알아봅시다.

1. 우선 메모리의 1000번지에 1001이라는 이진수가 들어있다고 가정해봅시다. CPU는 이 값이 필요합니다!
    
    ```mermaid
    classDiagram
    	class Memory
    		Memory : 1000번지 - 1001
    ```
    
2. 프로그램 카운터에는 1000이 저장됩니다. 이 주소에서 명령어를 가져옴을 의미합니다.
    
    ```mermaid
    classDiagram
    	class Programcounter
    		Programcounter : 1000
    ```
    
3. 프로그램 카운터는 이를 메모리 주소 레지스터로 보내고, ‘메모리 읽기’ 제어신호가 발생해 각각 주소 버스와 제어 버스를 통해 이동합니다.
    
    ```mermaid
    classDiagram
    	class PC["Program counter"]
    	PC : 1000
    	class MAR["memory adress register"]
    	MAR : 1000
    	class Memory
    	Memory : 1000 - 1001
    	class CU["Control Unit"]
    
    	PC --> MAR
    	CU --> Memory : control bus
    	MAR --> Memory : address bus
    ```
    
4. 메모리에 저장되어 있던 값인 1001이 데이터 버스를 통해 메모리 버퍼 레지스터로 이동합니다. 프로그램 카운터는 1 증가 합니다.
    
    ```mermaid
    classDiagram
    	class Memory
    	Memory : 1000 - 1001
    	class MBR["memory buffer register"]
    	MBR : 1001
    	Memory --> MBR : data bus
    	class PC["Program counter"]
    	PC : 1001 (1000 + 1)
    ```
    
5. 메모리 버퍼 레지스터의 값이 명령어 레지스터로 이동합니다.
    
    ```mermaid
    classDiagram
    	class MBR["memory buffer register"]
    	MBR : 1001
    	MBR --> CR
      class CR["command register"]
    	CR : 1001
    ```
    
6. 제어장치는 명령어를 해석하고 제어 신호을 발생시킵니다.

### 레지스터의 주소 지정 방식(1) : 스택 주소 지정 방식

스택 주소 지정 방식은 스택 포인터 (`stack pointer`)과 스택을 이용한 주소 지정 방식입니다.

스택은 “아래에서부터 천천히 쌓아올리고, 위에서부터 접근이 가능한 데이터 구조입니다. 스택 포인터는 이러한 스택의 꼭대기를 가리키는 포인터입니다. 
C++에서 stack.top()을 가리키고 있는 주소값이라고 생각할 수 있겠네요.

메모리 상에서 스택을 사용하기로 지정된 공간을 스택 영역(`stack domain`) 이라고 합니다.

### 레지스터의 주소 지정 방식(2) : 변위 주소 지정 방식

변위 주소 지정 방식(`displacement adressing mode`)은 특정 레지스터의 값 + 오퍼랜드 필드의 값 = 유효 주소로 사용하는 방식입니다.

이 방식을 쓰는 명령어에는 연산 코드 필드, 레지스터 필드, 오퍼랜드 필드가 있습니다.

무슨 레지스터의 값을 더하냐에 따라 상대 주소 지정 방식, 베이스 레지스터 주소 지정 방식 등으로 나뉩니다.

- 상대 주소 지정 방식 (`relative adressing mode`)
오퍼랜드 + 프로그램 카운터의 값입니다. 프로그램 카운터에는 명령어의 주소가 저장되어 있으므로, 오퍼랜드의 값에 따라 앞뒤로 왔다갔다 읽습니다.
- 베이스 레지스터 주소 지정 방식 (`base-register addressing mode`) 
오퍼랜드 + 베이스 레지스터의 값입니다. 베이스 레지스터는 “기준이 되는 주소값” 을 담고 있는 레지스터입니다.