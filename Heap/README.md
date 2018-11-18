# Heap

#### Stack이나 Queue와 같이 원소를 저장하는 어떤 공간을 뜻한다.



### 정의

- key 값을 가진 원소를 저장, 불러오는 공간.

- 가장 큰 key값을 가진 원소를 가장 먼저 불러온다.

  - key : 어떤 원소를 구분하는데 쓰이는 값 (고유한 값이어야 한다.)

- **Complete tree의 구조를 가진다.**

  - parent의 key값이 child의 key값 보다 **항상 크다.**

  - parent와의 관계만 성립한다면, 동일 level상의 관계는 신경쓸 필요가 없다

    (left, right가 따로 존재하지 않는다.)

### unordered array, ordered array, heap 의 time complexity비교

|            |                     **Unordered**                     |                         **Ordered**                          | **Heap** |
| :--------: | :---------------------------------------------------: | :----------------------------------------------------------: | :------: |
| **Insert** |         O(1) : 무작위로 집어넣기만 하면 된다.         |    O(n) :  처음부터 scan하며 insert할 위치를 찾아야 한다.    | O(log n) |
| **Delete** | O(n) : 처음부터 scan하며 delete할 위치를 찾아야 한다. | O(1) : 이미 정렬되어 있기때문에, delete하고자 하는 값을 바로 가져올 수 있다. | O(log n) |



### 표현

- complete한 tree이므로, **Array**를 사용하는 것이 적합하다.

- Array 0번째 원소는 사용하지 않는 것을 규칙으로 한다.

- Array 1번째 원소는 항상 **Root**를 저장하는데 사용한다.

  ###### [그림](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)을 통해 더욱 구체적으로 Heap의 구성이 어떻게 되는지 살펴보자.

  ![img](https://gmlwjd9405.github.io/images/data-structure-heap/heap-index-parent-child.png)

- i번째 원소의 left child : Array ( 2*i )번째 원소

- i번째 원소의 right child : Array ( 2*i +1 )번째 원소

- i번째 원소의 parent : ( i/2 )번째 원소 

  ###### parent는 정수형 나눗셈으로, 소숫점 밑의 자리는 내림한다. 



### 연산

- 먼저, heap 구현을 위해 element를 정의하는 class와 heap을 정의하는 class, 2개의 class를 생성하자.

  ```c++
  #include <iostream>
  #include <iomanip>
  #include <string>
  using namespace std;
  
  #define HSIZE 100
  
  class element{
  	public:
  		int key;
  		int data;
  		
  		element(){
  			key = 0;
  			data = 0;
  		}
  		
  		element(int k, int d){
  			key = k;
  			data = d;
  		}
  		
  		void set_data(int k, int d){
              key = k;
  			data = d;
  		}
  };
  
  
  class myheap{
  	public:
  		element h[HSIZE];
  		int csize;								//현재 원소의 갯수(= 현재 array size) 
  		
  		myheap(){
  			csize = 0;
  		} 
  		
  		void push(element t);
  		element pop();
  		
  		/*subtree를 재구성 하는 함수는 다음기회에 정의하자*/ 
  		/* void adjust(int troot); */			
   };
  ```


- 원소 추가(Push)

  - 새로운 node를 heap의 마지막에 삽입한 후, 작은 key 값을 발견하면 끌어내리고, 큰 key 값을 발견하면 root에 추가한다.
  - 현재 size가 n인 heap의 원소 추가
    1. error처리를 위한 full test
    2. insert
       1. size를 1 증가시킨다.
       2. 끝 node를 기준으로 넣으려는 원소의 key값과 parent의 key 값을 비교하여
          - parent의 key 값이 작으면, parent의 값을 child에 넣고, 위 과정을 반복한다.
          - parent의 key 값이 크면, 현 위치에 해당 원소를 넣고 종료한다.
          - 더이상 parent가 없으면(root를 발견하면) 종료한다.

  ![img](https://gmlwjd9405.github.io/images/data-structure-heap/maxheap-insertion.png)

  그림 참조는 [heejeong님의 blog](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)



  - Push Algorithm

    ```c++
    void myheap::push(element t){
    	int k;
    	
    	if(csize == HSIZE-1) {
    		cout << "\n Heap array is Full!\n";			//full test
    		return; 
    		}
    	
    	csize++ ;
    	k = csize;										//k는 끝원소의 위치를 가르킨다
    	
    	while((k != 1)&&(t.key > h[k/2].key)) {			//k가 끝 원소에 도달하지 않았고, parent의 key값이 자신(k)의 key값이 작다면 다음을 반복하라 
    		h[k] = h[k/2];								//heap의 k번째 원소(child)는 k의 parent원소로 대체한다. 
    		k /= 2;										//k를 2로 나눈다. (parent의 parent값(k의 ancestor값)을 k에 저장한 후 위의 과정을 반복한다.  
    	}
    	h[k] = t;										//현 위치에 해당 원소(t)값을 삽입한다. 
    }
    ```

- 원소 삭제(Pop)

  - Heap에 저장되어 있는 원소 중, 가장 큰 key값을 가진 원소를 삭제한다. heap에서 가장 큰 key값을 가진 node는 **Root**이므로, 삭제되는 원소는 root이다.

  - 그러나, 구조상  **heap의 가장 마지막 원소**가 삭제된다는 것을 주의해야 한다.

  - 현재 size가 n인 heap의 원소 삭제

    1. error처리를 위한 full test

    2. delete 과정

       1. n번째 원소(heap의 끝 node)를 기억할 변수 temp 선언
       2. return을 위한 root 원소 값 저장
       3. size를 1 감소시킨다.
       4. root부터 시작하여 아래쪽으로 다음을 반복한다.
          1. left 와 right의 key값을 서로 비교한다.
             - 이때, 만약 right에 node가 존재 한다면, 큰 key값을 가진 원소를 취한다.
          2. 큰 key값을 가진 원소와 temp값을 비교한다.
          3. temp값 보다 child가 크면, child를 parent 위치로 옮기고 child의 위치부터 위 과정을 다시 반복한다.
          4. child의 index가 size보다 커지면 종료한다.
          5. temp값 보다 child가 작거나, child가 없는 leaf 원소 이면 해당 위치에 temp를 넣는다.
          6. 저장했던 root 원소를 return하여 함수를 종료 한다.

       ![img](https://gmlwjd9405.github.io/images/data-structure-heap/maxheap-delete.png)

       그림 참조는 [heejeong님의 blog](https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html)

  - Pop Algorithm

    ```c++
    element myheap::pop(){
    	element deleted;
    	element tmp;
    	int parent, child;
    	
    	deleted = h[1];									//return을 위한 root원소 값 저장 
    	tmp = h[csize];									//끝 원소 저장 
    	
    	csize--;
    	parent = 1;
    	child = 2;
    	
    	while(child <= csize){												// child가 끝 원소에 도달하기 전까지 다음을 반복하라 
    			if((child < csize)&&(h[child].key < h[child+1].key))		//오른쪽 child가 있고, 오른쪽 child가 더 크면, 
    				child++ ;												//child를 1 증가 시킨다. (오른쪽 child값을 취한다.) 
    			if(tmp.key >= h[child].key)									//만약, temp의 key값이 child의 key값보다 더 크거나 같다면, 
    				break;													//loop문을 종료한다. 
    			else{														//이 외의 상황에서는 
    				h[parent] = h[child];									//child를 parent의 위치로 옮긴다. 
    				parent = child;											//parent는 현재 child가 되고 
    				child = parent*2;										//child는 현재 child(parent)의 left child가 된다. 
    			}
    	}
    	h[parent] = tmp;								//loop문을 통해 찾은 위치에 temp값을 넣는다. 
    	return deleted; 								//저장해두었던 root 원소를 return한다. 
    }
    ```


