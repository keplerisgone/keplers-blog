---
{"dg-publish":true,"permalink":"/02-Area/Algorithm/(Algorithm) 재귀 함수/","tags":["Area/Algorithm"],"noteIcon":"","created":"2025-01-05T15:54:58.000+09:00","updated":"2025-04-07T22:52:08.671+09:00"}
---

# 재귀 함수

재귀 함수는 자기 자신을 부르는 함수로, 복잡한 문제를 단순한 하위 문제로 나누어 해결하는데 유용하다.

```python
def factorial(n):
    if n == 1:
        return 1    else:
        return n * factorial(n-1)
print(factorial(4))
```

재귀 함수를 작성하기 위해서는 다음과 같은 개념이 필요하다.
- **본 문제** : 풀어야하는 문제
- **하위 문제** : 풀어야하는 문제를 나눈 것
- **Base case** : 굳이 재귀를 거치지 않더라도 답이 나오는 것
- **Recursive Case** : 재귀로 해결해야 하는 부분

따라서, 다음과 같이 문제를 나눌 수 있다.
- **factorial을 구하는 경우**
- *n*! = *n* * (*n*−1) * (*n*−2) * (*n*−3)... 이면…
- Base case : 1, 1! = 1이니까
- Recursive case : 나머지 *n* * (*n*−1) * (*n*−2) * ... * 2

## 재귀 함수 작성법

1. 본 문제에서 하위 문제 정하기
2. Base/Recursive Case를 찾기
3. 구현하기!

## vs 반복문

반복문을 안 쓰고 재귀함수를 쓰면 좋은 점이 있을까?
- 함수 구현 방식으로 쓰인다. 문제를 접근하는 한 방법이 된다.
- 효율이 안 좋기는 한데 컴파일러가 반복문으로 바꿔준다. (라고 교수님이 그러심)

하지만 단점도 있다.
- 효율이 구리다.
- stack overflow 문제가 있다.
- 함수를 호출할수록 호출 위치가 쌓이게 되는데, 이게 넘치면 오류가 발생한다.

## 재귀 함수 예시

### 삼각수

수학에서 n번째 삼각수는 정수 1부터 n까지의 합이다. 이를 구해보자.

- 1번째 삼각수: 1
- 2번째 삼각수: 1 + 2 = 3
- 3번째 삼각수: 1 + 2 + 3 = 6
- **Base case** : 인자로 받는 n이 1인 경우
- **Recursive case** : n-1번째 삼각수를 구해야 함 + n

```python
def triangle_number(n):
    # 여기에 코드를 작성하세요    if n == 1:
        return n
    return n + triangle_number(n-1)
# 테스트 코드for i in range(1, 11):
    print(triangle_number(i))
```

### 피보나치 수열

피보나치 수열을 구하자.

- **Base case** : 첫 번째, 두 번째 수인 경우 (1)
- **Recursive case** : n번째를 구하려면 n-1, n-2번째를 구해서 더해야 함

```python
def fib(n):
    # 여기에 코드를 작성하세요    if n <= 2:
        return 1
    return fib(n - 1) + fib(n - 2)
# 테스트 코드for i in range(1, 16):
    print(fib(i))
```

### 자릿수의 합

0보다 큰 정수 `n`을 파라미터로 받아서 `n`의 각 자릿수의 합을 구해서 리턴하는 함수 `sum_digits()`를 작성해보자. 예를 들어, `sum_digits(123)`은 1 + 2 + 3 = 6을 리턴한다.

- **Base case** : 한 자릿수인 경우 (그냥 리턴)
- **Recursive case** : 두 자릿수 이상인 경우, 일의 자리 수 / 나머지로 나누어 생각

```python
def sum_digits(n):
    # 여기에 코드를 작성하세요    if n < 10:
        return n
    return n%10 + sum_digits(n//10)
# 테스트 코드print(sum_digits(22541))
print(sum_digits(92130))
print(sum_digits(12634))
print(sum_digits(704))
print(sum_digits(3755))
```

### 리스트의 최댓값 찾기

리스트 `my_list`를 파라미터로 받아서 `my_list`의 최대 요소를 리턴하는 함수 `max_list()`를 작성해 주세요. `my_list`의 모든 요소는 숫자이고, 1개 이상의 요소가 있다고 가정합니다.

```python
def max_list(my_list):
    # 여기에 코드를 작성하세요    if len(my_list) <= 1:
        return my_list[0]
    temp_max = max_list(my_list[:-1])
    if my_list[-1] >= temp_max:
        return my_list[-1]
    else:
        return temp_max
# 테스트 코드print(max_list([1, 4, 3, 2, 5, 0, 2]))
print(max_list([-1, -3, -10, -5, -9]))
print(max_list([3, 7, 3, 7, 7]))
print(max_list([1, 2.7, -3, 2.8, 1.6]))
print(max_list([32, 2, 3, 0 , 1]))
```

### 팰린드롬

팰린드롬(palindrome)이란 앞으로 읽는 것과 뒤로 읽는 것이 같은 문자열입니다. 예를 들어, `'기러기'`, `'토마토'`, `'스위스'`, `'12344321'`은 모두 팰린드롬입니다. 빈 문자열 `''`도 팰린드롬으로 간주할 수 있습니다.

문자열 `my_str`을 파라미터로 받아서 `my_str`이 팰린드롬인지 판별하는 함수 `is_palindrome()` 을 작성해 주세요.

```python
def is_palindrome(my_str):
    # 여기에 코드를 작성하세요    if len(my_str) <= 1:
        return True    if (my_str[-1] != my_str[0]):
        return False    else:
        return is_palindrome(my_str[1:-1])
#     return reverse(my_str) == my_str# def reverse(my_str):#     if len(my_str) <= 1:#         return my_str#     return my_str[-1] + reverse(my_str[:-1])# 테스트 코드print(is_palindrome('기러기'))
print(is_palindrome('토마토'))
print(is_palindrome('바나나'))
print(is_palindrome('racecar'))
print(is_palindrome('radar'))
print(is_palindrome('stars'))
print(is_palindrome('123321'))
```

아래 방법을 생각을 못했다
