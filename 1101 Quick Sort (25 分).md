##  **1101 Quick Sort (25 分)** 

There is a classical process named **partition** in the famous quick sort algorithm. In this process we typically choose one element as the pivot. Then the elements less than the pivot are moved to its left and those larger than the pivot to its right. Given *N* distinct positive integers after a run of partition, could you tell how many elements could be the selected pivot for this partition?

For example, given *N*=5 and the numbers 1, 3, 2, 4, and 5. We have:

- 1 could be the pivot since there is no element to its left and all the elements to its right are larger than it;
- 3 must not be the pivot since although all the elements to its left are smaller, the number 2 to its right is less than it as well;
- 2 must not be the pivot since although all the elements to its right are larger, the number 3 to its left is larger than it as well;
- and for the similar reason, 4 and 5 could also be the pivot.

Hence in total there are 3 pivot candidates.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤105). Then the next line contains *N* distinct positive integers no larger than 109. The numbers in a line are separated by spaces.

### Output Specification:

For each test case, output in the first line the number of pivot candidates. Then in the next line print these candidates in increasing order. There must be exactly 1 space between two adjacent numbers, and no extra space at the end of each line.

### Sample Input:

```in
5
1 3 2 4 5
```

### Sample Output:

```out
3
1 4 5
```

### Idea:

- 主元需要满足比它左边的任意一个数都大，比它右边的任意一个数都小。
- 只是满足上述条件是不行的，由于保证了第一条，则它当前所处的位置与排序后所处的位置应该是一样的。
- 同样，也是不行的，还需保证当前的元素是目前探测到的最大的元素。因为如 *1,4,3,2,中的3，但3显然不是符合条件的主元* 。、

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n;
    scanf("%d", &n);
    int a[n], b[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &a[i]);
        b[i] = a[i];
    }
    vector<int> v;
    sort(b, b + n);
    int maxn = 0;
    for (int i = 0; i < n; i++) {
        if (a[i] > maxn)
            maxn = a[i];
        if (a[i] == b[i] && a[i] == maxn)
            v.push_back(a[i]);
    }
    printf("%d\n", v.size());
    if (v.size() == 0) {
        printf("\n");
        return 0;
    }
    printf("%d", v[0]);
    for (int i = 1; i < v.size(); i++)
        printf(" %d", v[i]);
    return 0;
}
```

