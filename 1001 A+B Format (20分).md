##  **1001** **A+B Format** (20分)

Calculate *a*+*b* and output the sum in standard format -- that is, the digits must be separated into groups of three by commas (unless there are less than four digits).

### Input Specification:

Each input file contains one test case. Each case contains a pair of integers *a* and *b* where −106≤*a*,*b*≤106. The numbers are separated by a space.

### Output Specification:

For each test case, you should output the sum of *a* and *b* in one line. The sum must be written in the standard format.

### Sample Input:

```in
-1000000 9
```

### Sample Output:

```out
-999,991
```

### Code:

```c++
#include <iostream>
using namespace std;

typedef long long ll;

int main() {
    ll a, b;
    cin >> a >> b;
    ll sum = a + b;
    string s;
    if (sum < 0) {
        cout << "-";
        sum = -1 * sum;
    }
    s = to_string(sum);
    if (s.length() <= 3) {
        cout << s;
        return 0;
    }
    if (s.length() % 3 != 0)
        cout << s.substr(0, s.length() % 3) << ",";
    for (int i = s.length() % 3; i < s.length(); i += 3) {
        if (i == s.length() % 3)
            cout << s.substr(i, 3);
        else
            cout << "," << s.substr(i, 3);
    }
    return 0;
}
```

