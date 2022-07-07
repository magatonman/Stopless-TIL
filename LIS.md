# 최장 부분 증가 수열(LIS)

임의의 수열 $A$이 존재할 때, 이 수열에서 임의의 갯수의 수만 골라 내서 만든 부분수열(순서는 그대로)들 중, 이하의 규칙을 만족하는 수열을 부분 증가 수열이라 한다.

* 부분수열을 $A'$라 하고, $A'$의 $n$번째 원소를 $a_n$이라고 할 때, $A'$의 임의의 원소 $a_n$은 $a_m$ (단, $m \lt n$) 보다 크다.

그리고 최장 부분 증가 수열은 부분 증가 수열들 중 가장 긴 수열이다.

## LIS의 길이 구하기

이제부터는, 수열 [2, 4, 3, 6, 1, 7, 9] 를 기준으로 설명한다. 이 수열의 LIS는 [2, 4, 6, 7, 9] 다. 다른 부분 증가 수열로 [2, 3, 6], [4, 7, 9] 같은 것도 있지만 길이가 가장 길지 않다.

### 방법 1

부분 증가 수열의 마지막 수를 기준으로 동적 계획법을 적용한다. 기존에 끊겼던 부분 증가 수열에 새로운 수를 더해도 규칙이 깨지지 않는다면 더 긴 부분 증가 수열이 된다.

```python
A=[2, 4, 3, 6, 1, 7, 9]
memoization=[1 for i in range(len(A))]
for i in range(len(A)):
  for j in range(i):
    if A[i]>A[j]:
      memoization[i]=max(memoization[i], memoization[j]+1)
      
print(max(memoization))
```

다 좋은데, 반복문이 2번 돈다는 것부터 알 수 있겠지만 이 알고리즘의 시간복잡도는 $O(n^2)$다. 더 좋은 방법을 찾아보자.

### 방법 2

숫자 하나하나당 검사를 하는 것은 배열을 다 순회해야 부분 수열을 만들 수 있기 때문에 자명하다. 하지만 꼭 자신 앞의 수들을 전부 봐야 하는가?

현재 검수 중인 부분 수열 배열과 새로 넣을 수를 비교해서, 그 수를 넣을 위치만 찾는다면 갱신 가능하다.

이진 탐색을 이용하면 위치 찾는 데에는 $O(log n)$이 걸리므로 시간복잡도 $(n log n)$에 해결 가능하다.

```python
import bisect # 이진 탐색 모듈
A=[2, 4, 3, 6, 1, 7, 9]
memoization=[A[0]]
 
for i in range(len(A)):
  if A[i]>memoization[-1]:
    memoization.append(A[i])
  else:
    memoization[bisect.bisect_left(memoization, A[i])]=A[i]
print(len(memoization))
```
