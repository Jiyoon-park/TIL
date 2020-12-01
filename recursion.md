# 11/09

## recursion

> 순환 or 재귀. 자기 자신을 호출하는 것.



* 무한 루프에 빠지지 않으려면 어떻게 해야하나?
  * base case(적어도 하나의 recursion에 빠지지 않는 경우)가 존재해야 한다.
  * recursive  case는 반복하다보면 결국 base case로 수렴해야 한다.

* 순환함수 == 수학적 귀납법

```python
def f(n):	# 0~n 까지의 합을 구하는 함수
    if n == 0:				# 만약 n == 0 : 합은 0
        return 0
    else:
        return n + f(n-1)	# 만약 n > 0 : 합은 n + (0부터 n-1까지 의 합)
```



* factorial

```python
def factorial(n):
    if n <= 1:
        return 1
    else:
        return n * factorial(n-1)
```

* x ** n

```python
def f(n):
    if n == 0:
        return 1
    else:
        return x * f(n-1)
```

* fibonacci num

```python
def fibo(n):
    if n == 0:
        return 0
    elif n == 1:	# 이거 n <= 1: return n 으로 해도 될 듯
        return 1
    else:
        return fibo(n-1) + fibo(n-2)
    
    
```

* 최대공약수

```python
# 내 처음 풀이
def gdc(n, m):
    global res
    if n == 0 or m == 0:
        return 1
    else:
        for i in range(min(n, m), 1, -1):
            if n % i == 0 and m % i == 0:
                res *= i
                return gdc(n//i, m//i)
            else:
                continue

res = 1
gdc(54, 63)
print(res)
```

```python
# better한 풀이
def gdc(n, m):
    if n > m :
        n, m = m, n
    if m % n == 0:
        return n
    else:
        return gdc(n, m%n)

res = gdc(54, 63)
print(res)
```

```python
# (내 기준)best한 풀이
def gdc(n,m):
    if m == 0:
        return n
    else:
        return gdc(m, n%m)
```

