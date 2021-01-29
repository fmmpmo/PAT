##  **1046** **Shortest Distance** (20分)

The task is really simple: given *N* exits on a highway which forms a simple cycle, you are supposed to tell the shortest distance between any pair of exits.

### Input Specification:

Each input file contains one test case. For each case, the first line contains an integer *N* (in [3,105]), followed by *N* integer distances *D*1 *D*2 ⋯ *D**N*, where *D**i* is the distance between the *i*-th and the (*i*+1)-st exits, and *D**N* is between the *N*-th and the 1st exits. All the numbers in a line are separated by a space. The second line gives a positive integer *M* (≤104), with *M* lines follow, each contains a pair of exit numbers, provided that the exits are numbered from 1 to *N*. It is guaranteed that the total round trip distance is no more than 107.

### Output Specification:

For each test case, print your results in *M* lines, each contains the shortest distance between the corresponding given pair of exits.

### Sample Input:

```in
5 1 2 4 14 9
3
1 3
2 5
4 1
```

### Sample Output:

```out
3
10
7
```

### Code:

```c++
#include <iostream>
using namespace std;

int main() {
    int n, m, s, e, sum = 0;
    scanf("%d", &n);
    int a[n + 1] = {0}, dis;
    for (int i = 1; i <= n; i++) {
        scanf("%d", &dis);
        sum += dis;
        a[i] = sum;
    }
    scanf("%d", &m);
    for (int i = 0; i < m; i++) {
        scanf("%d %d", &s, &e);
        if (s > e)
            swap(s, e);
        int sum1 = a[e - 1] - a[s - 1];
        printf("%d\n", min(sum1, sum - sum1));
    }
    return 0;
}

/*
int main() {
    int n, m, s, e, sum = 0;
    scanf("%d", &n);
    int a[n + 1];
    for (int i = 1; i <= n; i++) {
        scanf("%d", &a[i]);
        sum += a[i];
    }
    scanf("%d", &m);
    for (int i = 0; i < m; i++) {
        scanf("%d %d", &s, &e);
        int sum1 = 0;
        if (s > e)
            swap(s, e);
        while (s != e) { //最后一个测试点超时，17分
            sum1 += a[s];
            s++;
        }
        printf("%d\n", min(sum1, sum - sum1));
    }
    return 0;
}
*/
```

