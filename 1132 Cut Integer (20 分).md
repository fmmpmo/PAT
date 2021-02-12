##  **1132 Cut Integer (20 分)** 

Cutting an integer means to cut a K digits lone integer Z into two integers of (K/2) digits long integers A and B. For example, after cutting Z = 167334, we have A = 167 and B = 334. It is interesting to see that Z can be devided by the product of A and B, as 167334 / (167 × 334) = 3. Given an integer Z, you are supposed to test if it is such an integer.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer N (≤ 20). Then N lines follow, each gives an integer Z (10 ≤ Z <231). It is guaranteed that the number of digits of Z is an even number.

### Output Specification:

For each case, print a single line `Yes` if it is such a number, or `No` if not.

### Sample Input:

```in
3
167334
2333
12345678
```

### Sample Output:

```out
Yes
No
No
```

### Code:

```c++
#include <iostream>
#include <string>
using namespace std;

typedef long long ll;

int main() {
    int n;
    string s;
    cin >> n;
    while (n--) {
        cin >> s;
        ll a = stoll(s.substr(0, s.length() / 2));
        ll b = stoll(s.substr(s.length() / 2));
        ll x = stoll(s);
        if (a != 0 && b != 0 && x % (a * b) == 0)
            cout << "Yes\n";
        else
            cout << "No\n";
    }
    return 0;
}
```

