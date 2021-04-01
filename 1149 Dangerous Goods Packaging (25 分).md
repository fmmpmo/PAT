##  **1149 Dangerous Goods Packaging (25 分)** 

When shipping goods with containers, we have to be careful not to pack some incompatible goods into the same container, or we might get ourselves in serious trouble. For example, oxidizing agent （氧化剂） must not be packed with flammable liquid （易燃液体）, or it can cause explosion.

Now you are given a long list of incompatible goods, and several lists of goods to be shipped. You are supposed to tell if all the goods in a list can be packed into the same container.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers: *N* (≤104), the number of pairs of incompatible goods, and *M* (≤100), the number of lists of goods to be shipped.

Then two blocks follow. The first block contains N pairs of incompatible goods, each pair occupies a line; and the second one contains M lists of goods to be shipped, each list occupies a line in the following format:

```
K G[1] G[2] ... G[K]
```

where `K` (≤1,000) is the number of goods and `G[i]`'s are the IDs of the goods. To make it simple, each good is represented by a 5-digit ID number. All the numbers in a line are separated by spaces.

### Output Specification:

For each shipping list, print in a line `Yes` if there are no incompatible goods in the list, or `No` if not.

### Sample Input:

```in
6 3
20001 20002
20003 20004
20005 20006
20003 20001
20005 20004
20004 20006
4 00001 20004 00002 20003
5 98823 20002 20003 20006 10010
3 12345 67890 23333
```

### Sample Output:

```out
No
Yes
Yes
```

### Idea:

- 由于一个货物可能有多个对应的危险品，所以需要用不定长数组vector存储，同时为了方便找到每个货物的危险品，使用map，这里由于对键排序没有要求，所以可以用快点的unordered_map
- 无论是使用find函数还是binary_search函数判断当前货物的危险品集合中是否有这个物品，第三个测试点都会超时，所以应该采用标记的方式。

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <unordered_map>
#include <vector>
using namespace std;

int main() {
    int n, m, k, id, a, b;
    scanf("%d %d", &n, &m);
    unordered_map<int, vector<int>> mp;
    for (int i = 0; i < n; i++) {
        scanf("%d %d", &a, &b);
        mp[a].push_back(b), mp[b].push_back(a);
    }
    while (m--) {
        scanf("%d", &k);
        int vis[100000] = {0};
        vector<int> v;
        for (int i = 0; i < k; i++) {
            scanf("%d", &id);
            vis[id] = 1;
            v.push_back(id);
        }
        bool flag = true;
        for (int i = 0; i < k; i++) {
            for (int j = 0; j < mp[v[i]].size(); j++) {
                if (vis[mp[v[i]][j]]) {
                    flag = false;
                    break;
                }
            }
            if (!flag)
                break;
        }
        flag ? printf("Yes\n") : printf("No\n");
    }
    return 0;
}
```

