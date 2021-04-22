##  **1098 Insertion or Heap Sort (25 分)** 

According to Wikipedia:

**Insertion sort** iterates, consuming one input element each repetition, and growing a sorted output list. Each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there. It repeats until no input elements remain.

**Heap sort** divides its input into a sorted and an unsorted region, and it iteratively shrinks the unsorted region by extracting the largest element and moving that to the sorted region. it involves the use of a heap data structure rather than a linear-time search to find the maximum.

Now given the initial sequence of integers, together with a sequence which is a result of several iterations of some sorting method, can you tell which sorting method we are using?

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer *N* (≤100). Then in the next line, *N* integers are given as the initial sequence. The last line contains the partially sorted sequence of the *N* numbers. It is assumed that the target sequence is always ascending. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, print in the first line either "Insertion Sort" or "Heap Sort" to indicate the method used to obtain the partial result. Then run this method for one more iteration and output in the second line the resulting sequence. It is guaranteed that the answer is unique for each test case. All the numbers in a line must be separated by a space, and there must be no extra space at the end of the line.

### Sample Input 1:

```in
10
3 1 2 8 7 5 9 4 6 0
1 2 3 7 8 5 9 4 6 0
```

### Sample Output 1:

```out
Insertion Sort
1 2 3 5 7 8 9 4 6 0
```

### Sample Input 2:

```
10
3 1 2 8 7 5 9 4 6 0
6 4 5 1 0 3 2 7 8 9
```

### Sample Output 2:

```
Heap Sort
5 4 3 1 0 2 6 7 8 9
```

### Idea:

- 先判断好判断的，容易发现是插入排序，在某一轮排好序的数组中找到第一个第二个数比第一个数大的，此时停止，然后从该位置开始，比较两个数组中的数据是否都一样，如果都一样，则说明是插入排序，否则是堆排序。
- 对于堆排序，要进行调整，首先交换第一个和最后一个元素，此时最后一个是已经排好序的，然后向下进行调整即可，使其重新调整成为大顶堆（可以通过样例看出）。

### Code:

```c++
#include <algorithm>
#include <iostream>
using namespace std;

int a[101], b[101];

void down(int low, int high) {
    int init = low;
    low = low * 2;
    while (low <= high) {
        if (low + 1 <= high && b[low] < b[low + 1]) {
            low++;
        }
        if (b[low] > b[init]) {
            swap(b[low], b[init]);
            init = low;
            low *= 2;
        } else {
            break;
        }
    }
}

int main() {
    int n;
    cin >> n;
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
    }
    for (int i = 1; i <= n; i++) {
        cin >> b[i];
    }
    bool flag = true;
    int i;
    for (i = 2; i <= n; i++) {
        if (b[i] < b[i - 1]) {
            break;
        }
    }
    for (int j = i; j <= n; j++) {
        if (a[j] != b[j]) {
            flag = false;
            break;
        }
    }
    if (flag) {
        printf("Insertion Sort\n");
        sort(b + 1, b + i + 1);
        printf("%d", b[1]);
        for (int j = 2; j <= n; j++) {
            printf(" %d", b[j]);
        }
    } else {
        printf("Heap Sort\n");
        int pos = n;
        while (pos > 1 && b[pos - 1] <= b[pos])
            pos--;
        swap(b[1], b[pos]);
        down(1, pos - 1);
        for (int i = 1; i <= n; i++) {
            if (i > 1)
                printf(" ");
            printf("%d", b[i]);
        }
    }
    return 0;
}
```

