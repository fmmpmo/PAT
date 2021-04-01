##  **1121 Damn Single (25 分)** 

"Damn Single (单身狗)" is the Chinese nickname for someone who is being single. You are supposed to find those who are alone in a big party, so they can be taken care of.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer N (≤ 50,000), the total number of couples. Then N lines of the couples follow, each gives a couple of ID's which are 5-digit numbers (i.e. from 00000 to 99999). After the list of couples, there is a positive integer M (≤ 10,000) followed by M ID's of the party guests. The numbers are separated by spaces. It is guaranteed that nobody is having bigamous marriage (重婚) or dangling with more than one companion.

### Output Specification:

First print in a line the total number of lonely guests. Then in the next line, print their ID's in increasing order. The numbers must be separated by exactly 1 space, and there must be no extra space at the end of the line.

### Sample Input:

```in
3
11111 22222
33333 44444
55555 66666
7
55555 44444 10000 88888 22222 11111 23333
```

### Sample Output:

```out
5
10000 23333 44444 55555 88888
```

### Idea:

- 把每个人的伴侣存起来，待查询的人中，每个人也都存一遍，因为需要都输入完后才能判断是不是单身狗，同时把待查询的人的编号都标记为已出现过
- 单身狗有两种情况：一种是输入的couple中根本没有出现过的编号。另一种是虽然出现过，但是它的伴侣却没有在m个人当中，此时也会被判定为是单身狗。

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <set>
#include <unordered_map>
#include <vector>
using namespace std;

int main() {
    int n, m, a, b, id;
    scanf("%d", &n);
    unordered_map<int, int> mp;
    while (n--) {
        scanf("%d %d", &a, &b);
        mp[a] = b, mp[b] = a;
    }
    scanf("%d", &m);
    set<int> st;
    int vis[100000] = {0};
    vector<int> v;
    for (int i = 0; i < m; i++) {
        scanf("%d", &id);
        vis[id] = 1;
        v.push_back(id);
    }
    for (int i = 0; i < m; i++) {
        if (mp.find(v[i]) == mp.end() || !vis[mp[v[i]]])
            st.insert(v[i]);
    }
    printf("%d\n", st.size());
    for (auto it = st.begin(); it != st.end(); it++) {
        if (it != st.begin())
            printf(" ");
        printf("%05d", *it);
    }
    return 0;
}
```

