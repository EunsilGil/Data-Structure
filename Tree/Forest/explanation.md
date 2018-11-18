# Forest

### 정의

* n개(>=0) 의 disjoint tree의 모임

  ![disjoint tree forestì ëí ì´ë¯¸ì§ ê²ìê²°ê³¼](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRgK6k3P7PyhM05vhGXB1H08nrzsLAXqA4AEvg4eoO4C0V41qq_gA)

  # 카탈란 수

* n개의 node를 가지는 binary tree의 형태는 [카탈란수](https://ko.wikipedia.org/wiki/%EC%B9%B4%ED%83%88%EB%9E%91_%EC%88%98)로 정의 된다.

  ![kakaotalk_20181119_033337663](https://user-images.githubusercontent.com/44895889/48676590-1b511100-ebac-11e8-8dd1-0147d79bf870.jpg)



  * 즉, ![img](https://t1.daumcdn.net/cfile/tistory/22015249550A1D4007) 이다.

* 예제 1
  * Stack permination 
    * 철도를 예를 들어 설명해 보자.
    *  기차는 왼쪽에서 오른쪽 방향으로 이동하며, 각 기차는 stack에 들어가거나, 그냥 지나칠 수 있다.
    * Stack에 들어간 후에는 stack의 정의에 따라(First In Last Out) 가장 나중에 들어간 것이 가장 먼저 나올 수 있다.
    * n의 갯수에 따라 output의 경우의 수가 몇가지 인지 구하는 문제이다.

![kakaotalk_20181119_034507790](https://user-images.githubusercontent.com/44895889/48676687-9109ac80-ebad-11e8-93bf-0fa7b3ba2412.jpg)

* 예제 2
  * (n + 1)개의 matrix를 곱하는 방법의 수

   ![kakaotalk_20181119_035136196](https://user-images.githubusercontent.com/44895889/48676753-74ba3f80-ebae-11e8-9529-53d23d514211.jpg)

###### 위의 3 문제는 모두 **equvelent**하다.

* 이 외의 카탈란 수의 응용은 [yaraba님의 blog 6번 문제](http://yaraba.tistory.com/78)를 참고하길 바란다.





​	
