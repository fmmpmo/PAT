##  **1155 Heap Paths (30 分)** 

In computer science, a **heap** is a specialized tree-based data structure that satisfies the heap property: if P is a parent node of C, then the key (the value) of P is either greater than or equal to (in a max heap) or less than or equal to (in a min heap) the key of C. A common implementation of a heap is the binary heap, in which the tree is a complete binary tree. (Quoted from Wikipedia at https://en.wikipedia.org/wiki/Heap_(data_structure))

One thing for sure is that all the keys along any path from the root to a leaf in a max/min heap must be in non-increasing/non-decreasing order.

Your job is to check every path in a given complete binary tree, in order to tell if it is a heap or not.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (1<*N*≤1,000), the number of keys in the tree. Then the next line contains *N* distinct integer keys (all in the range of **int**), which gives the level order traversal sequence of a complete binary tree.

### Output Specification:

For each given tree, first print all the paths from the root to the leaves. Each path occupies a line, with all the numbers separated by a space, and no extra space at the beginning or the end of the line. The paths must be printed in the following order: for each node in the tree, all the paths in its right subtree must be printed before those in its left subtree.

Finally print in a line `Max Heap` if it is a max heap, or `Min Heap` for a min heap, or `Not Heap` if it is not a heap at all.

### Sample Input 1:

```in
8
98 72 86 60 65 12 23 50
```

### Sample Output 1:

```out
98 86 23
98 86 12
98 72 65
98 72 60 50
Max Heap
```

### Sample Input 2:

```in
8
8 38 25 58 52 82 70 60
```

### Sample Output 2:

```out
8 25 70
8 25 82
8 38 52
8 38 58 60
Min Heap
```

### Sample Input 3:

```in
8
10 28 15 12 34 9 8 56
```

### Sample Output 3:

```out
10 15 8
10 15 9
10 28 34
10 28 12 56
Not Heap
```

### Idea:

- 由于是完全二叉树，所以很容易想到的是采用顺序存储的方式。然后下标从1开始会方便一点，看个人习惯
- 关于最大堆，最小堆，不是堆的判断，就按照最大堆，最小堆的定义来就可以了，从第一个非叶结点开始判断，即编号为n/2的结点，因为叶结点肯定是符合定义的，毕竟它没有孩子啊
- 对于输出路径，我采用的是右、左的遍历方式，这样就可以做到先访问右子树再访问左子树，且可以做到按照层序搜索。

### Code:

```c++
#include <iostream>
#include <stack>
#include <vector>
using namespace std;

int a[1001], n;
vector<int> v;

bool maxheap() {
    for (int i = n / 2; i >= 1; i--) {
        if (2 * i <= n) {
            if (a[i] < a[2 * i])
                return false;
        }
        if (2 * i + 1 <= n) {
            if (a[i] < a[2 * i + 1])
                return false;
        }
    }
    return true;
}

void order(int i) {
    if (i > n)
        return;
    if (2 * i > n) {
        v.push_back(i);
        return;
    }
    order(2 * i + 1);
    order(2 * i);
}

bool minheap() {
    for (int i = n / 2; i >= 1; i--) {
        if (2 * i <= n) {
            if (a[i] > a[2 * i])
                return false;
        }
        if (2 * i + 1 <= n) {
            if (a[i] > a[2 * i + 1])
                return false;
        }
    }
    return true;
}

int main() {
    scanf("%d", &n);
    for (int i = 1; i <= n; i++) {
        scanf("%d", &a[i]);
    }
    order(1);
    for (int i = 0; i < v.size(); i++) {
        int k = v[i];
        stack<int> st;
        bool flag = true;
        while (k >= 1) {
            st.push(a[k]);
            k /= 2;
        }
        while (!st.empty()) {
            if (flag) {
                flag = false;
                printf("%d", st.top());
            } else {
                printf(" %d", st.top());
            }
            st.pop();
        }
        printf("\n");
    }
    if (maxheap())
        printf("Max Heap");
    else if (minheap())
        printf("Min Heap");
    else
        printf("Not Heap");
    return 0;
}
```

