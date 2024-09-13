```cpp
#include <vector>

using namespace std;

class Solution {
public:
    vector<int> findThePrefixCommonArray(vector<int>& A, vector<int>& B) {
        vector<int> freq(A.size() + 1);
        vector<int> result(A.size()); // ОШИБКА !!!!
        int common = 0;
        
        for (int i = 0; i < static_cast<int>(A.size()); ++i) {
            int a_item = A.at(i);
            int b_item = B.at(i);
            
            ++freq.at(a_item);
            ++freq.at(b_item);
            
            if (a_item == b_item) {
                result.push_back(++common);
                continue;
            }
            
            if (freq.at(a_item) == 2) {
                ++common;
            }
            
            if(freq.at(b_item) == 2) {
                ++common;
            }
            
            result.push_back(common);
        }
        
        return result;
    }
};
```
### Описание ошибки
Создал вектор из A.size() нулей и вставляю резульаты в конец, нужно просто зарезирвировать A.size() элементов 