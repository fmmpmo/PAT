##  **1027** **Colors in Mars** (20分)

People in Mars represent the colors in their computers in a similar way as the Earth people. That is, a color is represented by a 6-digit number, where the first 2 digits are for `Red`, the middle 2 digits for `Green`, and the last 2 digits for `Blue`. The only difference is that they use radix 13 (0-9 and A-C) instead of 16. Now given a color in three decimal numbers (each between 0 and 168), you are supposed to output their Mars RGB values.

### Input Specification:

Each input file contains one test case which occupies a line containing the three decimal color values.

### Output Specification:

For each test case you should output the Mars RGB value in the following format: first output `#`, then followed by a 6-digit number where all the English characters must be upper-cased. If a single color is only 1-digit long, you must print a `0` to its left.

### Sample Input:

```in
15 43 71
```

### Sample Output:

```out
#123456
```

### Code:

```c++
#include <algorithm>
#include <iostream>
using namespace std;

string Radix(int n) {
    string s = "";
    while (n != 0) {
        int x = n % 13;
        if (x >= 0 && x <= 9)
            s += to_string(x);
        else if (x == 10)
            s += string(1, 'A');
        else if (x == 11)
            s += string(1, 'B');
        else
            s += string(1, 'C');
        n /= 13;
    }
    reverse(s.begin(), s.end());
    return s;
}

int main() {
    int r, g, b;
    cin >> r >> g >> b;
    string s1 = Radix(r), s2 = Radix(g), s3 = Radix(b);
    string res = string(2 - s1.length(), '0') + s1 +
                 string(2 - s2.length(), '0') + s2 +
                 string(2 - s3.length(), '0') + s3;
    cout << "#" << res;
    return 0;
}
```

