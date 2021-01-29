##  **1005** **Spell It Right** (20分)

Given a non-negative integer *N*, your task is to compute the sum of all the digits of *N*, and output every digit of the sum in English.

### Input Specification:

Each input file contains one test case. Each case occupies one line which contains an *N* (≤10100).

### Output Specification:

For each test case, output in one line the digits of the sum in English words. There must be one space between two consecutive words, but no extra space at the end of a line.

### Sample Input:

```in
12345
```

### Sample Output:

```out
one five
```

### Code:

```c++
#include <iostream>
#include <vector>
using namespace std;

int main() {
    string str[10] = {"zero", "one", "two",   "three", "four",
                      "five", "six", "seven", "eight", "nine"};
    string n;
    vector<string> v;
    int sum = 0;
    cin >> n;
    for (int i = 0; i < n.length(); i++) {
        sum += n[i] - '0';
    }
    if (sum == 0) {
        cout << "zero";
        return 0;
    }
    while (sum != 0) {
        v.push_back(str[sum % 10]);
        sum /= 10;
    }
    cout << v[v.size() - 1];
    for (int i = v.size() - 2; i >= 0; i--) {
        cout << " " << v[i];
    }
    return 0;
}
```

