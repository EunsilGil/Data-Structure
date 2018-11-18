# Graph Search

### 종류

* DFS (Depth First Search)
  * 깊이 우선 탐색
  * 시작점을 기준으로 가장 아래로 이동하면서 탐색한다.
  * Stack을 이용하여 Algorithm을 구현할 수 있다.
* BFS (Breadth First Search)
  * 너비 우선 탐색
  * 같은 level에 있는 vertex들을 모두 탐색한 후에 그 다음 level을 탐색해간다.
  * Queue를 이용하여 Algorithm을 구현할 수 있다.

------------

### Algorithm

![img](https://t1.daumcdn.net/cfile/tistory/26048A485823286B39)

* 위의 그림에서의 Searching 순서
  * DFS : 1 - 2 - 3 - 5 - 6 - 7 - 9 - 10 - 8 - 4
  * BFS :  1 - 2 - 3 - 4 - 5 - 6 - 7 - 8 - 9 - 10
  * **Graph는 왼쪽과 오른쪽의 개념이 없으므로, 다른 답들이 충분히 나올 수 있다는 점에 유의해야 한다.**
  * 더욱 구체적으로 searching 순서에 따른 stack or queue의 변화를 보고 싶다면, [Crocus page의 DFS](https://www.crocus.co.kr/520?category=209527) 또는 [Crocus page의 BFS](https://www.crocus.co.kr/521?category=209527)를 참고하자.

#### DFS Algorithm

1. start vertex를 traverse하고, stack에 넣는다.
2. stack top원소와 adjacent한 vertex중에 아직 traverse하지 않은 vertex를 한 개 선택하여 traverse하고, stack에 넣는다.
3. stack top원소와 adjacent한 vertex가 더이상 없으면
   1. stack의 원소들을 pop하고, 위의 과정을 반복한다.
   2. stack이 empty이면 종료한다.

#### BFS Algorithm

1.  DFS의 stack을 queue로 바꾸어 생각하면 BFS가 된다.
2. stack의 top을 queue의 front(꺼낼 곳)으로 설정한다.

###### BFS의 부족한 개념들은 다음에 다시 언급하도록 하겠다.



