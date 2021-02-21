##  **1063 Set Similarity (25 分)** 

Given two sets of integers, the similarity of the sets is defined to be *N**c*/*N**t*×100%, where *N**c* is the number of distinct common numbers shared by the two sets, and *N**t* is the total number of distinct numbers in the two sets. Your job is to calculate the similarity of any given pair of sets.

### Input Specification:

Each input file contains one test case. Each case first gives a positive integer *N* (≤50) which is the total number of sets. Then *N* lines follow, each gives a set with a positive *M* (≤104) and followed by *M* integers in the range [0,109]. After the input of sets, a positive integer *K* (≤2000) is given, followed by *K* lines of queries. Each query gives a pair of set numbers (the sets are numbered from 1 to *N*). All the numbers in a line are separated by a space.

### Output Specification:

For each query, print in one line the similarity of the sets, in the percentage form accurate up to 1 decimal place.

### Sample Input:

```in
3
3 99 87 101
4 87 101 5 87
7 99 101 18 5 135 18 99
2
1 2
1 3
```

### Sample Output:

```out
50.0%
33.3%
```

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <set>
using namespace std;

int main() {
    int n, m, k, num;
    cin >> n;
    set<int> st[n];
    for (int i = 0; i < n; i++) {
        cin >> m;
        for (int j = 0; j < m; j++) {
            cin >> num;
            st[i].insert(num);
        }
    }
    cin >> k;
    int a, b;
    while (k--) {
        cin >> a >> b;
        set<int> s;
        set_intersection(st[a - 1].begin(), st[a - 1].end(), st[b - 1].begin(),
                         st[b - 1].end(), inserter(s, s.begin()));
        int len1 = s.size(), len2 = st[a - 1].size() + st[b - 1].size();
        printf("%.1lf%%\n", len1 * 1.0 / (len2 - len1) * 100.0);
    }
    return 0;
}
```

