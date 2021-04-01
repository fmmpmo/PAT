##  **1118 Birds in Forest (25 分)** 

Some scientists took pictures of thousands of birds in a forest. Assume that all the birds appear in the same picture belong to the same tree. You are supposed to help the scientists to count the maximum number of trees in the forest, and for any pair of birds, tell if they are on the same tree.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive number *N* (≤104) which is the number of pictures. Then *N* lines follow, each describes a picture in the format:

*K* *B*1 *B*2 ... *B**K*

where *K* is the number of birds in this picture, and *B**i*'s are the indices of birds. It is guaranteed that the birds in all the pictures are numbered continuously from 1 to some number that is no more than 104.

After the pictures there is a positive number *Q* (≤104) which is the number of queries. Then *Q* lines follow, each contains the indices of two birds.

### Output Specification:

For each test case, first output in a line the maximum possible number of trees and the number of birds. Then for each query, print in a line `Yes` if the two birds belong to the same tree, or `No` if not.

### Sample Input:

```in
4
3 10 1 2
2 3 4
4 1 5 7 8
3 9 6 4
2
10 5
3 7
```

### Sample Output:

```out
2 10
Yes
No
```

### Idea:

- 简易并查集问题，由于我初始化并查集数组的时候是把祖先设成了自己，即自己是一个集合，但题目中已经明确说明，输入的编号是1~10000之间随机的数，所以需要设置一个标记看是否出现过这个人，否则最后看有多少棵树的时候会多算

### Code:

```c++
#include <iostream>
#include <unordered_set>
using namespace std;

int f[10001];
bool vis[10001];

void init() {
    for (int i = 1; i <= 10000; i++)
        f[i] = i;
}

int find(int x) {
    if (x == f[x])
        return x;
    return f[x] = find(f[x]);
}

void merge(int x, int y) {
    int a = find(x), b = find(y);
    if (a != b)
        f[b] = a;
}

int main() {
    int n, k, first, id, q, a, b;
    scanf("%d", &n);
    init();
    unordered_set<int> st;
    for (int i = 0; i < n; i++) {
        scanf("%d %d", &k, &first);
        st.insert(first);
        vis[first] = true;
        for (int j = 0; j < k - 1; j++) {
            scanf("%d", &id);
            merge(first, id);
            vis[id] = true;
            st.insert(id);
        }
    }
    int cnt = 0;
    for (int i = 1; i <= 10000; i++) {
        if (f[i] == i && vis[i])
            cnt++;
    }
    printf("%d %d\n", cnt, st.size());
    scanf("%d", &q);
    for (int i = 0; i < q; i++) {
        scanf("%d %d", &a, &b);
        int x = find(a), y = find(b);
        x == y ? printf("Yes\n") : printf("No\n");
    }
    return 0;
}
```

