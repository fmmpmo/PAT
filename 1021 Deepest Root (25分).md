## **1021** **Deepest Root** (25分)

A graph which is connected and acyclic can be considered a tree. The height of the tree depends on the selected root. Now you are supposed to find the root that results in a highest tree. Such a root is called **the deepest root**.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive integer *N* (≤104) which is the number of nodes, and hence the nodes are numbered from 1 to *N*. Then *N*−1 lines follow, each describes an edge by given the two adjacent nodes' numbers.

### Output Specification:

For each test case, print each of the deepest roots in a line. If such a root is not unique, print them in increasing order of their numbers. In case that the given graph is not a tree, print `Error: K components` where `K` is the number of connected components in the graph.

### Sample Input 1:

```in
5
1 2
1 3
1 4
2 5
```

### Sample Output 1:

```out
3
4
5
```

### Sample Input 2:

```in
5
1 3
1 4
2 5
3 4
```

### Sample Output 2:

```out
Error: 2 components
```

### Code:

```c++
#include <cstring>
#include <iostream>
#include <vector>
using namespace std;

vector<int> graph[10001];//这种存储方式相当于邻接表
bool vis[10001] = {false};
int h = 0, n;

void dfs(int v, int height) {
    vis[v] = true;
    h = max(height, h);
    for (int i = 0; i < graph[v].size(); i++) {
        if (!vis[graph[v][i]])
            dfs(graph[v][i], height + 1);
    }
}

int main() {
    cin >> n;
    for (int i = 0; i < n - 1; i++) {
        int t1, t2;
        cin >> t1 >> t2;
        graph[t1].push_back(t2);
        graph[t2].push_back(t1);
    }
    int cnt = 0;
    for (int i = 1; i <= n; i++) {
        if (!vis[i]) {
            cnt++;
            dfs(i, 0);
        }
    }
    if (cnt > 1) {
        printf("Error: %d components", cnt);
        return 0;
    }
    int deep[n + 1], maxn = 0;
    for (int i = 1; i <= n; i++) {
        h = 0;
        memset(vis, false, sizeof(vis));
        dfs(i, 0);
        deep[i] = h;
        maxn = max(h, maxn);
    }
    for (int i = 1; i <= n; i++) {
        if (deep[i] == maxn)
            cout << i << endl;
    }
    return 0;
}
```

