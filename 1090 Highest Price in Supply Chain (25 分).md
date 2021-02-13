##  **1090 Highest Price in Supply Chain (25 分)** 

A supply chain is a network of retailers（零售商）, distributors（经销商）, and suppliers（供应商）-- everyone involved in moving a product from supplier to customer.

Starting from one root supplier, everyone on the chain buys products from one's supplier in a price *P* and sell or distribute them in a price that is *r*% higher than *P*. It is assumed that each member in the supply chain has exactly one supplier except the root supplier, and there is no supply cycle.

Now given a supply chain, you are supposed to tell the highest price we can expect from some retailers.

### Input Specification:

Each input file contains one test case. For each case, The first line contains three positive numbers: *N* (≤105), the total number of the members in the supply chain (and hence they are numbered from 0 to *N*−1); *P*, the price given by the root supplier; and *r*, the percentage rate of price increment for each distributor or retailer. Then the next line contains *N* numbers, each number *S**i* is the index of the supplier for the *i*-th member. *S**r**o**o**t* for the root supplier is defined to be −1. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print in one line the highest price we can expect from some retailers, accurate up to 2 decimal places, and the number of retailers that sell at the highest price. There must be one space between the two numbers. It is guaranteed that the price will not exceed 1010.

### Sample Input:

```in
9 1.80 1.00
1 5 4 4 -1 4 5 3 6
```

### Sample Output:

```out
1.85 2
```

### Code:

```c++
#include <cmath>
#include <iostream>
using namespace std;

int parent[100001] = {-1}, h[100001];

int geth(int x) {
    if (parent[x] == -1)
        h[x] = 1;
    else if (h[parent[x]])
        h[x] = h[parent[x]] + 1;
    else
        h[x] = geth(parent[x]) + 1;
    return h[x];
}

int main() {
    int n, pos, maxn = 0, cnt = 0;
    double p, r, res;
    scanf("%d %lf %lf", &n, &p, &r);
    for (int i = 0; i < n; i++) {
        scanf("%d", &pos);
        parent[i] = pos;
    }
    for (int i = 0; i < n; i++) {
        if (!h[i])
            geth(i);
        if (h[i] > maxn) {
            maxn = h[i];
            cnt = 1;
        } else if (h[i] == maxn)
            cnt++;
    }
    res = p * pow(1 + r / 100, maxn - 1);
    printf("%.2lf %d", res, cnt);
    return 0;
}
```

