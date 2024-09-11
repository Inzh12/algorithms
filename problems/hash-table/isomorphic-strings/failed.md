```cpp
#include <unordered_map>
#include <string>

using namespace std;

class Solution {
public:
    bool isIsomorphic(string s, string t) {
        unordered_map<char, char> s_map;
        unordered_map<char, char> t_map;
        
        for (int i = 0; i < static_cast<int>(s.size()); ++i) {
            s_char = s.at(i);
            t_char = t.at(i);
            
            auto s_it = s_map.find(s_char);
            if (s_it != s_map.end()) {
                if (s_map.at(s_char) != t_char) {
                    return false;
                }
            } else {
                s_map.insert({s_char, t_char});
            }
            
            auto t_it = t_map.find(t_char);
            if (t_it != t_map.end()) {
                if (t_map.at(t_char) != s_char) {
                    return false;
                }
            } else {
                t_map.insert({t_char, s_char});
            }
        }
        
        return true;
    }
};
```
### Описание ошибки
Забыл тип данный у символов, ахахах, капец, до чего доводит питон.