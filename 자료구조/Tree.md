2차원적인 자료 구조를 갖고 있음.

나무를 거꾸로 뒤집은 모양

# Tree의 기본

  - Root Node = 맨 위의 노드
  - Leaf Node = 맨 아래의 노드
  - Ancestor Node = 조상 노드
  - Decestor Node = 자손 노드
  - Level = Root Node를 기준으로 아래로 갈 수록 level은 증가한다.(root node는 대게 level 0으로 생각한다.) 
  - Height = Level의 갯수를 의미
  - Full Tree = 모든 Level이 꽉 차 있는 Tree.
  - Complete Tree = 최하위단 외에 모든 층이 꽉 차 있는 Tree.
  
  
### Tree의 특징
  - Root Node로 부터 다른 Node에 접근하는 경로가 유일해야 한다.

# Binary Tree의 특징
  - 하나의 Node는 최대 2개의 자식 Node를 가진다.
  - Leaf Node는 최대 2^(level)개 존재한다.
  - Root Node는 최대 1개 존재한다.
  - <strong>Full Tree 일 때, 2^(height) - 1 </strong>
  
# Binary Search Tree (BST)
  - Binary Tree에 새로운 값을 추가할 때, 하나의 입력 기준을 정한 것이다. 
  - 도착지점이 NULL이면 값을 저장하고, 값이 현재 노드보다 작으면 왼쪽, 크면 오른쪽으로 이동한다.
  - 가장 큰 사용 이유는 삽입, 삭제, 검색하는데 모든 복잡도가 O(logN)이다.
  - BST의 복잡도가 언제나 logN인 것은 아니다. tree가 골고루 퍼지지 않고 한쪽에 치중되어있다면,<br>
  모든 노드를 돌아야하는 경우가 생긴다. 하지만, 일반적으로 다들 logN이라고 한다.

# BST의 구성

### Node 구조
```c++
struct TreeNode
{
  ItemType info;
  TreeNode* left;
  TreeNode* right;
};
```

### 멤버 변수
```c++
  TreeNode* root; // RootNode를 가르킬 pointer
  QueType preQue; // 후에 추가 설명
  QueType inQue; // 후에 추가 설명
  QueType postQue; // 후에 추가 설명
```
### 멤버 함수
```c++
  TreeType();
  ~TreeType();
  TreeType(const TreeType& originalTree); 
  void operator=(const TreeType& originalTree);
  
  /* tree를 초기화하기 위한 함수 */
  void MakeEmpty();
  
  /* tree의 상태를 확인하기 위한 함수 */
  bool IsEmpty() const;
  bool IsFull() const;
  int GetLength() const; 
  
  /* tree의 data를 검색, 추가, 삭제하기 위한 함수 */
  ItemType GetItem(ItemType item, bool& found);
  void PutItem(ItemType item);
  void DeleteItem(ItemType item);
  
  /* tree의 item을 받아오기 위한 함수 */
  void ResetTree(OrderType order); 
  ItemType GetNextItem(OrderType order, bool& finished);
  void Print(std::ofstream& outFile) const;
```

# Tree Traversal = Tree의 모든 노드를 방문하는 방법
  - inorder = (안) 왼쪽으로 이동 후, 데이터를 처리하고, 오른쪽으로 이동 한다. 
  - preorder = (이전) 데이터를 처리하고, 왼쪽으로 이동 후, 오른쪽으로 이동 한다. 
  - postorder = (이후) 왼쪽으로 이동 후, 오른쪽으로 이동하고, 데이터를 처리하고
  - level by level traversal = 해당 노드에서 좌, 우 값을 queue에 넣고 데이터를 분석하고, queue에서 하나의 데이터를 dequeue한다.<br>
  dequeue된 노드를 이용하여 위의 과정을 반복한다.

### 코드 표현
```c++
void PreOrder(TreeNode* tree, 
     QueType& preQue)
// Post: preQue contains the tree items in preorder.
{
  if (tree != NULL)
  {
    preQue.Enqueue(tree->info);
    PreOrder(tree->left, preQue);
    PreOrder(tree->right, preQue);
  }
}


void InOrder(TreeNode* tree, 
     QueType& inQue)
// Post: inQue contains the tree items in inorder.
{
  if (tree != NULL)
  {
    InOrder(tree->left, inQue);
    inQue.Enqueue(tree->info);
    InOrder(tree->right, inQue);
  }
}


void PostOrder(TreeNode* tree, 
     QueType& postQue)
// Post: postQue contains the tree items in postorder.
{
  if (tree != NULL)
  {
    PostOrder(tree->left, postQue);
    PostOrder(tree->right, postQue);
    postQue.Enqueue(tree->info);
  }
}

void LevelByLevel (TreeNode* tree,
      QueType& levelQue, QueType& instantQue)
{
  if (tree != NULL)
  {
    TreeType get_next;
    instantQue.Enqueue(tree->left); //treetype*를 저장
    instantQue.Enqueue(tree->right);//treetype*를 저장
    levelQue.Enqueue(tree->info); // 아무 type이나 저장
    if (!instantQue.IsEmpty())
    {
      instantQue.dequeue(get_next);
      LevelByLevel(get_next, levelQue, instantQue);
    }
  }
}
```



