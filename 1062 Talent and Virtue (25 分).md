##  **1062 Talent and Virtue (25 分)** 

About 900 years ago, a Chinese philosopher Sima Guang wrote a history book in which he talked about people's talent and virtue. According to his theory, a man being outstanding in both talent and virtue must be a "sage（圣人）"; being less excellent but with one's virtue outweighs talent can be called a "nobleman（君子）"; being good in neither is a "fool man（愚人）"; yet a fool man is better than a "small man（小人）" who prefers talent than virtue.

Now given the grades of talent and virtue of a group of people, you are supposed to rank them according to Sima Guang's theory.

### Input Specification:

Each input file contains one test case. Each case first gives 3 positive integers in a line: *N* (≤105), the total number of people to be ranked; *L* (≥60), the lower bound of the qualified grades -- that is, only the ones whose grades of talent and virtue are both not below this line will be ranked; and *H* (<100), the higher line of qualification -- that is, those with both grades not below this line are considered as the "sages", and will be ranked in non-increasing order according to their total grades. Those with talent grades below *H* but virtue grades not are cosidered as the "noblemen", and are also ranked in non-increasing order according to their total grades, but they are listed after the "sages". Those with both grades below *H*, but with virtue not lower than talent are considered as the "fool men". They are ranked in the same way but after the "noblemen". The rest of people whose grades both pass the *L* line are ranked after the "fool men".

Then *N* lines follow, each gives the information of a person in the format:

```
ID_Number Virtue_Grade Talent_Grade
```

where `ID_Number` is an 8-digit number, and both grades are integers in [0, 100]. All the numbers are separated by a space.

### Output Specification:

The first line of output must give *M* (≤*N*), the total number of people that are actually ranked. Then *M* lines follow, each gives the information of a person in the same format as the input, according to the ranking rules. If there is a tie of the total grade, they must be ranked with respect to their virtue grades in non-increasing order. If there is still a tie, then output in increasing order of their ID's.

### Sample Input:

```in
14 60 80
10000001 64 90
10000002 90 60
10000011 85 80
10000003 85 80
10000004 80 85
10000005 82 77
10000006 83 76
10000007 90 78
10000008 75 79
10000009 59 90
10000010 88 45
10000012 80 100
10000013 90 99
10000014 66 60
```

### Sample Output:

```out
12
10000013 90 99
10000012 80 100
10000003 85 80
10000011 85 80
10000004 80 85
10000007 90 78
10000006 83 76
10000005 82 77
10000002 90 60
10000014 66 60
10000008 75 79
10000001 64 90
```

### Idea:

- 首先要明确，只有都不低于 l 的才会被排名输出，其余一概不看

- 德才均不低于h，则为圣人，第一输出
- 德不低于h，才低于，则为君子，第二输出
- 德才均低于h且德高于才，则为愚人，第三输出
- 其余不低于 l 的第四输出 

### Code:

```c++
#include <algorithm>
#include <iostream>
using namespace std;

typedef struct {
    string id;
    int virtue;
    int talent;
    int pos; //第几个输出
} Per;

bool cmp(Per p1, Per p2) {
    if (p1.pos != p2.pos)
        return p1.pos < p2.pos;
    else if (p1.virtue + p1.talent != p2.virtue + p2.talent)
        return p1.virtue + p1.talent > p2.virtue + p2.talent;
    else if (p1.virtue != p2.virtue)
        return p1.virtue > p2.virtue;
    else
        return p1.id < p2.id;
}

int main() {
    int n, l, h, cnt = 0;
    cin >> n >> l >> h;
    int virtue, talent;
    string id;
    Per per[n];
    for (int i = 0; i < n; i++) {
        cin >> id >> virtue >> talent;
        if (virtue >= h && talent >= h) {
            per[cnt].pos = 1;
            per[cnt].virtue = virtue;
            per[cnt].talent = talent;
            per[cnt].id = id;
            cnt++;
        } else if (talent >= l && virtue >= h) {
            per[cnt].pos = 2;
            per[cnt].virtue = virtue;
            per[cnt].talent = talent;
            per[cnt].id = id;
            cnt++;
        } else if (virtue >= l && talent >= l && virtue >= talent) {
            per[cnt].pos = 3;
            per[cnt].virtue = virtue;
            per[cnt].talent = talent;
            per[cnt].id = id;
            cnt++;
        } else if (virtue >= l && talent >= l) {
            per[cnt].pos = 4;
            per[cnt].virtue = virtue;
            per[cnt].talent = talent;
            per[cnt].id = id;
            cnt++;
        }
    }
    sort(per, per + cnt, cmp);
    cout << cnt << endl;
    for (int i = 0; i < cnt; i++) {
        cout << per[i].id << " " << per[i].virtue << " " << per[i].talent
             << endl;
    }
    return 0;
}
```

