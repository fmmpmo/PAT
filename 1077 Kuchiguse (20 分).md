##  **1077 Kuchiguse (20 分)** 

The Japanese language is notorious for its sentence ending particles. Personal preference of such particles can be considered as a reflection of the speaker's personality. Such a preference is called "Kuchiguse" and is often exaggerated artistically in Anime and Manga. For example, the artificial sentence ending particle "nyan~" is often used as a stereotype for characters with a cat-like personality:

- Itai nyan~ (It hurts, nyan~)
- Ninjin wa iyada nyan~ (I hate carrots, nyan~)

Now given a few lines spoken by the same character, can you find her Kuchiguse?

### Input Specification:

Each input file contains one test case. For each case, the first line is an integer *N* (2≤*N*≤100). Following are *N* file lines of 0~256 (inclusive) characters in length, each representing a character's spoken line. The spoken lines are case sensitive.

### Output Specification:

For each test case, print in one line the kuchiguse of the character, i.e., the longest common suffix of all *N* lines. If there is no such suffix, write `nai`.

### Sample Input 1:

```in
3
Itai nyan~
Ninjin wa iyadanyan~
uhhh nyan~
```

### Sample Output 1:

```out
nyan~
```

### Sample Input 2:

```in
3
Itai!
Ninjinnwaiyada T_T
T_T
```

### Sample Output 2:

```out
nai
```

### Code:

```c++
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n, maxn = 0, minlen = 260;
    cin >> n;
    getchar();
    string s;
    vector<string> v;
    for (int i = 0; i < n; i++) {
        getline(cin, s);
        v.push_back(s);
        if (s.length() < minlen) {
            minlen = s.length();
        }
    }
    int cnt = 0;
    if (minlen != 0) {
        for (int k = 1; k <= minlen; k++) {
            int i;
            for (i = 1; i < n; i++) {
                if (v[i][v[i].length() - k] != v[i - 1][v[i - 1].length() - k])
                    break;
            }
            if (i == n) {
                cnt++;
            } else {
                break;
            }
        }
    }
    if (cnt > 0)
        cout << v[0].substr(v[0].length() - cnt);
    else
        cout << "nai";
    return 0;
}
```

