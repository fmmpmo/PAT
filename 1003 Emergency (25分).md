##  **1003** **Emergency** (25分)

As an emergency rescue team leader of a city, you are given a special map of your country. The map shows several scattered cities connected by some roads. Amount of rescue teams in each city and the length of each road between any pair of cities are marked on the map. When there is an emergency call to you from some other city, your job is to lead your men to the place as quickly as possible, and at the mean time, call up as many hands on the way as possible.

### Input Specification:

Each input file contains one test case. For each test case, the first line contains 4 positive integers: *N* (≤500) - the number of cities (and the cities are numbered from 0 to *N*−1), *M* - the number of roads, *C*1 and *C*2 - the cities that you are currently in and that you must save, respectively. The next line contains *N* integers, where the *i*-th integer is the number of rescue teams in the *i*-th city. Then *M* lines follow, each describes a road with three integers *c*1, *c*2 and *L*, which are the pair of cities connected by a road and the length of that road, respectively. It is guaranteed that there exists at least one path from *C*1 to *C*2.

### Output Specification:

For each test case, print in one line two numbers: the number of different shortest paths between *C*1 and *C*2, and the maximum amount of rescue teams you can possibly gather. All the numbers in a line must be separated by exactly one space, and there is no extra space allowed at the end of a line.

### Sample Input:

```in
5 6 0 2
1 2 1 5 3
0 1 1
0 2 2
0 3 1
1 2 1
2 4 1
3 4 1
```

### Sample Output:

```out
2 4
```

### Code:

```c++
#include <iostream>
using namespace std;

int graph[501][501], save[501], num[501], cnt[501];
bool vis[501] = {false};
int dis[501];
const int inf = 65535;
int n, m, c1, c2;

void init() {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (i == j)
                graph[i][j] = 0;
            else
                graph[i][j] = inf;
        }
    }
}

void dijkstra() {
    num[c1] = 1;
    int u;
    cnt[c1] = save[c1];
    for (int i = 0; i < n; i++) {
        int minx = inf;
        for (int j = 0; j < n; j++) {
            if (!vis[j] && dis[j] < minx) {
                minx = dis[j];
                u = j;
            }
        }
        vis[u] = true;
        for (int j = 0; j < n; j++) {
            if (!vis[j] && dis[j] > dis[u] + graph[u][j]) {
                dis[j] = dis[u] + graph[u][j];
                num[j] = num[u];
                cnt[j] = cnt[u] + save[j];
            } else if (!vis[j] && dis[j] == dis[u] + graph[u][j]) {
                num[j] = num[u] + num[j];
                cnt[j] = max(cnt[u] + save[j], cnt[j]);
            }
        }
    }
}

int main() {
    cin >> n >> m >> c1 >> c2;
    init();
    for (int i = 0; i < n; i++) {
        cin >> save[i];
    }
    for (int i = 0; i < m; i++) {
        int t1, t2, t3;
        cin >> t1 >> t2 >> t3;
        graph[t1][t2] = graph[t2][t1] = t3;
    }
    for (int i = 0; i < n; i++) {
        dis[i] = graph[c1][i];
    }
    dijkstra();
    cout << num[c2] << " " << cnt[c2];
    return 0;
}
```

