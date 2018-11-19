# Activity NetWork

### AOV network (Activity On Vertex)

* 정의

  * vertex가 task(또는 activity)를 의미
  * directed edge는 tack간의 선후 관계를 의미한다.

* Topological sort

  * cycle이 없는 directed graph여야 한다.

  * topological order를 찾는 방법

  * topological order : AOV network에서 predecessor와 successor의 관계를 유지하는 a linear order

   * **A ---> B**에서    A 는 B의 predecessor,   B 는 A의 successor 이다. 

  * 방법

   1. predecessor를 갖지 않는 vertex를 한 개 선택하고, 그 vertex와 그의 모든 outgoing edge를 제거한다.

   2. 1번을 n번 반복한다.



     * topological sort의 방법은 모두 몇가지인지 알기 위해서 수형도를 그려볼 수 있다.

    ![Directed acyclic graph 2.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/0/03/Directed_acyclic_graph_2.svg/180px-Directed_acyclic_graph_2.svg.png)이 [graph](https://en.wikipedia.org/wiki/Topological_sorting)의 topological sort는 총 **6가지**이다.

    * 5, 7, 3, 11, 8, 2, 9, 10 

    - 3, 5, 7, 8, 11, 2, 9, 10 
    - 5, 7, 3, 8, 11, 10, 9, 2 
    - 7, 5, 11, 3, 10, 8, 9, 2 
    - 5, 7, 11, 2, 3, 8, 9, 10 
    - 3, 7, 8, 5, 11, 10, 2, 9 

### AOE network (Activity On Edge)

* 정의

  * edge가 task(또는 activity)를 의미한다.
  * vertex는 activity의 종료를 의미하는 event이다.
  * 주로 작업 공정을 설명할 때 사용될 수 있다.

* 용어

  * critical path : a path that has the largest length

  * ealist time 

    * 어떤 event(vertex)의 의미가 이루어지기 위한 최소한의 시간
    * 어떤 activity를 시작할 수 있는 최소한의 시간
    * start vertex로부터 largest path의 length
    * **빠르면 (          ) 안에 시작할 수 있다.**

  * latest time

    * 어떤 activity의 시작을, 전제 project의 소요시간을 지연시키지 않는 범위 내에서 늦출 수 있는 최대한의 시간
    * **늦어도 (          ) 전에 시작해야 한다.**

    ###### [그림](http://blog.naver.com/PostView.nhn?blogId=heojh93&logNo=220019810426&parentCategoryNo=&categoryNo=12&viewDate=&isShowPopularPosts=true&from=search)을 통해 자세하게 알아보자.

    ![img](http://postfiles6.naver.net/20140603_37/heojh93_1401806517312VbOhL_PNG/q2.PNG?type=w1)

  * V3의 earlist time : V3은 a2가 지난 후 시작할 수 있으므로, **8**

  * V3의 latest time : 전체 공정시간(critical path) - 남은 공정시간 = (a0+a3+a6+a8) - (a5+a9) = 21-6 = **15** 

