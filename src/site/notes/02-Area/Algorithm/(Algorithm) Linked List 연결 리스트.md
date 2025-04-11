---
{"dg-publish":true,"permalink":"/02-Area/Algorithm/(Algorithm) Linked List 연결 리스트/","tags":["Area/Algorithm"],"noteIcon":"","created":"2025-01-05T15:54:58.000+09:00","updated":"2025-04-07T22:51:26.487+09:00"}
---


# 리스트

![[Screenshot 2024-01-03 at 12.15.32 AM.png\|500]]

- 배열은 _****************메모리가 할당된 대로 순차적으로 데이터가 저장****************_되지만, 리스트는 여기저기 흩어져서 저장이 가능
    - 포인터를 이용해서 저장하기 때문
- 노드(`node`) - 데이터 요소 + 포인터
- 헤드(`head`) - 진입점을 가리키는 포인터
- 포인터의 개수, 방향에 따라 종류가 나뉨
    - **단방향 연결 리스트**(`singly linked list`) - 포인터가 한 방향만을 가리키는 리스트
    - **양방향 연결 리스트**(`doubly linked list`) - 포인터가 양방향을 가리킴, 노드에는 포인터가 두 개 포함
    - **순환 연결 리스트**(`circluar linked list`) - 마지막 포인터가 null이 아닌 head를 가리킴

## 왜 사용하나?

크기가 정해져 있는 배열과는 달리 얼마든지 새로운 값을 추가할 수 있고, 삽입/삭제가 용이하다. 하지만 배열과는 달리 임의 접근이 불가능해 요소에 접근을 하고 싶다면 앞에서부터 순차적으로 접근해야 한다. 또한 요소에 포인터가 포함되기 때문에 메모리는 더 많이 필요하다.

# C++

C++에서 Linked list를 구현한다. `struct`를 이용해 포인터 + 값을 가지는 노드를 만든다.
[전체 소스 코드](https://github.com/keplerisgone/TechDev/blob/main/CPPBasic/LinkedList.cpp)

```cpp
template <typename T>struct Node {    T data;    node* next;}
```