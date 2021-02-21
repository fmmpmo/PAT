##  **1074 Reversing Linked List (25 分)** 

Given a constant *K* and a singly linked list *L*, you are supposed to reverse the links of every *K* elements on *L*. For example, given *L* being 1→2→3→4→5→6, if *K*=3, then you must output 3→2→1→6→5→4; if *K*=4, you must output 4→3→2→1→5→6.

### Input Specification:

Each input file contains one test case. For each case, the first line contains the address of the first node, a positive *N* (≤105) which is the total number of nodes, and a positive *K* (≤*N*) which is the length of the sublist to be reversed. The address of a node is a 5-digit nonnegative integer, and NULL is represented by -1.

Then *N* lines follow, each describes a node in the format:

```
Address Data Next
```

where `Address` is the position of the node, `Data` is an integer, and `Next` is the position of the next node.

### Output Specification:

For each case, output the resulting ordered linked list. Each node occupies a line, and is printed in the same format as in the input.

### Sample Input:

```in
00100 6 4
00000 4 99999
00100 1 12309
68237 6 -1
33218 3 00000
99999 5 68237
12309 2 33218
```

### Sample Output:

```out
00000 4 33218
33218 3 12309
12309 2 00100
00100 1 99999
99999 5 68237
68237 6 -1
```

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

int val[100001], xnext[100001];
vector<int> v;

int main() {
    int n, k, head, add;
    cin >> head >> n >> k;
    for (int i = 0; i < n; i++) {
        cin >> add;
        cin >> val[add] >> xnext[add];
    }
    while (head != -1) {
        v.push_back(head);
        head = xnext[head];
    }
    int x = v.size();//有可能有不在里边的结点，所以不能用n来遍历
    for (int i = 0; i < x - x % k; i += k)
        reverse(v.begin() + i, v.begin() + i + k);
    for (int i = 0; i < x - 1; i++)
        printf("%05d %d %05d\n", v[i], val[v[i]], v[i + 1]);
    printf("%05d %d -1", v[x - 1], val[v[x - 1]]);
    return 0;
}
```

