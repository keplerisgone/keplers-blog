---
{"dg-publish":true,"permalink":"/02-Area/Algorithm/(Algorithm) 행렬의 거듭제곱/","tags":["Area/Algorithm"],"noteIcon":"","created":"2025-01-05T15:54:58.000+09:00","updated":"2025-04-07T22:52:14.343+09:00"}
---


# 행렬의 거듭제곱과 피보나치 수열

**행렬의 거듭제곱**을 이용하면 일반적인 수학적 점화식을 사용하는 방법보다 **더 효율적으로** 알고리즘을 설계할 수 있다. 그 대표적인 예가 **피보나치 수열**을 계산하는 방법이다.

## 피보나치 수열과 점화식

피보나치 수열은 다음과 같은 **점화식**으로 정의된다:
- **F(n) = F(n-1) + F(n-2)** (n ≥ 2)
- F(0) = 0, F(1) = 1

일반적으로 이 점화식을 **재귀적** 또는 **반복적**으로 계산할 경우, 시간 복잡도는 **O(N)**이다. 그러나 **행렬의 거듭제곱**을 이용하면 **O(log N)**의 복잡도로 피보나치 수를 구할 수 있다.

## 행렬을 이용한 피보나치 수 계산

피보나치 수열을 행렬로 표현할 수 있다. 다음과 같은 행렬 `A`를 사용한다:

```
A = [ 1 1 ]
    [ 1 0 ]
```

행렬 `A`를 거듭제곱하면 피보나치 수를 계산할 수 있다. 예를 들어, **A^n**을 구한 후, 그 결과 행렬의 2열에 있는 항의 합이 피보나치 수 **F(n)**가 된다.

- 즉, **A^(n-1)**을 구하면, **F(n)**을 얻을 수 있다.

## 행렬의 거듭제곱을 이용한 피보나치 수 계산 과정

행렬의 거듭제곱을 빠르게 계산하기 위해서는 **분할 정복**을 이용한다. 거듭제곱을 단순히 반복해서 계산하는 대신, **2의 거듭제곱**을 미리 계산하여 곱하는 방식으로 효율성을 높인다.

- 예를 들어, **A8을 계산하려면, A4**을 먼저 구하고, 이를 제곱하여 **A^8**을 얻을 수 있다.
- 더 나아가, **A4는 A2**의 제곱으로 구할 수 있다. 즉, 이 방법을 통해 시간 복잡도를 **O(log N)**으로 줄일 수 있다.

## 행렬의 거듭제곱을 이진법으로 구하는 방법

행렬 A의 **N-1제곱**을 빠르게 계산하기 위해서는 **2의 거듭제곱**을 사용한다. 이 방법은 **이진법**을 사용하여, 각 지수에 해당하는 거듭제곱을 미리 계산한 뒤 필요한 값을 곱하는 방식이다.

예를 들어, **A^9**을 계산하려면:
1. A^1, A^2, A^4, A^8을 미리 계산해 놓는다.
2. **9 = 2^3 + 20이므로, A9 = A^8 * A^1**로 구할 수 있다.

이 방식으로 행렬의 거듭제곱을 구하면 **O(log N)**의 복잡도로 피보나치 수열을 빠르게 계산할 수 있다.

### 요약

- 피보나치 수열은 점화식으로 O(N)의 시간 복잡도로 계산할 수 있지만, **행렬의 거듭제곱**을 이용하면 **O(log N)**으로 효율적으로 계산할 수 있다.
- 피보나치 수를 행렬로 계산할 때, 기본적으로 행렬 **A = [1 1, 1 0]**을 사용하여 피보나치 수열을 표현할 수 있다.
- 행렬의 거듭제곱을 **이진법**으로 빠르게 계산하면, 피보나치 수를 빠르게 구할 수 있다.