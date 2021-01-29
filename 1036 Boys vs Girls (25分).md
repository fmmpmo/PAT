##  **1036** **Boys vs Girls** (25分)

This time you are asked to tell the difference between the lowest grade of all the male students and the highest grade of all the female students.

### Input Specification:

Each input file contains one test case. Each case contains a positive integer *N*, followed by *N* lines of student information. Each line contains a student's `name`, `gender`, `ID` and `grade`, separated by a space, where `name` and `ID` are strings of no more than 10 characters with no space, `gender` is either `F` (female) or `M` (male), and `grade` is an integer between 0 and 100. It is guaranteed that all the grades are distinct.

### Output Specification:

For each test case, output in 3 lines. The first line gives the name and ID of the female student with the highest grade, and the second line gives that of the male student with the lowest grade. The third line gives the difference *g**r**a**d**e**F*−*g**r**a**d**e**M*. If one such kind of student is missing, output `Absent` in the corresponding line, and output `NA` in the third line instead.

### Sample Input 1:

```in
3
Joe M Math990112 89
Mike M CS991301 100
Mary F EE990830 95
```

### Sample Output 1:

```out
Mary EE990830
Joe Math990112
6
```

### Sample Input 2:

```in
1
Jean M AA980920 60
```

### Sample Output 2:

```out
Absent
Jean AA980920
NA
```

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

typedef struct {
    string name;
    string gender;
    string id;
    int grade;
} Stu;

bool cmp(Stu s1, Stu s2) { return s1.grade > s2.grade; }

int main() {
    int n;
    cin >> n;
    vector<Stu> v1, v2;
    for (int i = 0; i < n; i++) {
        Stu stu;
        cin >> stu.name >> stu.gender >> stu.id >> stu.grade;
        if (stu.gender == "F")
            v1.push_back(stu);
        else
            v2.push_back(stu);
    }
    if (v1.empty())
        cout << "Absent" << endl;
    else {
        sort(v1.begin(), v1.end(), cmp);
        cout << v1[0].name << " " << v1[0].id << endl;
    }
    if (v2.empty())
        cout << "Absent" << endl;
    else {
        sort(v2.begin(), v2.end(), cmp);
        cout << v2[v2.size() - 1].name << " " << v2[v2.size() - 1].id << endl;
    }
    if (v1.empty() || v2.empty())
        cout << "NA";
    else
        cout << v1[0].grade - v2[v2.size() - 1].grade;
    return 0;
}
```

