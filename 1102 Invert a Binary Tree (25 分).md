##  **1102 Invert a Binary Tree (25 分)** 

The following is from Max Howell @twitter:

```repl
Google: 90% of our engineers use the software you wrote (Homebrew), but you can't invert a binary tree on a whiteboard so fuck off.
```

Now it's your turn to prove that YOU CAN invert a binary tree!

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤10) which is the total number of nodes in the tree -- and hence the nodes are numbered from 0 to *N*−1. Then *N* lines follow, each corresponds to a node from 0 to *N*−1, and gives the indices of the left and right children of the node. If the child does not exist, a `-` will be put at the position. Any pair of children are separated by a space.

### Output Specification:

For each test case, print in the first line the level-order, and then in the second line the in-order traversal sequences of the inverted tree. There must be exactly one space between any adjacent numbers, and no extra space at the end of the line.

### Sample Input:

```in
8
1 -
- -
0 -
2 7
- -
- -
5 -
4 6
```

### Sample Output:

```out
3 7 2 6 4 0 5 1
6 5 7 4 3 2 0 1
```

### Idea:

- 这题有点憨啊，是先输入右孩子，再输入左孩子，不然得出的序列一个两两相反，一个彻底逆序

### Code:

```c++
#include <iostream>
#include <queue>
using namespace std;

typedef struct {
    int left = -1;
    int right = -1;
} Node;

Node node[11];
bool vis[11], flag = true;

void inorder(int root) {
    if (root == -1)
        return;
    inorder(node[root].left);
    if (flag) {
        cout << root;
        flag = false;
    } else {
        cout << " " << root;
    }
    inorder(node[root].right);
}

void levelorder(int root) {
    if (root == -1)
        return;
    queue<int> qe;
    qe.push(root);
    while (!qe.empty()) {
        int t = qe.front();
        qe.pop();
        if (flag) {
            cout << t;
            flag = false;
        } else {
            cout << " " << t;
        }
        if (node[t].left != -1)
            qe.push(node[t].left);
        if (node[t].right != -1)
            qe.push(node[t].right);
    }
}

int main() {
    int n, root;
    char left, right;
    cin >> n;
    getchar();
    for (int i = 0; i < n; i++) {
        cin >> right >> left;
        if (left != '-') {
            vis[left - '0'] = true;
            node[i].left = left - '0';
        }
        if (right != '-') {
            vis[right - '0'] = true;
            node[i].right = right - '0';
        }
    }
    for (int i = 0; i < n; i++) {
        if (!vis[i]) {
            root = i;
            break;
        }
    }
    levelorder(root);
    printf("\n");
    flag = true;
    inorder(root);
    return 0;
}
```

