---
{"dg-publish":true,"permalink":"/02-Area/CodingTest/(CodingTest) 111111111!/","noteIcon":"","created":"2025-03-13T13:24:58.959+09:00","updated":"2025-04-01T22:45:33.628+09:00"}
---

## 문제

2와 5로 나누어 떨어지지 않는 정수 n(1 ≤ n ≤ 10000)가 주어졌을 때, 각 자릿수가 모두 1로만 이루어진 n의 배수를 찾는 프로그램을 작성하시오.

### 입력

입력은 여러 개의 테스트 케이스로 이루어져 있다. 각 테스트 케이스는 한 줄로 이루어져 있고, n이 주어진다.

### 출력

각 자릿수가 모두 1로만 이루어진 n의 배수 중 가장 작은 수의 자리수를 출력한다.

## 풀이 과정

- 가장 중요 > 나머지 연산은 각 항에 나머지 연산을 해도 됨
- 즉 111 mod 3 = (11 * 10 + 1) mod 3 -> 귀찮으니 (11 mod 3 * 10 + 1) mod 3을 하면 재귀적으로 구현할 수 있습니다
- 최대 input이 10000이므로 일반적인 나머지 연산을 하면 크기가 커져서 무한 루프에 빠집니다
- input의 개수가 주어지지 않으므로 `while`과 `cin`을 사용해야 합니다

## 코드

```cpp
#include <iostream>

using namespace std;

int main() {
    cin.tie(0);
    ios::sync_with_stdio(0);

    int n;

    while (cin >> n) {
        int remainder = 1 % n;  // 1을 n으로 나눈 나머지
        int count = 1;

        while (remainder != 0) {  
            remainder = (remainder * 10 + 1) % n;  // 새로운 1의 나머지를 구함
            count++;
        }

        cout << count << "\n";
    }

    return 0;
}
```

## 배운 것

- 나머지 연산의 특징. 사실 전에 알고리즘 공부하면서 배운 건데 까먹었다. 다시 떠올렸으니 됐다
- input의 개수가 주어지지 않으면 `while`을 써야 한다