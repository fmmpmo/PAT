##  **1093 Count PAT's (25 分)** 

The string `APPAPT` contains two `PAT`'s as substrings. The first one is formed by the 2nd, the 4th, and the 6th characters, and the second one is formed by the 3rd, the 4th, and the 6th characters.

Now given any string, you are supposed to tell the number of `PAT`'s contained in the string.

### Input Specification:

Each input file contains one test case. For each case, there is only one line giving a string of no more than 105 characters containing only `P`, `A`, or `T`.

### Output Specification:

For each test case, print in one line the number of `PAT`'s contained in the string. Since the result may be a huge number, you only have to output the result moded by 1000000007.

### Sample Input:

```in
APPAPT
```

### Sample Output:

```out
2
```

### Idea:

- 对每一个确定位置的A来说，以它形成的PAT的个数等于它左边P的个数乘以它右边T的个数。
- 比较快的获得每一位左边P的个数的方法是，设定一个数组leftP，记录每一位左边P的个数（含当前位，下同）。接着从左到右遍历字符串，如果当前位i是P，那么leftP[ i ] = leftP[ i - 1],如果不是，则leftP[ i ] = left[ i - 1 ];只需O(len)复杂度即可统计出leftP数组
- 以同样思路计算每一位右边T的个数，在统计个数过程中直接计算出答案，注意取模

### Code:

```c++
#include <iostream>
using namespace std;

int main() {
    string s;
    cin >> s;
    int leftP[100001] = {0}; //每一位A左边P的个数
    for (int i = 0; i < s.length(); i++) {
        if (i > 0)
            leftP[i] = leftP[i - 1];
        if (s[i] == 'P')
            leftP[i]++;
    }
    int ans = 0, rightT = 0;
    for (int i = s.length() - 1; i >= 0; i--) {
        if (s[i] == 'T')
            rightT++;
        else if (s[i] == 'A')
            ans = (ans + leftP[i] * rightT) % 1000000007;
    }
    cout << ans;
    return 0;
}
```

