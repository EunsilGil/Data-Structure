# Spannig Tree

### 정의

* 원 graph의 모든 vertex를 포함하는 tree
  * tree : cycle이 없는 graph

![spanning treeì ëí ì´ë¯¸ì§ ê²ìê²°ê³¼](https://www.tutorialspoint.com/data_structures_algorithms/images/spanning_trees.jpg)

사진 참조는 [tutorials point](https://www.tutorialspoint.com/data_structures_algorithms/spanning_tree.htm)

  * 만약 vertex의 수가 n개라면, edge는 (n-1)개 존재한다.

### DFS Spanning Tree & BFS Spanning Tree

* 각각의 Spanning Tree는 Searching 하는 순서에 따라 그려진다.

-----------

### Connected component

- 정의 
  - 원 graph의 부분 graph를 **component **라고 하고, component에 속한 모든 node에 대해 path가 존재하는 부분 graph를 **connected component**라고 한다.
  - connected graph의 connect component는 **1개** 이다.

### Biconnected component

* 정의

  * articulation point를 갖지 않는 maximal connected component
    * articulation point : 제거했을 때, 두 개 이상의 connected component로 분리되는 vertex



  ![Biconnected1](https://www.geeksforgeeks.org/wp-content/uploads/Biconnected1-300x177.png)        ![Biconnected4](https://www.geeksforgeeks.org/wp-content/uploads/Biconnected4-300x160.png)

  두 개의 graph를 보고 정확하게 이해하자. **articulation point가 없는** 것이 biconnected component이다.

----

## Minimum Cost Spannig Tree

### 정의

* weighted graph에서 weight(cost)의 합이 최소가 되는 spanning tree

### 제약조건

1. graph에 속한 edge만으로 구성되어야 한다.
2. (n-1)개의 edge를 가진다
3. tree의 구조를 가지므로, cycle이 없어야 한다.

### Algorithm

* minimum cost spanning tree의 3가지 Algorithm에 대하여 소개하겠다.
* 3가지의 알고리즘은 점차적으로 발전하는 형태이다.
* vertex가 선택되는 순서는 다를 수 있지만, 3가지 Algorithm의 결과는 유일하게 나타난다.

1. Kruskal's Algoritnm

   1. 전체 edge를 cost순서대로 취하여

      * cycle을 이루지 않으면 accept
      * cycle을 이루면 reject
   2. (n-1)개의 edge가 선택될 때까지 1번을 반복한다.

   ![k](https://user-images.githubusercontent.com/44895889/48679781-b4e1e800-ebd7-11e8-9a39-88c37b3ea8cd.png)

   * 단점 : graph전체를 sorting 해야한다

2. Prim's Algorithm

   1. 첫번째(start)  vertex부터 시작하여 현재 connected component와 **외부를 연결하는 edge**중에서 최소 cost edge를 취해 나간다.
   2. (n-1)개의 edge가 선택될 때까지 1을 반복한다.

   ![p](https://user-images.githubusercontent.com/44895889/48679778-b27f8e00-ebd7-11e8-9af5-b370e1fa3301.png)

3. Sollin's Algorithm

   * 초기에 각 vertex를 개별 tree로 하는 forest를 고려
   * 동시 다발적으로 parallel processing 한다.

   1. 각 tree로 부터 외부로 연결된 edge 중에서 최소 cost edge를 선택하여 tree를 확장시킨다.

      (단계별로 tree당 1개의 edge가 추가되도록)

   2. 전체가 하나의 tree로 결합될 때까지 반복한다.

   ![s](https://user-images.githubusercontent.com/44895889/48679776-b0b5ca80-ebd7-11e8-912c-f63a38da9e14.png)

   #### Reference

   * Text Book

     * 제목 : Fundamentals of Data Structures in C

     * 저자 : HOROWITZ, SAHNI, ANDERSON-FREED
