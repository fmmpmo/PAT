##  **1023** **Have Fun with Numbers** (20分)

Notice that the number 123456789 is a 9-digit number consisting exactly the numbers from 1 to 9, with no duplication. Double it we will obtain 246913578, which happens to be another 9-digit number consisting exactly the numbers from 1 to 9, only in a different permutation. Check to see the result if we double it again!

Now you are suppose to check if there are more numbers with this property. That is, double a given number with *k* digits, you are to tell if the resulting number consists of only a permutation of the digits in the original number.

### Input Specification:

Each input contains one test case. Each case contains one positive integer with no more than 20 digits.

### Output Specification:

For each test case, first print in a line "Yes" if doubling the input number gives a number that consists of only a permutation of the digits in the original number, or "No" if not. Then in the next line, print the doubled number.

### Sample Input:

```in
1234567899
```

### Sample Output:

```out
Yes
2469135798
```

### Code:

```c++
#include <algorithm>
#include <iostream>
using namespace std;

int main() {
    int a[40], b[40], c[10] = {0}, d[10] = {0};
    int p = 0, q = 0, num;
    string s;
    cin >> s;
    for (int i = 0; i < s.length(); i++) {
        a[p++] = s[i] - '0';
        c[s[i] - '0']++;
    }
    int jin = 0, ben;
    for (int i = p - 1; i >= 0; i--) {
        int ben = (a[i] * 2 + jin) % 10;
        jin = (a[i] * 2 + jin) / 10;
        b[q++] = ben;
    }
    bool flag = true;
    if (jin > 0) {
        b[q++] = jin;
    }
    for (int i = q - 1; i >= 0; i--) {
        d[b[i]]++;
    }
    for (int i = 0; i < 10; i++) {
        if (c[i] != d[i]) {
            flag = false;
            break;
        }
    }
    cout << (flag ? "Yes" : "No") << endl;
    for (int i = q - 1; i >= 0; i--) {
        cout << b[i];
    }
    return 0;
}
```

