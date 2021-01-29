##  **1002** **A+B for Polynomials** (25分)

This time, you are supposed to find *A*+*B* where *A* and *B* are two polynomials.

### Input Specification:

Each input file contains one test case. Each case occupies 2 lines, and each line contains the information of a polynomial:

*K* *N*1 *a**N*1 *N*2 *a**N*2 ... *N**K* *a**N**K*

where *K* is the number of nonzero terms in the polynomial, *N**i* and *a**N**i* (*i*=1,2,⋯,*K*) are the exponents and coefficients, respectively. It is given that 1≤*K*≤10，0≤*N**K*<⋯<*N*2<*N*1≤1000.

### Output Specification:

For each test case you should output the sum of *A* and *B* in one line, with the same format as the input. Notice that there must be NO extra space at the end of each line. Please be accurate to 1 decimal place.

### Sample Input:

```in
2 1 2.4 0 3.2
2 2 1.5 1 0.5
```

### Sample Output:

```out
3 2 1.5 1 2.9 0 3.2
```

### Code:

```c++
#include <iostream>
#include <map>
using namespace std;

int main() {
    map<int, double> mp;
    int expo, k, cnt = 0;
    double coef;
    cin >> k;
    while (k--) {
        cin >> expo >> coef;
        mp[expo] += coef;
    }
    cin >> k;
    while (k--) {
        cin >> expo >> coef;
        mp[expo] += coef;
    }
    for (auto it = mp.begin(); it != mp.end(); it++) {
        if (it->second != 0)
            cnt++;
    }
    cout << cnt;
    for (auto it = mp.rbegin(); it != mp.rend(); it++) {
        if (it->second != 0) {
            printf(" %d %.1lf", it->first, it->second);
        }
    }
    return 0;
}
```

