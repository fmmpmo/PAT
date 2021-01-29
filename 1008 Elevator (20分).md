##  **1008** **Elevator** (20分)

The highest building in our city has only one elevator. A request list is made up with *N* positive numbers. The numbers denote at which floors the elevator will stop, in specified order. It costs 6 seconds to move the elevator up one floor, and 4 seconds to move down one floor. The elevator will stay for 5 seconds at each stop.

For a given request list, you are to compute the total time spent to fulfill the requests on the list. The elevator is on the 0th floor at the beginning and does not have to return to the ground floor when the requests are fulfilled.

### Input Specification:

Each input file contains one test case. Each case contains a positive integer *N*, followed by *N* positive numbers. All the numbers in the input are less than 100.

### Output Specification:

For each test case, print the total time on a single line.

### Sample Input:

```in
3 2 3 1
```

### Sample Output:

```out
41
```

### Code:

```c++
#include <iostream>
using namespace std;

int main() {
    int n, opt, sum = 0, pre = 0;
    cin >> n;
    while (n--) {
        cin >> opt;
        if (opt > pre) {
            sum += (opt - pre) * 6;
        } else if (opt < pre) {
            sum += (pre - opt) * 4;
        }
        sum += 5;
        pre = opt;
    }
    cout << sum;
    return 0;
}
```

