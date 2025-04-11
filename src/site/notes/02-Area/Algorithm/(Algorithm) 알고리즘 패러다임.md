---
{"dg-publish":true,"permalink":"/02-Area/Algorithm/(Algorithm) 알고리즘 패러다임/","tags":["Area/Algorithm"],"noteIcon":"","created":"2025-01-05T15:54:58.000+09:00","updated":"2025-04-07T22:52:02.956+09:00"}
---


# Summary

- 알고리즘 패러다임
- Brute Force
- Divide and Conquer
- Dynamic Programming
- Greedy Algorithm
- Backtracking + Branch and Bound

# 알고리즘 패러다임

- 알고리즘 패러다임이란?
- **알고리즘을 만드는 방법**.
    - 알고리즘을 설계하고 구현할 때 사용하는 접근 방식이나 방법론
- 알고리즘이 문제의 풀이 방법에 가깝다면, 패러다임은 접근 방식에 가깝다.

## Brute Force

- **무차별 대입법**
- 가능한 경우의 수를 모두 대입하는 방법이다.
- *장점*
    - 가장 간단하게 구현할 수 있다
    - 직관적이고 명확하다
    - 답을 확실하게 알 수 있다
- *단점*
    - 다른 방식에 비해 매우 비효율적이다.
    - 최소 시간 복잡도가 *O*(*n*)이다. (일반적으로 input 크기에 따라 변하기 때문)

### 예시) 카드 쌍 고르기

- 두 카드 그룹에서 카드를 한 장 씩 골라 가장 큰 곱을 만들고자 한다.
- 이를 브루트 포스 방식으로 구현하면…

```python
def max_product(left_cards, right_cards):
    max = 0    for first_card in left_cards:
        for second_card in right_cards:
            result = first_card * second_card
            if result > max:
                max = result
    return max
```

- 나올 수 있는 모든 조합을 계산한 뒤 `max`를 업데이트, 최종 `max`를 반환한다.
- `max`는 내장 함수 이름인데, 왜 변수명으로 사용이 되는지는 모르겠다..

> [!notes]
- 이는 python의 변수명 사용이 별칭(alias) 방식으로 사용되기 때문에 그렇다.
- 정확히는 max라는 이름은 built-in namespace 내부의 max 함수를 가리키고 있는데, 이를 사용자가 새로 정의할 경우 local에서 사용하는 max (타입 무관)로 가려지게 된다. 신기해!
- 따라서 max 함수를 사용하고 싶으면 del max로 변수를 지우고 사용해야 한다.
> 

## Divide and Conquer

- **문제를 더 작은 문제들로 분할하여 해결한 후, 이를 종합해 큰 문제를 해결한다.**
- 즉 문제를 재귀적으로 해결하는 방식이다. (실제로 재귀 함수로 구현되는 경우가 많다)
- Divide and Conquer는 다음과 같은 과정으로 진행된다.
1. **Divide** : 문제를 작은 문제로 나눈다.
2. **Conquer** : 각 작은 문제를 정복한다.
3. **Combine** : 해결한 작은 문제를 병합해 큰 문제를 해결한다.
- 정말 간단하게 예시를 들면…
- *두 자리 수 덧셈*을 할 때,
    - 
        1. 일단 (*십의 자리 / 일의 자리*)로 나누어 계산하려고 한다.
    - 
        1. 둘 다 계산한다.
    - 
        1. 이걸 다시 더한다. 끝!

### 예시) 병합 정렬 (Merge Sort)

- [[병합 정렬 (Merge Sort)\|병합 정렬 (Merge Sort)]] 문서를 참고.
1. **Divide** : list를 나눈다.
2. **Conquer** : 나눈 list를 정렬한다. (selection sort를 이용해도.. 되지만 combine 과정에서 자동으로 정렬된다)
3. **Combine** : 정렬된 리스트를 합친다. 나눈 리스트의 앞 원소부터 비교해 새로운 리스트에 추가한다.

### 예시) 퀵 정렬 (Quick Sort)

- [[퀵 정렬 (Quick Sort)\|퀵 정렬 (Quick Sort)]] 문서를 참고.
1. **Divide** : pivot을 정한 뒤, pivot을 기준으로 비교 및 정렬 후 양쪽으로 나누고…
2. **Conquer** : 나눈 위치에서 다시 pivot을 정해 정렬하는 것을 반복한다.
3. **Combine** : 위 과정을 진행하면 자동으로 정렬된다.

## Dynamic Programming

- 위의 **Divide and Conquer** 과정은 *반복되는 부분이 존재한다는* 단점이 있다.
- 이는 효율 측면에서 문제가 될 수 있다.
    - 예를 들어 거듭제곱을 계산하는 `power()` 함수를 재귀 방식으로 구현하면 내부에서 `power(0)`까지 반복적으로 호출하는 단점이 있다.
- 따라서 **Dynamic Programming**에서는 이미 계산한 값을 저장하는 방식으로 문제를 해결한다.
    - **Memoization** : 계산한 것을 기록해나가는 top-down 방식.
    - **Tabulation** : 가장 작은 문제부터 기록하면서 해결하는 bottom-up 방식, 이 경우는 반복문을 활용한다.
- Dynamic Programming은 다음과 같은 조건을 만족하면 쓸 수 있다.
    - **최적 부분 구조** (Optimal Substructure) : 부분 문제의 최적의 답이 큰 문제의 최적의 답을 이룬다.
    - **중복되는 부분 문제** (Overlapping Subproblems) : 한 번 푼 문제를 다시 활용해야 한다.

### 예시) 피보나치 수열 구하기

### Memoization 방식

```python
def fib_memo(n, cache):
    # 여기에 코드를 작성하세요    if n in cache:
        return cache[n]
    if n < 3:
        return 1    fib = fib_memo(n-1, cache) + fib_memo(n-2, cache)
    cache[n] = fib
    return fib
def fib(n):
    # n번째 피보나치 수를 담는 사전    fib_cache = {}
    return fib_memo(n, fib_cache)
```

- 리스트에 없으면 계산하고, 리스트에 존재할 경우 이를 리턴하는 `fib_memo()` 함수가 핵심이다.

### Tabulation 방식

```python
def fib_tab(n):
    # 여기에 코드를 작성하세요    fib_table = [0, 1, 1]
    for i in range(0, n-2):
        fib_table.append(fib_table[i + 1] + fib_table[i + 2])
    return fib_table[n]
```

- 단순히 처음 단계부터 차근차근 리스트에 담아가며 계산한 후, 마지막 원소를 리턴한다.

## Greedy Algorithm

- **현재 가장 최선인 선택을 하는 방식**
- 간단하고 빠르다.
- *최적 부분 구조*를 포함하며, 탐욕적 선택이 곧 최적의 선택인 *탐욕적 선택 속성*이 존재하면 Greedy Algotirhm으로 최적의 답을 구할 수 있다.
- 이외에도 적당한 답이 필요한 경우에는 좋은 방식이 될 수 있다.

### 예시) 카드 합 고르기

```python
def max_product(card_lists):
    max = 1    for cards in card_lists:
        max *= max(cards)
    return max
```

- 위에서 Brute Force로 구현한 예시는 Greedy algorithm으로 최적의 답을 구할 수 있다.
- 그냥 각 그룹에서 가장 큰 카드를 고르면 된다.
## Etc

### Backtracking

- 후보를 구성하다가 현재 후보가 해답이 될 것 같지 않으면 포기하는 방식
- 깊이 우선 탐색 (Depth-First Search)와 유사한 방식이다.
- *가능한 모든 해를 찾거나*, *해의 존재 여부를 판단*하는데 사용한다.
- N-퀸 문제, 미로 찾기, 부분 집합 합 문제에서 사용한다.

### Branch and Bound

- 현재 노드 (해답)의 경로를 확장하면서 최적의 해를 찾기 위해 분기하고, 불필요한 경로를 제거해 효율을 높이는 방법이다.
- 답을 찾는다기보단 최적의 답을 찾기 위한 접근 방식에 가깝다