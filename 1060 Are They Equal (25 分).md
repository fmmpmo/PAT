##  **1060 Are They Equal (25 分)** 

If a machine can save only 3 significant digits, the float numbers 12300 and 12358.9 are considered equal since they are both saved as 0.123×105 with simple chopping. Now given the number of significant digits on a machine and two float numbers, you are supposed to tell if they are treated equal in that machine.

### Input Specification:

Each input file contains one test case which gives three numbers *N*, *A* and *B*, where *N* (<100) is the number of significant digits, and *A* and *B* are the two float numbers to be compared. Each float number is non-negative, no greater than 10100, and that its total digit number is less than 100.

### Output Specification:

For each test case, print in a line `YES` if the two numbers are treated equal, and then the number in the standard form `0.d[1]...d[N]*10^k` (`d[1]`>0 unless the number is 0); or `NO` if they are not treated equal, and then the two numbers in their standard form. All the terms must be separated by a space, with no extra space at the end of a line.

Note: Simple chopping is assumed without rounding.

### Sample Input 1:

```in
3 12300 12358.9
```

### Sample Output 1:

```out
YES 0.123*10^5
```

### Sample Input 2:

```in
3 120 128
```

### Sample Output 2:

```out
NO 0.120*10^3 0.128*10^3
```

### Idea:

- 思路来源算法笔记-胡凡，好难啊，甲级做不下去了。。。。
- ![字符串例题](图片/字符串例题.png)

### Code:

```c++
#include <iostream>
using namespace std;

int n;

string deal(string s, int &expo) {
    int k = 0; // s的下标
    while (s.length() > 0 && s[0] == '0')
        s.erase(s.begin()); //去掉前导符0
    if (s[0] == '.') { //去掉前导0后是小数点，说明s是小于1的小数
        s.erase(s.begin()); //去掉小数点
        while (s.length() > 0 && s[0] == '0') {
            s.erase(s.begin()); //去掉小数点后非零位前的所有零
            expo--;             //每去掉一个0，指数e减1
        }
    } else { //去掉前导0后不是小数点，则找到后面的小数点删除
        while (k < s.length() && s[k] != '.') { //寻找小数点
            k++;
            expo++; //只要不碰到小数点就让指数e++
        }
        if (k < s.length()) { //说明找到了小数点，将小数点删除
            s.erase(s.begin() + k);
        }
    }
    if (s.length() == 0) //如果去除前导0后s的长度是0，说明这个数是0
        expo = 0;
    int num = 0;
    k = 0;
    string res;
    while (num < n) { //只要精度还没有到n
        if (k < s.length())
            res += s[k++]; //只要还有数字，就添加到res末尾
        else
            res += '0'; //否则末尾添加0
        num++;          //精度+1
    }
    return res;
}

int main() {
    string a, b, s1, s2;
    cin >> n >> a >> b;
    int expo1 = 0, expo2 = 0;
    s1 = deal(a, expo1);
    s2 = deal(b, expo2);
    if (s1 == s2 && expo1 == expo2)
        cout << "YES 0." << s1 << "*10^" << expo1;
    else
        cout << "NO 0." << s1 << "*10^" << expo1 << " 0." << s2 << "*10^"
             << expo2;
    return 0;
}
```

