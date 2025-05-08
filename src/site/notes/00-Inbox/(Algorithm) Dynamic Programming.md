---
{"dg-publish":true,"permalink":"/00-Inbox/(Algorithm) Dynamic Programming/","tags":["Area/Algorithm"],"noteIcon":"","created":"2025-05-03T00:06:11.000+09:00","updated":"2025-05-08T16:30:14.913+09:00"}
---

# (Algorithm) Dynamic Programming
## Summary

Dynamic Programming(DP)은 복잡한 문제를 더 단순한 부분 문제(subproblem)로 나누어 해결하고, 한 번 계산한 결과를 저장(memoization 또는 tabulation)하여 중복 계산을 방지하는 알고리즘 기법이다.

## Contents

- DP는 Dynamic Programming의 약자로, 주어진 입력에 대해 결과를 계산하고, 추가적인 입력이 들어오면 그 결과를 재사용하는 풀이 방식이다.
- 핵심 아이디어는 “큰 문제를 작은 문제로 나누고, 작은 문제의 답을 저장하여(saving state) 동일한 계산을 반복하지 않는다”는 것.
	- 예를 들어, 피보나치 수열을 일반 재귀로 구현하면 같은 함수를 n번씩 중복으로 불러오는 경우가 발생한다.
	- 이를 DP를 활용해 다음과 같이 ‘값을 저장’하는 방식으로 구현하면 훨씬 효율적이다.

```cpp
vector<long long> memo(1001, -1);
long long fib(int n) {
  if (n <= 1) return n;
  if (memo[n] != -1) return memo[n];
  return memo[n] = fib(n-1) + fib(n-2);
}
```

주요 특징은 다음과 같다.

1. 최적 부분 구조(Optimal Substructure)  
	- 문제의 최적 해(optimal solution)가 그 부분 문제들의 최적 해로부터 구성될 수 있어야 한다.
	- **하위 문제**를 고려한다는 점에서 **순간의 선택**에서만 최적을 고려하는 **Greedy algorithm**과는 차이를 보인다.
2. 중복 부분 문제(Overlapping Subproblems)  
	- 동일한 부분 문제가 여러 번 계산될 때, 한 번만 계산하고 저장해 두면 효율적이다.
	- DP를 사용하는 이유!

아래는 구현 방식.
1. Top–Down (Memoization)  
	- 재귀 호출하면서, 계산한 결과를 해시맵 또는 배열에 저장했다가 다음에 동일한 호출이 들어오면 저장된 값을 반환.
2. Bottom–Up (Tabulation)  
	- 작은 문제부터 순차적으로 테이블(배열)에 채워 나가면서, 최종 원하는 값에 도달하는 방식.

### 관련 문제

- 백준 16059: Überwatchㅔ
	- 쿨타임이 있는 궁극기를 활용해서 가장 많은 적을 쓰러뜨리는 문제
	- *현재까지의 최대치*와 *몇 번 포기하고 현재 궁극기를 사용했을 때* (표현이 좀 이상하지만)를 비교하는 DP의 모범적인 문제이다.

```cpp
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

int main() {
  ios::sync_with_stdio(false);
  cin.tie(0);

  int n, m, mx, temp = 0;
  cin >> n >> m;
  vector<int> data;

  for (int i = 0; i < n; i++) {
    cin >> temp;
    if (i < m) {
      data.push_back(0);
      continue;
    }
    // 이부분이 DP 핵심 부분
    mx = max((temp + data[i - m]), data[i - 1]);
    data.push_back(mx);
  }
  int result = *(data.end() - 1);
  cout << result;
  return 0;
}
```

* 주석다는 습관을 기르자
## Reference

https://www.acmicpc.net/problem/16059