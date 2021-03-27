##  **1034 Head of a Gang (30 分)** 

One way that the police finds the head of a gang is to check people's phone calls. If there is a phone call between *A* and *B*, we say that *A* and *B* is related. The weight of a relation is defined to be the total time length of all the phone calls made between the two persons. A "Gang" is a cluster of more than 2 persons who are related to each other with total relation weight being greater than a given threshold *K*. In each gang, the one with maximum total weight is the head. Now given a list of phone calls, you are supposed to find the gangs and the heads.

### Input Specification:

Each input file contains one test case. For each case, the first line contains two positive numbers *N* and *K* (both less than or equal to 1000), the number of phone calls and the weight threthold, respectively. Then *N* lines follow, each in the following format:

```
Name1 Name2 Time
```

where `Name1` and `Name2` are the names of people at the two ends of the call, and `Time` is the length of the call. A name is a string of three capital letters chosen from `A`-`Z`. A time length is a positive integer which is no more than 1000 minutes.

### Output Specification:

For each test case, first print in a line the total number of gangs. Then for each gang, print in a line the name of the head and the total number of the members. It is guaranteed that the head is unique for each gang. The output must be sorted according to the alphabetical order of the names of the heads.

### Sample Input 1:

```in
8 59
AAA BBB 10
BBB AAA 20
AAA CCC 40
DDD EEE 5
EEE DDD 70
FFF GGG 30
GGG HHH 20
HHH FFF 10
```

### Sample Output 1:

```out
2
AAA 3
GGG 3
```

### Sample Input 2:

```in
8 70
AAA BBB 10
BBB AAA 20
AAA CCC 40
DDD EEE 5
EEE DDD 70
FFF GGG 30
GGG HHH 20
HHH FFF 10
```

### Sample Output 2:

```out
0
```

### Idea:（算法笔记）

- 当一个连通块的总边权大于给定的阈值k且总个数大于2时，才会被输出
- 由于通话记录的条数最多有1000条，这意味着不同的人可能有2000人，所以数组大小要以2000为依据
- 在递归过程中，对每个边权都加了两次，所以在计算最后的连通块边权之和是否大于k之前，需要将其/2再判断。

### Code:

```c++
#include <iostream>
#include <map>
using namespace std;

map<int, string> intToString; //编号->姓名
map<string, int> stringToInt; //姓名->编号
map<string, int> gang;        // head
int g[2001][2001], weight[2001];
bool vis[2001];
int n, k, idx;

int change(string name) {
    if (stringToInt.find(name) != stringToInt.end()) {
        return stringToInt[name]; //返回编号
    } else {
        stringToInt[name] = idx; // name的编号为index
        intToString[idx] = name; // index对应name
        return idx++;            //总人数+1
    }
}

void dfs(int nowVisit, int &head, int &num, int &sum) {
    num++;
    vis[nowVisit] = true;
    if (weight[nowVisit] >
        weight[head]) { //当前访问结点的点权大于头目的点权，更新头目
        head = nowVisit;
    }
    for (int i = 0; i < idx; i++) {
        if (g[nowVisit][i]) { //路径可达
            sum += g[nowVisit][i];
            if (!vis[i]) {
                dfs(i, head, num, sum);
            }
        }
    }
}

void dfsTrave() {
    for (int i = 0; i < idx; i++) {
        if (!vis[i]) {
            int head = i, num = 0, sum = 0; //头目，成员人数，总权值
            dfs(i, head, num, sum);         //遍历i所在的连通块
            if (num > 2 && sum / 2 > k) { //每条边的权值被加了2次，所以除2
                gang[intToString[head]] = num;
            }
        }
    }
}

int main() {
    cin >> n >> k;
    int time;
    string a, b;
    for (int i = 0; i < n; i++) {
        cin >> a >> b >> time;
        int x = change(a), y = change(b);
        weight[x] += time, weight[y] += time; //点权增加
        g[x][y] += time, g[y][x] += time;     //边权增加
    }
    dfsTrave(); //遍历整个图的所有连通块，获取gang信息
    cout << gang.size() << endl;
    for (auto it = gang.begin(); it != gang.end(); it++) {
        cout << it->first << " " << it->second << endl;
    }
    return 0;
}
```

