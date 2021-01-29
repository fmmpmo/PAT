##  **1012** **The Best Rank** (25分)

To evaluate the performance of our first year CS majored students, we consider their grades of three courses only: `C` - C Programming Language, `M` - Mathematics (Calculus or Linear Algrbra), and `E` - English. At the mean time, we encourage students by emphasizing on their best ranks -- that is, among the four ranks with respect to the three courses and the average grade, we print the best rank for each student.

For example, The grades of `C`, `M`, `E` and `A` - Average of 4 students are given as the following:

```
StudentID  C  M  E  A
310101     98 85 88 90
310102     70 95 88 84
310103     82 87 94 88
310104     91 91 91 91
```

Then the best ranks for all the students are No.1 since the 1st one has done the best in C Programming Language, while the 2nd one in Mathematics, the 3rd one in English, and the last one in average.

### Input Specification:

Each input file contains one test case. Each case starts with a line containing 2 numbers *N* and *M* (≤2000), which are the total number of students, and the number of students who would check their ranks, respectively. Then *N* lines follow, each contains a student ID which is a string of 6 digits, followed by the three integer grades (in the range of [0, 100]) of that student in the order of `C`, `M` and `E`. Then there are *M* lines, each containing a student ID.

### Output Specification:

For each of the *M* students, print in one line the best rank for him/her, and the symbol of the corresponding rank, separated by a space.

The priorities of the ranking methods are ordered as `A` > `C` > `M` > `E`. Hence if there are two or more ways for a student to obtain the same best rank, output the one with the highest priority.

If a student is not on the grading list, simply output `N/A`.

### Sample Input:

```in
5 6
310101 98 85 88
310102 70 95 88
310103 82 87 94
310104 91 91 91
310105 85 90 90
310101
310102
310103
310104
310105
999999
```

### Sample Output:

```out
1 C
1 M
1 E
1 A
3 A
N/A
```

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <map>
using namespace std;

typedef struct {
    int id;
    int c, m, e;
    double ave;
    int rankc, rankm, ranke, rankave;
    int rank;
    char ch;
} Stu;

bool cmp1(Stu s1, Stu s2) { return s1.c > s2.c; }
bool cmp2(Stu s1, Stu s2) { return s1.m > s2.m; }
bool cmp3(Stu s1, Stu s2) { return s1.e > s2.e; }
bool cmp4(Stu s1, Stu s2) { return s1.ave > s2.ave; }

int main() {
    int n, m;
    map<int, int> mp;
    scanf("%d %d", &n, &m);
    Stu stu[n];
    for (int i = 0; i < n; i++) {
        scanf("%d %d %d %d", &stu[i].id, &stu[i].c, &stu[i].m, &stu[i].e);
        stu[i].ave = (stu[i].c + stu[i].m + stu[i].e) * 1.0 / 3;
        mp[stu[i].id] = 1;
    }
    sort(stu, stu + n, cmp1);
    stu[0].rankc = 1;
    for (int i = 1; i < n; i++) {
        if (stu[i].c == stu[i - 1].c)
            stu[i].rankc = stu[i - 1].rankc;
        else
            stu[i].rankc = i + 1;
    }
    sort(stu, stu + n, cmp2);
    stu[0].rankm = 1;
    for (int i = 1; i < n; i++) {
        if (stu[i].m == stu[i - 1].m)
            stu[i].rankm = stu[i - 1].rankm;
        else
            stu[i].rankm = i + 1;
    }
    sort(stu, stu + n, cmp3);
    stu[0].ranke = 1;
    for (int i = 1; i < n; i++) {
        if (stu[i].e == stu[i - 1].e)
            stu[i].ranke = stu[i - 1].ranke;
        else
            stu[i].ranke = i + 1;
    }
    sort(stu, stu + n, cmp4);
    stu[0].rankave = 1;
    for (int i = 1; i < n; i++) {
        if (stu[i].ave == stu[i - 1].ave)
            stu[i].rankave = stu[i - 1].rankave;
        else
            stu[i].rankave = i + 1;
    }
    for (int i = 0; i < n; i++) {
        int minx = 6;
        if (stu[i].rankave < minx) {
            minx = stu[i].rankave;
            stu[i].ch = 'A';
        }
        if (stu[i].rankc < minx) {
            minx = stu[i].rankc;
            stu[i].ch = 'C';
        }
        if (stu[i].rankm < minx) {
            minx = stu[i].rankm;
            stu[i].ch = 'M';
        }
        if (stu[i].ranke < minx) {
            minx = stu[i].ranke;
            stu[i].ch = 'E';
        }
        stu[i].rank = minx;
    }
    int id;
    while (m--) {
        scanf("%d", &id);
        if (mp[id] == 0)
            printf("N/A\n");
        else {
            for (int i = 0; i < n; i++) {
                if (stu[i].id == id) {
                    printf("%d %c\n", stu[i].rank, stu[i].ch);
                }
            }
        }
    }
    return 0;
}
```

