---
{"dg-publish":true,"permalink":"/02-area/coding-test/coding-test/","noteIcon":"","created":"2025-03-15T01:21:26.541+09:00","updated":"2025-04-01T22:46:22.635+09:00"}
---


## 문제

양수 A가 N의 진짜 약수가 되려면, N이 A의 배수이고, A가 1과 N이 아니어야 한다. 어떤 수 N의 진짜 약수가 모두 주어질 때, N을 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 N의 진짜 약수의 개수가 주어진다. 이 개수는 50보다 작거나 같은 자연수이다. 둘째 줄에는 N의 진짜 약수가 주어진다. 1,000,000보다 작거나 같고, 2보다 크거나 같은 자연수이고, 중복되지 않는다.

## 출력

첫째 줄에 N을 출력한다. N은 항상 32비트 부호있는 정수로 표현할 수 있다.

## 풀이 과정

아주 간단하다. 약수를 크기 기준으로 오름차순으로 정리 한 뒤 가장 처음에 나오는 약수와 가장 마지막에 있는 약수를 곱하면 된다.
이제 이를 어떻게 할 것이느냐가 문제인데, 나는 vector에 정리한 다음에 sort 함수를 이용하는 버그를 쓰기로 했다. 

## 전체 코드 

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    cin.tie(0);
    ios::sync_with_stdio(0);

    int N;
    cin >> N;

	// 벡터에 약수 넣기
    vector<int> vec;
    for (size_t i = 0; i < N; i++)
    {
        int temp;
        cin >> temp;
        vec.push_back(temp);
    }

	// 정렬 하기
    sort(vec.begin(), vec.end());

    cout << vec.front() * vec.back() << "\n";

    return 0;
}
```

## 배운 것

- vector외에도 multiset, set과 같은 자료 구조가 있었구나
- 너무 야매로 푼 것 같아서 문제에 비밀이 있는지 GPT한테 물어봤다.
	- 내 방법이 맞대...