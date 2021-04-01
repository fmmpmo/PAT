##  **1017 Queueing at Bank (25 分)** 

Suppose a bank has *K* windows open for service. There is a yellow line in front of the windows which devides the waiting area into two parts. All the customers have to wait in line behind the yellow line, until it is his/her turn to be served and there is a window available. It is assumed that no window can be occupied by a single customer for more than 1 hour.

Now given the arriving time *T* and the processing time *P* of each customer, you are supposed to tell the average waiting time of all the customers.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 2 numbers: *N* (≤104) - the total number of customers, and *K* (≤100) - the number of windows. Then *N* lines follow, each contains 2 times: `HH:MM:SS` - the arriving time, and *P* - the processing time in minutes of a customer. Here `HH` is in the range [00, 23], `MM` and `SS` are both in [00, 59]. It is assumed that no two customers arrives at the same time.

Notice that the bank opens from 08:00 to 17:00. Anyone arrives early will have to wait in line till 08:00, and anyone comes too late (at or after 17:00:01) will not be served nor counted into the average.

### Output Specification:

For each test case, print in one line the average waiting time of all the customers, in minutes and accurate up to 1 decimal place.

### Sample Input:

```in
7 3
07:55:00 16
17:00:01 2
07:59:59 15
08:01:00 60
08:00:00 30
08:00:02 2
08:03:00 10
```

### Sample Output:

```out
8.2
```

### Idea:

- 自己想的思路自己都蒙，写的一塌糊涂，参考的柳神的答案 https://blog.csdn.net/liuchuo/article/details/54573734

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <queue>
using namespace std;

typedef struct {
    int come;
    int time;
} Per;

Per per[10001];

bool cmp(Per p1, Per p2) { return p1.come < p2.come; }

int main() {
    int n, k, h, m, s, time;
    bool flag = false;
    scanf("%d %d", &n, &k);
    int index = 0;
    for (int i = 0; i < n; i++) {
        scanf("%d:%d:%d %d", &h, &m, &s, &time);
        int come = h * 3600 + m * 60 + s;
        if (come > 61200)
            continue;
        flag = true;
        per[index].time = time * 60;
        per[index].come = come;
        index++;
    }
    sort(per, per + index, cmp);
    priority_queue<int, vector<int>, greater<int>> qe;
    for (int i = 0; i < k; i++) {
        qe.push(28800);
    }
    int ans;
    for (int i = 0; i < index; i++) {
        if (qe.top() <= per[i].come) {
            qe.push(per[i].come + per[i].time);
            qe.pop();
        } else {
            ans += qe.top() - per[i].come;
            qe.push(qe.top() + per[i].time);
            qe.pop();
        }
    }
    flag ? printf("%.1lf", ans * 1.0 / 60.0 / index) : printf("0.0\n");
    return 0;
}
```

