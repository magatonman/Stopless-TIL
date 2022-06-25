# 미친 척하고 Pivot을 랜덤하게 잡는다면?

* 의사코드(정렬할 배열: A)

배열 A에서, p~q번째 작은 수 중 i번째로 작은 수를 찾는 임의 선택 알고리즘

>if p=q: return A[P]</br>
>r=p, q 사이의 랜덤한 수</br>
>k=r-p+1(즉 k는 r이 A에서 몇 번째로 작은 수인지를 나타낸다)</br>
>i=k면 탐색 종료</br>
>i<k면 p부터 r-1까지를 탐색 범위로 하는 부분 배열에서 반복</br>
>i>k면 r+1부터 q까지를 탐색 범위로 하는 부분 배열에서 반복</br>

그런데, 이 알고리즘에서 pivot을 한쪽 끝의 수로만 계속 잡는다면 이 알고리즘의 실행 시간
$T(n)$은 $T(n-1)+\Theta(n)$이 되어 버린다. 이 경우 $T(n)$은 $\Theta(n^2)$가 되어 버리는데 이러면 차라리 정렬하고 찾는 게 낫다!

하지만, 운이 좋다면 pivot이 딱 정중앙의 수로만 계속 잡힐 수도 있다. 사실, 정중앙이 아니라도 $T(n)$이 $T(n/b)+O(n)$의 형태로만 나오게 자를 수 있다면 마스터 정리에서 a=1이므로 $O(n)$이 된다.

# 현실적인 경우

pivot의 위치가 1/4부터 3/4까지 중, 어느 한 곳에 있다면 **좋은** pivot이라고 하자. 이 경우 부분배열의 크기가 양쪽 다 원 배열 크기의 3/4를 넘지 않는다.

pivot이 좋은 pivot이 될 확률은 50%이고, $T(n) \le T(3n/4)+O(n)$이 된다.

# 실행 시간 예측

위의 의사코드에서 랜덤하게 잡는 pivot k에 대해서 지시확률변수 $X_k$는 r이 k번째로 큰 수가 될 확률에 대한 확률변수라고 정의하자.

이 경우, $T(n)
을 급수로 나타내면

$\sum\limits_{k=0}^{n-1} X_k (T(max ( k, n-k-1 ))+\Theta(n))$이 된다.

이 확률변수에 대한 기댓값, $E[\sum\limits_{k=0}^{n-1} X_k (T(max ( k, n-k-1 ))+\Theta(n))]$을 계산하면...
$E[\sum\limits_{k=0}^{n-1} X_k (T(max ( k, n-k-1 ))+\Theta(n))]$

$=\sum\limits_{k=0}^{n-1} E[X_k (T(max ( k, n-k-1 ))+\Theta(n))]$

$=\sum\limits_{k=0}^{n-1} E[X_k] \cdot E[(T(max ( k, n-k-1 ))+\Theta(n))]$

여기서, 이 확률변수는 선형적이므로 $E[X_k]=1/n$이기 때문에

$=\frac{1}{n} \sum\limits_{k=0}^{n-1} E[(T(max ( k, n-k-1 ))]+\frac{1}{n}\sum\limits_{k=0}^{n-1}\Theta(n))$

$k=\lfloor n/2\rfloor$를 기준으로 기댓값이 대칭적으로 나오므로, 위의 식은 $\frac{2}{n}\sum\limits_{k=\lfloor \frac{2}{n}\rfloor}^{n-1} E[T(k)]+\Theta(n)$ 이하다.

# $T(n)$의 기댓값이 선형적임을 증명하기

$\sum\limits_{k=\lfloor n/2\rfloor}^{n-1}k\le \frac{3n^2}{8}$ 이므로

$E[T(n)]\ \le \frac{2}{n}\sum\limits_{k=\lfloor n/2\rfloor}^{n-1} ck +\Theta(n)$ (c는 충분히 큰 임의의 상수)

$\le \frac{2c}{n}\left(\frac{3n^2}{8}\right)+\Theta(n)$

$=\frac{3cn}{4}+\Theta(n)$

즉, c가 충분히 크다면 $Theta(n)$을 무시해도 좋으므로 시간 복잡도는 $O(n)$이 된다.
