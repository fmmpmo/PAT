##  **1153 Decode Registration Card of PAT (25 分)** 

A registration card number of PAT consists of 4 parts:

- the 1st letter represents the test level, namely, `T` for the top level, `A` for advance and `B` for basic;
- the 2nd - 4th digits are the test site number, ranged from 101 to 999;
- the 5th - 10th digits give the test date, in the form of `yymmdd`;
- finally the 11th - 13th digits are the testee's number, ranged from 000 to 999.

Now given a set of registration card numbers and the scores of the card owners, you are supposed to output the various statistics according to the given queries.

### Input Specification:

Each input file contains one test case. For each case, the first line gives two positive integers *N* (≤104) and *M* (≤100), the numbers of cards and the queries, respectively.

Then *N* lines follow, each gives a card number and the owner's score (integer in [0,100]), separated by a space.

After the info of testees, there are *M* lines, each gives a query in the format `Type Term`, where

- `Type` being 1 means to output all the testees on a given level, in non-increasing order of their scores. The corresponding `Term` will be the letter which specifies the level;
- `Type` being 2 means to output the total number of testees together with their total scores in a given site. The corresponding `Term` will then be the site number;
- `Type` being 3 means to output the total number of testees of every site for a given test date. The corresponding `Term` will then be the date, given in the same format as in the registration card.

### Output Specification:

For each query, first print in a line `Case #: input`, where `#` is the index of the query case, starting from 1; and `input` is a copy of the corresponding input query. Then output as requested:

- for a type 1 query, the output format is the same as in input, that is, `CardNumber Score`. If there is a tie of the scores, output in increasing alphabetical order of their card numbers (uniqueness of the card numbers is guaranteed);
- for a type 2 query, output in the format `Nt Ns` where `Nt` is the total number of testees and `Ns` is their total score;
- for a type 3 query, output in the format `Site Nt` where `Site` is the site number and `Nt` is the total number of testees at `Site`. The output must be in non-increasing order of `Nt`'s, or in increasing order of site numbers if there is a tie of `Nt`.

If the result of a query is empty, simply print `NA`.

### Sample Input:

```in
8 4
B123180908127 99
B102180908003 86
A112180318002 98
T107150310127 62
A107180908108 100
T123180908010 78
B112160918035 88
A107180908021 98
1 A
2 107
3 180908
2 999
```

### Sample Output:

```out
Case 1: 1 A
A107180908108 100
A107180908021 98
A112180318002 98
Case 2: 2 107
3 260
Case 3: 3 180908
107 2
123 2
102 1
Case 4: 2 999
NA
```

### Idea:

- 根据题目要求进行分类即可，对于输出T A B类型的，可以在输入的时候就对其进行存储，这样方便后续输出
- 关于输出3，可以使用map的键值对形式存储，最后存入vector中按照规定排序，这样方便统计对应site的对应数量，我采用的是unordered_map，因为这里不需要按照键排序，改用后可以降低运行时间
- 直接写完后提交最后两个测试点超时，不用说，首先一堆cin cout的输出那就过不去，都改为scanf和printf即可，注意字符串的输入。建议char数组输入，然后使用string的构造函数转为string类型，否则有时候容易出问题

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <unordered_map>
#include <vector>
using namespace std;

typedef struct {
    string pat;
    string site, date, test;
    int score;
} Kao;

bool cmp1(Kao k1, Kao k2) {
    if (k1.score != k2.score)
        return k1.score > k2.score;
    return k1.pat < k2.pat;
}

bool cmp2(pair<string, int> p1, pair<string, int> p2) {
    if (p1.second != p2.second)
        return p1.second > p2.second;
    return p1.first < p2.first;
}

int main() {
    int n, m;
    scanf("%d %d", &n, &m);
    Kao kao[n];
    vector<Kao> v1, v2, v3;
    char pat[15];
    for (int i = 0; i < n; i++) {
        scanf("%s %d", pat, &kao[i].score);
        kao[i].pat = string(pat);
        kao[i].site = kao[i].pat.substr(1, 3);
        kao[i].date = kao[i].pat.substr(4, 6);
        kao[i].test = kao[i].pat.substr(10);
        if (pat[0] == 'T')
            v1.push_back(kao[i]);
        else if (pat[0] == 'A')
            v2.push_back(kao[i]);
        else
            v3.push_back(kao[i]);
    }
    int index;
    char op[7];
    for (int i = 1; i <= m; i++) {
        scanf("%d %s", &index, op);
        printf("Case %d: %d %s\n", i, index, op);
        string opt = string(op);
        if (index == 1) {
            if (opt == "T") {
                if (v1.empty())
                    printf("NA\n");
                else {
                    sort(v1.begin(), v1.end(), cmp1);
                    for (int j = 0; j < v1.size(); j++) {
                        printf("%s %d\n", v1[j].pat.c_str(), v1[j].score);
                    }
                }
            } else if (opt == "A") {
                if (v2.empty())
                    printf("NA\n");
                else {
                    sort(v2.begin(), v2.end(), cmp1);
                    for (int j = 0; j < v2.size(); j++) {
                        printf("%s %d\n", v2[j].pat.c_str(), v2[j].score);
                    }
                }
            } else {
                if (v3.empty())
                    printf("NA\n");
                else {
                    sort(v3.begin(), v3.end(), cmp1);
                    for (int j = 0; j < v3.size(); j++) {
                        printf("%s %d\n", v3[j].pat.c_str(), v3[j].score);
                    }
                }
            }
        } else if (index == 2) {
            int nt = 0, ns = 0;
            for (int j = 0; j < n; j++) {
                if (kao[j].site == opt) {
                    nt++;
                    ns += kao[j].score;
                }
            }
            if (nt == 0)
                printf("NA\n");
            else
                printf("%d %d\n", nt, ns);
        } else {
            unordered_map<string, int> mp;
            vector<pair<string, int>> v;
            for (int j = 0; j < n; j++) {
                if (kao[j].date == opt) {
                    mp[kao[j].site]++;
                }
            }
            if (mp.size() == 0)
                printf("NA\n");
            else {
                for (auto it = mp.begin(); it != mp.end(); it++) {
                    v.push_back(make_pair(it->first, it->second));
                }
                sort(v.begin(), v.end(), cmp2);
                for (int j = 0; j < v.size(); j++) {
                    printf("%s %d\n", v[j].first.c_str(), v[j].second);
                }
            }
        }
    }
    return 0;
}
```

