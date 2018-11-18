# Tree

### 계층적 구조의 표현을 위해 사용된다.  

#### 정의

- 유한개(>=1)의 node로 이루어지면, 다음 조건을 만족한다.
  - root라는 특별한 node가 있음.
  - root는 subtree라고 부르는 n개(>=1)의 disjoint set으로 구성되어 있다.
    - 각 subtree는 tree의 정의를 만족한다.

#### 용어

- Node : tree에서 data를 저장하는 기본 단위 원소

- Branch : node와 node간의 연결 (관계가 있음을 나타내는 것)

- Degree

  - Degree of a node : the **number of subtrees** of the nodes
  - Degree of a tree : the **maximum** degree of the node in the tree

- Root : 가장 상위 **한개** node

- Leaf(= terminal node) : degree가 0인 node (child가 없는 node)

- Internal node : degree가 0보다 큰 node

- Level : root를 level 1이라 가정했을 때, root와 어떤 node간의 상대적 거리

- Height (=Depth) : maximum level of the tree

- Node간의 관계를 정의하는 용어들

  ```
  Parent : 직속 연결 된 상위 Node
  Child(Children) : 직속 연결된 하위 node
  
  Ancestors 
  Descendants
  
  Siblings : 동일 parent를 갖는 nodes
  ```

  ##### Tree는 직관적인 이해가 필수적이므로, 그림으로 이해해보자. 

![03B65E65-8752-4D4E-9E43-48CA9D04F85C](https://farm5.staticflickr.com/4482/36997131684_89ddd642cf_o.png)

​							(그림 출처는 [Jiwon 님의 Blog](https://jiwondh.github.io/2017/10/15/tree/) )

- A는 tree의 root 
- degree of a tree는 **3** (B의 degree가 tree의 maximum degree이다.)
- degree of  **C** 는 **2**
- tree의 depth는 **4**
- C는 subtree가 있으므로, **internal node** 이다.
- I, J, K, L, M, N은 **leaf node (terminal node)** 이다.
- A는 I의 **ancestor**, I는 A의 **descendant**
- D와 E는 **sibling**
- G는 L의 **parent**, L은 G의 **child**



# Binary Tree

##### 정의

- 유한개 (>= 0)의 node로 구성 (root가 없는 것도 binary tree로 인정)
  - root와 2개의 disjoiint binary tree로 구성
  - 두 개의 subtree, **left subtree/ right subtree**를 갖는다.         

##### 특징

- level i 에서의 최대 node 수? 

  - 2^(i-1) 개           

- depth 가 k인 binary tree의 최대 node 수?

  - 2^k - 1개

- n0 : leaf node의 수, n2 : degree가 2인 node의 수 일때

  binary tree는 **n0 = n2 + 1** 를 만족한다.

  - 예시 : 90개의 team이 토너먼트로 게임을 한다면, 1등이 나올 때 까지 총 89회의 게임을 해야한다.

##### complete binary tree

- level 순서대로, 동일 level에서는 left -> right 순으로 채워진 binary tree

##### full binary tree

- 빈틈없이 모두 채워진 binary tree

###### complete binary tree와 full binar tree는 동일 level에서는 유일한 형태로 나타난다.

​										**Complete** Binary Tree

![?](http://web.cecs.pdx.edu/~sheard/course/Cs163/Graphics/CompleteBinary.jpg)

![?](http://web.cecs.pdx.edu/~sheard/course/Cs163/Graphics/FullBinary.jpg)

​									(그림 출처는 [wikipedia](http://web.cecs.pdx.edu/~sheard/course/Cs163/Doc/FullvsComplete.html))



# Binary Search Tree

##### 정의

- a Binary tree
- Maybe empty
- Empty가 아닌 경우, 다음을 만족한다.
  - 각 node는 1개의 key값을 가진다. (모든 node의 key값은 고유하다.)
  - **left subtree**에 속한 모든 node의 key값은 root의 key값 보다 **작다**.
  - **right subtree**에 속한 모든 node의 key값은 root의 key값 보다 **크다**.
  - subtree는 Binary search tree이다.

###### Searching을 node의 수 만큼 하는 것이 아니라, depth만큼만 하면 된다는 간편함이 있다.

- 대상 공간을 1/2씩 줄여나가기 때문에 최대 **log n** 번 만에 찾을 수 있다.  



##### 연산

###### 연산에 앞서, readablity를 높이기 위해 Node를 정의하는 Class와 Tree를 정의하는 Class, 2개의 Class를 먼저 구현하자.

```C++
#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

#define LEFT 5
#define RIGHT 6

class BstNode{
	public :
		int key;
		int data;
		void set_data(int k, int d){
			key = k;
			data = d;
		}
		BstNode *left, *right;
};

class BstTree{
	public :
		BstNode *root;
		BstTree(){								//constructer 
			root = NULL;
		}
		bool insert_node(BstNode t);
		int num_nodes();
		void traverse();
		int data_sum();
};

int count_by_recursion(BstNode *p);
int sum_by_recursion(BstNode *p);
void inorder_traverse(BstNode *p);
void preorder_traverse(BstNode *p);
void postorder_traverse(BstNode *p);
```



- Insert

  1. key 값을 넣을 위치를 찾는다.

  2. 그 곳에 넣는다.

     ```c++
     bool BstTree::insert_node(BstNode t){
     	BstNode *temp, *tparent, *lchild, *rchild;
     	int lrcheck;
     	int thekey = t.key;
     	
     	temp = new BstNode;
     	*temp = t;
     	temp->left = NULL;					//새로운 node는 leaf node이다 
     	temp->right = NULL;
     	
     	if(root==NULL){						//초기 empty상황에서의 추가 
     		root = temp;
     		return true;
     	} 
     	
     	//초기 상황이 empty가 아니라면 다음과 같이 initializing 해준다. 
     	tparent = root;						
     	lchild = tparent->left;
     	rchild = tparent->right;
     	
     	while(1){
     		if(tparent->key==thekey)			//tparent의 key값과 thekey값이 같다면 
     			return false;					//실패 
     			
     		if(tparent->key>thekey){			//tparent의 key값이 thekey값보다 크고 
     			if(lchild == NULL){				//1.child가 없을 때 
     				lrcheck = LEFT; 			//성공 -> left에 넣으면 된다. 
     				break;
     			}
     			else if(lchild->key == thekey)	// 2.child의 key값과 thekey값이 같을 때 
     				return false;				// 실패 
     			else{							// 3.child가 있을 때 
     				tparent = lchild;			//tparent, lchild, rchild값을 다시 설정해준다. 
     				lchild = tparent->left;
     				rchild = tparent->right;
     			}
     		}
     		else{								//tparent의 key값이 thekey값보다 작을 때 
     			if(rchild == NULL){				//위와 같은 과정을 반복 
     				lrcheck = RIGHT;			// 성공시 lrcheck의 값을 RIGHT로 바꿔준다. 
     				break;
     			}
     			else if(rchild->key == thekey)
     				return false;
     			else{
     				tparent = rchild;
     				rchild = tparent->right;
     				lchild = tparent->left;
     			}
     		}
     	}
     	if(lrcheck == LEFT)	 					//lrcheck가 LEFT라면 
     		tparent->left = temp;				//loop문 이후에 바뀐 tparent의 left에 temp값을 입력한다. 
     	else									//lrcheck가 RIGHT라면 
     		tparent->right = temp;				//loop문 이후에 바뀐 tparent의 right에 temp값을 입력한다. 
     	return true;
     } 
     ```

- Delete

  - Delete하고자 하는 node가 

  1. terminal node이면, parent의 해당 link를 *NULL*로 처리한다.

     ![img](https://t1.daumcdn.net/cfile/tistory/990B3B33598965B71D)

  2. child가 1개인 node이면, parent의 해당 link를 child로 연결한다.

     ![img](https://t1.daumcdn.net/cfile/tistory/99594633598965C009)

  3. child가 2개인 node이면, 해당 node를

     - left subtree의 largest node로 대체하거나,

     - right subtree의 smallest node로 대체한다.

       ![img](https://t1.daumcdn.net/cfile/tistory/99CE0533598965C701)

       (Delete연산을 설명하는 모든 그림의 출처는 [wisecow님의 blog](http://mattlee.tistory.com/30))

- Search

  Binary Search Tree의 searching방법은 [Sorting](https://github.com/EunsilGil/Data-Structure/Sorting/explanation.md)에서 다루도록 하겠다. 



- Recursion을 활용한 추가 연산

  - Tree의 모든 node 갯수를 세는 program

  - 모든 node의 data값의 합을 구하는 program 등, 다양한 알고리즘을 구현 할 수 있다

    ```c++
    //Recursion Function to count nodes
    int BstTree::num_nodes(){
    	return count_by_recursion(root);
    }
    
    int count_by_recursion(BstNode *p){
    	if(p == NULL)
    		return 0;
    	return count_by_recursion(p->left) + count_by_recursion(p->right) + 1;					//root의 left, right의 node갯수 + 자기자신 
    }
    
    //Recursion Function to sum data of all nodes
    int BstTree::data_sum(){
    	return sum_by_recursion(root);
    } 
    
    int sum_by_recursion(BstNode *p){
    	if(p == NULL)
    		return 0;
    	return sum_by_recursion(p->left) + sum_by_recursion(p->right) + p->data;
    ```

## Traversal

- Travers 방법에는 4가지 방식이 있다.
  - inorder		:  Left subtree -> **Root(Domain)** -> Right subtree 
  - preorder        : **Root(Domain) **-> Left subtree -> Right subtree
  - posrtorder     :  Left subtree -> Right subtree -> **Root(Domain)**
  - level - oreder : Root(Domain)부터 level 순서대로, 동일 level에서는 left먼저 travers하는 방식

###### level - order를 제외한 3가지 방법에 대하여 그림과 함께 알아보자.

![Example Tree](https://www.geeksforgeeks.org/wp-content/uploads/2009/06/tree12.gif)

[Example Tree]![Example Tree](https://www.geeksforgeeks.org/wp-content/uploads/2009/06/tree12.gif)

- Inorder : 4 - 2 - 5 - 1 - 3
- Preorder : 1 - 2 - 4 - 5 - 3
- Postorder : 4 - 5 - 2 - 3 - 1	

![img](https://t1.daumcdn.net/cfile/tistory/223AE24F573DB3FD0B)

![img](https://t1.daumcdn.net/cfile/tistory/2522554F573DB3FD26)

![img](https://t1.daumcdn.net/cfile/tistory/2522554F573DB3FD26)

###### 위의 [그림](https://www.crocus.co.kr/348?category=150836)과 같은 방식으로 traversal 할 수 있으며, 다음 예제를 통해 조금 더 정확하게 이해해보자.

![kakaotalk_20181118_193649753](https://user-images.githubusercontent.com/44895889/48672086-bb8b4380-eb74-11e8-90cf-99f641095b13.jpg)




- 연산

  - Treversal 연산들은 Recursion Function으로 구현할 수 있다.
  - Traversal 방법(Inorder, Preorder, Postorder)에 따라, 순서만 바꿔주면 된다.

  ```C++
  //Recursion Function to traverse
  void BstTree::traverse(){
  	cout << "\nInorder Traversal Result is... \n";
  	inorder_traverse(root);
    	cout << "\nPreorder Traversal Result is... \n";
    	preorder_traverse(root);
    	cout << "\nPostorder Traversal Result is... \n";
    	postorder_traverse(root);
  }
  
  void inorder_traverse(BstNode *p){			 //inorder 
  	if(p == NULL)
  		return;
  	inorder_traverse(p->left);				//left 먼저 
  	cout<< " " << p->key <<"\t";			//자기자신 
  	inorder_traverse(p->right);				//right 나중에 
  }
  
  void preorder_traverse(BstNode *p){			//preorder
  	if(p == NULL)
  		return;
  	cout<< " " << p->key <<"\t";			//자기자신 먼저 
  	preorder_traverse(p->left);				//left
  	preorder_traverse(p->right);			//right
  }
  
  void postorder_traverse(BstNode *p){		//postorder 
  	if(p == NULL)
  		return;
  	postorder_traverse(p->left);			//left 먼저 
  	postorder_traverse(p->right);			//right	
  	cout<< " " << p->key <<"\t";			//자기자신 나중에 
  ```

##### Expression Tree

###### Arithmetic expression을 Binary tree로 표현

- 정의 

  - internal node : **Operator**를 의미한다.
  - leaf node : **Operand**를 의미한다.
  - **Subtree** 연산의 우선순위가 높다.

- 예제

  ![img](https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/Exp-tree-ex-11.svg/250px-Exp-tree-ex-11.svg.png)

  [Expression tree]![img](https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/Exp-tree-ex-11.svg/250px-Exp-tree-ex-11.svg.png)

  - inorder : (((a + b) * c) + 7)

  - preorder : + * + a b c 7

  - postorder : a b + c * 7 +

    **즉, Expression 의 결과는 Treversal의 결과와 동일하다.**



