---
{"dg-publish":true,"permalink":"/02-Area/Algorithm/(Algorithm) 그래프 알고리즘/","tags":["Area/Algorithm"],"noteIcon":"","created":"2025-01-05T15:54:58.000+09:00","updated":"2025-04-07T22:51:34.454+09:00"}
---


# 그래프

**그래프**는 여러 대상 간의 관계를 나타내는 **네트워크 구조**이다. 각 **정점(노드, Vertex)**는 연결된 **간선(Edge)**을 통해 서로 이어져 있다. 그래프는 다양한 방식으로 대상을 연결하고 표현할 수 있으며, 그래프 이론은 컴퓨터 과학과 수학에서 중요한 역할을 한다.

## 그래프의 종류

1. **무향 그래프 (Undirected Graph)**:
    - **정점 간의 간선에 방향이 없는 그래프**이다. 즉, A에서 B로 가는 간선이 있을 때, B에서 A로도 이동할 수 있다.
    - **다이어그램**:
    
    ```mermaid
    graph TD;
        A---B;
        B---C;
        A---C;
    ```
    
2. **유향 그래프 (Directed Graph)**:
    - **간선에 방향이 있는 그래프**로, A에서 B로 가는 간선이 있더라도 B에서 A로는 이동할 수 없을 수 있다.
    - **다이어그램**:
    
    ```mermaid
    graph TD;
        A-->B;
        B-->C;
        A-->C;
    ```
    
3. **가중치 그래프 (Weighted Graph)**:
    - **각 간선에 가중치**(비용, 거리 등)가 할당된 그래프이다. 가중치는 두 정점을 연결하는 데 드는 비용을 나타낼 수 있다.
    - **다이어그램**:
    
    ```mermaid
    graph TD;
        A--5-->B;
        B--3-->C;
        A--2-->C;
    ```
    
4. **이분 그래프 (Bipartite Graph)**:
    - **두 개의 집합으로 나누어진 그래프**로, 각 집합에 속한 정점끼리는 간선이 존재하지 않고, 다른 집합의 정점과만 연결된다.
    - **다이어그램**:
    
    ```mermaid
    graph TD;
        A---1;
        A---2;
        B---1;
        B---2;
    ```
    
5. **평면 그래프 (Planar Graph)**:
    - **간선이 교차하지 않고** 평면 위에 그려질 수 있는 그래프이다. 간선이 교차하지 않는 그래프는 평면 그래프라 부른다.
6. **오일러 그래프 (Eulerian Graph)**:
    - 모든 **간선을 한 번씩만 지나서 시작점으로 돌아올 수 있는 경로**(오일러 회로)를 가지는 그래프이다.
7. **완전 그래프 (Complete Graph)**:
    - **모든 정점이 서로 연결된 그래프**이다. `N`개의 정점이 있을 때, 모든 정점 쌍 사이에 간선이 존재한다.
    - **다이어그램**:
    
    ```mermaid
    graph TD;
        A---B;
        B---C;
        A---C;
    ```
    
8. **정규 그래프 (Regular Graph)**:
    - **모든 정점의 차수(연결된 간선의 개수)가 같은 그래프**이다.
9. **완전 이분 그래프 (Complete Bipartite Graph)**:
    - 두 집합의 모든 정점이 서로 연결된 **이분 그래프**이다.
10. **유향 비순환 그래프 (DAG, Directed Acyclic Graph)**:
    - **방향성이 있으면서 순환하지 않는 그래프**이다. 주로 작업 간의 **의존성**을 표현하는 데 사용된다.

## 그래프의 활용

**그래프**는 다양한 문제에서 유용하게 사용된다. 예를 들어:

- **경로 표현하기**: 도시 간의 이동 경로나 네트워크의 연결 상태를 나타낼 수 있다.
- **작업 의존 관계**: 작업의 순서와 의존 관계를 나타내기 위해 그래프를 사용한다. 예를 들어, 하나의 작업이 완료되어야 다음 작업이 시작될 수 있는 상황에서 그래프는 작업 간의 관계를 명확히 나타낸다.
- **실생활 문제**: 네트워크 라우팅, 지도 상의 경로 탐색, 소셜 네트워크 분석 등 다양한 분야에서 그래프가 사용된다.

## 그래프 관련 용어

- **인접 관계 (Adjacency)**: 두 정점이 간선으로 연결되어 있는 관계를 말한다.
- **연결 성분 (Connected Components)**: 서로 연결된 정점들의 집합을 말한다. 그래프가 여러 개의 연결 성분으로 나눠질 수 있다.
- **정점의 차수 (Degree)**: 한 정점에 연결된 간선의 개수이다. 무향 그래프에서는 들어오는 간선과 나가는 간선의 개수가 같지만, 유향 그래프에서는 **진입 차수**와 **진출 차수**로 구분된다.
- **다중변 (Multiedge)**: 두 정점 사이에 **복수의 간선**이 존재하는 경우를 말한다.
- **자기 루프 (Self-loop)**: 한 정점에서 자기 자신으로 연결된 간선이다.
- **최단거리 (Shortest Path)**: 두 정점 사이의 경로 중에서 **가장 짧은 경로**를 말한다. 최단 거리 문제는 그래프에서 자주 등장하는 문제로, 다익스트라 알고리즘이나 플로이드-워셜 알고리즘을 이용해 해결할 수 있다.

## 그래프 구현

그래프를 구현하는 방법 중 하나는 **인접 리스트 (Adjacency List)**를 사용하는 것이다. 각 정점에 번호를 부여하고, 그 정점과 인접한 정점의 번호를 리스트로 연결한다.

```cpp
#include <iostream>#include <vector>using namespace std;int main() {    // 정점 수와 간선 수    int V = 5;    // 인접 리스트 방식으로 그래프 구현    vector<vector<int>> adj(V);    // 간선 추가    adj[0].push_back(1);    adj[0].push_back(4);    adj[1].push_back(0);    adj[1].push_back(2);    adj[2].push_back(1);    adj[2].push_back(3);    adj[3].push_back(2);    adj[3].push_back(4);    adj[4].push_back(0);    adj[4].push_back(3);    // 출력    for (int i = 0; i < V; i++) {        cout << "정점 " << i << "에 인접한 정점: ";        for (int j : adj[i]) {            cout << j << " ";        }        cout << endl;    }    return 0;}
```

## 그래프 탐색 알고리즘

그래프에서 가장 자주 사용되는 알고리즘 중 하나는 **정점 탐색**이다. **깊이 우선 탐색(DFS)**과 **너비 우선 탐색(BFS)** 두 가지 방법이 있다.

1. **깊이 우선 탐색(DFS, Depth First Search)**:
    - 한 정점에서 **가능한 깊이까지 내려간 후** 더 이상 갈 수 없을 때 **다시 돌아오면서** 다른 경로를 탐색하는 방식이다.
    - **재귀 호출** 또는 **스택**을 사용하여 구현할 수 있다.
2. **너비 우선 탐색(BFS, Breadth First Search)**:
    - **가까운 정점부터** 차례대로 탐색하는 방식이다. 시작 정점에서 가까운 정점들을 먼저 탐색한 후, 그 다음으로 가까운 정점들을 탐색한다.
    - **큐**(Queue)를 사용하여 구현하며, **최단 경로**를 찾는 문제에서 자주 사용된다.

```cpp
#include <iostream>#include <vector>#include <queue>using namespace std;// BFS 알고리즘 구현void bfs(int start, vector<vector<int>>& adj, int V) {    vector<bool> visited(V, false);  // 방문 여부    queue<int> q;    visited[start] = true;    q.push(start);    while (!q.empty()) {        int node = q.front();        q.pop();        cout << node << " ";        for (int next : adj[node]) {            if (!visited[next]) {                visited[next] = true;                q.push(next);            }        }    }}int main() {    int V = 5;    vector<vector<int>> adj(V);    adj[0].push_back(1);    adj[0].push_back(4);    adj[1].push_back(0);    adj[1].push_back(2);    adj[2].push_back(1);    adj[2].push_back(3);    adj[3].push_back(2);    adj[3].push_back(4);    adj[4].push_back(0);    adj[4].push_back(3);    cout << "너비 우선 탐색(BFS) 결과: ";    bfs(0, adj, V);    cout << endl;    return 0;}
```

## 요약

- **그래프**는 **정점(Vertex)**과 **간선(

Edge)**으로 구성된 네트워크 구조이다.

- **그래프의 종류**: 무향, 유향, 가중치 그래프, 이분 그래프, 평면 그래프, 오일러 그래프, 완전 그래프 등 다양한 형태의 그래프가 있다.
- **그래프의 활용**: 경로 탐색, 작업 의존성 분석 등 다양한 문제 해결에 이용된다.
- **그래프 탐색 알고리즘**: 깊이 우선 탐색(DFS)과 너비 우선 탐색(BFS)은 그래프에서 자주 사용되는 탐색 기법으로, 각각 다른 상황에 맞는 유용한 방법이다.