##  **1097 Deduplication on a Linked List (25 分)** 

Given a singly linked list *L* with integer keys, you are supposed to remove the nodes with duplicated absolute values of the keys. That is, for each value *K*, only the first node of which the value or absolute value of its key equals *K* will be kept. At the mean time, all the removed nodes must be kept in a separate list. For example, given *L* being 21→-15→-15→-7→15, you must output 21→-15→-7, and the removed list -15→15.

### Input Specification:

Each input file contains one test case. For each case, the first line contains the address of the first node, and a positive *N* (≤105) which is the total number of nodes. The address of a node is a 5-digit nonnegative integer, and NULL is represented by −1.

Then *N* lines follow, each describes a node in the format:

```
Address Key Next
```

where `Address` is the position of the node, `Key` is an integer of which absolute value is no more than 104, and `Next` is the position of the next node.

### Output Specification:

For each case, output the resulting linked list first, then the removed list. Each node occupies a line, and is printed in the same format as in the input.

### Sample Input:

```in
00100 5
99999 -7 87654
23854 -15 00000
87654 15 -1
00000 -15 99999
00100 21 23854
```

### Sample Output:

```out
00100 21 23854
23854 -15 99999
99999 -7 -1
00000 -15 87654
87654 15 -1
```

### Code:

```c++
#include <cmath>
#include <iostream>
using namespace std;

typedef struct {
    int data;
    int next;
} Node;

Node node[100001];
int res1[100001], res2[100001];
bool vis[100001];

int main() {
    int head, n, add, p = 0, k = 0;
    cin >> head >> n;
    for (int i = 0; i < n; i++) {
        cin >> add;
        cin >> node[add].data >> node[add].next;
    }
    while (head != -1) {
        int x = abs(node[head].data);
        if (!vis[x]) {
            vis[x] = true;
            res1[p++] = head;
        } else
            res2[k++] = head;
        head = node[head].next;
    }
    for (int i = 0; i < p - 1; i++)
        printf("%05d %d %05d\n", res1[i], node[res1[i]].data, res1[i + 1]);
    printf("%05d %d -1\n", res1[p - 1], node[res1[p - 1]].data);
    if (k) {
        for (int i = 0; i < k - 1; i++)
            printf("%05d %d %05d\n", res2[i], node[res2[i]].data, res2[i + 1]);
        printf("%05d %d -1\n", res2[k - 1], node[res2[k - 1]].data);
    }
    return 0;
}
```

