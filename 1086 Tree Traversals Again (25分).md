##  **1086** **Tree Traversals Again** (25分)

An inorder binary tree traversal can be implemented in a non-recursive way with a stack. For example, suppose that when a 6-node binary tree (with the keys numbered from 1 to 6) is traversed, the stack operations are: push(1); push(2); push(3); pop(); pop(); push(4); pop(); pop(); push(5); push(6); pop(); pop(). Then a unique binary tree (shown in Figure 1) can be generated from this sequence of operations. Your task is to give the postorder traversal sequence of this tree.

![img](https://images.ptausercontent.com/30)
Figure 1

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive integer *N* (≤30) which is the total number of nodes in a tree (and hence the nodes are numbered from 1 to *N*). Then 2*N* lines follow, each describes a stack operation in the format: "Push X" where X is the index of the node being pushed onto the stack; or "Pop" meaning to pop one node from the stack.

### Output Specification:

For each test case, print the postorder traversal sequence of the corresponding tree in one line. A solution is guaranteed to exist. All the numbers must be separated by exactly one space, and there must be no extra space at the end of the line.

### Sample Input:

```in
6
Push 1
Push 2
Push 3
Pop
Pop
Push 4
Pop
Pop
Push 5
Push 6
Pop
Pop
```

### Sample Output:

```out
3 4 2 6 5 1
```

### Code:

```c++
#include <iostream>
#include <stack>
using namespace std;

typedef struct Node {
    int data;
    struct Node *left, *right;
} Node, *Tree;

bool flag = true;

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
    if (flag) {
        flag = false;
        cout << tree->data;
    } else {
        cout << " " << tree->data;
    }
}

int main() {
    stack<int> st;
    string index;
    int num, n, p = 0, k = 0;
    cin >> n;
    int pre[n], in[n];
    for (int i = 0; i < 2 * n; i++) {
        cin >> index;
        if (index == "Push") {
            cin >> num;
            st.push(num);
            pre[p++] = num;
        } else {
            in[k++] = st.top();
            st.pop();
        }
    }
    Tree tree = create(n, pre, in);
    postorder(tree);
    return 0;
}
```

