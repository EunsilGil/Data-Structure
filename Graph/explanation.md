# Graph

### 형태

* vertex와 edge의 임의의 연결로 이루어진 형태

### 기본 용어

* G라는 group
* V(G) : vertex의 집합 (like node)
* E(G) : edge의 집합 (like branch)

--------

### 표현 방법

![img](https://i.imgur.com/SYsNnEB.png)

그림 참조는 [ratsgo님의 블로그](https://ratsgo.github.io/data%20structure&algorithm/2017/11/18/graph/)

##### Graph에는 위상이 존재하지 않는다. 따라서 Graph를 공부할 때는 Tree와 헷갈리지 않도록 유의해야한다.

---------

### Directed Graph

* 방향성이 존재하는 Graph
* Directed Graph의 edge는 <tail, head> 로 표기한다.
  * 화살표가 향하는 방향이 head, 화살표의 시작이 tail

------------

### Full connected graph

* n개의 vertex가 있는 **full connected praph**라면, edge는 ![20181119041353](https://user-images.githubusercontent.com/44895889/48676969-910bab80-ebb1-11e8-9de3-4cd4471cf84e.png)개가 존재한다.
* 따라서 총 edge의 갯수는 ![20181119041202](https://user-images.githubusercontent.com/44895889/48676970-936e0580-ebb1-11e8-8f7a-a8e4d59a8686.png)개가 된다.
  * Domain과 관계된 node의 갯수가 n-1개, 모든 node에 적용하므로 n*(n-1)
  * 전체 node에 대하여 이중으로 계산되므로 /2 해준다.
  * 만약, **directed graph**라면, **n*(n-1)**개의 edge가 생긴다.

---------

### 용어

* path(경로) : 두 vertex간에 edge로서 연결되는 vertex의 sequence
  * simple path : 처음과 끝을 제외한 path 상의 node가 고유한, cycle이 없는 path
* cycle : 처음과 끝이 동일 node인 simple path
* adjacent(인접한) : 두 vertex 간의 edge가 존재함을 의미하는, vertex 사이의 직접 연결되어있는 path
* connected : 두 vertex간의 path가 존재함을 의미한다.
  * adjacent한 것은 connected의 special case
* strongly connected : directed graph에서 양뱡향 path가 존재함을 의미
* incident : vertex와 edge를 설명할 때 사용한다.
  * e1은 v1에 incident하다.
* degree of a vertex : 어떤 한 vertex에 incident한 edge의 수
  * in directed graph
    * indegree : incomming edge의 수
    * outdegree : outgoing edge의 수
* length of a path : path를 구성하는 edge의 갯수
  * 자기자신까지의 거리는 0 이 타당하기때문에 vertex(node)의 수를 세는 것이 아니라, edge의 수로 정의한다.

-------

### 표현

* adjacency matrix

  ![AdjacencyMatrix](http://mathworld.wolfram.com/images/eps-gif/AdjacencyMatrix_1002.gif)

  그림 참조는 [MathWorld](http://mathworld.wolfram.com/AdjacencyMatrix.html)

     * 방향성이 없는 그래프(Undirected graph)에서 는 metrix에 '1'의 갯수(edge의 수)가 **2배**로 나타난다.

    * undirected graph에서는 행과 열이 같은 경우(metrix의 대각선)을 기준으로 **대칭**을 이룬다.
    * directed graph에서 행은 **out degree**를, 열은 **indegree**를 나타낸다.

* adjacency list (linked list)

  * 각 vertex에 대하여 adjacent한 vertex들을 linked list로 연결
  * 각 vertex별로 존재하는 연결들의 모음이라고 생각하면 된다.
  * node의 갯수는 edge 수의 **2배**로 나타난다.

![img](https://t1.daumcdn.net/cfile/tistory/255D9035591DE4DF11)

그림 참조는 [12bme 님의 blog](https://12bme.tistory.com/123)

-----------

### Network

* weighted edge를 갖는 graph

  * weighted edge : 상대적 가중치를 가지는 edge

* 표현 방법

  * adjacency matrix의 data값을 weighted edge 값으로 표현

  [아래의 Graph](https://i.stack.imgur.com/ea2UI.png)를 metrix로 표현해 본다면 오른쪽과 같은 형태의 metrix를 만들 수 있다.![enter image description here](https://i.stack.imgur.com/ea2UI.png)                                   ![20181119061544](https://user-images.githubusercontent.com/44895889/48678150-9ae9da80-ebc2-11e8-9f97-2212a4808b05.png)

   * network 또한 undirected graph의 경우 대각선을 기준으로 **대칭**을 이룬다.

  --------------
