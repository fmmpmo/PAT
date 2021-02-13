##  **1146 Topological Order (25 分)** 

This is a problem given in the Graduate Entrance Exam in 2018: Which of the following is NOT a topological order obtained from the given directed graph? Now you are supposed to write a program to test each of the options.

![gre.jpg](https://images.ptausercontent.com/5d35ed2a-4d19-4f13-bf3f-35ed59cebf05.jpg)

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers N (≤ 1,000), the number of vertices in the graph, and M (≤ 10,000), the number of directed edges. Then M lines follow, each gives the start and the end vertices of an edge. The vertices are numbered from 1 to N. After the graph, there is another positive integer K (≤ 100). Then K lines of query follow, each gives a permutation of all the vertices. All the numbers in a line are separated by a space.

### Output Specification:

Print in a line all the indices of queries which correspond to "NOT a topological order". The indices start from zero. All the numbers are separated by a space, and there must no extra space at the beginning or the end of the line. It is graranteed that there is at least one answer.

### Sample Input:

```in
6 8
1 2
1 3
5 2
5 4
2 3
2 6
3 4
6 4
5
1 5 2 3 6 4
5 1 2 6 3 4
5 1 2 3 6 4
5 2 1 6 3 4
1 2 3 4 5 6
```

### Sample Output:

```out
3 4
```

### Idea:

- 存储边，拓扑序列每次选取的应该是入度为0的顶点，所以解决也从这里下手
- 当当前输入的数是某条边的终点（弧头）时，若其起点（弧尾）未被访问，即仍有边指向该顶点，则说明该顶点的入度此时并不为0，不能选取，即该序列不是合法的拓扑排序序列。

### Code:

```c++
#include <cstring>
#include <iostream>
#include <vector>
using namespace std;

typedef struct {
    int from, to;
} Node;

int n, m, k;
vector<Node> v;
bool vis[1001], flag = true;

int main() {
    scanf("%d %d", &n, &m);
    Node node;
    for (int i = 0; i < m; i++) {
        scanf("%d %d", &node.from, &node.to);
        v.push_back(node);
    }
    scanf("%d", &k);
    int id;
    for (int i = 0; i < k; i++) {
        bool islegel = true;
        for (int j = 0; j < n; j++) {
            scanf("%d", &id);
            if (!islegel)
                continue;
            for (int p = 0; p < m; p++) {
                if (v[p].to == id && !vis[v[p].from]) {
                    islegel = false;
                    break;
                }
            }
            vis[id] = true;
        }
        if (!islegel) {
            if (flag) {
                flag = false;
                printf("%d", i);
            } else {
                printf(" %d", i);
            }
        }
        memset(vis, false, sizeof(vis));
    }
    return 0;
}
```

