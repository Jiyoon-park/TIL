# 0826

## stack

> 나중에 넣은 데이터를 가장 먼저 꺼내 쓸 수 있도록 설계된 자료구조이다. 택배 상하차 를 생각해보자.
>
> (LIFO : Last In First Out)

 주요기능은 `push():맨 마지막에 데이터 삽입`, `pop():맨 마지막 데이터 꺼내기`, `peak():맨 마지막 데이터 확인`, `isEmpty():스택이 비어있나요?` 가 있다. python에서는 `pop()`, `append()`, `st[-1]`, `len(st)` 를 사용한다.

```python
arr = [1,2,3,4]
st = []
for a in arr:
    st.append(a)
print(st)						// [1,2,3,4]
print(st.pop())					// 4
print(st.pop())					// 3	
print(st[-1])					// 2
print(True if st else False)	// True
```



## queue

> 가장 먼저 넣은 데이터를 가장 먼저 꺼내 쓸 수 있도록 설계된 자료구조이다. 마트 계산 줄 을 생각해보자.
>
> (FIFO : First In First Out)

주요 기능은 `add():맨 마지막에 데이터 추가`, `remove():맨 앞 데이터 꺼내기`, `peek():맨 앞 데이터 확인`, `isEmpty():큐가 비어있나요?` 가 있다. python에서는 `append()`, `pop(0)`, `q[0]`, `len(q)` 를 사용한다.

```python
arr = [1,2,3,4]
q = []
for a in arr:
    q.append(a)
print(q)						// [1,2,3,4]
print(q.pop(0))					// 1
print(q.pop(0))					// 2	
print(q[0])						// 3
print(True if st else False)	// True
```

* 원형 큐
* 우선순위 큐



## from collections import deque

> collections 모듈의 deque를 통해 st과 q를 손쉽게 구현할 수 있다. 

`pop()`, `popleft()`, `append()` 