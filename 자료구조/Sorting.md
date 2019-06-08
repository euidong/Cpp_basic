# Sorting
대상을 정렬하는 방법.
`크게는 두 종류 : simple, complex`

## Simple Sorting Algorithm
  1. Selection Sort
  2. Bubble Sort
  3. Insertion Sort

* 모두 오름차순으로 설명하겠습니다.
### 1. Selection Sort
전체 리스트에서 제일 작은 수를 찾아 배열의 앞에서부터 정렬하는 알고리즘.

한 번 정렬되면 그 위치에 고정됨.
```c++
int minimum;
int temp;
for (int i = 0 ; i < size ; i++)
{
    minimum = i;
    for (int j = 0 ; j < size - i ; j++) // 작은 값을 찾기
    {
        if (values[i] < values[minimum])
        {
            minimum = j;
        }
    }
    temp = values[minimum];
    values[minimum] = values[i];
    values[i] = temp;
}
```
복잡도 : O(N^2)

원소의 수 : N <br>
1차시 시행 횟수 : N<br>
2차시 시행 횟수 : N - 1<br>
K차시 시행 횟수 : N - (K - 1)<br>

총 시행 횟수 : N + (N - 1) + ... + 1 = N * (N + 1) / 2

### 2. Bubble Sort
뒤에서 부터 : 전체 리스트를 이동하며 가장 작은 수를 앞으로 끌고가는 알고리즘.<br>
앞에서 부터 : 전체 리스트를 이동하며 가장 큰 수를 뒤로 끌고가는 알고리즘.

한 번이라도 Swap이 일어났는지 여부를 저장하여 조기에 끝내는 것도 가능하다.

한 번 정렬되면 그 위치에 고정됨.
```c++
void bubble_up(int a, int b, bool& bubble)
{
    int temp;
    if (a > b)
    {
        temp = a;
        a = b;
        b = temp;
        bubble = true;
    }
}
void bubble_Sort(int* arr, int size)
{
    bool bubble = false;
    for (int i = 0 ; i < size ; i++)
    {
        for (int j = size - 1; j  > i; j--)
        {
            bubble_up(arr[j], arr[j -1], bubble)
        }
        if (bubble == false)
            break;
        else
            bubble = false;
    }
    return ;
}
```
복잡도 : O(N^2)

원소의 수 : N<br>
1차시 시행 횟수 : N - 1<br>
2차시 시행 횟수 : N - 2<br>
K차시 시행 횟수 : N - K<br>

총 시행 횟수 : (N - 1) + (N - 2) + ... + (... + 1) =>(Worst Case) N * (N + 1) / 2

### 3. Insertion Sort
평상 시 카드 정리할 때를 생각하면 쉽게 이해할 수 있다. 어지러진 카드 리스트에서 하나씩 뽑으며 정렬 리스트를 만들고, 다시 하나씩 뽑아 정렬하는 알고리즘.

기존 리스트에서 하나를 뽑아 리스트에서 쪼개진 정렬 리스트에 삽입하는 알고리즘. <br>
(앞에서 시작하면 앞에서부터 정렬리스트가 생성되고, 뒤에서 시작하면 뒤에서부터이다.)

한 번 정렬되었더라도 그 위치가 고정이 아니다.


	1) sorting된 배열에 새로운 값을 삽입하는 함수를 만든다.
	2) 배열의 크기를 늘리며 그 함수를 N번 호출한다.
```c++
void InsertItem(Student ary[], int startIndex, int endIndex) // 임시 정렬 리스트에 값을 삽입
{
	bool finished = false;
	int current = endIndex;
	bool moreToSearch = (current != startIndex);
	string name1, name2;

	while (moreToSearch && !finished)
	{
		name1 = ary[current].getName();
		name2 = ary[current - 1].getName();
		if (name1 < name2)
		{
			Swap(ary[current], ary[current - 1]);
			current--;
			moreToSearch = (current != startIndex);
		}
		else
			finished = true;
	}
}

void InsertionSort(Student ary[], int numElems)
{
	for (int count = 0; count < numElems; count++) //앞에 부분은 임시 정렬 리스트
		InsertItem(ary, 0, count);
}
```
복잡도 : O(N^2)

원자의 수 : N

1차 시행 횟수 : 1 (뒤에서 두번째 원소와 맨 뒤 원소를 비교한다.) <br>
2차 시행 홧수 : 최대 2 (뒤에서 세 번째 원소와 뒤에 있는 값을 비교한다.)<br>
K차 시행 횟수 : 최대 K (뒤에서 K+1 번째 원소와 뒤에 있는 값을 비교한다.)<br>

총 시행 횟수 : 1 + 2 + ... + N - 1 => (Worst case) N * (N - 1) / 2

=> 항상 그런 것은 아니지만, 대게 적은 수를 Sorting할 때는 속도가 빠르다.

### Bubble VS Insert
=> bubble : 모든 시행을 안할 수도 있지만, 한 번 시행 시 모든 값을 탐색해야한다. <br>
=> insert : 모든 시행을 해야하지만, 시행 시에 모든 값을 탐색하지 않는 경우가 많다.
## Complex Sorting Algorithm

  1. Heap Sort
  2. Quick Sort
  3. Merge Sort

### 1. Heap Sort
Selection Sort와 같은 논리로 가장 작은 수를 찾아서 앞에서부터 채웁니다.<br>
But, Heap을 이용합니다.

	1. Maximum Heap 형태로 데이터를 재정렬합니다.
	2. Maximum Heap에서 값을 뽑습니다.
	3. 제일 끝에 값(Max로 저장된 값을 제외한)을 root로 올리고 ReHeapDown을 수행합니다.
	4. 배열의 크기만큼 (2~3)을 수행합니다. 
	
Point. Heap으로 만들어야 하는 대상은 누구일까?<br>
=> Heap의 정의 : 부모 노드가 자식 노드보다 크다.<br>
=> Leaf 노드는 이미 Heap을 만족한다.<br>
=> Leaf 노드를 제외하고 ReHeapDown을 수행하자.<br>
=> <strong>Complete Tree의 Leaf 노드가 아닌 노드의 수 = N / 2 </strong>

```c++
void HeapSort(Student ary[], int numElems)
{
	HeapType<Student> stu(numElems);

	//make heap
	for (int i = 0; i < numElems; i++)
	{
		stu.elements[i] = ary[i];
	}

	for (int i = numElems / 2 -1; i >= 0; i--)
	{
		stu.ReheapDown(i,i * 2);
	}

	//heap에서 정렬하기
	for (int i = 0; i < numElems - 1; i++)
	{
		Swap(stu.elements[0], stu.elements[numElems - 1 - i]);
		stu.ReheapDown(0, numElems - 2 - i);
	}

	for (int i = 0; i < numElems; i++)
	{
		ary[i] = stu.elements[i];
	}
}
```
복잡도 : O(N * logN)

원자의 수 : N

0 회차 : Heap으로 만들기 => N / 2 <br>
1 회차 : Heap에서 데이터 빼기 + leaf Node를 위로 올리고 ReHeapDown => 최대 logN <br>
K 회차 :                         //			       => 최대 logN

총 시행 횟수 : N / 2 + logN * N => N * logN

### 2. Quick Sort Algorithm
Idea : 중간값을 기준으로 배열을 쪼개고, 다시 쪼개면서 값을 구하면 더 빠르지 않을까?

Issue : 중간값을 찾는 것이 비싼 연산 과정이다.<br>
=> 완전한 중간값을 찾으면 좋지만, random한 수라면 적절하게 배열을 잘라줄 것이다. <br>
=> random한 수 = 배열의 첫 번째 수로 하자.

	1. 배열의 첫 번째 값을 기준으로 삼는다.
	2. 배열의 첫 번째 값을 제외한 양 끝 지점을 index로 가르키는 포인터를 만든다.
	3. 왼쪽은 크면 이동, 오른쪽은 작으면 이동한다.
	4. 둘이 교차할 때까지 움직이며, 그 전에 둘 다 멈추게 되면 두 값을 Swap한다.
	5. 둘이 교차하고, back에서 온 포인터가 가르키는 값과 배열의 첫 번째 값을 Swap한다.

	- Generic case : 기준점의 위치를 찾고 배열을 둘로 쪼갠다.
	- Base case : 배열의 크기가 2라면, 서로 값을 비교하고 끝낸다.<br>
	1이라면 그냥 끝낸다. 
	
```c++
void QuickSort(Student values[], int first, int last)
{
	if (first + 1 == last)
	{
		if (values[first] > values[last])
			Swap(values[first], values[last]);
		return;
	}
	else if (first == last + 1)
		return;

	int front_point = first + 1;
	int back_point =last;


	while (front_point <= back_point)
	{
		if (values[first] > values[front_point])
			front_point++;
		else if (values[first] < values[back_point])
			back_point--;
		else
			Swap(values[front_point], values[back_point]);
	}

	Swap(values[first], values[back_point]);
	QuickSort(values, first, back_point - 1);
	QuickSort(values, back_point + 1, last);

	return;
}
```

복잡도 : O(N * logN)

원자의 수 : N

1 회차 : 기준점으로 배열 나누기 => N <br>
2 회차 : 2개의 배열을 각 각의 기준점으로 나누기 => N = a + (N - a) <br>
K 회차 : 2^(K - 1)개의 배열을 각 각의 기준점으로 나누기 => N

총 시행 횟수 : logN * N => (Best case) N * logN
이미 정렬되어 있다면, N^2까지 수행한다.

### 3. Merge Sort Algorithm
Idea : Quick이 쪼개면서 내려갔다면, Merge는 합치면서 올라오자.
=> 중간값을 정확히 찾을 수는 없지만, 배열의 크기를 반으로 자르는 것은 가능하다.

	1. 배열을 모두 잘게 쪼갠다.
	2. 밑에서부터 배열을 정렬하면서 합친다.
	3. 정렬하면서 합칠 때는, 두개의 배열의 인덱스 값을 가르킬 포인터가 필요.
	
```c++
Student* merge(Student values[], int front, int middle, int back)
{
	Student* temp;
	temp = new Student[back - front + 1];

	int ptr1 = front;
	int ptr2 = middle + 1;
	int size1 = middle - front + 1;
	int size2 = back - middle;
	int count = 0;
	while (ptr1 < size1 && ptr2 < size2+ middle + 1)
	{
		if (values[ptr1] < values[ptr2])
		{
			temp[count] = values[ptr1];
			ptr1++;
			count++;
		}
		else
		{
			temp[count] = values[ptr2];
			ptr2++;
			count++;
		}
	}
	if (ptr1 != size1)
	{
		while (ptr1 < size1)
		{
			temp[count] = values[ptr1];
			ptr1++;
			count++;
		}
	}
	else if (ptr2 != size2)
	{
		while (ptr2 < size2)
		{
			temp[count] = values[ptr2];
			ptr2++;
			count++;
		}
	}

	for (int i = 0; i < count; i++)
	{
		values[front + i] = temp[i];
	}
	delete temp;

	return values;
}

void MergeSort(Student values[], int front, int back)
{
	if (front == back)
		return;

	int middle = (back - front) / 2;
	MergeSort(values, front, middle);
	MergeSort(values, middle + 1, back);
	merge(values, front, middle, back);

	return;
}
```

복잡도 : O(N * logN)

0 회차 : 배열을 모두 잘게 자른다. => N
1 회차 : N개의 배열을 N/2개로 Merge한다. => N
K 회차 : N- K - 1개의 배열을 Merge한다. => N

총 시행 횟수 : N + N + N + ... + N = N + logN

### 4. Hash Table Sort
[Search - Hashing table sort](https://github.com/euidong/Cpp_basic/blob/master/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0/Search.md#hash-table-sort)
