---
{"dg-publish":true,"permalink":"/02-Area/Algorithm/(Algorithm) 선형 데이터 구조/","tags":["Area/Algorithm"],"noteIcon":"","created":"2025-01-05T15:54:58.000+09:00","updated":"2025-04-07T22:51:58.530+09:00"}
---


## 컴퓨터 메모리

- 컴퓨터 메모리는 컴퓨터가 데이터를 저장하는 저장 공간
- 데이터 구조는 컴퓨터가 자원을 효과적으로 관리하기 위해 만들어 진 것
- 컴퓨터 메모리에는 다양한 종류가 있는데, 이를 적층 구조로 표현하면 다음과 같다
![[Screenshot 2024-01-02 at 6.58.50 PM.png\|Screenshot 2024-01-02 at 6.58.50 PM.png]]
- 이는 메모리의 크기 순으로 위로 쌓아올린 것이다
- **하드 디스크**: 컴퓨터에 존재하는 디스크 저장장치, SSD나 HDD를 말한다. RAM에 저장되는 데이터를 저장한다.
- **메인 메모리** : RAM이다. RAM에 저장된 데이터는 CPU 칩 내부의 캐시(Cache)라는 데이터 유형에 저장된 후, CPU의 레지스터에 저장된다.
- **캐시 메모리** : CPU가 가장 많이 사용하는 데이터를 저장, 연산 속도를 빠르게 한다. L1, L2 종류가 존재
- **레지스터** : CPU가 직접 사용하는 메모리, 연산 처리 속도가 굉장히 빠르며 CPU에 장착될 정도로 크기가 작다
- 적층 구조는 연산 처리 속도로도 정렬이 된다
- **메모리 주소** : 실제 데이터가 저장되는 주소
- **가상 메모리** : 데이터가 저장되어 있지는 않지만 물리적인 주소에 매핑되어 있는 것, 메모리를 관리하는 데 필요
    - **페이징** : 가상 메모리를 일정한 크기의 페이지로 나눠서 사용
    - **페이지 테이블** : 가상의 주소를 실제 물리적인 주소로 변환하는 것
- 페이지가 없다면 프로그램이 실행되지 않는다 (안전!)

## 선형 데이터 구조란?

- 데이터가 서로 인접해 연결되어 있는 데이터 구조
- 다른 복잡한 데이터 구조의 기반이 됨

### 배열

- 자료형이 같은 요소(`element`)를 선형으로 정리
- 각 요소는 인덱스(`index`)가 매겨져 저장됨
- 데이터를 추가하거나 삭제할 때 다른 데이터를 모두 앞으로 밀어야 하므로 비효율적이다
- 대개 프로그래머가 알아서 크기를 미리 지정해줘야 한다
- 다차원 배열(`multidimensional array`)은 행과 열로 이루어져 있으며, 그리드 형태로 데이터를 저장할 때 유리

### 리스트

![[Screenshot 2024-01-03 at 12.15.32 AM.png\|Screenshot 2024-01-03 at 12.15.32 AM.png]]

- 배열은 _****************메모리가 할당된 대로 순차적으로 데이터가 저장****************_되지만, 리스트는 여기저기 흩어져서 저장이 가능
    - 포인터를 이용해서 저장하기 때문
- 노드(`node`) - 데이터 요소 + 포인터
- 헤드(`head`) - 진입점을 가리키는 포인터
- **단방향 연결 리스트**(`singly linked list`) - 포인터가 한 방향만을 가리키는 리스트
- **양방향 연결 리스트**(`doubly linked list`) - 포인터가 양방향을 가리킴, 노드에는 포인터가 두 개 포함
- **순환 연결 리스트**(`circluar linked list`) - 마지막 포인터가 null이 아닌 head를 가리킴
- <> 그림

💡 파이썬에서는 배열 = 리스트로 취급, 모든 것이 리스트이다

### 스택

![[Screenshot 2024-01-03 at 12.11.35 AM.png\|Screenshot 2024-01-03 at 12.11.35 AM.png]]

- 후입선출(`LIFO`)의 데이터 구조
- 항아리를 생각하면 쉽다
- 푸시(`push`) - 스택에 데이터를 넣는 과정
- 팝(`pop`) - 스택에서 데이터를 뺴내는 과정
- 정적 스택(`static stack`)과 동적 스택(`dynamic stack`)으로 나뉨, 각각 배열, 리스트로 구현 가능

```python
# stackclass stack:
    stck = []
    def __init_(self):
        self.stck = []
    def pop(self):
        a = self.stck(len(self.stck) - 1)
        self.stck.pop(len(self.stck) - 1)
        return a
    def push(self, arg):
        self.stck.append(arg)
stack1 = stack()
stack1.push(1)
print(stack1.stck)
```

### 큐

![[Screenshot 2024-01-03 at 12.12.21 AM.png\|Screenshot 2024-01-03 at 12.12.21 AM.png]]

- 각 요소에 우선순위를 부여하는 데이터 구조
- 선입선출(`FIFO`)의 데이터 구조
- 인큐(`inqueue`) - 데이터를 넣는 과정, 맨 뒤에 넣음
- 데큐(`dequeue`) - 데이터를 삭제하는 과정, 맨 앞을 뺌

```python
# Queueclass queue:
    q = []
    def __init__(self):
        self.q = []
    def inqueue(self, arg):
        self.q.append(arg)
    def dequeue(self):
        a = self.q[0]
        self.pop(0)
        return a
queue1 = queue()
queue1.inqueue(1)
print(queue1.q)
```

### 우선순위 큐

- 키와 값의 체계를 이용해 요소를 정렬하는 큐
- 우선순위에 따라 데이터가 추가, 삭제됨