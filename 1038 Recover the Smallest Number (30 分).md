##  **1038 Recover the Smallest Number (30 分)** 

Given a collection of number segments, you are supposed to recover the smallest number from them. For example, given { 32, 321, 3214, 0229, 87 }, we can recover many numbers such like 32-321-3214-0229-87 or 0229-32-87-321-3214 with respect to different orders of combinations of these segments, and the smallest number is 0229-321-3214-32-87.

### Input Specification:

Each input file contains one test case. Each case gives a positive integer *N* (≤104) followed by *N* number segments. Each segment contains a non-negative integer of no more than 8 digits. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print the smallest number in one line. Notice that the first digit must not be zero.

### Sample Input:

```in
5 32 321 3214 0229 87
```

### Sample Output:

```out
22932132143287
```

### Idea:

- 自己没整明白，看了网上的讲解之后自己才写的
- 这里并不完全是按字典序进行排，而是两字符串a和b比较的时候（即cmp函数），a+b和b+a进行字典序排序，比如32 和 321 比较，常规字典序比较是：32 < 321，实际上组合之后：321-32 比 32-321 要小，因为32132 < 32321
- 还学到了一种新的排序，我之前都没有这么写过排序规则

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

bool cmp(string s1, string s2) { return s1 + s2 < s2 + s1; }

int main() {
    string s, res;
    int n, cnt = 0;
    vector<string> v;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> s;
        if (stoll(s) == 0)
            cnt++;
        v.push_back(s);
    }
    if (cnt == n)
        cout << 0;
    else {
        sort(v.begin(), v.end(), cmp);
        for (int i = 0; i < v.size(); i++) {
            res += v[i];
        }
        while (res[0] == '0')
            res.erase(res.begin());
        cout << res;
    }
    return 0;
}
```

