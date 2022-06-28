# 트리의 순회법

* 전위 순회
* 후위 순회
* 너비 우선 순위 순회(BFT)
* 중위 순회
## 전위 순회(Preorder Traversal)
자녀 노드 방문 전에 부모 노드를 우선적으로 방문하는 형식의 순회법이다.

의사코드로 나타내면
```
preorder(v)
  visit(v)
  for each child w of v:
    preorder(v)
```
즉 특정 subtree를 한 번 방문했다면, 그 subtree의 모든 노드를 전부 다 방문해야 같은 depth의 노드를 root로 하는 다른 subtree를 방문할 수 있게 된다.

## 후위 순회(Postorder Traversal)
자녀 노드를 전부 방문해여 그 부모 노드를 방문할 수 있는 형식의 순회법이다.

의사코드로 나타내면
```
postorder(v)
  for each child w of v:
    postorder(v)
  visit(v)
```

## 너비 우선 트리 순회(Breadth-First Tre Traversal, a.k.a. BFT)
같은 depth의 노드를 좌측부터 순서대로 방문하고, 전부 방문한 후에 다음 depth의 노드에 대해 똑같은 짓을 반복한다.

의사코드로 나타내면
```
BFT(T)
  Q.enqueue(T.root())
   while not Q.is_empty:
    p=Q.dequeue()
    visit(p)
    for each child w of T.children(p):
      Q.enqueue(w)
```

## 중위 순회(Inorder Traversal)
임의의 subtree에서, 그 subtree의 왼쪽 자녀 노드를 root로 하는 subtree를 중위 순회하고, root를 방문한 다음, 오른쪽 자녀 노드를 root로 하는 subtree를 중위 순회한다.

의사코드로 나타내면
```
inorder(v)
  if v has a left child:
    inorder(left(v))
  if v has a right child:
    inorder(right(v))
```

