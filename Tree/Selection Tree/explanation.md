# Selection Tree

### 정의

* Selection Tree는 Complete binary tree이다.
* k개의 ordered sequence를 한 개의 ordered sequence로 merge(병합)한 것
* 즉, 이미 크기 순으로 나열되어 있는 k개의 sequence를 합쳐서, 크기 순으로 다시 나열하는 것

###### k개의 sequence를 한 줄씩 계속 훑어가며 merge하는 것은 너무 비효율 적이라는 생각에서 출발



### 종류

* Winner Tree
  * 각 sequence의 첫 원소들이 key값이 되어 selection tree의 **leaf node**가 된다.
  * 토너먼트 형식에 따라 서로 다른 2개 tree의 key 값을 비교하여 더 작은 key값이 winner가 된다.
  * 따라서, root node는 **Tree에서 가장 작은 key 값을 가진 node**가 된다.

![img](http://www.icodeguru.com/vc/10book/books/book1/394_a.gif)

* Loser Tree
  * 각 sequence의 첫 원소들이 key값이 되어 selection tree의 **leaf node**가 된다.
  * Winner Tree의 문제점을 보완하고자 만들어졌다.
    * winner tree에서 가장 작은 key값을 가진 원소를 찾기 위해서는 sibling node들 끼리의 비교가 필요하지만, loser tree에서는 parent와의 비교로 root node를 찾을 수 있기때문에 훨씬 간편하다.
  * Loser Tree에 표시되어 지는 값은 loser이지만, 실제 winner는 더 작은 숫자이며, winner를 표시하기 위한 node가 추가적으로 필요하다.

![img](http://www.icodeguru.com/vc/10book/books/book1/396_a.gif)

#### Reference

http://www.icodeguru.com/vc/10book/books/book1/chap08.htm

http://www.engineering-bachelors-degree.com/algorithm/uncategorized/treestournament-trees/
