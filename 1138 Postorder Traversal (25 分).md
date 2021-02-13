##  **1138 Postorder Traversal (25 分)** 

Suppose that all the keys in a binary tree are distinct positive integers. Given the preorder and inorder traversal sequences, you are supposed to output the first number of the postorder traversal sequence of the corresponding binary tree.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer N (≤ 50,000), the total number of nodes in the binary tree. The second line gives the preorder sequence and the third line gives the inorder sequence. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print in one line the first number of the postorder traversal sequence of the corresponding binary tree.

### Sample Input:

```in
7
1 2 3 4 5 6 7
2 3 1 5 4 7 6
```

### Sample Output:

```out
3
```

### Code:

```c++
#include <iostream>
using namespace std;

typedef struct Node {
    int data;
    struct Node *left, *right;
} Node, *Tree;

bool flag = false;

Tree create(int n, int *pre, int *in) {
    if (n < 1)
        return NULL;
    Tree tree = (Tree)malloc(sizeof(Node));
    tree->data = pre[0];
    tree->left = tree->right = NULL;
    int i;
    for (i = 0; i < n; i++) {
        if (pre[0] == in[i])
            break;
    }
    tree->left = create(i, pre + 1, in);
    tree->right = create(n - i - 1, pre + i + 1, in + i + 1);
    return tree;
}

void postorder(Tree tree) {
    if (!tree)
        return;
    postorder(tree->left);
    postorder(tree->right);
    if (!flag) {
        flag = true;
        cout << tree->data;
    }
}

int main() {
    int n;
    cin >> n;
    int pre[n], in[n];
    for (int i = 0; i < n; i++) {
        cin >> pre[i];
    }
    for (int i = 0; i < n; i++) {
        cin >> in[i];
    }
    Tree tree = create(n, pre, in);
    postorder(tree);
    return 0;
}
```

