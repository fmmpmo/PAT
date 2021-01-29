##  **1020** **Tree Traversals** (25分)

Suppose that all the keys in a binary tree are distinct positive integers. Given the postorder and inorder traversal sequences, you are supposed to output the level order traversal sequence of the corresponding binary tree.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤30), the total number of nodes in the binary tree. The second line gives the postorder sequence and the third line gives the inorder sequence. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print in one line the level order traversal sequence of the corresponding binary tree. All the numbers in a line must be separated by exactly one space, and there must be no extra space at the end of the line.

### Sample Input:

```in
7
2 3 1 5 7 6 4
1 2 3 4 5 6 7
```

### Sample Output:

```out
4 1 6 3 5 7 2
```

### Code:

```c++
#include <iostream>
#include <queue>
using namespace std;

typedef struct Node {
    int data;
    struct Node *left, *right;
} Node, *Tree;

Tree create(int n, int *in, int *post) {
    if (n < 1)
        return NULL;
    Tree tree = (Tree)malloc(sizeof(Node));
    tree->data = post[n - 1];
    tree->left = tree->right = NULL;
    int i;
    for (i = 0; i < n; i++) {
        if (in[i] == post[n - 1])
            break;
    }
    tree->left = create(i, in, post);
    tree->right = create(n - i - 1, in + i + 1, post + i);
    return tree;
}

void levelorder(Tree tree) {
    if (!tree)
        return;
    queue<Tree> qe;
    qe.push(tree);
    bool flag = true;
    while (!qe.empty()) {
        Tree t = qe.front();
        qe.pop();
        if (flag) {
            cout << t->data;
            flag = false;
        } else {
            cout << " " << t->data;
        }
        if (t->left)
            qe.push(t->left);
        if (t->right)
            qe.push(t->right);
    }
}

int main() {
    int n;
    cin >> n;
    int post[n], in[n];
    for (int i = 0; i < n; i++) {
        cin >> post[i];
    }
    for (int i = 0; i < n; i++) {
        cin >> in[i];
    }
    Tree tree = create(n, in, post);
    levelorder(tree);
    return 0;
}
```

