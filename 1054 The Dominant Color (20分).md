##  **1054** **The Dominant Color** (20分) 

Behind the scenes in the computer's memory, color is always talked about as a series of 24 bits of information for each pixel. In an image, the color with the largest proportional area is called the dominant color. A **strictly** dominant color takes more than half of the total area. Now given an image of resolution *M* by *N* (for example, 800×600), you are supposed to point out the strictly dominant color.

### Input Specification:

Each input file contains one test case. For each case, the first line contains 2 positive numbers: *M* (≤800) and *N* (≤600) which are the resolutions of the image. Then *N* lines follow, each contains *M* digital colors in the range [0,224). It is guaranteed that the strictly dominant color exists for each input image. All the numbers in a line are separated by a space.

### Output Specification:

For each test case, simply print the dominant color in a line.

### Sample Input:

```in
5 3
0 0 255 16777215 24
24 24 0 0 24
24 0 24 24 24
```

### Sample Output:

```out
24
```

### Code:

```c++
#include <iostream>
#include <map>
using namespace std;

int main() {
    int m, n, num;
    scanf("%d %d", &m, &n);
    map<int, int> mp;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            scanf("%d", &num);
            mp[num]++;
        }
    }
    for (auto it = mp.begin(); it != mp.end(); it++) {
        if (it->second > m * n / 2) {
            printf("%d", it->first);
            break;
        }
    }
    return 0;
}
```

