# Problema-1200
# Atividade ESTD II




class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

class BST:
    def __init__(self):
        self.root = None

    def insert(self, key):
        self.root = self._insert(self.root, key)

    def _insert(self, node, key):
        if node is None:
            return Node(key)
        if key < node.key:
            node.left = self._insert(node.left, key)
        elif key > node.key:
            node.right = self._insert(node.right, key)
        return node

    def search(self, key):
        return self._search(self.root, key)

    def _search(self, node, key):
        if node is None:
            return False
        if key == node.key:
            return True
        elif key < node.key:
            return self._search(node.left, key)
        else:
            return self._search(node.right, key)

    def preorder(self, node, result):
        if node:
            result.append(node.key)
            self.preorder(node.left, result)
            self.preorder(node.right, result)

    def inorder(self, node, result):
        if node:
            self.inorder(node.left, result)
            result.append(node.key)
            self.inorder(node.right, result)

    def postorder(self, node, result):
        if node:
            self.postorder(node.left, result)
            self.postorder(node.right, result)
            result.append(node.key)


import sys
bst = BST()

for line in sys.stdin:
    parts = line.strip().split()
    if not parts:
        continue

    if parts[0] == "I":
        bst.insert(parts[1])
    elif parts[0] == "P":
        if bst.search(parts[1]):
            print(f"{parts[1]} existe")
        else:
            print(f"{parts[1]} nao existe")
    elif parts[0] == "INFIXA":
        result = []
        bst.inorder(bst.root, result)
        print(" ".join(result))
    elif parts[0] == "PREFIXA":
        result = []
        bst.preorder(bst.root, result)
        print(" ".join(result))
    elif parts[0] == "POSFIXA":
        result = []
        bst.postorder(bst.root, result)
        print(" ".join(result))
