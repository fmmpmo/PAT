##  **1070 Mooncake (25 分)** 

Mooncake is a Chinese bakery product traditionally eaten during the Mid-Autumn Festival. Many types of fillings and crusts can be found in traditional mooncakes according to the region's culture. Now given the inventory amounts and the prices of all kinds of the mooncakes, together with the maximum total demand of the market, you are supposed to tell the maximum profit that can be made.

Note: partial inventory storage can be taken. The sample shows the following situation: given three kinds of mooncakes with inventory amounts being 180, 150, and 100 thousand tons, and the prices being 7.5, 7.2, and 4.5 billion yuans. If the market demand can be at most 200 thousand tons, the best we can do is to sell 150 thousand tons of the second kind of mooncake, and 50 thousand tons of the third kind. Hence the total profit is 7.2 + 4.5/2 = 9.45 (billion yuans).

### Input Specification:

Each input file contains one test case. For each case, the first line contains 2 positive integers *N* (≤1000), the number of different kinds of mooncakes, and *D* (≤500 thousand tons), the maximum total demand of the market. Then the second line gives the positive inventory amounts (in thousand tons), and the third line gives the positive prices (in billion yuans) of *N* kinds of mooncakes. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print the maximum profit (in billion yuans) in one line, accurate up to 2 decimal places.

### Sample Input:

```in
3 200
180 150 100
7.5 7.2 4.5
```

### Sample Output:

```out
9.45
```

### Code:

```c++
#include <algorithm>
#include <iostream>
using namespace std;

typedef struct {
    double zong, amounts, danjia;
} Cake;

bool cmp(Cake c1, Cake c2) { return c1.danjia > c2.danjia; }

int main() {
    int n, d;
    cin >> n >> d;
    Cake cake[n];
    for (int i = 0; i < n; i++) {
        cin >> cake[i].amounts;
    }
    for (int i = 0; i < n; i++) {
        cin >> cake[i].zong;
        cake[i].danjia = cake[i].zong / cake[i].amounts;
    }
    double sum = 0;
    sort(cake, cake + n, cmp);
    for (int i = 0; i < n && d > 0; i++) {
        if (d >= cake[i].amounts) {
            d -= cake[i].amounts;
            sum += cake[i].zong;
        } else {
            sum += d * cake[i].danjia;
            d = 0;
        }
    }
    printf("%.2lf", sum);
    return 0;
}
```

