---
{"dg-publish":true,"permalink":"/02-area/coding-test/coding-test/","noteIcon":"","created":"2025-03-15T15:42:58.455+09:00","updated":"2025-04-01T22:46:19.040+09:00"}
---


나는 이거 시간 초과 날 줄 알았다. 뭔가 공식이 있겠거니 싶었음.

## 문제

두 자연수 A와 B가 있을 때, A = BC를 만족하는 자연수 C를 A의 약수라고 한다. 예를 들어, 2의 약수는 1, 2가 있고, 24의 약수는 1, 2, 3, 4, 6, 8, 12, 24가 있다. 자연수 A의 약수의 합은 A의 모든 약수를 더한 값이고, f(A)로 표현한다. x보다 작거나 같은 모든 자연수 y의 f(y)값을 더한 값은 g(x)로 표현한다.

자연수 N이 주어졌을 때, g(N)을 구해보자.

## 입력

첫째 줄에 자연수 N(1 ≤ N ≤ 1,000,000)이 주어진다.

## 출력

첫째 줄에 g(N)를 출력한다.

## 문제 풀이

### 처음에 쓴 멍청한 코드

```cpp
#include <iostream>
#include <vector>
#include <math.h>

using namespace std;

void find_num(int N, vector<int>::iterator it) {

}

int main() {
    cin.tie(0);
    ios::sync_with_stdio(0);

    int N;
    cin >> N;
    long long int sum = 0;
    
    for (size_t i = 1; i <= N; i++)
    {
        for (size_t j = 1; j <= sqrt(i); j++)
        {
            if (i % j == 0 && j != sqrt(i)) 
            {
                sum += j;
                sum += i / j;
            } else if (j == sqrt(i)) {
                sum += j;
            }
            // 이거 n(n+1)/2 + n정도는 해도 되는거 아님? 아낄 수 있잖아
        }
    }

    cout << sum;    

    return 0;
}

// 시간 초과
```

정말 단순히 각 수의 약수를 for 문으로 (매우 비효율적으로) 구한 뒤 전부 더하는 방식이다. 그와중에 연산을 줄이겠다고 `sqrt()`를 사용한 것이 눈에 띈다.
위 코드는 시간 초과가 나서 사용할 수 없다. 

### 고친 코드

다만 다음과 같은 방법을 이용하면 더 쉽고 빠르게 구현할 수 있다. 잘 생각해보자.

- 약수 1은 어디에 포함되는가? : 1, 2, 3, 4... 1의 배수.
- 약수 2는 어디에 포함되는가?: 2, 4, 6... 2의 배수.
- 3도 마찬가지로 3의 배수에 포함될 것.

따라서 $N$까지의 수에서 어떤 약수 $k$는 $\left[ \frac{N}{k} \right]$개가 존재할 것이다. 따라서 $N$보다 같거나 작은 자연수들의 약수의 합은

$$g(N) = \sum_{k=1}^{N}f(N) = \sum_{k=1}^{N}k\times{[\frac{N}{k}]}$$

로 나타낼 수 있다. 재미있다 수학!

```cpp
#include <iostream>
#include <vector>
#include <math.h>

using namespace std;

void find_num(int N, vector<int>::iterator it) {

}

int main() {
    cin.tie(0);
    ios::sync_with_stdio(0);

    int N;
    cin >> N;
    long long int sum = 0;
    
    for (size_t i = 1; i <= N; i++)
    {
        sum += i * (N / i);
    }

    cout << sum;    

    return 0;
}
```