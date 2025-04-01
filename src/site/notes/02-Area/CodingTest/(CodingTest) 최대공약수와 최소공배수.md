---
{"dg-publish":true,"permalink":"/02-Area/CodingTest/(CodingTest) 최대공약수와 최소공배수/","noteIcon":"","created":"2025-03-18T22:58:56.817+09:00","updated":"2025-04-01T22:46:28.628+09:00"}
---

## 문제

두 개의 자연수를 입력받아 최대 공약수와 최소 공배수를 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에는 두 개의 자연수가 주어진다. 이 둘은 10,000이하의 자연수이며 사이에 한 칸의 공백이 주어진다.

## 출력

첫째 줄에는 입력으로 주어진 두 수의 최대공약수를, 둘째 줄에는 입력으로 주어진 두 수의 최소 공배수를 출력한다.

## 문제 풀이

최대공약수는 유클리드 호제법을 사용하고, 최소공배수는 구한 최대공약수를 이용해 구하면 된다.

유클리드 호제법은 수를 계속 나누어가며 최대공약수를 찾아내는 방법이다. 18과 24를 예로 들어보자.
1. 큰 수를 작은 수로 나눈 나머지를 구한다: $24 \mod 18 = 6$
2. 나머지가 0이 나올 때까지 반복: 18 mod 6 = 0
3. 0이 나온 순간의 작은 수가 최대공약수가 된다: 6

최소공배수는 두 수의 곱을 최대공약수로 나누면 된다.

```cpp
#include <iostream>

using namespace std;

int main() {
    cin.tie(0);
    ios::sync_with_stdio(0);

    int M, N;
    cin >> M >> N;
    int max, min;

    if (M > N)
    {
        max = M;
        min = N;
    } else 
    {
        max = N;
        min = M;
    }

    int temp = max % min;

    while (temp != 0)
    {
        max = min;
        min = temp;
        temp = max % min;
    }
    
    cout << min << "\n" << M * N / min;

    return 0;
}
```