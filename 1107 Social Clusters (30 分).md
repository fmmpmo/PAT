##  **1107 Social Clusters (30 分)** 

When register on a social network, you are always asked to specify your hobbies in order to find some potential friends with the same hobbies. A **social cluster** is a set of people who have some of their hobbies in common. You are supposed to find all the clusters.

### Input Specification:

Each input file contains one test case. For each test case, the first line contains a positive integer *N* (≤1000), the total number of people in a social network. Hence the people are numbered from 1 to *N*. Then *N* lines follow, each gives the hobby list of a person in the format:

*K**i*: *h**i*[1] *h**i*[2] ... *h**i*[*K**i*]

where *K**i* (>0) is the number of hobbies, and *h**i*[*j*] is the index of the *j*-th hobby, which is an integer in [1, 1000].

### Output Specification:

For each case, print in one line the total number of clusters in the network. Then in the second line, print the numbers of people in the clusters in non-increasing order. The numbers must be separated by exactly one space, and there must be no extra space at the end of the line.

### Sample Input:

```in
8
3: 2 7 10
1: 4
2: 5 3
1: 4
1: 3
1: 4
4: 6 8 1 5
1: 4
```

### Sample Output:

```out
3
4 3 1
```

### Code:

```c++
#include <algorithm>
#include <iostream>
using namespace std;

int f[1001], n, k, vis[1001];
int num[1001];

void init() {
    for (int i = 1; i <= n; i++) {
        f[i] = i;
    }
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
    scanf("%d", &n);
    init();
    int id;
    for (int i = 1; i <= n; i++) {
        scanf("%d:", &k);
        for (int j = 0; j < k; j++) {
            scanf("%d", &id);
            if (!vis[id])
                vis[id] = i;
            else
                merge(i, vis[id]);
        }
    }
    int cnt = 0;
    for (int i = 1; i <= n; i++) {
        int x = find(i);
        num[x]++;
    }
    for (int i = 1; i <= n; i++) {
        if (num[i])
            cnt++;
    }
    sort(num + 1, num + n + 1);
    printf("%d\n", cnt);
    bool flag = true;
    for (int i = n; i >= 1; i--) {
        if (num[i]) {
            if (flag) {
                flag = false;
                printf("%d", num[i]);
            } else
                printf(" %d", num[i]);
        } else
            break;
    }
    return 0;
}
```

