##  **1040 Longest Symmetric String (25 分)** 

Given a string, you are supposed to output the length of the longest symmetric sub-string. For example, given `Is PAT&TAP symmetric?`, the longest symmetric sub-string is `s PAT&TAP s`, hence you must output `11`.

### Input Specification:

Each input file contains one test case which gives a non-empty string of length no more than 1000.

### Output Specification:

For each test case, simply print the maximum length in a line.

### Sample Input:

```in
Is PAT&TAP symmetric?
```

### Sample Output:

```out
11
```

### Idea:

- 一个从前往后，一个从后往前，只要相等，就移动

### Code:

```c++
#include <iostream>
using namespace std;

int main() {
    string s;
    getline(cin, s);
    int maxn = 1;
    for (int i = 0; i < s.length(); i++) {
        for (int j = s.length() - 1; j >= i; j--) {
            int st = i, en = j;
            while (st <= en && s[st] == s[en]) {
                st++;
                en--;
            }
            if (st > en && j - i + 1 > maxn)
                maxn = j - i + 1;
        }
    }
    cout << maxn;
    return 0;
}
```

