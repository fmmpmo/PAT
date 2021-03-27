##  **1053 Path of Equal Weight (30 分)** 

Given a non-empty tree with root *R*, and with weight *W**i* assigned to each tree node *T**i*. The **weight of a path from \*R\* to \*L\*** is defined to be the sum of the weights of all the nodes along the path from *R* to any leaf node *L*.

Now given any weighted tree, you are supposed to find all the paths with their weights equal to a given number. For example, let's consider the tree showed in the following figure: for each node, the upper number is the node ID which is a two-digit number, and the lower number is the weight of that node. Suppose that the given number is 24, then there exists 4 different paths which have the same given weight: {10 5 2 7}, {10 4 10}, {10 3 3 6 2} and {10 3 3 6 2}, which correspond to the red edges in the figure.

 ![212](https://images.ptausercontent.com/212) 

### Input Specification:

Each input file contains one test case. Each case starts with a line containing 0<*N*≤100, the number of nodes in a tree, *M* (<*N*), the number of non-leaf nodes, and 0<*S*<230, the given weight number. The next line contains *N* positive numbers where *W**i* (<1000) corresponds to the tree node *T**i*. Then *M* lines follow, each in the format:

```
ID K ID[1] ID[2] ... ID[K]
```

where `ID` is a two-digit number representing a given non-leaf node, `K` is the number of its children, followed by a sequence of two-digit `ID`'s of its children. For the sake of simplicity, let us fix the root ID to be `00`.

### Output Specification:

For each test case, print all the paths with weight S in **non-increasing** order. Each path occupies a line with printed weights from the root to the leaf in order. All the numbers must be separated by a space with no extra space at the end of the line.

Note: sequence {*A*1,*A*2,⋯,*A**n*} is said to be **greater than** sequence {*B*1,*B*2,⋯,*B**m*} if there exists 1≤*k*<*m**i**n*{*n*,*m*} such that *A**i*=*B**i* for *i*=1,⋯,*k*, and *A**k*+1>*B**k*+1.

### Sample Input:

```in
20 9 24
10 2 4 3 5 10 2 18 9 7 2 2 1 3 12 1 8 6 2 2
00 4 01 02 03 04
02 1 05
04 2 06 07
03 3 11 12 13
06 1 09
07 2 08 10
16 1 15
13 3 14 16 17
17 2 18 19
```

### Sample Output:

```out
10 5 2 7
10 4 10
10 3 3 6 2
10 3 3 6 2
```

### Idea:（算法笔记）

- 这是一棵普通性质的树，因此令结构体node存放结点的数据域和指针域，其中指针域使用vector存放所有孩子结点的编号，又考虑到最后的输出需要按权值从大到小排序，因此不妨在读入时就事先对每个结点的子结点vector进行排序，这样在遍历时就会优先遍历到 权值大的子结点
- 令int型数组path存放递归过程中产生的路径上的结点编号，dfs中有三个参数：当前访问的结点编号index，当前路径path上的结点个数num（也是递归层数，因为每深入一层，path上就会多一个结点），当前路径上的权值和sum
- 若sum > s，直接return；若sum==s，说明到当前访问结点index为止，判断此时index结点是否为叶子结点，不是则return，是则打印；若sum < s，说明还未满足要求，继续向下枚举递归

### Code:

```c++
#include <algorithm>
#include <iostream>
#include <vector>
using namespace std;

typedef struct {
    int weight;        //数据域
    vector<int> child; //孩子指针域
} Node;

Node node[110];
int n, m, s;
int path[110]; //路径

//按节点数据域从大到小排序
bool cmp(int a, int b) { return node[a].weight > node[b].weight; }

//当前访问结点为index，num为当前路径上的结点个数，sum为当前所有结点的点权之和
void dfs(int index, int num, int sum) {
    if (sum > s)
        return;
    if (sum == s) {
        if (node[index].child.size() != 0) //不是叶子结点
            return;
        for (int i = 0; i < num; i++) {
            printf("%d", node[path[i]].weight);
            if (i < num - 1)
                printf(" ");
            else
                printf("\n");
        }
        return;
    }
    for (int i = 0; i < node[index].child.size(); i++) {
        int x = node[index].child[i];
        path[num] = x;
        dfs(x, num + 1, sum + node[x].weight);
    }
}

int main() {
    scanf("%d %d %d", &n, &m, &s);
    for (int i = 0; i < n; i++) {
        scanf("%d", &node[i].weight);
    }
    int id, k, child;
    for (int i = 0; i < m; i++) {
        scanf("%d %d", &id, &k);
        for (int j = 0; j < k; j++) {
            scanf("%d", &child);
            node[id].child.push_back(child);
        }
        sort(node[id].child.begin(), node[id].child.end(), cmp);
    }
    path[0] = 0; //路径的第一个结点设置为0号结点
    dfs(0, 1, node[0].weight);
    return 0;
}
```

