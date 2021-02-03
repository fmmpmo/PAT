##  **1100 Mars Numbers (20 分)** 

People on Mars count their numbers with base 13:

- Zero on Earth is called "tret" on Mars.
- The numbers 1 to 12 on Earth is called "jan, feb, mar, apr, may, jun, jly, aug, sep, oct, nov, dec" on Mars, respectively.
- For the next higher digit, Mars people name the 12 numbers as "tam, hel, maa, huh, tou, kes, hei, elo, syy, lok, mer, jou", respectively.

For examples, the number 29 on Earth is called "hel mar" on Mars; and "elo nov" on Mars corresponds to 115 on Earth. In order to help communication between people from these two planets, you are supposed to write a program for mutual translation between Earth and Mars number systems.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive integer *N* (<100). Then *N* lines follow, each contains a number in [0, 169), given either in the form of an Earth number, or that of Mars.

### Output Specification:

For each number, print in a line the corresponding number in the other language.

### Sample Input:

```in
4
29
5
elo nov
tam
```

### Sample Output:

```out
hel mar
may
115
13
```

### Code:

```c++
#include <iostream>
using namespace std;

int main() {
    string str1[] = {"tret", "jan", "feb", "mar", "apr", "may", "jun",
                     "jly",  "aug", "sep", "oct", "nov", "dec"};
    string str2[] = {"",    "tam", "hel", "maa", "huh", "tou", "kes",
                     "hei", "elo", "syy", "lok", "mer", "jou"};
    int n, res = 0;
    cin >> n;
    string s;
    getchar();
    while (n--) {
        getline(cin, s);
        if (s[0] >= '0' && s[0] <= '9') {
            int x = stoi(s);
            if (x == 0)
                cout << str1[0] << endl;
            else if (x / 13 > 0) {
                cout << str2[x / 13];
                x = x % 13;
                if (x != 0)
                    cout << " " << str1[x];
                cout << endl;
            } else {
                cout << str1[x % 13] << endl;
            }
        } else {
            if (s.length() > 3) {
                if (s == "tret")
                    cout << 0 << endl;
                else {
                    res = 0;
                    string s1 = s.substr(0, 3);
                    string s2 = s.substr(4);
                    for (int i = 0; i < 13; i++) {
                        if (str2[i] == s1) {
                            res += 13 * i;
                            break;
                        }
                    }
                    for (int i = 0; i < 13; i++) {
                        if (str1[i] == s2) {
                            res += i;
                            break;
                        }
                    }
                    cout << res << endl;
                }
            } else {
                res = 0;
                for (int i = 0; i < 13; i++) {
                    if (str2[i] == s) {
                        cout << i * 13 << endl;
                        break;
                    }
                }
                for (int i = 0; i < 13; i++) {
                    if (str1[i] == s) {
                        cout << i << endl;
                        break;
                    }
                }
            }
        }
    }
    return 0;
}
```

