---
{"dg-publish":true,"permalink":"/02-Area/Algorithm/(Algorithm) 컴퓨터로 도형 문제 풀기/","tags":["Area/Algorithm"],"noteIcon":"","created":"2025-01-05T15:54:58.000+09:00","updated":"2025-04-07T22:52:12.377+09:00"}
---

# 컴퓨터로 도형 문제 풀기

**컴퓨터로 도형 문제를 푼다**는 것은 곧 **벡터**와 **삼각함수**를 사용하여 기하학적인 문제를 해결하는 과정이다. 이 중에서도 **벡터**는 2차원 및 3차원 공간에서 도형의 크기와 방향을 나타내는 중요한 수단이다. 벡터는 두 점 사이의 위치를 나타내거나 도형의 변, 면적, 방향 등을 계산할 때 사용된다.

## 벡터의 정의

**벡터**는 **크기**와 **방향**을 동시에 가지는 양이다. 이는 **좌표 공간**에서 두 점을 연결하는 선분으로 생각할 수 있다. 예를 들어, 두 점 A(x₁, y₁)와 B(x₂, y₂) 사이의 벡터는 다음과 같이 정의된다:

- **벡터 AB = (x₂ - x₁, y₂ - y₁)**

벡터는 두 가지 중요한 연산을 할 수 있는데, 그것이 바로 **내적(dot product)**과 **외적(cross product)**이다. 이 연산들을 통해 벡터의 다양한 특성을 이용하여 도형의 문제를 해결할 수 있다.

## 벡터의 내적 (Dot Product)

**내적**은 두 벡터가 이루는 각도를 계산하는 데 사용된다. 벡터 `A`와 `B`의 내적은 다음과 같이 계산된다:

- **A · B = |A| |B| cosθ**
    - 여기서 `|A|`와 `|B|`는 벡터 A와 B의 크기, `θ`는 두 벡터 사이의 각도이다.

내적을 통해 두 벡터가 이루는 각도를 구하거나, 두 벡터가 **직교**(서로 수직)하는지 확인할 수 있다. 벡터 A와 B가 수직이면 내적 값은 0이 된다.

**2차원 내적 계산**:

```cpp
#include <iostream>#include <cmath>using namespace std;struct Vector {    double x, y;};double dot_product(Vector A, Vector B) {    return A.x * B.x + A.y * B.y;}int main() {    Vector A = {3, 4};    Vector B = {5, 6};    double result = dot_product(A, B);    cout << "벡터 A와 B의 내적: " << result << endl;    return 0;}
```

**내적의 활용**: 두 벡터가 **수직**인지 확인하려면 내적이 0인지 체크하면 된다.

## 벡터의 외적 (Cross Product)

**외적**은 두 벡터가 이루는 **평행사변형의 넓이**를 구하거나, 세 점이 시계 방향으로 나열되어 있는지, 반시계 방향으로 나열되어 있는지 판정하는 데 사용된다. 벡터 A(x₁, y₁)와 B(x₂, y₂)의 외적은 다음과 같이 계산된다:

- **A × B = |A| |B| sinθ**
    - 여기서 `|A|`와 `|B|`는 벡터 A와 B의 크기, `θ`는 두 벡터가 이루는 각도이다.
    - **결과값**은 두 벡터가 이루는 평행사변형의 넓이를 나타낸다.

2차원에서의 외적은 두 벡터의 성분으로 간단히 계산할 수 있다:

- **A × B = (x₁ _ y₂) - (y₁ _ x₂)**

**2차원 외적 계산**:

```cpp
#include <iostream>using namespace std;struct Vector {    double x, y;};double cross_product(Vector A, Vector B) {    return A.x * B.y - A.y * B.x;}int main() {    Vector A = {3, 4};    Vector B = {5, 6};    double result = cross_product(A, B);    cout << "벡터 A와 B의 외적: " << result << endl;    return 0;}
```

## 외적을 이용한 시계/반시계 방향 판정

세 점이 이루는 방향을 확인하기 위해 외적을 사용할 수 있다. 예를 들어, 세 점 P, Q, R이 있을 때, 벡터 PQ와 PR의 외적을 통해 세 점의 나열 순서를 알 수 있다:

- **외적 > 0**: 세 점이 **반시계 방향**으로 나열되어 있다.
- **외적 < 0**: 세 점이 **시계 방향**으로 나열되어 있다.
- **외적 = 0**: 세 점이 **일직선 상**에 있다.

**시계/반시계 방향 판정 코드 예시**:

```cpp
#include <iostream>using namespace std;struct Point {    double x, y;};double cross_product(Point P, Point Q, Point R) {    return (Q.x - P.x) * (R.y - P.y) - (Q.y - P.y) * (R.x - P.x);}void check_direction(Point P, Point Q, Point R) {    double result = cross_product(P, Q, R);    if (result > 0) {        cout << "세 점은 반시계 방향입니다." << endl;    } else if (result < 0) {        cout << "세 점은 시계 방향입니다." << endl;    } else {        cout << "세 점은 일직선 상에 있습니다." << endl;    }}int main() {    Point P = {0, 0};    Point Q = {1, 1};    Point R = {2, 0};    check_direction(P, Q, R);    return 0;}
```

**외적의 특수성**: 외적의 결과는 벡터가 이루는 평면의 넓이뿐만 아니라, 그 방향도 판별할 수 있다. 이를 이용해 세 점의 배치가 **시계 방향**인지 **반시계 방향**인지, 또는 일직선상에 있는지 판단할 수 있다.

## 요약

- **벡터**는 **크기와 방향**을 가지는 물리량으로, 2차원 또는 3차원 공간에서 중요한 도구이다.
- 벡터의 **내적**은 두 벡터 사이의 **각도**를 계산하고, 두 벡터가 **직교**하는지 여부를 확인하는 데 사용된다.
- 벡터의 **외적**은 두 벡터가 이루는 **평행사변형의 넓이**를 구하며, 이를 통해 세 점이 **시계 방향**인지 **반시계 방향**인지 판정할 수 있다.
- 내적과 외적을 활용하여 컴퓨터 상에서 도형 문제를 풀고, 공간적인 문제를 해결할 수 있다.