##  **1133 Splitting A Linked List (25 分)** 

Given a singly linked list, you are supposed to rearrange its elements so that all the negative values appear before all of the non-negatives, and all the values in [0, K] appear before all those greater than K. The order of the elements inside each class must not be changed. For example, given the list being 18→7→-4→0→5→-6→10→11→-2 and K being 10, you must output -4→-6→-2→7→0→5→10→18→11.

### Input Specification:

Each input file contains one test case. For each case, the first line contains the address of the first node, a positive N (≤105) which is the total number of nodes, and a positive K (≤103). The address of a node is a 5-digit nonnegative integer, and NULL is represented by −1.

Then N lines follow, each describes a node in the format:

```
Address Data Next
```

where `Address` is the position of the node, `Data` is an integer in [−105,105], and `Next` is the position of the next node. It is guaranteed that the list is not empty.

### Output Specification:

For each case, output in order (from beginning to the end of the list) the resulting linked list. Each node occupies a line, and is printed in the same format as in the input.

### Sample Input:

```in
00100 9 10
23333 10 27777
00000 0 99999
00100 18 12309
68237 -6 23333
33218 -4 00000
48652 -2 -1
99999 5 68237
27777 11 48652
12309 7 33218
```

### Sample Output:

```out
33218 -4 68237
68237 -6 48652
48652 -2 12309
12309 7 00000
00000 0 99999
99999 5 23333
23333 10 00100
00100 18 27777
27777 11 -1
```

### Code:

```c++
#include <iostream>
#include <vector>
using namespace std;

int val[100001], xnext[100001];
vector<int> v, fu, ink, bigk;

int main() {
    int head, n, k, add;
    cin >> head >> n >> k;
    for (int i = 0; i < n; i++) {
        cin >> add;
        cin >> val[add] >> xnext[add];
    }
    while (head != -1) {
        v.push_back(head);
        head = xnext[head];
    }
    for (int i = 0; i < v.size(); i++) {
        if (val[v[i]] < 0)
            fu.push_back(v[i]);
        else if (val[v[i]] >= 0 && val[v[i]] <= k)
            ink.push_back(v[i]);
        else
            bigk.push_back(v[i]);
    }
    int len1 = fu.size(), len2 = ink.size(), len3 = bigk.size();
    for (int i = 0; i < len1 - 1; i++)
        printf("%05d %d %05d\n", fu[i], val[fu[i]], fu[i + 1]);
    if (len1) {
        printf("%05d %d ", fu[len1 - 1], val[fu[len1 - 1]]);
        if (len2)
            printf("%05d\n", ink[0]);
        else if (len3)
            printf("%05d\n", bigk[0]);
        else
            printf("-1");
    }
    if (len2) {
        for (int i = 0; i < len2 - 1; i++)
            printf("%05d %d %05d\n", ink[i], val[ink[i]], ink[i + 1]);
        printf("%05d %d ", ink[len2 - 1], val[ink[len2 - 1]]);
        if (len3)
            printf("%05d\n", bigk[0]);
        else
            printf("-1");
    }
    if (len3) {
        for (int i = 0; i < len3 - 1; i++)
            printf("%05d %d %05d\n", bigk[i], val[bigk[i]], bigk[i + 1]);
        printf("%05d %d -1", bigk[len3 - 1], val[bigk[len3 - 1]]);
    }
    return 0;
}
```

