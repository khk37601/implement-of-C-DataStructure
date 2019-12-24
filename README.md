# 자료구조 
------------------------------------------------
## LinkedList  why use Double Pointer ?
```
이중포인터 사용 이유 ?

결국은 주소 문제 때문에 사용한다.

단일 포인터를 쓸경우 문제점을 보여 주는 예시이다.
i)
  List           haed           NewNode
---------       ------          -------
  NULL  |      | 0x01 |         | 117 |          *head 값은 NULL이다.
---------       ------          -------
  0X01           0x02            0x03 

head의 값이 NULL 이면 NewNode를 가르킨다.

if(head == NULL)
  head = NewNode;

  List           haed           NewNode
---------       ------          -------
  NULL  |      | 0x03 |------>  | 117 |       
---------       ------          -------
  0X01           0x02            0x03 

함수를 벗어 나면서 변수값은다  메모리를 반납 한다. 
문제 없이 진행 하는것처럼 보인다.

ii)

else
{
      Node *tail = head;
      while(tail != NULL)
      {
          tail = tail -> next;
      }

       tail->next =newNode;
 
}
                                  tail
  List           haed           frist_Node     NewNode
---------       ------          -------        ------
  NULL  |      | 0x03 |------>  | 117 |   ---> | 118 |
---------       ------          -------        ------
  0X01           0x02            0x03           0x04


하지만 우리가 원하는 것처럼 연결을 못하는 것뿐만 아니라 
head 노드를 접근 조차 할 수 없다.
그이유는 아직 head는 즉 List가 가지고 있는 주소값은 여전히 NULL 이기떄문이다.

그래서 우리가 이중포인터를 써야 하는이유 이다 List즉 head가 가지고 있는 주소를
바뀌기 위해서다.

append_node(Node **head , Node*newNode)
 
  if(*head == NULL)
  {
     *head = newNode;
  }

 *head : head를 통해서 역참조를 통해서 List가 가지고 있는 주소값을 NewNode의 
  주소값으로 변경 시켜 주는것이다.
  이렇게 하면 우리가 원하는 싱글리스트를 구현 할 수 있다.

                                  tail
  List           haed           frist_Node     NewNode
---------       ------          -------        ------
  0x02  |      | 0x03 |------>  | 117 |   ---> | 118 |
---------       ------          -------        ------
  0X01 |         0x02            0x03           0x04
       |          ^                 
       -----------|
```

### 큐
```
 큐의 자료구조 형태는 FIFO(first-in first-out)이다. 
 예제) A ,B, C 가 순서대로 들어 왔다고 가정 한다.
  ------------------
   A |  B   |  C  |
  -------------------
  나오는 순서는 A->b->C로 나오게 된다.
  
  큐는 두가지로  구현이 되어진다.
  1. 원형 큐
  2. 링크트 큐
  
  첫번째 원형큐는 배열 기반으로 만든다. 
  Rear : 입력 , Front : 출력 일때
  원형 큐가 가득 찼을 경우 어떻게 확인 할 수 있을 까?

```

### 스택
```
  스택의 자료구조 형태는 FILO(first-in Last-out)이다. 
 예제) A ,B, C 가 순서대로 들어 왔다고 가정 한다.
  ------------------
   A |  B   |  C  |
  -------------------
  나오는 순서는 c->b->a로 나오게 된다.
  
  큐는 두가지로  구현이 되어진다.
 
  스택 자료구조로 큐를 만들 수 있다.
 
```
### 트리
```
 
             2
        8           52
   13     37     67     161     
17   43  88  

노드와 간선으로 이루어진 자료구조이다.

루트 노드(root node): 부모가 없는 노드, 트리는 하나의 루트 노드만을 가진다.
단말 노드(leaf node): 자식이 없는 노드, ‘말단 노드’ 또는 ‘잎 노드’라고도 부른다.
내부(internal) 노드: 단말 노드가 아닌 노드
간선(edge): 노드를 연결하는 선 (link, branch 라고도 부름)
형제(sibling): 같은 부모를 가지는 노드
노드의 크기(size): 자신을 포함한 모든 자손 노드의 개수
노드의 깊이(depth): 루트에서 어떤 노드에 도달하기 위해 거쳐야 하는 간선의 수
노드의 레벨(level): 트리의 특정 깊이를 가지는 노드의 집합


3개의 level로 이루어진 트리이다.

```

### 힙
```
  완전 이진트리를 말한다.
  트래 내의 모든 노드가 부모 노드보다 커야 하는 규칙을 가지고 있다.
  예시)
             2
        8           52
   13     37     67     161     
17   43  88      

깊이 n의 노드 (2의n승)는  2^n-1 ~ 2^n+1 -2 인덱스에 저장된다.

      -----------------------------------------------------------------
       2  |   8  |   52  |   13  |   37  |   67  |  161  | 17 | 43 | 88
      -----------------------------------------------------------------
깊이   0      1      1        2      2         2      2      3   3    3

n번 인덱스에 위치한 노드의 양쪽 자식 노드 위치한 인덱스
 * 왼쪽 자식 : 2n+1
 * 오른 자식 : 2n+2
n번 인덱스에 위치한 부모 위치한 인덱스
  *  (n-1)/2 몫 값 
 
 자세히 보면 이진 검색이 가능 하지 못하는걸 볼 수 있다.
 찾고 싶은 값을 찾기 위해서 는 모든 노드를 순회 해야 한다.
 그러면 힙을 쓰는 이유는  '힙에서 가장 작은 데이터를 갖는 노드는  루트 노드'
 라는 것을 보장 하고 있기 때문이다.     
 
  최대값 및 최소값을 빠르게 찾아 내기 위함이다."


```

### 그래프

```
   * 정점과 간선으로 이루어진 자료구조

    그래프 순회 방식
    
    1. 높이 우선 탐색
     1. 자료구조 Stack 를 사용한다.
     2. 인접 정점에 방문할 정점이 있는 지 확인
     3. 인접 정점  Stack 에 쌓는다.
     4. 정점에 방문할 정점이 없는 경우pop
     5. Stack이 top == NULL 일때까지 2~4을 반복 한다.
    
    2. 넓이 우선 탐색
     1. 자료구조  Queue 를 사용한다.
```
 
