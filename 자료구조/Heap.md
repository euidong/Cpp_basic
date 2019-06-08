# Heap
= Binary Tree + 2개의 조건.

    1. Complete Tree이다.
    2. 부모노드는 자식 노드보다 크다.(작다)
    //크면 MaxHeap, 작으면 MinHeap
    
## Heap의 표현

Heap은 level by level 배열로 값을 저장한다. 

## Heap의 구성요소

```c++
struct HeapType
{
    void ReHeapDown(int root, int bottom); => 힙을 재구성한다. 
    void ReHeapUp(int root, int bottom); => 힙을 재구성한다.
 pivate:  
    ItemType* elements;
    int numElements;
}
```
### ReHeapDown
 입력된 Root Node에서 시작하여 자식 노드 중에 큰 값이 root Node보다 크다면 swap하는 것을 반복하여 swap이 불가능하거나, bottom에 도달할 때까지 Down한다.

### ReHeapUp
 입력된 Bottom Node에서 시작하여 자신보다 부모노드가 작다면 서로 swap하는 것을 반복하여 swap이 불가능하거나, root에 도달할 때까지 Up한다.

## Insert 
 새로운 값을 추가할 때는 Heap의 형태를 유지하기 위해서는 배열의 맨 뒤에 값을 추가하고, 그 지점부터 root Node까지 ReHeapUp을 수행해준다.

## Remove
 값을 삭제하더라도 Heap의 형태를 유지하기 위해서는 root Node의 값을 제일 아래 값과 swap하고 bottom Node를 삭제한다. 그 후, root에서부터 ReHeapDown을 수행한다.
