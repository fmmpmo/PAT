##  **1110 Complete Binary Tree (25 分)** 

Given a tree, you are supposed to tell if it is a complete binary tree.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤20) which is the total number of nodes in the tree -- and hence the nodes are numbered from 0 to *N*−1. Then *N* lines follow, each corresponds to a node, and gives the indices of the left and right children of the node. If the child does not exist, a `-` will be put at the position. Any pair of children are separated by a space.

### Output Specification:

For each case, print in one line `YES` and the index of the last node if the tree is a complete binary tree, or `NO` and the index of the root if not. There must be exactly one space separating the word and the number.

### Sample Input 1:

```in
9
7 8
- -
- -
- -
0 1
2 3
4 5
- -
- -
```

### Sample Output 1:

```out
YES 8
```

### Sample Input 2:

```in
8
- -
4 5
0 6
- -
2 3
- 7
- -
- -
```

### Sample Output 2:

```out
NO 1
```

### Idea:

- 我是按照建树的方式来的，通过完全二叉树的特点，如果左子树为空，但右子树不为空，则肯定不是。如果左为空右不为空或者左右都为空，说明如果后边还有结点，则一定是左右都为空的。
- 注意测试点2 3 4，一定要注意编号可能是两位数（或者以上），所以一定要用字符串进行输入，而不能使char类型，这个测试点找了好久，直到看到一篇博客。https://blog.csdn.net/weixin_43684570/article/details/106375351

### Code:

```c++
#include <iostream>
#include <queue>
using namespace std;

typedef struct {
    int left, right;
} Node;

Node node[21];
bool vis[21];
int last, n;

bool judge(int root) {
    if (n == 1)
        return true;
    queue<int> qe;
    int cnt = 0;
    qe.push(root);
    bool isleaf = false;
    while (!qe.empty()) {
        int t = qe.front();
        cnt++;
        if(cnt == n)
            last = t;
        qe.pop();
        if (node[t].left == -1 && node[t].right != -1)
            return false;
        if (isleaf && (node[t].left != -1 || node[t].right != -1))
            return false;
        if (node[t].left == -1 && node[t].right == -1 ||
            node[t].left != -1 && node[t].right == -1)
            isleaf = true;
        if (node[t].left != -1)
            qe.push(node[t].left);
        if (node[t].right != -1)
            qe.push(node[t].right);
    }
    return true;
}

int main() {
    string left, right;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> left >> right;
        if (left[0] != '-') { // 一定要注意结点可能是两位数，所以不能用char类型输入，应用string
            int a = stoi(left);
            node[i].left = a;
            vis[a] = true;
        } else
            node[i].left = -1;
        if (right[0] != '-') {
            int b = stoi(right);
            vis[b] = true;
            node[i].right = b;
        } else
            node[i].right = -1;
    }
    int root;
    for (int i = 0; i < n; i++) {
        if (!vis[i]) {
            root = i;
            break;
        }
    }
    last = root;
    if (judge(root))
        cout << "YES " << last;
    else
        cout << "NO " << root;
    return 0;
}
```



