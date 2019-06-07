# Sorting
대상을 정렬하는 방법.
`크게는 두 종류 : simple, complex`

## Simple Sort Algorithm
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

원소의 수 : N
1차시 시행 횟수 : N
2차시 시행 횟수 : N - 1
K차시 시행 횟수 : N - (K - 1)

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
원소의 수 : N
1차시 시행 횟수 : N - 1
2차시 시행 횟수 : N - 2
K차시 시행 횟수 : N - K

총 시행 횟수 : (N - 1) + (N - 2) + ... + (... + 1) =>(Worst Case) N * (N + 1) / 2

###3. Insertion Sort
평상 시 카드 정리할 때를 생각하면 쉽게 이해할 수 있다. 어지러진 카드 리스트에서 하나씩 뽑으며 정렬 리스트를 만들고, 다시 하나씩 뽑아 정렬하는 알고리즘.

기존 리스트에서 하나를 뽑아 리스트에서 쪼개진 정렬 리스트에 삽입하는 알고리즘. <br>
(앞에서 시작하면 앞에서부터 정렬리스트가 생성되고, 뒤에서 시작하면 뒤에서부터이다.)

한 번 정렬되었더라도 그 위치가 고정이 아니다.


	1) 배열에 새로운 값을 삽입하는 함수를 만든다.
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
원자의 수 : N
1차 시행 횟수 : 1 (뒤에서 두번째 원소와 맨 뒤 원소를 비교한다.) 
2차 시행 홧수 : 최대 2 (뒤에서 세 번째 원소와 뒤에 있는 값을 비교한다.)
K차 시행 횟수 : 최대 K (뒤에서 K+1 번째 원소와 뒤에 있는 값을 비교한다.)

총 시행 횟수 : 1 + 2 + ... + N - 1 => (Worst case) N * (N - 1) / 2
