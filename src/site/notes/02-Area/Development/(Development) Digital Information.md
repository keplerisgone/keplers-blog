---
{"dg-publish":true,"permalink":"/02-Area/Development/(Development) Digital Information/","tags":["Area/Development"],"noteIcon":"","created":"2025-01-05T15:54:46.000+09:00","updated":"2025-04-07T23:13:20.163+09:00"}
---

# Summary

컴퓨터에서 정보를 처리하고 저장하는 방법에 대해서 알아봅시다.
# Contents
## Limitation of storing number

데이터는 메모리에 비트의 형식으로 저장되기 때문에, 비트의 수에 따라 저장할 수 있는 데이터의 가짓수도 달라진다. *n*개의 비트가 있다면, 이는 2*n* 가지의 데이터를 표현할 수 있다.
따라서 64비트 운영체제에서는 264가지의 데이터를 표현할 수 있는 셈이다. 만약 이 데이터를 숫자라고 하자. 그렇다면 이 범위($0 \~ 2^{64}-1$)를 넘는 수를 표현할 경우 **overflow**가 발생한다. 오버플로우가 발생하는 수에서 연산을 진행하면 위험하므로, JS에서는 253 − 1까지를 *safe integer*로 지정해놓고 있다. 이 이후는 연산은 가능하나 권장되지는 않는다.

**floating point representation**는 부동 소수점 수를 *mantissa*와 2의 제곱수로 나타내는 방법이다. mantissa는 1.0과 2.0 사이의 수이다. 가장 중요한 점은 이렇게 수를 표현하기 때문에 1.3과 같은 수를 정확히 표현할 수 없다. -> **Round-off Error!!**
## Storing Text in Binary

## Converting analog data to binary

- 아날로그 -> 연속적인 데이터
- 디지털 -> discrete signal

다음과 같은 과정을 거쳐서 analog -> digital의 변환이 일어난다.
1. sampling : 연속적인 데이터에서 일정 간격으로 데이터를 뽑아내는 과정
2. quantization : 데이터의 값을 일정한 값으로 반올림하는 과정 (round-off)
1. 가장 가까운 예시는 volume bar가 아닐까
3. binary encoding : 해당 값을 바이너리로 표현

이를 다시 digital -> analog로 표현하는 것을 reconstruction이라고 하는데, 이 때의 smooth curve는 무슨 기준일까요?