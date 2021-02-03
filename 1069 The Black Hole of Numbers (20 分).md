##  **1069 The Black Hole of Numbers (20 分)** 

For any 4-digit integer except the ones with all the digits being the same, if we sort the digits in non-increasing order first, and then in non-decreasing order, a new number can be obtained by taking the second number from the first one. Repeat in this manner we will soon end up at the number `6174` -- the **black hole** of 4-digit numbers. This number is named Kaprekar Constant.

For example, start from `6767`, we'll get:

```
7766 - 6677 = 1089
9810 - 0189 = 9621
9621 - 1269 = 8352
8532 - 2358 = 6174
7641 - 1467 = 6174
... ...
```

Given any 4-digit number, you are supposed to illustrate the way it gets into the black hole.

### Input Specification:

Each input file contains one test case which gives a positive integer *N* in the range (0,104).

### Output Specification:

If all the 4 digits of *N* are the same, print in one line the equation `N - N = 0000`. Else print each step of calculation in a line until `6174` comes out as the difference. All the numbers must be printed as 4-digit numbers.

### Sample Input 1:

```in
6767
```

### Sample Output 1:

```out
7766 - 6677 = 1089
9810 - 0189 = 9621
9621 - 1269 = 8352
8532 - 2358 = 6174
```

### Sample Input 2:

```in
2222
```

### Sample Output 2:

```out
2222 - 2222 = 0000
```

### Code:

```c++
#include <algorithm>
#include <iostream>
using namespace std;

int main() {
    string s;
    cin >> s;
    s = string(4 - s.length(),'0') + s;
    while (true) {
        sort(s.begin(), s.end());
        int a = (s[3] - '0') * 1000 + (s[2] - '0') * 100 + (s[1] - '0') * 10 +
                s[0] - '0';
        int b = (s[0] - '0') * 1000 + (s[1] - '0') * 100 + (s[2] - '0') * 10 +
                s[3] - '0';
        if (a - b == 6174) {
            printf("%04d - %04d = 6174\n", a, b);
            break;
        } else if (a - b == 0) {
            printf("%04d - %04d = 0000\n", a, b);
            break;
        } else {
            printf("%04d - %04d = %04d\n", a, b, a - b);
            string ss = to_string(a - b);
            s = string(4 - ss.length(), '0') + ss;
        }
    }
    return 0;
}
```

