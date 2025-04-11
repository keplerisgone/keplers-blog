---
{"dg-publish":true,"permalink":"/02-Area/Development/(Development) Data Compression/","tags":["Area/Development"],"noteIcon":"","created":"2025-01-05T15:54:46.000+09:00","updated":"2025-04-07T23:13:20.163+09:00"}
---

# Summary

디지털 기기에서 데이터를 압축하는 방법에 대해서 알아보자.
# Contents
## Data compression

데이터의 압축은 *용량을 적게 사용하고, 더 많은 데이터를 담기 위해서* 몹시 중요하다. 데이터 압축은 데이터의 손실 정도에 따라 두 가지로 나뉜다.

- **lossless compression** : 정보 손실이 없는 압축 방법으로, original data를 보존한다. text, simple image에서 이용.
- **lossy compression** : 정보 손실이 존재하는 압축 방법으로, 정보 손실이 있는 대신 압축률이 높다.
### lossless compression

주로 text를 압축할 때 많이 쓰는 방법이다. 가장 많이 쓰이는 글자를 짧은 비트의 나열로 치환한다.

![https://i.imgur.com/InKZei9.png](https://i.imgur.com/InKZei9.png)

단순한 image도 lossless compression을 사용할 수 있다.
-

**bitmap**

: 픽셀이 존재하는 위치를 1, 아닌 부분을 0으로 나타낸 map

![https://i.imgur.com/q5OMXs6.png](https://i.imgur.com/q5OMXs6.png)

-

**RLE compression algorithm**

: run-length encoding의 준말로, 연속된 비트 수를 숫자로 나타내는 것 -> JPEG에서 마지막 단계에 사용

![https://i.imgur.com/uDFD3Ww.png](https://i.imgur.com/uDFD3Ww.png)

-

**compression ratio**

: 단순한, 큰 이미지일 수록 saving spaces가 늘어남, 하지만 복잡한 이미지일 수록 효율이 줄어듦. => 따라서 icon과 같은 단순한 이미지에서 사용
#### Huffman coding algorithmlossless bit compression의 일종으로,

*가장 많이 등장하는 문자에 적은 수의 비트를 할당하는 것*

이 때 decoding에 문제가 되지 않도록 length, pattern 모두 신경 써야함

![https://i.imgur.com/y4sby4Y.png](https://i.imgur.com/y4sby4Y.png)

PNG, LZ77 방식에서 사용