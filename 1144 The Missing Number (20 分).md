##  **1144 The Missing Number (20 分)** 

Given N integers, you are supposed to find the smallest positive integer that is NOT in the given list.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer N (≤105). Then N integers are given in the next line, separated by spaces. All the numbers are in the range of **int**.

### Output Specification:

Print in a line the smallest positive integer that is missing from the input list.

### Sample Input:

```in
10
5 -25 9 6 1 3 4 2 5 17
```

### Sample Output:

```out
7
```

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n, num;
    vector<int> v;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &num);
        if (num >= 0)
            v.push_back(num);
    }
    if (v.size() == 0) {
        printf("1");
        return 0;
    } else if (v.size() == 1) {
        printf("%d", v[0] + 1);
        return 0;
    }
    sort(v.begin(), v.end());
    for (int i = 1; i < v.size(); i++) {
        if (v[i] - v[i - 1] > 1) {
            printf("%d", v[i - 1] + 1);
            break;
        }
        if (i == v.size() - 1)
            printf("%d", v[i] + 1);
    }
    return 0;
}
```

