---
{"dg-publish":true,"permalink":"/02-Area/Algorithm/(Algorithm) 정렬과 탐색/","tags":["Area/Algorithm"],"noteIcon":"","created":"2025-01-05T15:54:58.000+09:00","updated":"2025-04-07T22:52:10.445+09:00"}
---


# 정렬과 탐색

## 개요

정렬은 데이터를 특정 순서에 따라 배열하는 과정이며, 다양한 문제를 해결하기 위한 기본 도구로 활용된다. 이 문서에서는 정렬 알고리즘의 주요 개념과 시간 복잡도, 그리고 이를 활용한 문제 풀이 및 탐색 알고리즘을 다룬다.

## 본문

### 1. 정렬 알고리즘

### 1.1 버블 정렬 (Bubble Sort)

- 연속된 두 원소를 비교하여 크기가 순서대로 정렬되도록 위치를 바꾸는 과정을 반복하는 알고리즘이다.
- 가장 큰 원소가 반복적으로 정렬된 위치로 이동한다.
- **역위(Inversion):** 배열에서 앞의 원소가 뒤의 원소보다 큰 상태를 의미하며, 역위의 개수에 비례해 작업량이 증가한다.
- 시간 복잡도:
    - 최악: (O(n^2))
    - 최선: (O(n)) (이미 정렬된 경우)

```cpp
void bubble_sort (vector<int>& vec) {    int n = vec.size();    for (int i = n-1; i > 0 ; i--) {        for (int j = 0; j < i; j++) {            if (vec[j] > vec[j + 1]) swap(vec, j, j+1);        }    }}
```

### 1.2 병합 정렬 (Merge Sort)

- 배열을 나누고 합치는 과정에서 정렬을 수행하는 분할 정복 알고리즘이다.
- 재귀적으로 구현되며, 호출 횟수와 호출당 복잡도의 곱으로 시간 복잡도를 계산한다.
- 시간 복잡도: (O(n n))

```cpp
vector<int> merge_sort(vector<int>& vec) {    int n = vec.size();    // 1. 개수가 하나라면 반환    // 2. 절반으로 나누어 각각 정렬한 것을 반환    // 3. 정렬의 방식은 맨 앞 원소 비교 (O(n))    vector<int> slicedA(vec.begin(), vec.begin() + n/2);    vector<int> slicedB(vec.begin() + n/2, vec.end());    if (n == 1) return vec;    vector<int> sortedA = merge_sort(slicedA);    vector<int> sortedB = merge_sort(slicedB);    return merge_vector(sortedA, sortedB);}
```

### 1.3 계수 정렬 (Counting Sort)

- 비교를 하지 않고 원소의 개수를 세어 정렬하는 알고리즘이다.
- 개수대로 배열에 원소를 추가하는 방식으로 작동한다.
- 제한 사항: 데이터의 크기가 클수록 많은 메모리를 필요로 한다.
- 시간 복잡도: (O(n))

```cpp
void counting_sort(vector<int>& vec) {    if (vec.empty()) return; // 빈 벡터 처리    // 1. 입력 데이터의 최대값과 최소값 계산    int max_val = *max_element(vec.begin(), vec.end());    int min_val = *min_element(vec.begin(), vec.end());    int range = max_val - min_val + 1; // 데이터의 범위    // 2. 카운트 배열 초기화    vector<int> count(range, 0);    // 3. 데이터 값의 빈도 계산    for (int val : vec) {        count[val - min_val]++;    }    // 4. 원본 배열을 정렬된 순서로 채우기    int index = 0;    for (int i = 0; i < range; i++) {        while (count[i] > 0) {            vec[index++] = i + min_val;            count[i]--;        }    }}
```

근데 사실 실전에서는 sort() 쓴다.

### 2. 정렬을 이용한 문제 풀이

### 2.1 스위프 라인 알고리즘 (Sweep Line Algorithm)

- 정렬된 이벤트의 순서대로 문제를 처리하는 모델링 기법이다.
- 예시: 음식점에 가장 많은 손님이 있었던 시간을 찾는 문제
    - 손님이 들어오고 나가는 시간을 정렬하여 처리

### 2.2 이벤트 스케줄링

- 정렬을 통해 과목의 최대 개수를 처리할 수 있는 시간표를 짜는 문제를 해결한다.

### 2.3 작업과 데드라인

- 작업 소요 시간과 데드라인이 주어진 문제에서 점수를 최대화하기 위한 접근법:
    1. 작업을 완료하는 시점이 늦어질수록 얻는 점수가 줄어든다.
    2. 데드라인 자체는 점수에 영향을 미치지 않는다.
    3. 작업 소요 시간이 짧은 순서대로 작업을 수행하는 탐욕 알고리즘을 적용한다.

### 3. 탐색

### 3.1 이진 탐색 (Binary Search)

- 데이터를 절반씩 나누어 탐색 범위를 좁히는 방식의 알고리즘이다.
- 시간 복잡도: (O(n))
- 구현 방식:
    1. **범위를 절반으로 나누는 방식:** 탐색 대상의 범위를 이분법으로 좁힌다.
    2. **건너뛰는 크기를 절반으로 나누는 방식:** 건너뛰며 대상 범위를 축소한다.

### 3.2 최적해 구하기

- 문제의 조건에 따라 특정 값에서 True 또는 False로 구분할 수 있다면, 다음 방식으로 최적해를 구할 수 있다:
    1. False가 되는 값 중 최대값을 찾는다.
    2. 이 값에 1을 더한 값이 최적해가 된다.