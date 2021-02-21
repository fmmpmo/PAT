##  **1122 Hamiltonian Cycle (25 分)** 

The "Hamilton cycle problem" is to find a simple cycle that contains every vertex in a graph. Such a cycle is called a "Hamiltonian cycle".

In this problem, you are supposed to tell if a given cycle is a Hamiltonian cycle.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 2 positive integers *N* (2<*N*≤200), the number of vertices, and *M*, the number of edges in an undirected graph. Then *M* lines follow, each describes an edge in the format `Vertex1 Vertex2`, where the vertices are numbered from 1 to *N*. The next line gives a positive integer *K* which is the number of queries, followed by *K* lines of queries, each in the format:

*n* *V*1 *V*2 ... *V**n*

where *n* is the number of vertices in the list, and *V**i*'s are the vertices on a path.

### Output Specification:

For each query, print in a line `YES` if the path does form a Hamiltonian cycle, or `NO` if not.

### Sample Input:

```in
6 10
6 2
3 4
1 5
2 5
3 1
4 1
1 6
6 3
1 2
4 5
6
7 5 1 4 3 6 2 5
6 5 1 4 3 6 2
9 6 2 1 6 3 4 5 2 6
4 1 2 5 1
7 6 1 3 4 5 2 6
7 6 1 2 5 4 3 1
```

### Sample Output:

```out
YES
NO
NO
NO
YES
NO
```

### Code:

```c++
#include <cstring>
#include <iostream>
using namespace std;

int graph[201][201];
int vis[201];

int main() {
    int n, m, t1, t2, k;
    scanf("%d %d", &n, &m);
    for (int i = 0; i < m; i++) {
        scanf("%d %d", &t1, &t2);
        graph[t1][t2] = graph[t2][t1] = 1;
    }
    scanf("%d", &k);
    int init, id, num, pre;
    while (k--) {
        bool flag = true;
        scanf("%d %d", &num, &pre);
        init = pre;
        vis[pre]++;
        for (int i = 2; i <= num; i++) {
            scanf("%d", &id);
            if (graph[pre][id])
                vis[id]++;
            else
                flag = false;
            pre = id;
        }
        if (vis[init] != 2)
            flag = false;
        for (int i = 1; i <= n; i++) {
            if (i != init && (!vis[i] || vis[i] > 1)) {
                flag = false;
                break;
            }
        }
        if (flag)
            printf("YES\n");
        else
            printf("NO\n");
        memset(vis, false, sizeof(vis));
    }
    return 0;
}
```

