```cpp
#include <vector>
#include <algorithm>

using namespace std;

class Solution {
public:
    int hIndex(vector<int>& citations) {
        vector<int> count(citations.size() + 1);
        
        for (int num : citations) {
            ++count.at(min(num, static_cast<int>(citations.size())));
        }
        
        int cnt = 0;
        
        for (int i = static_cast<int>(count.size()) - 1; i >= 0; --i) {
            cnt += count.at(i);
            
            if (cnt >= i) {
                return i;
            }
        }
        
        return cnt;
    }
};
```
```cpp

```
### Оценка по времени: O(n)
### Оценка по памяти: O(n)
### Описание решения
