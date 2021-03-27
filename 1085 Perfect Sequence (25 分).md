##  **1085 Perfect Sequence (25 分)** 

Given a sequence of positive integers and another positive integer *p*. The sequence is said to be a **perfect sequence** if *M*≤*m*×*p* where *M* and *m* are the maximum and minimum numbers in the sequence, respectively.

Now given a sequence and a parameter *p*, you are supposed to find from the sequence as many numbers as possible to form a perfect subsequence.

### Input Specification:

Each input file contains one test case. For each case, the first line contains two positive integers *N* and *p*, where *N* (≤105) is the number of integers in the sequence, and *p* (≤109) is the parameter. In the second line there are *N* positive integers, each is no greater than 109.

### Output Specification:

For each test case, print in one line the maximum number of integers that can be chosen to form a perfect subsequence.

### Sample Input:

```in
10 8
2 3 20 4 5 1 6 7 8 9
```

### Sample Output:

```out
8
```

### Idea:

- 输入数据，并按照从小到大排序，从第一个开始寻找，使用二分查找寻找第一个大于m*p的位置，通过该位置判断中间有多个数，这其中的数都是符合要求的，和最大值比较即可。

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

typedef long long ll;

int main() {
    ll n, p, num;
    scanf("%lld %lld", &n, &p);
    vector<ll> v;
    for (ll i = 0; i < n; i++) {
        scanf("%lld", &num);
        v.push_back(num);
    }
    sort(v.begin(), v.end());
    ll maxn = 0;
    for (ll i = 0; i < n; i++) {
        ll cnt = 0;
        ll x = v[i] * p;
        vector<ll>::iterator it = upper_bound(v.begin(), v.end(), x);
        if (it == v.end()) {
            cnt = n - i;
        } else {
            cnt = it - v.begin() - i;
        }
        if (cnt > maxn) {
            maxn = cnt;
        }
    }
    printf("%lld", maxn);
    return 0;
}
```

