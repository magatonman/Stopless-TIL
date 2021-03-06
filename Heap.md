# 힙(Heap)
## 힙이란?

Data Structure를 만지다 보면 최댓값이나 최솟값을 연속적으로 빼내고 싶을 때가 분명히 있다. 아니, 자주 존재한다.

힙은 이 문제를 해결하기 위해 만들어진 자료 구조라고 할 수 있다.

## 힙 구조의 설계

힙 구조의 최우선적인 목적은 최댓값이나 최솟값(둘 중 설계할 때 필요한 값)이 루트 노드로 가게 하는 것이다. 이는 힙 구조의 모든 subtree에 대해서도 성립하므로, 최대힙에서는 무조건 자녀 노드의 값이 부모 노드보가 작고, 최소힙은 그 반대이다.

이를 좀 더 명확하게 정의하면 '힙 속성(Heap Property)'이라고 할 수 있다.

힙 $A$에서 임의의 주소 $i$인 칸에 저장된 값을 $A[i]$ 라고 한다면, 모든 주소에 대해서...

* 최대힙의 경우: $A[Parent(i)] \ge A[i]$
* 최소힙의 경우: $A[Parent(i)] \le A[i]$

를 항상 만족시킨다. 즉 어떤 주소를 잡던 간에, 부모 노드와 자녀 노드의 값의 대소 관계는 항상 일정하게 나오게 된다.  

이 구조를 만족시키게 트리를 짠다면 루트 노드의 값이 최댓값 / 최솟값이 될 수 있다.

힙 구조는 완전이진트리 형태이다. 즉, 마지막 level만 빼고 모든 level을 채우는 형식의 이진 트리이다.

힙 구조에서의 자료 구조는 이하와 같이 이루어진다.
* i번째 노드의 부모 노드의 주소: $\lfloor i/2 \rfloor$
* i번째 노드의 자녀 노드의 주소: 좌측은 $2i$, 우측은 $2i+1$.

즉, 부모 노드의 주소를 안다면 자녀 노드 2종의 주소를 자연스럽게 알 수 있고, 그 반대 역시 마찬가지이다.

## 힙에 원소를 삽입하는 방법

힙(으로 추정되는 무엇인가)을 보았을 때, 특정 노드에서 부모-자녀 노드 간에 최대힙 / 최소힙의 대소 관계를 만족하지 않는 부분이 있다면 그 배열-내지는 Tree 구조는 더 이상 힙이라고 부를 수 없다.
이를 해결하기 위해, 그 문제의 부분을 '힙화(Heapify)' 하는 과정이 필요하다.

* 최대힙의 경우
$$ l=Left(i) $$
$$ r=Right(i) $$
$$ if  l \ge A의 크기 and A[l]>A[i]: max=l $$
$$ else max=i $$
$$ if r \ge A의 크기 and A[r]>A[max]: max=r $$
$$ if max \ne i: A[i]의 값과 A[max]의 값을 맞바꾸고 max 주소의 노드에서 이 알고리즘을 다시 한 번 반복 $$

* 이 알고리즘의 실행 시간 구하기
특정 노드 하나와, 그 노드의 자녀 노드들과 대소 관계를 정리하는 데 걸리는 시간은 $\Theta(1)$, 그러니까 그냥 1이다.

그리고 이 때 잡은 노드의 자녀 노드 하나에서 힙화 알고리즘을 재귀적으로 돌린다면, 이 자녀 노드의 subtree의 크기는 최대 $2n/3$이다. (마지막 level이 딱 절반만 차 있는 경우). 원소가 n개인 트리에 이 알고리즘 돌리는 데 걸리는 시간을 $T(n)$이라고 하면, $T(n)$은 $T(2n/3)+\Theta(1)$ 이하일 수밖에 없다.

여기서 마스터 정리를 이용하면 $\Theta(1)=\Theta(n^{log_{2/3} 1})$
이므로 $T(n)$은
$\Theta(lg n)$
이 된다.

### 왜 힙은 완전이진트리인가?

왜냐하면 완전이진트리를 써야 시간복잡도를 최소로 만들 수 있기 때문이다.

당연하겠지만, 미친 척하고 힙을 변질 트리로 만든 다음 그걸 보고 힙이라고 주장할 수는 있다.
(변질 트리: 모든 부모 노드의 자식 노드가 1개뿐인 트리.)

하지만 트리는 배열이 아니기에, 마음대로 찢고 붙이는 것이 불가능하다. 무조건 두 노드의 값을 하나씩 바꿔 나갈 수밖에 없다.
당연히, 2부터 8까지의 수가 차례대로 들어가 있는 최대힙에 1을 삽입한다면 더할 나위 없이 쉽다. 2의 자녀 노드를 하나 만들고 그 안에 1을 넣으면 되니까.
하지만 그 '최대힙'에 1 대신 9를 삽입한다면? 힙을 아주 들었다가 놓는 것 말고는 방법이 따로 없다.

즉 완전이진트리가 아니라면, 최악의 경우 시간복잡도가 $O(n)$이 나올 수 있다. 게다가 이걸 방지할 방법도 없다.

하지만 잘 짜인 완전이진트리로 만들어진 힙의 경우, 위에서 확인한 것처럼 시간복잡도가 $O(lg n)$이 되도록 할 수 있다.


## 힙 정렬

아무렇게나 숫자가 들어가 있는 배열을 힙화한 다음, 그 안에서 정렬하는 방식이다. 시간 복잡도가 $O(nlgn)$이 나온다.

### 최대 힙화 과정

배열 A가 있고, 이 배열의 크기를 l이라고 한다면
$\lfloor l/2 \rfloor$부터 1번째 노드에 대해 죄다 최대 힙화 알고리즘을 돌려버리면 된다.

이렇게 되면 여기서 검수하는 노드들은 죄다 부모 노드인 동시에 자녀 노드가 된다. 완전이진트리인 힙의 특성상, 자녀 노드가 없는 노드들은 검수할 필요가 없으며 자녀 노드가 있는 노드의 수는 전체 노드 수의 절반을 넘길 수 없다. 한 검수가 끝난 노드의 subtree 2개는 전부 이미 최대 힙화된 상태가 되므로 재귀적으로 모든 노드가 최대 힙을 만족하게 된다.

### 정렬 과정(오름차순)

이후, 이 최대힙에 대해서 루트 노드(루트 노드의 두 자녀 노드를 정렬하면 정렬이 끝나기 때문)가 아닌 모든 노드에 대해, 노드 주소를 역순으로 추적하면서 그 노드와 루트 노드의 값을 바꾼 이후, 바뀐 노드 바로 앞 노드까지만을 원소로 취하는 배열을 임시로 잡은 다음, 그 배열을 힙화하는 과정을 반복한다.

이렇게 되면 최댓값을 정렬되지 않은 부분에서 맨 뒤로 보내 버리고, 아직 정렬되지 않은 노드들에 대해 힙화를 거치기 때문에 루트 노드의 값이 항상 정렬되지 않은 값 중 최댓값이 된다.

최대 힙화 과정에 걸리는 시간이 $O(lg n)$이고 이 과정을 n-1번 반복하므로 시간복잡도는 $O(n lgn)$이다.

## 예시 문제: 백준 2075

N×N의 표에 수가 $N^2$개 채워져 있다. 채워진 수에는 한 가지 특징이 있는데, 모든 수는 자신의 한 칸 위에 있는 수보다 크다는 것이다. N=5일 때의 예를 보자.

12	7	9	15	5

13	8	11	19	6

21	10	26	31	16

48	14	28	35	25

52	20	32	41	49

이러한 표가 주어졌을 때, N번째 큰 수를 찾는 프로그램을 작성하시오. 표에 채워진 수는 모두 다르다.

### 풀이

N개의 원소만 받는 최소힙을 만들었을 경우, 새로운 값을 입력받고 root 값을 pop 하는 과정을 반복한다면 마지막에 남는 N개의 원소 중 root 값은 위 표에서 N번째로 큰 수가 된다.

매번 힙에 숫자를 집어넣을 때마다, 힙 정렬을 2번 하므로(새로운 수 삽입 이후 최솟값 제거) 수 1개당 시간복잡도는 $2 O(lgN)$이 된다. 이 과정을 총 $N(N-1)$번 반복하므로(첫째 줄은 패스), 이 과정에 걸리는 총 시간은 $O(2N(N-1) lgN)$이 된다.

초기 과정에서, N개의 수를 힙화하는 데 걸리는 시간은 $O(N lgN)$이므로 합하면 $O((2N^2-N) lgN)$이 된다. 문제에서 주어진 시간 안에 충분히 풀 수 있다.

```pypy
import heapq

#문제에서 사용할 힙과 표 생성
heap=[]

table=[]

#입력
N=int(input())
for i in range(N):
  table.append(list(map(int, input().split())))

for i in table:
  #초기 선언
  if heap==[]:
    for j in i:
      heapq.heappush(heap, j)
  #2번째 줄부터 힙 관리
  else:
    for j in i:
      heapq.heappush(heap, j)
      heapq.heappop(heap)

#손질한 최소힙의 최솟값이 N번째로 큰 수가 됨
print(heapq.heappop(heap))
```
