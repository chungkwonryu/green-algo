# 27. 그래프의 표현과 정의

## 그래프의 종류
그래프에도 다양한 종류가 있기 때문에, 문제에 알맞은 그래프 종류를 찾는게 중요하다  
- 방향 그래프
- 가중치 그래프
- 다중 그래프
- 루트 없는 트리
- 이분 그래프 (Bipartite Graph)
- DAG (Directed Acyclic Graph)

다양한 문제들을 풀면서, 이런 문제들도 그래프로 풀 수 있구나 하는 경험을 쌓는게 중요하다
- 철도망의 안정성 분석
- 소셜 네트워크 분석
- 인터넷 전송 속도 계산
- 한 붓 그리기
- 외환 거래
- 할 일 목록 정리 (e.g. 깊이 우선 탐색)
- 15-퍼즐
- 게임판 덮기 (e.g. 이분 그래프)
- 회의실 배정 = satisfiability problem

그래프는 어떻게 표현하는지에 따라 장단점이 있다
- 인접 리스트
  ```
  // 일반적인 경우
  vector<list<int>> adjacent;
  
  // 가중치가 있는 경우
  vector<list<pair<int,int>>> adjacent;
  ```
- 인접 행렬
  ```
  // 일반적인 경우
  vector<vector<bool>> adjacent;
  
  // 가중치가 있는 경우
  vector<vector<int>> adjacent;
  ```
- 암시적 그래프 표현
  하지만 반드시 명시적인 그래프로 표현해야 하는 건 아니다. 필요에 따라 더 간단하다면 암시적 표현으로도 할 수 있다.
  e.g. 칸으로 구성된 미로에서 최단 경로 찾기

# 28. 깊이 우선 탐색(DFS)

- 재귀를 통해 구현한 인접 리스트의 DFS
  ```
  vector<vector<int>> adj; //그래프의 인접 리스트
  vector<bool> visited; // 각 정점의 방문 여부

  void dfs(int here) {
    visited[here] = true;
    for (int i = 0; i < adj[here].size(); ++i) {
      int there = adj[here][i];
      if (!visited[there])
        dfs(there);
    }
    // 더이상 방문할 정점이 없는 경우
  }
  void dfsAll() {
    visited = vector<bool>(adj.size(), false);
    for (int i = 0; i < adj.size(); ++i)
      if (!visited[i])
        dfs(i);
  }
  ```

- 시간 복잡도
  - 인접 리스트를 사용한 경우 : O(|V| + |E|)  
  - 인접 행렬을 사용한 경우 : O(|V|^2)

- DFS를 활용할 수 있는 예시
  - 두 정점이 서로 연결되어 있는지 확인하기
  - 연결된 부분집합(component)의 개수 세기
  - 위상 정렬 (e.g. 깊이 탐색해서 먼저 끝나는 순서의 역순으로 배열)
