# 파이썬과 트리

안타깝게도 파이썬에는 트리 구조가 없다. 따라서 직접 구현해야 한다.

## 트리에 필요한 것들

당연하지만 트리는 자료 구조의 형태 중 하나이기에, 노드들과 그 노드들의 관계(간선)를 저장할 수 있는 형태로 클래스를 구현해야 한다.

또한, 트리에 원소를 삽입, 삭제하는 등 다양한 방식으로 트리를 조정할 수 있는 명령어 역시 필요하다.


그 외에도 트리 구조체에서 써먹을 만한 명령어들을 찾아 본다면 대충 이하와 같다.

* p.element(): 주소 p에 있는 원소 return.
* T.root(): T의 root 노드값을 return, 빈 트리의 경우 None을 return.
* T.is_root(p): 주소 p가 root 노드의 주소인지를 return.
* T.parent(p): p 주소의 노드의 부모 노드의 주소를 return. p가 root의 주소면 None을 return.
* T.num_children(p): p 주소의 노드가 가지는 자녀 노드의 수를 return.
* T.is_leaf(p): p가 자녀 노드가 없는지를 따지는 불 함수.
* len(T): T의 원소 개수를 return한다.
* T.is_empty(): T가 원소가 없는지를 따지는 불 함수.

### 기초 다지기

먼저 트리의 자료들을 저장해 둘 최소한의 구조체를 만들자.

```python
class Tree:
  class Position:
  
  def __init__(self, container, node):
    self._container=container
    self._node=node
  
  def element(self):
    return self._node._element
```

