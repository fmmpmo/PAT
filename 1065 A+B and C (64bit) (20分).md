##  **1065** **A+B and C (64bit)** (20分)

Given three integers *A*, *B* and *C* in [−263,263], you are supposed to tell whether *A*+*B*>*C*.

### Input Specification:

The first line of the input gives the positive number of test cases, *T* (≤10). Then *T* test cases follow, each consists of a single line containing three integers *A*, *B* and *C*, separated by single spaces.

### Output Specification:

For each test case, output in one line `Case #X: true` if *A*+*B*>*C*, or `Case #X: false` otherwise, where *X* is the case number (starting from 1).

### Sample Input:

```in
3
1 2 3
2 3 4
9223372036854775807 -9223372036854775808 0
```

### Sample Output:

```out
Case #1: false
Case #2: true
Case #3: false
```

### Code:

```c++
#include <iostream>
using namespace std;

typedef long long ll;

int main() {
    ll a, b, c;
    int t;
    scanf("%d", &t);
    for (int i = 1; i <= t; i++) {
        scanf("%lld %lld %lld", &a, &b, &c);
        ll res = a + b;
        if (a > 0 && b > 0 && res < 0)
            printf("Case #%d: true\n", i);
        else if (a < 0 && b < 0 && res >= 0)
            printf("Case #%d: false\n", i);
        else if (res > c)
            printf("Case #%d: true\n", i);
        else
            printf("Case #%d: false\n", i);
    }
    return 0;
}
```

