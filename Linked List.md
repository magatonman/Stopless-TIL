# 연결 리스트

조악하게 요약하면, 배열을 고상하게 말하는 거라고 할 수 있겠지만, 절대 아니다. 배열에는 치명적인 문제점이 있다.

## 배열의 문제점: 수정 시의 시간복잡도

배열에 뭔가 새로운 원소를 삽입/삭제하려면 삭제 이후 빈 칸을 메우기 위해 빈칸 뒤의 **모든** 원소가 이동한다.

즉, 최악의 경우 맨 앞 자리에 새로운 원소를 삽입/삭제한다면 나머지 모든 원소들을 이동해야 하는 불상사가 발생한다. 삽입/삭제 한 번 하겠다고 시간복잡도가 $O(n)$인 연산을 돌리는 미친 짓을 해야 하는 셈이다.

## 연결 리스트란?

각 원소(노드)들 자신이 다른 노드와의 연결 관계를 저장하고 있는 형태의 자료 구조다. 단일 연결 리스트와 이중 연결 리스트가 있으며, 후자가 일반적으로 더 많이 쓰인다.

## 단일 연결 리스트

단일 연결 리스트에서, 노드는 그 자신이 저장하고 있는 원소의 값뿐만 아니라, 자신 바로 뒤에 오는 노드의 주소 값까지 저장하고 있다.
즉 모든 노드는 자기 바로 뒤에 오는 노드와 논리적으로 연결된 셈이다. (하지만 앞의 노드와는 연결되지 않는다)

### 단일 연결 리스트에서의 삽입/삭제

연결 리스트의 맨 앞에 원소를 삽입하는 과정은 간단한데, 아무 노드나 한 개 새로 만든 이후, 그 노드가 저장하는 주소 값을 현재 노드의 head 노드의 주소 값으로 잡는다. 그 이후, 새로 삽입한 노드가 head 노드라고 선언하면 된다.

맨 뒤에 원소를 삽입하는 과정도 간단하다. 똑같이 노드를 만들되, 이번에는 현재 tail 노드가 저장하고 있는 주소 값(원래는 null)을 새로 추가한 노드의 주소로 바꾸고, 새로 추가한 노드가 tail 노드라고 선언하면 된다.

삭제의 경우, 맨 앞의 원소를 삭제하는 과정은 간단하다. head 노드를 2번째 노드(즉, 현재 head 노드의 포인터가 가리키고 있는 노드로)라고 선언한 이후, 원래 head 노드였던 노드를 삭제하면 끝이다.

하지만 맨 뒤의 원소를 삭제한다면? tail 노드는 자기 바로 앞의 노드의 값을 저장할 수 없다. 즉 앞의 3과정과 다르게 시간 복잡도가 배열과 다를 바 없는 셈이다.

## 이중 연결 리스트

이 문제를 해결하기 위해 만들어진 것이 이중 연결 리스트로, 기존의 단일 연결 리스트와 다르게 각 노드는 자신 앞의 노드의 주소 역시 저장한다. 즉 한 노드가 자신의 앞, 뒤의 노드 주소를 전부 저장하는 셈이다.

추가적으로, head 노드와 tail 노드를 위한 노드인 header와 tailer 노드가 존재한다. 이 두 노드는 값을 저장하지 않는 논리적인 노드로, header 노드는 head 노드의 주소를, tailer 노드는 tail 노드의 주소를 저장한다. 반대로 말하자면, head 노드는 자신의 앞 노드로 header 노드를, tail 노드는 자신의 뒷 노드로 tailer 노드를 취한다고 해도 무방하다.

### 이중 연결 리스트에서의 삽입/삭제

삽입의 경우, 삽입하고 싶은 원소를 담은 노드(편의상 z로 호칭)를 하나 생성한 다음, 그 노드를 넣고 싶은 위치(편의상, 노드 x와 y 사이로 가정)를 잡고 앞 노드를 x, 뒷 노드를 y로 잡는다. 그 후, x 노드의 뒷 노드를 z로, y 노드의 앞 노드도 z로 잡는다.

삭제의 경우, 삭제하고 싶은 노드를 지정하고, 그 노드의 앞/뒤 노드의 연결 관계 역시 수정해야 한다. 앞 노드를 x, 뒤 노드를 y라 하면 x의 뒤 노드를 y로, 역으로 y의 앞 노드를 x로 조정하면 된다.

두 과정 모두 시간 복잡도는 $O(1)$.

### 파이썬에서 이중연결리스트 구현

우선 이중연결리스트의 노드를 구현한다. 노드를 구현할 때는 노드의 원소, 이전 노드 주소, 이후 노드 주소 이 3가지를 구현해야 한다.

```python
class _Node:
  __slots__='_element', '_prev', '_next'
  
  def __init__(self, element, prev, naxt):
    self._element=element
    self._prev=prev
    self._next=next
```

이후 초기 상태를 선언하는 __init__ 함수를 정의한다. 이 함수는 header, trailer 노드와 연결리스트의 최초 크기(0)을 정의하며, header와 trailer 노드를 논리적으로 연결한다.


```python
  class _DoublyLinkedBase:
  
  class _Node:
    __slots__='_element', '_prev', '_next'

    def __init__(self, element, prev, naxt):
      self._element=element
      self._prev=prev
      self._next=next
    
  def __init__(self):
    self._header=self._Node(None, None, None)
    self._trailer=self._Node(None, None, None)
    self._header._next=self._trailer
    self._trailer._prev=self._header
    self._size=0
```

마지막으로, 연결리스트의 크기를 정의하는 함수와 삽입, 삭제를 담당하는 함수를 생성하면 기초적인 구조체가 완성된다.

```python
  class _DoublyLinkedBase:
  
  class _Node:
    __slots__='_element', '_prev', '_next'

    def __init__(self, element, prev, naxt):
      self._element=element
      self._prev=prev
      self._next=next
    
  def __init__(self):
    self._header=self._Node(None, None, None)
    self._trailer=self._Node(None, None, None)
    self._header._next=self._trailer
    self._trailer._prev=self._header
    self._size=0
  
 def __len__(self):
    return self._size
    
 def is_empty(self):
    return self._size==0
    
 def _insert._between(self, e, predecessor, successor):
    newest=self._Node(e, predecessor, successor)
    predecessor._next=newest
    successor._prev=newest
    self._size+=1
    return newest
    
 def _delete_node(self, node):
    predecesor=node._prev
    successor=node._next
    predecessor._next=sucessor
    successor._prev=predecessor
    self._size-=1
    element=node._element
    node._prev=node._next=node._element=None
    return element
```

