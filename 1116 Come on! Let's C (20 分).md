##  **1116 Come on! Let's C (20 分)** 

"Let's C" is a popular and fun programming contest hosted by the College of Computer Science and Technology, Zhejiang University. Since the idea of the contest is for fun, the award rules are funny as the following:

- 0、 The Champion will receive a "Mystery Award" (such as a BIG collection of students' research papers...).
- 1、 Those who ranked as a prime number will receive the best award -- the Minions (小黄人)!
- 2、 Everyone else will receive chocolates.

Given the final ranklist and a sequence of contestant ID's, you are supposed to tell the corresponding awards.

### Input Specification:

Each input file contains one test case. For each case, the first line gives a positive integer N (≤104), the total number of contestants. Then N lines of the ranklist follow, each in order gives a contestant's ID (a 4-digit number). After the ranklist, there is a positive integer K followed by K query ID's.

### Output Specification:

For each query, print in a line `ID: award` where the award is `Mystery Award`, or `Minion`, or `Chocolate`. If the ID is not in the ranklist, print `Are you kidding?` instead. If the ID has been checked before, print `ID: Checked`.

### Sample Input:

```in
6
1111
6666
8888
1234
5555
0001
6
8888
0001
1111
2222
8888
2222
```

### Sample Output:

```out
8888: Minion
0001: Chocolate
1111: Mystery Award
2222: Are you kidding?
8888: Checked
2222: Are you kidding?
```

### Code:

```c++
#include <iostream>
#include <map>
using namespace std;

bool isprime(int n) {
	if(n<=1)
		return false;
	for(int i = 2; i*i<=n; i++) {
		if(n%i==0)
			return false;
	}
	return true;
}

int main() {
	map<int,int> mp;
	int vis[10000] = {0};
	int n,k,id;
	cin >> n;
	for(int i = 1; i<=n; i++) {
		cin >> id;
		mp[id] = i;
	}
	cin >> k;
	while(k--) {
		cin >> id;
		if(mp[id]==0)
			printf("%04d: Are you kidding?\n",id);
		else {
			if(vis[id])
				printf("%04d: Checked\n",id);
			else {
				if(mp[id]==1)
					printf("%04d: Mystery Award\n",id);
				else if(isprime(mp[id]))
					printf("%04d: Minion\n",id);
				else
					printf("%04d: Chocolate\n",id);
				vis[id] = 1;
			}
		}
	}
	return 0;
}
```

