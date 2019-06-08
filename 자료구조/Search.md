# Search Algorithm

  - Linear Search (순차적 검색)
  - High Probablility Ordering (높은 빈도순 검색)
  - Key Ordering (키를 통한 검색)

=> Search를 빨리하려면 정렬을 통해 규칙을 만들어내고 이를 이용해 찾는 것이 정설이다. <br>
=> 또는 사용 빈도가 높은 대상을 우선 검색하는 것 또한 고려해볼만하다. (locality)<br>
=> 지난 번에 검색했던 데이터 근처의 데이터도 같이 쓸 확률이 높다. (locality)

여기서는 규칙을 만드는 방법에 대해서 고민해볼 것이다.

## Binary Search

기본적으로 제일 먼저 떠오르는 것이다.

데이터를 정렬하면 가운데 값이 가운데 위치에 오게 된다는 규칙을 이용해서 데이터를 logN만에 찾아낼 수 있다.

```C++
void BinarySearch(int ary[], int data, int front,int back)
{ 
    int size = back - front + 1;
    
    if (size == 1)
    {
        if(ary[front] == data)
          return front;
        else 
          return -1;
    }
    if (ary[size / 2] == data)
      return size / 2;
    else if (ary[size / 2] > data)
      return BinarySearch(ary, data, front, size / 2 - 1);
    else
      return BinarySearch(ary, data, size / 2, back);
}
```
## Hashing

잘게 썰어낸다는 뜻이다. 데이터를 잘게 썰어내서 한 번에 데이터를 찾을 수 있도록하는 것이다.

`즉, 목표는 O(1)을 만드는 것이다.`



