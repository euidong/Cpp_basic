# Heap
= Binary Tree + 2개의 조건.
    1. Complete Tree이다.
    2. 부모노드는 자식 노드보다 크다.(작다) <br>
    //크면 MaxHeap, 작으면 MinHeap
    
## Heap의 표현

Heap은 level by level 배열로 값을 저장한다. 

## Heap의 구성요소

```c++
struct HeapType
{
    void ReHeapDown(int root, int bottom); => 힙을 재구성한다. 
    void ReHeapUp(int root, int bottom); => 힙을 재구성한다.
    ItemType* elements;
    int numElements;
}
```
