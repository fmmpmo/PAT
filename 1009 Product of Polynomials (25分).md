##  **1009** **Product of Polynomials** (25分)

This time, you are supposed to find *A*×*B* where *A* and *B* are two polynomials.

### Input Specification:

Each input file contains one test case. Each case occupies 2 lines, and each line contains the information of a polynomial:

*K* *N*1 *a**N*1 *N*2 *a**N*2 ... *N**K* *a**N**K*

where *K* is the number of nonzero terms in the polynomial, *N**i* and *a**N**i* (*i*=1,2,⋯,*K*) are the exponents and coefficients, respectively. It is given that 1≤*K*≤10, 0≤*N**K*<⋯<*N*2<*N*1≤1000.

### Output Specification:

For each test case you should output the product of *A* and *B* in one line, with the same format as the input. Notice that there must be **NO** extra space at the end of each line. Please be accurate up to 1 decimal place.

### Sample Input:

```in
2 1 2.4 0 3.2
2 2 1.5 1 0.5
```

### Sample Output:

```out
3 3 3.6 2 6.0 1 1.6
```

### Code:

```c++
#include <iostream>
#include <map>
using namespace std;

int main() {
    map<int, double> m1, m2, m3;
    int k, expo;
    double coef;
    cin >> k;
    while (k--) {
        cin >> expo >> coef;
        m1[expo] = coef;
    }
    cin >> k;
    while (k--) {
        cin >> expo >> coef;
        m2[expo] = coef;
    }
    for (auto it = m1.begin(); it != m1.end(); it++) {
        for (auto itt = m2.begin(); itt != m2.end(); itt++) {
            m3[it->first + itt->first] += it->second * itt->second;
        }
    }
    int cnt = 0;
    for (auto it = m3.rbegin(); it != m3.rend(); it++) {
        if (it->second)
            cnt++;
    }
    cout << cnt;
    for (auto it = m3.rbegin(); it != m3.rend(); it++) {
        if (it->second)
            printf(" %d %.1lf", it->first, it->second);
    }
    return 0;
}
```

