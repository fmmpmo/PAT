##  **1115 Counting Nodes in a BST (30 分)** 

A Binary Search Tree (BST) is recursively defined as a binary tree which has the following properties:

- The left subtree of a node contains only nodes with keys less than or equal to the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

Insert a sequence of numbers into an initially empty binary search tree. Then you are supposed to count the total number of nodes in the lowest 2 levels of the resulting tree.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤1000) which is the size of the input sequence. Then given in the next line are the *N* integers in [−1000,1000] which are supposed to be inserted into an initially empty binary search tree.

### Output Specification:

For each case, print in one line the numbers of nodes in the lowest 2 levels of the resulting tree in the format:

```
n1 + n2 = n
```

where `n1` is the number of nodes in the lowest level, `n2` is that of the level above, and `n` is the sum.

### Sample Input:

```in
9
25 30 42 16 20 20 35 -5 28
```

### Sample Output:

```out
2 + 4 = 6
```

### Idea:

- 最底层的结点对应的高度最大，次底层的结点对应的高度为最大高度-1，所以可以通过求得每一个结点的高度来判断是否是最底层或次底层。

### Code:

```c++
#include <iostream>
#include <queue>
using namespace std;

typedef struct Node {
    int data;
    struct Node *left, *right;
    int h; //深度
} Node, *Tree;

int maxh = 0, cnt1 = 0, cnt2 = 0;

Tree create(Tree tree, int num) {
    if (!tree) {
        tree = (Tree)malloc(sizeof(Node));
        tree->data = num;
        tree->left = tree->right = NULL;
    } else if (num <= tree->data)
        tree->left = create(tree->left, num);
    else
        tree->right = create(tree->right, num);
    return tree;
}

void geth(Tree tree) {
    if (!tree)
        return;
    queue<Tree> qe;
    tree->h = 1;
    qe.push(tree);
    while (!qe.empty()) {
        Tree t = qe.front();
        qe.pop();
        if (t->h > maxh)
            maxh = t->h;
        if (t->left) {
            t->left->h = t->h + 1;
            qe.push(t->left);
        }
        if (t->right) {
            t->right->h = t->h + 1;
            qe.push(t->right);
        }
    }
}

void count(Tree tree) {
    if (!tree)
        return;
    if (tree->h == maxh)
        cnt1++;
    else if (tree->h == maxh - 1)
        cnt2++;
    count(tree->left);
    count(tree->right);
}

int main() {
    int n, num;
    cin >> n;
    Tree tree = NULL;
    for (int i = 0; i < n; i++) {
        cin >> num;
        tree = create(tree, num);
    }
    geth(tree);
    count(tree);
    printf("%d + %d = %d", cnt1, cnt2, cnt1 + cnt2);
    return 0;
}
```

