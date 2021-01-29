##  **1099** **Build A Binary Search Tree** (30分)

A Binary Search Tree (BST) is recursively defined as a binary tree which has the following properties:

- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
- Both the left and right subtrees must also be binary search trees.

Given the structure of a binary tree and a sequence of distinct integer keys, there is only one way to fill these keys into the tree so that the resulting tree satisfies the definition of a BST. You are supposed to output the level order traversal sequence of that tree. The sample is illustrated by Figure 1 and 2.

![image-20210129171712162](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20210129171712162.png)

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤100) which is the total number of nodes in the tree. The next *N* lines each contains the left and the right children of a node in the format `left_index right_index`, provided that the nodes are numbered from 0 to *N*−1, and 0 is always the root. If one child is missing, then −1 will represent the NULL child pointer. Finally *N* distinct integer keys are given in the last line.

### Output Specification:

For each test case, print in one line the level order traversal sequence of that tree. All the numbers must be separated by a space, with no extra space at the end of the line.

### Sample Input:

```in
9
1 6
2 3
-1 -1
-1 4
5 -1
-1 -1
7 -1
-1 8
-1 -1
73 45 11 58 82 25 67 38 42
```

### Sample Output:

```out
58 25 82 11 38 67 45 73 42
```

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <queue>
using namespace std;

typedef struct {
    int data;
    int left;
    int right;
} Node;

Node node[101];
int num[101], n, pos = 0;

void create(int i) {
    if (i == -1)
        return;
    create(node[i].left);
    node[i].data = num[pos++];
    create(node[i].right);
}

void levelorder(int i) {
    if (i == -1)
        return;
    queue<Node> qe;
    qe.push(node[i]);
    bool flag = true;
    while (!qe.empty()) {
        Node t = qe.front();
        qe.pop();
        if (flag) {
            flag = false;
            printf("%d", t.data);
        } else {
            printf(" %d", t.data);
        }
        if (t.left != -1)
            qe.push(node[t.left]);
        if (t.right != -1)
            qe.push(node[t.right]);
    }
}

int main() {
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d %d", &node[i].left, &node[i].right);
    }
    for (int i = 0; i < n; i++) {
        scanf("%d", &num[i]);
    }
    sort(num, num + n);
    create(0);
    levelorder(0);
    return 0;
}
```

