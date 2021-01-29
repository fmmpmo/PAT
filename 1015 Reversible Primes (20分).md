##  **1015** **Reversible Primes** (20分)

A **reversible prime** in any number system is a prime whose "reverse" in that number system is also a prime. For example in the decimal system 73 is a reversible prime because its reverse 37 is also a prime.

Now given any two positive integers *N* (<105) and *D* (1<*D*≤10), you are supposed to tell if *N* is a reversible prime with radix *D*.

### Input Specification:

The input file consists of several test cases. Each case occupies a line which contains two integers *N* and *D*. The input is finished by a negative *N*.

### Output Specification:

For each test case, print in one line `Yes` if *N* is a reversible prime with radix *D*, or `No` if not.

### Sample Input:

```in
73 10
23 2
23 10
-2
```

### Sample Output:

```out
Yes
Yes
No
```

### Code:

```c++
#include <algorithm>
#include <iostream>
using namespace std;

typedef long long ll;

bool isprime(ll n) {
    if (n <= 1)
        return false;
    for (ll i = 2; i * i <= n; i++) {
        if (n % i == 0)
            return false;
    }
    return true;
}

string Radix(ll n, int radix) {
    string s = "";
    while (n != 0) {
        s += (n % radix + '0');
        n /= radix;
    }
    reverse(s.begin(), s.end());
    return s;
}

ll toDecimal(string n, int radix) {
    ll res = 0;
    for (int i = 0; i < n.length(); i++) {
        if (n[i] >= '0' && n[i] <= '9')
            res = res * radix + n[i] - '0';
        else
            res = res * radix + n[i] - 'A' + 10;
    }
    return res;
}

int main() {
    ll n, d;
    while (true) {
        cin >> n;
        if (n < 0)
            break;
        cin >> d;
        if (!isprime(n)) {
            cout << "No" << endl;
            continue;
        }
        string s = Radix(n, d);
        reverse(s.begin(), s.end());
        n = toDecimal(s, d);
        if (isprime(n))
            cout << "Yes" << endl;
        else
            cout << "No" << endl;
    }
    return 0;
}
```

