##  **1123 Is It a Complete AVL Tree (30 分)** 

 An AVL tree is a self-balancing binary search tree. In an AVL tree, the heights of the two child subtrees of any node differ by at most one; if at any time they differ by more than one, rebalancing is done to restore this property. Figures 1-4 illustrate the rotation rules. 

 ![F1.jpg](https://images.ptausercontent.com/fb337acb-93b0-4af2-9838-deff5ce98058.jpg)  

![F2.jpg](https://images.ptausercontent.com/d1635de7-3e3f-4aaa-889b-ba29f35890db.jpg) 

 ![F3.jpg](https://images.ptausercontent.com/e868e4b9-9fea-4f70-b7a7-1f5d8a3be4ef.jpg) 

 ![F4.jpg](https://images.ptausercontent.com/98aa1782-cea5-4792-8736-999436cf43a9.jpg) 

Now given a sequence of insertions, you are supposed to output the level-order traversal sequence of the resulting AVL tree, and to tell if it is a complete binary tree.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive integer N (≤ 20). Then N distinct integer keys are given in the next line. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, insert the keys one by one into an initially empty AVL tree. Then first print in a line the level-order traversal sequence of the resulting AVL tree. All the numbers in a line must be separated by a space, and there must be no extra space at the end of the line. Then in the next line, print `YES` if the tree is complete, or `NO` if not.

### Sample Input 1:

```in
5
88 70 61 63 65
```

### Sample Output 1:

```out
70 63 88 61 65
YES
```

### Sample Input 2:

```in
8
88 70 61 96 120 90 65 68
```

### Sample Output 2:

```out
88 65 96 61 70 90 120 68
NO
```

### Idea:

- AVL树学的一向不是很好，参考了柳神的解题思路和代码，放上链接，励志记住AVL树的操作思路和模板。https://blog.csdn.net/liuchuo/article/details/53561924

### Code:

```c++
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

typedef struct Node {
    int data;
    struct Node *left, *right;
} Node, *Tree;

bool flag = true;
vector<int> v;

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

void levelOrder(Tree tree) {
    if (!tree)
        return;
    queue<Tree> qe;
    qe.push(tree);
    bool isleaf = false;
    while (!qe.empty()) {
        Tree t = qe.front();
        qe.pop();
        v.push_back(t->data);
        if (!t->left && t->right)
            flag = false;
        if (isleaf && (t->left || t->right))
            flag = false;
        if (!isleaf && (t->left && !t->right || !t->left && !t->right))
            isleaf = true;
        if (t->left)
            qe.push(t->left);
        if (t->right)
            qe.push(t->right);
    }
}

int main() {
    int n, num;
    Tree tree = NULL;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &num);
        tree = insert(tree, num);
    }
    levelOrder(tree);
    for (int i = 0; i < v.size(); i++) {
        if (i > 0)
            printf(" ");
        printf("%d", v[i]);
    }
    flag ? printf("\nYES") : printf("\nNO");
    return 0;
}
```

