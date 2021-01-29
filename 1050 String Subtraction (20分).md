##  **1050** **String Subtraction** (20分)

Given two strings *S*1 and *S*2, *S*=*S*1−*S*2 is defined to be the remaining string after taking all the characters in *S*2 from *S*1. Your task is simply to calculate *S*1−*S*2 for any given strings. However, it might not be that simple to do it **fast**.

### Input Specification:

Each input file contains one test case. Each case consists of two lines which gives *S*1 and *S*2, respectively. The string lengths of both strings are no more than 104. It is guaranteed that all the characters are visible ASCII codes and white space, and a new line character signals the end of a string.

### Output Specification:

For each test case, print *S*1−*S*2 in one line.

### Sample Input:

```in
They are students.
aeiou
```

### Sample Output:

```out
Thy r stdnts.
```

### Code:

```c++
#include <iostream>
using namespace std;

int main() {
    string s1, s2;
    getline(cin, s1);
    getline(cin, s2);
    for (int i = 0; i < s1.length(); i++) {
        int j;
        for (j = 0; j < s2.length(); j++) {
            if (s1[i] == s2[j])
                break;
        }
        if (j == s2.length())
            printf("%c", s1[i]);
    }
    return 0;
}
```

