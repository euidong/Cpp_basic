# Recursion (재귀)

Recursion Function = 자기 자신을 호출하는 함수

모든 Recursion 함수는 Iterator 구문으로 변경할 수 있다. (역도 성립한다.)

## Recursion Function 만들기
Base case : recursion를 마무리할 부분. end case라고 볼 수 있음.

General case : recursion을 쓰고 논리를 수행하는 부분. 반복하면 반복할 수록 base case로 다가가게 된다.

size factor : recursion이 진행되면 점점 줄어들 요소.

size factor를 정하고 해당 케이스를 직접 쓰고 설계한 후 각 각 구현해서 합치는 것이 알맞게 재귀 함수를 만들 수 있다.

<strong> Recursion이 진행될 수록 Base case로 수렴해야한다. </strong>

## 재귀 함수의 장점

똑같은 코드라도 이해하기 쉽고, 간략하게 표현하여 가독성이 좋은 코드를 만들 수 있음.

## 재귀 함수의 단점v

함수를 호출하게 되면, run-time stack에 return address, parameter, local value를 모두 저장한다.<br>
함수에서 return이 호출되면, run-time stack에서 return address, parameter, local value를 다시 불러옵니다. <br>
이렇게 메모리에 값을 저장하고, 다시 불러오는 과정은 많은 시간과 메모리를 필요로 한다. <br>
따라서 재귀함수는 일반 iterator구문보다 시간이 더 걸린다.

## 재귀 함수의 시각화

나는 시각화를 해야 쉽게 이해를 하므로, 내 방식대로 시각화해보았다.<br>
재귀 호출될 수록 아래로 구덩이를 판다고 생각하자. 그리고 구덩이에서 나오면 안에서는 못보던 요소를 볼 수 있다. 
```
____________                                               ___________ 
            |                                             |
            |_______________               _______________|
                           |               |
                           |_______________|   
```


```
____________                                  ___________________ 
            |                                 |
            |______________________           |
                                   |          |
                                   |__________|   
(generic case1)  (generic case2)    (base case)                                                 
```
