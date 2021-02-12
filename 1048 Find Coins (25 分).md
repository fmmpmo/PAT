##  **1048 Find Coins (25 分)** 

Eva loves to collect coins from all over the universe, including some other planets like Mars. One day she visited a universal shopping mall which could accept all kinds of coins as payments. However, there was a special requirement of the payment: for each bill, she could only use exactly two coins to pay the exact amount. Since she has as many as 105 coins with her, she definitely needs your help. You are supposed to tell her, for any given amount of money, whether or not she can find two coins to pay for it.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 2 positive numbers: *N* (≤105, the total number of coins) and *M* (≤103, the amount of money Eva has to pay). The second line contains *N* face values of the coins, which are all positive numbers no more than 500. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print in one line the two face values *V*1 and *V*2 (separated by a space) such that *V*1+*V*2=*M* and *V*1≤*V*2. If such a solution is not unique, output the one with the smallest *V*1. If there is no solution, output `No Solution` instead.

### Sample Input 1:

```in
8 15
1 2 8 7 2 4 11 15
```

### Sample Output 1:

```out
4 11
```

### Sample Input 2:

```in
7 14
1 8 7 2 4 11 15
```

### Sample Output 2:

```out
No Solution
```

### Idea:

- 不能遍历去寻找，会有测试点超时（应该是测试点2和3），因为本身寻找的过程就是耗时间的，需要寻找其他办法
- 本人想的方法是对出现过的数进行标记，因为有可能有所选取的两个coin是一样大小的，只进行是否存在的0和1标记是不可行的，所以每出现一个数，其所在位置的计数器就++。
- 遍历寻找的时候，要分两种情况自然，相等情况和不相等情况，注意当不相等时，有可能会出现m-x(x为当前所选取的较小icon)为负数的情况，这样下标就错了，所以需要提前判断一下。

### Code:

```c++
#include <algorithm>
#include <iostream>
using namespace std;

int main() {
    int n, m;
    int a[100001], vis[1001] = {0};
    scanf("%d %d", &n, &m);
    for (int i = 0; i < n; i++) {
        scanf("%d", &a[i]);
        vis[a[i]]++;
    }
    sort(a, a + n);
    for (int i = 0; i < n; i++) {
        int x = a[i];
        if (x == m - x && vis[x] > 1 || x != m - x && m - x > 0 && vis[m - x] >= 1) {
            printf("%d %d", x, m - x);
            return 0;
        }
    }
    printf("No Solution");
    return 0;
}
```

