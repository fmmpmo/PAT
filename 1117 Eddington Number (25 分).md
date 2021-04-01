##  **1117 Eddington Number (25 分)** 

British astronomer Eddington liked to ride a bike. It is said that in order to show off his skill, he has even defined an "Eddington number", *E* -- that is, the maximum integer *E* such that it is for *E* days that one rides more than *E* miles. Eddington's own *E* was 87.

Now given everyday's distances that one rides for *N* days, you are supposed to find the corresponding *E* (≤*N*).

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤105), the days of continuous riding. Then *N* non-negative integers are given in the next line, being the riding distances of everyday.

### Output Specification:

For each case, print in a line the Eddington number for these *N* days.

### Sample Input:

```in
10
6 7 6 9 3 10 8 2 7 8
```

### Sample Output:

```out
6
```

### Idea:

- 可以从前往后找，因为是有E天的骑行路程大于E，所以找到大于的就停止即可。前提是排好序
- 如果只是这么写，测试点4错误，只能得24分，这是因为如果没有符合条件的，按照我写的是没有输出的，而实际上应该输出0，所以判断一下标志变量的值即可。

### Code:

```c++
#include <algorithm>
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n;
    int a[n];
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }
    sort(a, a + n);
    bool flag = false;
    for (int i = 0; i < n; i++) {
        if (a[i] > n - i) {
            cout << n - i;
            flag = true;
            break;
        }
    }
    if (!flag)
        cout << 0;
    return 0;
}
```

