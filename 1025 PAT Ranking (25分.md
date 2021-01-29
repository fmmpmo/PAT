##  **1025** **PAT Ranking** (25分

Programming Ability Test (PAT) is organized by the College of Computer Science and Technology of Zhejiang University. Each test is supposed to run simultaneously in several places, and the ranklists will be merged immediately after the test. Now it is your job to write a program to correctly merge all the ranklists and generate the final rank.

### Input Specification:

Each input file contains one test case. For each case, the first line contains a positive number *N* (≤100), the number of test locations. Then *N* ranklists follow, each starts with a line containing a positive integer *K* (≤300), the number of testees, and then *K* lines containing the registration number (a 13-digit number) and the total score of each testee. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, first print in one line the total number of testees. Then print the final ranklist in the following format:

```
registration_number final_rank location_number local_rank
```

The locations are numbered from 1 to *N*. The output must be sorted in nondecreasing order of the final ranks. The testees with the same score must have the same rank, and the output must be sorted in nondecreasing order of their registration numbers.

### Sample Input:

```in
2
5
1234567890001 95
1234567890005 100
1234567890003 95
1234567890002 77
1234567890004 85
4
1234567890013 65
1234567890011 25
1234567890014 100
1234567890012 85
```

### Sample Output:

```out
9
1234567890005 1 1 1
1234567890014 1 2 1
1234567890001 3 1 2
1234567890003 3 1 2
1234567890004 5 1 4
1234567890012 5 2 2
1234567890002 7 1 5
1234567890013 8 2 3
1234567890011 9 2 4
```

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

typedef struct {
    string id;
    int score;
    int kao;
    int finalrank;
    int kaorank;
} Stu;

bool cmp(Stu s1, Stu s2) {
    if (s1.score != s2.score)
        return s1.score > s2.score;
    else
        return s1.id < s2.id;
}

int main() {
    int n, k, p = 0, sum = 0;
    Stu stu[30001];
    cin >> n;
    for (int i = 1; i <= n; i++) {
        cin >> k;
        sum += k;
        vector<Stu> v;
        Stu st;
        for (int j = 0; j < k; j++) {
            cin >> st.id >> st.score;
            st.kao = i;
            v.push_back(st);
        }
        sort(v.begin(), v.end(), cmp);
        v[0].kaorank = 1;
        stu[p++] = v[0];
        for (int j = 1; j < k; j++) {
            if (v[j].score == v[j - 1].score)
                v[j].kaorank = v[j - 1].kaorank;
            else
                v[j].kaorank = j + 1;
            stu[p++] = v[j];
        }
    }
    sort(stu, stu + p, cmp);
    stu[0].finalrank = 1;
    for (int i = 1; i < p; i++) {
        if (stu[i].score == stu[i - 1].score)
            stu[i].finalrank = stu[i - 1].finalrank;
        else
            stu[i].finalrank = i + 1;
    }
    cout << sum << endl;
    for (int i = 0; i < p; i++) {
        cout << stu[i].id << " " << stu[i].finalrank << " " << stu[i].kao << " "
             << stu[i].kaorank << endl;
    }
    return 0;
}
```

