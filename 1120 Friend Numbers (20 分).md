##  **1120 Friend Numbers (20 分)** 

Two integers are called "friend numbers" if they share the same sum of their digits, and the sum is their "friend ID". For example, 123 and 51 are friend numbers since 1+2+3 = 5+1 = 6, and 6 is their friend ID. Given some numbers, you are supposed to count the number of different friend ID's among them.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer N. Then N positive integers are given in the next line, separated by spaces. All the numbers are less than 104.

### Output Specification:

For each case, print in the first line the number of different frind ID's among the given integers. Then in the second line, output the friend ID's in increasing order. The numbers must be separated by exactly one space and there must be no extra space at the end of the line.

### Sample Input:

```in
8
123 899 51 998 27 33 36 12
```

### Sample Output:

```out
4
3 6 9 26
```

### Code:

```c++
#include <iostream>
#include <set>
#include <algorithm>
using namespace std;

int main() {
	set<int> s;
	int n,num;
	cin >> n;
	while(n--) {
		cin >> num;
		int sum = 0;
		while(num!=0) {
			sum += num%10;
			num /= 10;
		}
		s.insert(sum);
	}
	cout << s.size() << endl;
	for(auto it = s.begin(); it!=s.end(); it++) {
		if(it!=s.begin())
			cout << " ";
		cout << *it;
	}
	return 0;
}
```

