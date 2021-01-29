##  **1013** **Battle Over Cities** (25分)

It is vitally important to have all the cities connected by highways in a war. If a city is occupied by the enemy, all the highways from/toward that city are closed. We must know immediately if we need to repair any other highways to keep the rest of the cities connected. Given the map of cities which have all the remaining highways marked, you are supposed to tell the number of highways need to be repaired, quickly.

For example, if we have 3 cities and 2 highways connecting *c**i**t**y*1-*c**i**t**y*2 and *c**i**t**y*1-*c**i**t**y*3. Then if *c**i**t**y*1 is occupied by the enemy, we must have 1 highway repaired, that is the highway *c**i**t**y*2-*c**i**t**y*3.

### Input Specification:

Each input file contains one test case. Each case starts with a line containing 3 numbers *N* (<1000), *M* and *K*, which are the total number of cities, the number of remaining highways, and the number of cities to be checked, respectively. Then *M* lines follow, each describes a highway by 2 integers, which are the numbers of the cities the highway connects. The cities are numbered from 1 to *N*. Finally there is a line containing *K* numbers, which represent the cities we concern.

### Output Specification:

For each of the *K* cities, output in a line the number of highways need to be repaired if that city is lost.

### Sample Input:

```in
3 2 3
1 2
1 3
1 2 3
```

### Sample Output:

```out
1
0
0
```

### Code:

```c++
#include <cstring>
#include <iostream>
using namespace std;

int graph[1001][1001];
bool vis[1001] = {false};
int n, m, k;

void dfs(int v) {
    vis[v] = true;
    for (int i = 1; i <= n; i++) {
        if (!vis[i] && graph[v][i])
            dfs(i);
    }
}

int count() {
    int cnt = 0;
    for (int i = 1; i <= n; i++) {
        if (!vis[i]) {
            dfs(i);
            cnt++;
        }
    }
    memset(vis, false, sizeof(vis));
    return cnt;
}

int main() {
    cin >> n >> m >> k;
    int t1, t2, id;
    for (int i = 0; i < m; i++) {
        cin >> t1 >> t2;
        graph[t1][t2] = graph[t2][t1] = 1;
    }
    while (k--) {
        cin >> id;
        vis[id] = true;
        cout << count() - 1 << endl;
    }
    return 0;
}
```

