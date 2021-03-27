##  **1055 The World's Richest (25 分)** 

Forbes magazine publishes every year its list of billionaires based on the annual ranking of the world's wealthiest people. Now you are supposed to simulate this job, but concentrate only on the people in a certain range of ages. That is, given the net worths of *N* people, you must find the *M* richest people in a given range of their ages.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 2 positive integers: *N* (≤105) - the total number of people, and *K* (≤103) - the number of queries. Then *N* lines follow, each contains the name (string of no more than 8 characters without space), age (integer in (0, 200]), and the net worth (integer in [−106,106]) of a person. Finally there are *K* lines of queries, each contains three positive integers: *M* (≤100) - the maximum number of outputs, and [`Amin`, `Amax`] which are the range of ages. All the numbers in a line are separated by a space.

### Output Specification:

For each query, first print in a line `Case #X:` where `X` is the query number starting from 1. Then output the *M* richest people with their ages in the range [`Amin`, `Amax`]. Each person's information occupies a line, in the format

```
Name Age Net_Worth
```

The outputs must be in non-increasing order of the net worths. In case there are equal worths, it must be in non-decreasing order of the ages. If both worths and ages are the same, then the output must be in non-decreasing alphabetical order of the names. It is guaranteed that there is no two persons share all the same of the three pieces of information. In case no one is found, output `None`.

### Sample Input:

```in
12 4
Zoe_Bill 35 2333
Bob_Volk 24 5888
Anny_Cin 95 999999
Williams 30 -22
Cindy 76 76000
Alice 18 88888
Joe_Mike 32 3222
Michael 5 300000
Rosemary 40 5888
Dobby 24 5888
Billy 24 5888
Nobody 5 0
4 15 45
4 30 35
4 5 95
1 45 50
```

### Sample Output:

```out
Case #1:
Alice 18 88888
Billy 24 5888
Bob_Volk 24 5888
Dobby 24 5888
Case #2:
Joe_Mike 32 3222
Zoe_Bill 35 2333
Williams 30 -22
Case #3:
Anny_Cin 95 999999
Michael 5 300000
Alice 18 88888
Cindy 76 76000
Case #4:
None
```

### Idea:

- 找出年龄符合条件的最富有的人，输出的人数最多为m，而不是一定要输出m个，初始排一次序即可，然后按照给定的m，minage，maxage判断输出即可。
- 使用cin会超时，所以采用scanf和printf，字符串类型的输入转为char数组后会快很多，这个也是在之前做题的经验上总结的教训。

### Code:

```c++
#include <algorithm>
#include <iostream>
using namespace std;

typedef struct {
    string name;
    int age;
    int worth;
} Rich;

bool cmp(Rich r1, Rich r2) {
    if (r1.worth != r2.worth)
        return r1.worth > r2.worth;
    else if (r1.age != r2.age)
        return r1.age < r2.age;
    else
        return r1.name < r2.name;
}

int main() {
    int n, m, k, minage, maxage;
    scanf("%d %d", &n, &k);
    Rich rich[n];
    char name[10];
    for (int i = 0; i < n; i++) {
        scanf("%s %d %d", name, &rich[i].age, &rich[i].worth);
        rich[i].name = string(name);
    }
    sort(rich, rich + n, cmp);
    for (int i = 1; i <= k; i++) {
        bool flag = false;
        scanf("%d %d %d", &m, &minage, &maxage);
        printf("Case #%d:\n", i);
        for (int j = 0, cnt = 0; j < n && cnt < m; j++) {
            if (rich[j].age >= minage && rich[j].age <= maxage) {
                flag = true;
                cnt++;
                printf("%s %d %d\n", rich[j].name.c_str(), rich[j].age, rich[j].worth);
            }
        }
        if (!flag)
            printf("None\n");
    }
    return 0;
}
```

