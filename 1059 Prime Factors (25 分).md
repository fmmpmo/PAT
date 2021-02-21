##  **1059 Prime Factors (25 分)** 

Given any positive integer *N*, you are supposed to find all of its prime factors, and write them in the format *N* = *p*1*k*1×*p*2*k*2×⋯×*p**m**k**m*.

### Input Specification:

Each input file contains one test case which gives a positive integer *N* in the range of **long int**.

### Output Specification:

Factor *N* in the format *N* `=` *p*1`^`*k*1`*`*p*2`^`*k*2`*`…`*`*p**m*`^`*k**m*, where *p**i*'s are prime factors of *N* in increasing order, and the exponent *k**i* is the number of *p**i* -- hence when there is only one *p**i*, *k**i* is 1 and must **NOT** be printed out.

### Sample Input:

```in
97532468
```

### Sample Output:

```out
97532468=2^2*11*17*101*1291
```

### Idea:

- 思路来源，算法笔记 p167-p169

### Code:

```c++
#include <cmath>
#include <iostream>
using namespace std;

const int maxn = 100010;
int prime[maxn], cnt = 0;

struct factor {
    int x, cnt; // x为质因子，cnt为其个数
} fac[10];

bool isprime(int n) { //判断是否为素数
    if (n <= 1)
        return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0)
            return false;
    }
    return true;
}

void findPrime() { //求素数表
    for (int i = 1; i < maxn; i++) {
        if (isprime(i))
            prime[cnt++] = i;
    }
}

int main() {
    findPrime();
    int n, num = 0; // num为n的不同质因子的个数
    cin >> n;
    if (n == 1)
        cout << "1=1";
    else {
        cout << n << "=";
        int t = (int)sqrt(n);
        for (int i = 0; i < cnt && prime[i] <= t; i++) {
            if (n % prime[i] == 0) {   //如果prime[i]是n的因子
                fac[num].x = prime[i]; //记录该因子
                fac[num].cnt = 0;
                while (n % prime[i] == 0) { //记录出质因子prime[i]的个数
                    fac[num].cnt++;
                    n /= prime[i];
                }
                num++; //不同质因子个数+1
            }
            if (n == 1)
                break;
        }
        if (n != 1) { //如果无法被根号n以内的质因子除尽
            fac[num].x = n; //那么一定有一个大于根号n的质因子，即n本身
            fac[num++].cnt = 1;
        }
        for (int i = 0; i < num; i++) {
            if (i > 0)
                printf("*");
            printf("%d", fac[i].x);
            if (fac[i].cnt > 1)
                printf("^%d", fac[i].cnt);
        }
    }
    return 0;
}
```

