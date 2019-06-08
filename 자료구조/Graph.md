# Graph
= Vertex와 Edge(Vertex와 Vertex를 잇는)의 집합.

## 종류

  - Undirected Graph = 방향성이 존재하지 않음.
  - Directed Graph = 방향성이 존재함.

## 용어
  - vertex : 점 = Node
  - edge : 변
  - 인접 노드 : edge로 연결된 Vertex
  - 경로 : 하나의 vertex에서 다른 vertex로 이동하기위한 vertices의 집합.
  - Complete Graph : 모든 vertices가 연결된 그래프
  - 가중치 : edge가 갖는 값. 도형에서는 변의 길이가 될 수 있다.
  
## Program으로 표현하기

### 배열로 표현(Adjacency matrix)
Vertices는 1차원 배열로 표현하고, Edge의 값을 저장하는 2차원 배열로 표현하는 것이 일반적이다.

Edge의 행,열은 각 각 Vertex를 의미하고, 행,열의 교차점은 edge의 weight 값이 들어간다.(연결이 없다면, 0)

### list로 표현하기
Vertices는 1차원 배열로 표현하고, 인접한 모든 vertex를 list로 연결한 형태.

list에서는 우선 순위가 없고, 어느 vertex에서 연장되었는지가 중요하다.

