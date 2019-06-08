# Heap
= Binary Tree + 2개의 조건.

    1. Complete Tree이다.
    2. 부모노드는 자식 노드보다 크다.(작다)
    //크면 MaxHeap, 작으면 MinHeap
    
## Heap의 표현

Heap은 level by level 배열로 값을 저장한다. 

## Heap의 구성요소

```c++
template<class ItemType>
struct HeapType
{
  void ReheapDown(int root, int bottom);
  void NonrecursiveRHD(int root, int bottom);
  void ReheapUp(int root, int bottom);
  void NonrecursiveRHU(int root, int bottom);
  ItemType* elements;   // Array to be allocated dynamically
  int numElements;
};
```
### ReHeapDown
 입력된 Root Node에서 시작하여 자식 노드 중에 큰 값이 root Node보다 크다면 swap하는 것을 반복하여 swap이 불가능하거나, bottom에 도달할 때까지 Down한다.
```c++
template<class ItemType>
void HeapType<ItemType>::ReheapDown(int root, int bottom)
{
  int maxChild;
  int rightChild;
  int leftChild;

  leftChild = root*2+1;
  rightChild = root*2+2;
  if (leftChild <= bottom)
  {
    if (leftChild == bottom)
      maxChild = leftChild;
    else
    {
      if (elements[leftChild] <= elements[rightChild])
        maxChild = rightChild;
      else
        maxChild = leftChild;
    }
    if (elements[root] < elements[maxChild])
    {
      Swap(elements[root], elements[maxChild]);
      ReheapDown(maxChild, bottom);
    }
  }
}
```

### ReHeapUp
 입력된 Bottom Node에서 시작하여 자신보다 부모노드가 작다면 서로 swap하는 것을 반복하여 swap이 불가능하거나, root에 도달할 때까지 Up한다.
```c++
template<class ItemType>
void HeapType<ItemType>::ReheapUp(int root, int bottom)
{
  int parent;
  
  if (bottom > root)
  {
    parent = (bottom-1) / 2;
    if (elements[parent] < elements[bottom])
    {
      Swap(elements[parent], elements[bottom]);
      ReheapUp(root, parent);
    }
  }
}
```

# Priority Queue

우선 순위 큐는 여러가지 방식으로 규현할 수 있지만, Heap을 이용하는 것이 가장 효과적이다.

먼저들어오는 값에 우선순위가 존재하면서도, 가장 작은 값을 자동으로 찾을 수 있기 때문이다.

## Enqueue 
 새로운 값을 추가할 때는 Heap의 형태를 유지하기 위해서는 배열의 맨 뒤에 값을 추가하고, 그 지점부터 root Node까지 ReHeapUp을 수행해준다.
```c++
template<class ItemType>
void PQType<ItemType>::Enqueue(ItemType newItem)
{
  if (length == maxItems)
    throw FullPQ();
  else
  {
    length++;
    items.elements[length-1] = newItem;
    items.ReHeapUp(0, length-1);
  }
}
```
## Dequeue
 값을 삭제하더라도 Heap의 형태를 유지하기 위해서는 root Node의 값을 제일 아래 값과 swap하고 bottom Node를 삭제한다. 그 후, root에서부터 ReHeapDown을 수행한다.

```c++
template<class ItemType>
void PQType<ItemType>::Dequeue(ItemType& item)
{
  if (length == 0)
    throw EmptyPQ();
  else
  {
    item = items.elements[0];
    items.elements[0] = items.elements[length-1];
    length--;
    items.ReHeapDown(0, length-1);
  }
}
```
