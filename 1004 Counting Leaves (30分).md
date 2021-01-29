##  **1004** **Counting Leaves** (30分)

A family hierarchy is usually presented by a pedigree tree. Your job is to count those family members who have no child.

### Input Specification:

Each input file contains one test case. Each case starts with a line containing 0<*N*<100, the number of nodes in a tree, and *M* (<*N*), the number of non-leaf nodes. Then *M* lines follow, each in the format:

```
ID K ID[1] ID[2] ... ID[K]
```

where `ID` is a two-digit number representing a given non-leaf node, `K` is the number of its children, followed by a sequence of two-digit `ID`'s of its children. For the sake of simplicity, let us fix the root ID to be `01`.

The input ends with *N* being 0. That case must NOT be processed.

### Output Specification:

For each test case, you are supposed to count those family members who have no child **for every seniority level** starting from the root. The numbers must be printed in a line, separated by a space, and there must be no extra space at the end of each line.

The sample case represents a tree with only 2 nodes, where `01` is the root and `02` is its only child. Hence on the root `01` level, there is `0` leaf node; and on the next level, there is `1` leaf node. Then we should output `0 1` in a line.

### Sample Input:

```in
2 1
01 1 02
```

### Sample Output:

```out
0 1
```

### Code:

```c++
#include <iostream>
#include <map>
#include <queue>
#include <vector>
using namespace std;

int main() {
    vector<vector<int>> v(101);
    queue<int> qe;
    map<int, int> m1, m2;
    int n, m, k, id, first;
    cin >> n >> m;
    for (int i = 0; i < m; i++) {
        cin >> first >> k;
        for (int j = 0; j < k; j++) {
            cin >> id;
            v[first].push_back(id);
        }
    }
    if (n == 1) {
        cout << 1;
        return 0;
    }
    qe.push(1);
    m1[1] = 1;
    while (!qe.empty()) {
        int t = qe.front();
        qe.pop();
        for (int i = 0; i < v[t].size(); i++) {
            m1[v[t][i]] = m1[t] + 1;
            qe.push(v[t][i]);
            if (v[v[t][i]].size() == 0) {
                m2[m1[t] + 1]++;
            }
        }
    }
    int level = 0;
    for (int i = 1; i <= n; i++) {
        level = max(level, m1[i]);
    }
    cout << 0;
    for (int i = 2; i <= level; i++) {
        cout << " " << m2[i];
    }
    return 0;
}
```

