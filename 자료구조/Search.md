# Search Algorithm

  - Linear Search (순차적 검색)
  - High Probablility Ordering (높은 빈도순 검색)
  - Key Ordering (키를 통한 검색)

=> Search를 빨리하려면 정리를 통해 규칙을 만들어내고 이를 이용해 찾는 것이 정설이다. <br>
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

### Hashing의 원리.
 	 1. 데이터에서 Key로 쓸 값을 정한다.
 	 2. Key값과 Hash 함수를 통해 index를 얻는다.
	 3. Hash Table에 해당 index위치에 데이터를 저장한다.<br>
 	 // 여기서 Hash Table이란 어려운 말 같지만, 단지 데이터를 저장하는 배열이다.
 	 4. Collision을 각자의 방식으로 해결한다. <br>
 	 // 비어 있는 칸이 있다면 그곳에 넣는다. or linked list 방식을 이용해서 공간을 더 확보한다.
 	 5. Search할 때는 Key값을 통해 얻은 index로 데이터에 바로 접근한다.

### Hash Table 실생활 예시.
  	1. 옷을 어떻게 정리할지 정한다. (반팔, 긴팔, 반바지, 바지, 등)
  	2. 종류에 따라 서랍장의 몇 층에 넣을지 정한다.
  	3. 각 각에 층에 옷을 알맞게 넣는다.
  	4. 같은 층에 넣게 되는 옷이 발생하면 알맞게 이를 해결한다. <br> 
  	// 비어 있는 아래칸에 넣는다 or 공간을 확보해서 같은 층에 넣는다.
  	5. 옷을 찾을 때는 해당 층에 무슨 옷이 있는지를 기억하며 바로 꺼낸다.

### Collision Problem
데이터를 저장할 때, 한 개의 서랍에는 한 개의 데이터 밖에 담지못하는 문제가 발생한다.

	1. Linear probing<Br>
	= 바로 다음 칸이 비었는지 확인하고 없으면 넣고 있다면, 다음으로 또 넘어간다. <br>
	값을 찾을 때는 그 위치부터 값을 찾으며 빈방을 찾읍시다.<br>
	=> 데이터 삭제 시에 유의해야함. 중간에 빈칸이 생기게 된다. 한 번이라도 삭제된 적이 있는지를 알리는 flag가 필요하다.
	2. quaratic probing<br>
	=> 중복 횟수만큼 제곱을 수행합니다.
	3. random probing<br>
	=> 중복 발생 시 random 수와 연산을 수행합니다. random수를 저장해야됨.
	4. hash table size Up<br>
	=> Hash Table의 크기를 올리면 더 골고루 퍼지게 된다.
	5. Make good Hash Function<br>
	=> 해당 데이터의 특징을 파악하여 가능한한 데이터를 고르게 퍼트릴 수 있는 Hash Function을 만든다.
	6. Chain 
	=> Hash Table를 linked list 배열로 만들고 중복이 발생할 시 link를 확장하는 방식을 택한다.

### Hash Table Sort
Idea : N진법을 이용한 sorting

	1. 데이터가 N진법의 수라면, N개의 Hash Table을 만든다.
	2. 일의 자리 수가 1인 경우 1-Hash Table, 2인 경우 2-Hash Table에 저장한다. (9까지)
	3. 이렇게 되면 데이터들은 hash Table 밖에서는 정렬되어보인다.
	4. 데이터의 자릿수만큼 수행한다.
	
복잡도 : O(N)

1 회차 : 일의 자릿수를 기준으로 모든 데이터에 접근하여 알맞은 위치에 넣는다. => N
2 회차 : 십의 자릿수를 기준으로 모든 데이터에 접근하여 알맞은 위치에 넣는다. => N
K 회차 : k 자릿수를 기준으로 모든 데이터에 접근하여 알맞은 위치에 넣는다. => N

총 시행 횟수 : N + N + N + ... + N = N * K
