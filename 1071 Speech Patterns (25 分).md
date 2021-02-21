##  **1071 Speech Patterns (25 分)** 

People often have a preference among synonyms of the same word. For example, some may prefer "the police", while others may prefer "the cops". Analyzing such patterns can help to narrow down a speaker's identity, which is useful when validating, for example, whether it's still the same person behind an online avatar.

Now given a paragraph of text sampled from someone's speech, can you find the person's most commonly used word?

### Input Specification:

Each input file contains one test case. For each case, there is one line of text no more than 1048576 characters in length, terminated by a carriage return `\n`. The input contains at least one alphanumerical character, i.e., one character from the set [`0-9 A-Z a-z`].

### Output Specification:

For each test case, print in one line the most commonly occurring word in the input text, followed by a space and the number of times it has occurred in the input. If there are more than one such words, print the lexicographically smallest one. The word should be printed in all lower case. Here a "word" is defined as a continuous sequence of alphanumerical characters separated by non-alphanumerical characters or the line beginning/end.

Note that words are case **insensitive**.

### Sample Input:

```in
Can1: "Can a can can a can?  It can!"
```

### Sample Output:

```out
can 5
```

### Code:

```c++
#include <iostream>
#include <map>
using namespace std;

int main() {
    map<string, int> mp;
    string s;
    getline(cin, s);
    for (int i = 0; i < s.length();) {
        int j = i;
        while (j < s.length() && isalnum(s[j]))
            j++;
        string ss = s.substr(i, j - i);
        for (int k = 0; k < ss.length(); k++) {
            if (ss[k] >= 'A' && ss[k] <= 'Z')
                ss[k] = ss[k] - 'A' + 'a';
        }
        i = j + 1;
        if (ss.length())//可能存在空串的情况，键不能为空，需要判断
            mp[ss]++;
    }
    int maxn = 0;
    string res;
    for (auto it = mp.begin(); it != mp.end(); it++) {
        if (it->second > maxn) {
            maxn = it->second;
            res = it->first;
        }
    }
    cout << res << " " << maxn;
    return 0;
}
```

