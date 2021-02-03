##  **1088 Rational Arithmetic (20 分)** 

For two rational numbers, your task is to implement the basic arithmetics, that is, to calculate their sum, difference, product and quotient.

### Input Specification:

Each input file contains one test case, which gives in one line the two rational numbers in the format `a1/b1 a2/b2`. The numerators and the denominators are all in the range of long int. If there is a negative sign, it must appear only in front of the numerator. The denominators are guaranteed to be non-zero numbers.

### Output Specification:

For each test case, print in 4 lines the sum, difference, product and quotient of the two rational numbers, respectively. The format of each line is `number1 operator number2 = result`. Notice that all the rational numbers must be in their simplest form `k a/b`, where `k` is the integer part, and `a/b` is the simplest fraction part. If the number is negative, it must be included in a pair of parentheses. If the denominator in the division is zero, output `Inf` as the result. It is guaranteed that all the output integers are in the range of **long int**.

### Sample Input 1:

```in
2/3 -4/2
```

### Sample Output 1:

```out
2/3 + (-2) = (-1 1/3)
2/3 - (-2) = 2 2/3
2/3 * (-2) = (-1 1/3)
2/3 / (-2) = (-1/3)
```

### Sample Input 2:

```in
5/3 0/6
```

### Sample Output 2:

```out
1 2/3 + 0 = 1 2/3
1 2/3 - 0 = 1 2/3
1 2/3 * 0 = 0
1 2/3 / 0 = Inf
```

### Code:

```c++
#include <iostream>
using namespace std;

typedef long long ll;

ll gcd(ll a, ll b) { return b == 0 ? a : gcd(b, a % b); }

void print(ll a, ll b) {
    if (b < 0) {
        a = -1 * a;
        b = -1 * b;
    }
    if (a == 0) {
        printf("0");
    } else if (a < 0) {
        if (a % b == 0) {
            printf("(%lld)", a / b);
        } else if (abs(a) > b) {
            printf("(%lld ", a / b);
            a = -1 * (a - a / b * b);
            ll res = gcd(abs(a), b);
            printf("%lld/%lld)", a / res, b / res);
        } else {
            ll res = gcd(abs(a), b);
            printf("(%lld/%lld)", a / res, b / res);
        }
    } else {
        if (a % b == 0) {
            printf("%lld", a / b);
        } else if (a > b) {
            printf("%lld ", a / b);
            a = a % b;
            ll res = gcd(a, b);
            printf("%lld/%lld", a / res, b / res);
        } else {
            ll res = gcd(a, b);
            printf("%lld/%lld", a / res, b / res);
        }
    }
}

void add(ll a, ll b) { print(a, b); }

void diff(ll a, ll b) { print(a, b); }

void mult(ll a, ll b) { print(a, b); }

void divi(ll a, ll b) {
    if (b == 0)
        printf("Inf");
    else
        print(a, b);
}

int main() {
    ll a1, b1, a2, b2;
    scanf("%lld/%lld %lld/%lld", &a1, &b1, &a2, &b2);
    ll res1 = gcd(a1, b1);
    ll res2 = gcd(a2, b2);
    a1 /= res1;
    b1 /= res1;
    a2 /= res2;
    b2 /= res2;
    print(a1, b1);
    printf(" + ");
    print(a2, b2);
    printf(" = ");
    add(a1 * b2 + a2 * b1, b1 * b2);
    printf("\n");
    print(a1, b1);
    printf(" - ");
    print(a2, b2);
    printf(" = ");
    diff(a1 * b2 - a2 * b1, b1 * b2);
    printf("\n");
    print(a1, b1);
    printf(" * ");
    print(a2, b2);
    printf(" = ");
    mult(a1 * a2, b1 * b2);
    printf("\n");
    print(a1, b1);
    printf(" / ");
    print(a2, b2);
    printf(" = ");
    divi(a1 * b2, b1 * a2);
    return 0;
}
```

