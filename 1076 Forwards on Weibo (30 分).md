##  **1076 Forwards on Weibo (30 分)** 

Weibo is known as the Chinese version of Twitter. One user on Weibo may have many followers, and may follow many other users as well. Hence a social network is formed with followers relations. When a user makes a post on Weibo, all his/her followers can view and forward his/her post, which can then be forwarded again by their followers. Now given a social network, you are supposed to calculate the maximum potential amount of forwards for any specific user, assuming that only *L* levels of indirect followers are counted.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 2 positive integers: *N* (≤1000), the number of users; and *L* (≤6), the number of levels of indirect followers that are counted. Hence it is assumed that all the users are numbered from 1 to *N*. Then *N* lines follow, each in the format:

```
M[i] user_list[i]
```

where `M[i]` (≤100) is the total number of people that `user[i]` follows; and `user_list[i]` is a list of the `M[i]` users that followed by `user[i]`. It is guaranteed that no one can follow oneself. All the numbers are separated by a space.

Then finally a positive *K* is given, followed by *K* `UserID`'s for query.

### Output Specification:

For each `UserID`, you are supposed to print in one line the maximum potential amount of forwards this user can trigger, assuming that everyone who can view the initial post will forward it once, and that only *L* levels of indirect followers are counted.

### Sample Input:

```in
7 3
3 2 3 4
0
2 5 6
2 3 1
2 3 4
1 4
1 5
2 2 6
```

### Sample Output:

```out
4
5
```

### Idea:

- 样例中共有7个用户，转发层数上限为3，当2号用户发布信息时，第一层转发的用户是1号，第二层转发的用户是4号，第三层转发的用户是5号和6号，因此在转发层数上限内，共有四个用户转发。当6号用户发布信息时，第一层转发的用户是3号，第二层转发的用户是1号、4号和5号，第三层转发的用户是7号，因此在转发层数上限内，共有五个用户转发。
- 注意题目中给的的数据是用户关注的情况（而不是被关注的情况），因此如果用户X关注了用户Y，则需要建立由Y指向X的有向边，来表示Y发布的消息可以传递到X并被X转发，

### Code:

```c++
#include <cstring>
#include <iostream>
#include <queue>
#include <vector>
using namespace std;

typedef struct {
    int id;
    int level;
} User;

vector<User> users[1001];
bool vis[1001];

void bfs(int id, int l) {
    queue<User> qe;
    User us;
    us.id = id, us.level = 0;
    qe.push(us);
    vis[us.id] = true;
    int cnt = 0;
    while (!qe.empty()) {
        User t = qe.front();
        qe.pop();
        int u = t.id;
        for (int i = 0; i < users[u].size(); i++) {
            User x = users[u][i];
            x.level = t.level + 1;
            if (x.level <= l && !vis[x.id]) {
                qe.push(x);
                cnt++;
                vis[x.id] = true;
            }
        }
    }
    printf("%d\n", cnt);
    memset(vis, false, sizeof(vis));
}

int main() {
    int n, l, m, id;
    scanf("%d %d", &n, &l);
    for (int i = 1; i <= n; i++) {
        scanf("%d", &m);
        User tmp;
        tmp.id = i;
        for (int j = 0; j < m; j++) {
            scanf("%d", &id);
            users[id].push_back(tmp);
        }
    }
    int k;
    scanf("%d", &k);
    while (k--) {
        scanf("%d", &id);
        bfs(id, l);
    }
    return 0;
}
```

