##  **1073 Scientific Notation (20 分)** 

Scientific notation is the way that scientists easily handle very large numbers or very small numbers. The notation matches the regular expression [+-][1-9]`.`[0-9]+E[+-][0-9]+ which means that the integer portion has exactly one digit, there is at least one digit in the fractional portion, and the number and its exponent's signs are always provided even when they are positive.

Now given a real number *A* in scientific notation, you are supposed to print *A* in the conventional notation while keeping all the significant figures.

### Input Specification:

Each input contains one test case. For each case, there is one line containing the real number *A* in scientific notation. The number is no more than 9999 bytes in length and the exponent's absolute value is no more than 9999.

### Output Specification:

For each test case, print in one line the input number *A* in the conventional notation, with all the significant figures kept, including trailing zeros.

### Sample Input 1:

```in
+1.23400E-03
```

### Sample Output 1:

```out
0.00123400
```

### Sample Input 2:

```in
-1.2E+10
```

### Sample Output 2:

```out
-12000000000
```

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s;
    cin >> s;
    if (s[0] == '+')
        s = s.substr(1);
    else if (s[0] == '-') {
        cout << "-";
        s = s.substr(1);
    }
    string s1, s2;
    for (int i = 0; i < s.length(); i++) {
        if (s[i] == '.') {
            s1 = s.substr(0, i);
            s2 = s.substr(i + 1);
            break;
        }
    }
    int cnt;
    char pos;
    for (int i = 0; i < s2.length(); i++) {
        if (s2[i] == 'E') {
            pos = s2[i + 1];
            cnt = stoi(s2.substr(i + 2));
            s2 = s2.substr(0, i);
            break;
        }
    }
    if (cnt == 0)
        cout << s1 << "." << s2;
    else if (pos == '-') {
        cout << "0." << string(cnt - 1, '0') << s1 << s2;
    } else if (pos == '+') {
        if (cnt >= s2.length()) {
            cout << s1 << s2 << string(cnt - s2.length(), '0');
        } else {
            cout << s1 << s2.substr(0, cnt) << "." << s2.substr(cnt);
        }
    }
    return 0;
}
```

