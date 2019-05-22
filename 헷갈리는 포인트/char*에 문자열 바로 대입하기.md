# 함수에 인자가 char*라면 문자열을 바로 대입할 수 없다.

ex)
```c++

  int main()
  {
    char* good = "good";
    return 0;
  }
```
=> error 발생


### 해결책

(char*)"good"로 대입하기
```c++
  int main()
  {
    char* good = (char*)"good";
    return 0;
  }
```

2) 변수에 저장해서 전달하기
