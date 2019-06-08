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
int BinarySearch(int ary[], int data, int front, int back)
{
	int size = back - front + 1;

	if (size == 1)
	{
		if (ary[front] == data)
			return front;
		else
			return -1;
	}
	if (ary[front + size / 2] == data)
		return front + size / 2;
	else if (ary[front + size / 2] > data)
		return BinarySearch(ary, data, front, front + size / 2 - 1);
	else
		return BinarySearch(ary, data, front + size / 2, back);
}
```
## Hashing

잘게 썰어낸다는 뜻이다. 데이터를 잘게 썰어내서 한 번에 데이터를 찾을 수 있도록하는 것이다.

`즉, 목표는 O(1)을 만드는 것이다.`

기존의 binary Search가 여러 물체를 한줄로 세웠다면, Hashing 방법은 서랍장에 물체를 담는 방식으로 생각하면 쉽다.
한 마디로 같은 줄에 여러 명을 세우는 거 같은 효과를 가져다준다.

Hash Table의 원리.
  1. 데이터에서 Key로 쓸 값을 정한다.
  2. Key값과 Hash 함수를 통해 index를 얻는다.
  3. Hash Table에 해당 index위치에 데이터를 저장한다.<br>
  // 여기서 Hash Table이란 어려운 말 같지만, 단지 데이터를 저장하는 배열이다.
  4. Collision을 각자의 방식으로 해결한다. <br>
  // 비어 있는 칸이 있다면 그곳에 넣는다. or linked list 방식을 이용해서 공간을 더 확보한다.
  5. Search할 때는 Key값을 통해 얻은 index로 데이터에 바로 접근한다.

Hash Table 실생활 예시.
  1. 옷을 어떻게 정리할지 정한다. (반팔, 긴팔, 반바지, 바지, 등)
  2. 종류에 따라 서랍장의 몇 층에 넣을지 정한다.
  3. 각 각에 층에 옷을 알맞게 넣는다.
  4. 같은 층에 넣게 되는 옷이 발생하면 알맞게 이를 해결한다. <br> 
  // 비어 있는 아래칸에 넣는다 or 공간을 확보해서 같은 층에 넣는다.
  5. 옷을 찾을 때는 해당 층에 무슨 옷이 있는지를 기억하며 바로 꺼낸다.
