##  **1032 Sharing (25 分)** 

 To store English words, one method is to use linked lists and store a word letter by letter. To save some space, we may let the words share the same sublist if they share the same suffix. For example, `loading` and `being` are stored as showed in Figure 1. 

 ![fig.jpg](https://images.ptausercontent.com/ef0a1fdf-3d9f-46dc-9a27-21f989270fd4.jpg) 

Figure 1

You are supposed to find the starting position of the common suffix (e.g. the position of `i` in Figure 1).

### Input Specification:

Each input file contains one test case. For each case, the first line contains two addresses of nodes and a positive *N* (≤105), where the two addresses are the addresses of the first nodes of the two words, and *N* is the total number of nodes. The address of a node is a 5-digit positive integer, and NULL is represented by −1.

Then *N* lines follow, each describes a node in the format:

```
Address Data Next
```

where`Address` is the position of the node, `Data` is the letter contained by this node which is an English letter chosen from { a-z, A-Z }, and `Next` is the position of the next node.

### Output Specification:

For each case, simply output the 5-digit starting position of the common suffix. If the two words have no common suffix, output `-1` instead.

### Sample Input 1:

```in
11111 22222 9
67890 i 00002
00010 a 12345
00003 g -1
12345 D 67890
00002 n 00003
22222 B 23456
11111 L 00001
23456 e 67890
00001 o 00010
```

### Sample Output 1:

```out
67890
```

### Sample Input 2:

```in
00001 00002 4
00001 a 10001
10001 s -1
00002 a 10002
10002 t -1
```

### Sample Output 2:

```out
-1
```

### Code:

```c++
#include <iostream>
using namespace std;

typedef struct {
    int data;
    int next;
} Node;

Node tmp[100001];
int vis[100001];

int main() {
    int head1, head2, n, add;
    scanf("%d %d %d", &head1, &head2, &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &add);
        getchar();
        scanf("%c %d", &tmp[add].data, &tmp[add].next);
    }
    while (head1 != -1) {
        vis[head1] = 1;
        head1 = tmp[head1].next;
    }
    while (head2 != -1) {
        if (vis[head2]) {
            printf("%05d", head2);
            return 0;
        }
        head2 = tmp[head2].next;
    }
    printf("-1");
    return 0;
}

/*
不知道哪里错了
#include <iostream>
using namespace std;

typedef struct {
    int data;
    int next;
} Node;

Node tmp[100001];
int res1[100001], res2[100001];

int main() {
    int head1, head2, n, add;
    scanf("%d %d %d", &head1, &head2, &n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &add);
        getchar();
        scanf("%c %d", &tmp[add].data, &tmp[add].next);
    }
    int t1 = head1, t2 = head2, p = 0, k = 0;
    while (t1 != -1) {
        res1[p++] = t1;
        t1 = tmp[t1].next;
    }
    while (t2 != -1) {
        res2[k++] = t2;
        t2 = tmp[t2].next;
    }
    int i;
    for (i = 0; i < p && i < k; i++) {
        if (res1[i] == res2[i]) {
            printf("%05d", res1[i]);
            break;
        }
    }
    if (i == p || i == k)
        printf("-1");
    return 0;
}
*/
```

