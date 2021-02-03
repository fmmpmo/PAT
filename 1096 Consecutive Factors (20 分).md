##  **1096 Consecutive Factors (20 分)** 

Among all the factors of a positive integer N, there may exist several consecutive numbers. For example, 630 can be factored as 3×5×6×7, where 5, 6, and 7 are the three consecutive numbers. Now given any positive N, you are supposed to find the maximum number of consecutive factors, and list the smallest sequence of the consecutive factors.

### Input Specification:

Each input file contains one test case, which gives the integer N (1<N<231).

### Output Specification:

For each test case, print in the first line the maximum number of consecutive factors. Then in the second line, print the smallest sequence of the consecutive factors in the format `factor[1]*factor[2]*...*factor[k]`, where the factors are listed in increasing order, and 1 is NOT included.

### Sample Input:

```in
630
```

### Sample Output:

```out
3
5*6*7
```

### Code:

```c++
#include <iostream>
using namespace std;

typedef long long ll;

int main() {
    ll n, sum, maxn = 0, s;
    cin >> n;
    for (ll i = 2; i * i <= n; i++) {
        sum = 1;
        for (ll j = i; sum * j <= n; j++) {
            sum *= j;
            if (n % sum != 0)
                break;
            else {
                if (j - i + 1 > maxn) {
                    maxn = j - i + 1;
                    s = i;
                }
            }
        }
    }
    if (maxn == 0)
        cout << 1 << endl << n;
    else {
        cout << maxn << endl << s;
        for (ll i = s + 1; i < s + maxn; i++)
            cout << "*" << i;
    }
    return 0;
}
```

