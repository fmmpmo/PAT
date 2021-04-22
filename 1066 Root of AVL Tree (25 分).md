##  **1066 Root of AVL Tree (25 分)** 

  An AVL tree is a self-balancing binary search tree. In an AVL tree, the heights of the two child subtrees of any node differ by at most one; if at any time they differ by more than one, rebalancing is done to restore this property. Figures 1-4 illustrate the rotation rules. 

 ![img](https://images.ptausercontent.com/33) 

 ![img](https://images.ptausercontent.com/34) 

Now given a sequence of insertions, you are supposed to tell the root of the resulting AVL tree.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive integer *N* (≤20) which is the total number of keys to be inserted. Then *N* distinct integer keys are given in the next line. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print the root of the resulting AVL tree in one line.

### Sample Input 1:

```in
5
88 70 61 96 120
```

### Sample Output 1:

```out
70
```

### Sample Input 2:

```
7
88 70 61 96 120 90 65
```

### Sample Output 2:

```
88
```

### Idea:

- AVL树的建立。固定模板即可。

### Code:

```c++
#include <iostream>
using namespace std;

typedef struct Node {
    int data;
    struct Node *left, *right;
} Node, *Tree;

Tree leftRotate(Tree tree) {
    Tree t = tree->right;
    tree->right = t->left;
    t->left = tree;
    return t;
}

Tree rightRotate(Tree tree) {
    Tree t = tree->left;
    tree->left = t->right;
    t->right = tree;
    return t;
}

Tree leftRightRotate(Tree tree) {
    tree->left = leftRotate(tree->left);
    return rightRotate(tree);
}

Tree rightLeftRotate(Tree tree) {
    tree->right = rightRotate(tree->right);
    return leftRotate(tree);
}

int getHeight(Tree tree) {
    if (!tree)
        return 0;
    int lh = getHeight(tree->left), rh = getHeight(tree->right);
    return max(lh, rh) + 1;
}

Tree insert(Tree tree, int num) {
    if (!tree) {
        tree = (Tree)malloc(sizeof(Node));
        tree->data = num;
        tree->left = tree->right = NULL;
    } else if (num < tree->data) {
        tree->left = insert(tree->left, num);
        int lh = getHeight(tree->left), rh = getHeight(tree->right);
        if (lh - rh >= 2) {
            if (num < tree->left->data)
                tree = rightRotate(tree);
            else
                tree = leftRightRotate(tree);
        }
    } else {
        tree->right = insert(tree->right, num);
        int lh = getHeight(tree->left), rh = getHeight(tree->right);
        if (rh - lh >= 2) {
            if (num > tree->right->data)
                tree = leftRotate(tree);
            else
                tree = rightLeftRotate(tree);
        }
    }
    return tree;
}

int main() {
    int n, num;
    Tree tree = NULL;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &num);
        tree = insert(tree, num);
    }
    cout << tree->data;
    return 0;
}
```

