##  **1084 Broken Keyboard (20 分)** 

On a broken keyboard, some of the keys are worn out. So when you type some sentences, the characters corresponding to those keys will not appear on screen.

Now given a string that you are supposed to type, and the string that you actually type out, please list those keys which are for sure worn out.

### Input Specification:

Each input file contains one test case. For each case, the 1st line contains the original string, and the 2nd line contains the typed-out string. Each string contains no more than 80 characters which are either English letters [A-Z] (case insensitive), digital numbers [0-9], or `_` (representing the space). It is guaranteed that both strings are non-empty.

### Output Specification:

For each test case, print in one line the keys that are worn out, in the order of being detected. The English letters must be capitalized. Each worn out key must be printed once only. It is guaranteed that there is at least one worn out key.

### Sample Input:

```in
7_This_is_a_test
_hs_s_a_es
```

### Sample Output:

```out
7TI
```

### Code:

```c++
#include <iostream>
using namespace std;

int main() {
    string s1, s2;
    int vis[256] = {0};
    cin >> s1 >> s2;
    for (int i = 0; i < s1.length(); i++) {
        if (s2.find(s1[i]) == -1) {
            if (s1[i] >= 'a' && s1[i] <= 'z') {
                s1[i] = s1[i] - 'a' + 'A';
                if (vis[s1[i]] == 0) {
                    printf("%c", s1[i]);
                    vis[s1[i]] = 1;
                }
            } else {
                if (vis[s1[i]] == 0) {
                    printf("%c", s1[i]);
                    vis[s1[i]] = 1;
                }
            }
        }
    }
    return 0;
}
```

