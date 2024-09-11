```cpp
#include <unordered_map>
#include <string>

using namespace std;

class Solution {
public:
    bool isIsomorphic(string s, string t) {
	    // ключ s-симовол, значение - t-символ
        unordered_map<char, char> s_map;

		// ключ t-симовол, значение - s-символ
        unordered_map<char, char> t_map;
        
        for (int i = 0; i < static_cast<int>(s.size()); ++i) {
            char s_char = s.at(i);
            char t_char = t.at(i);
            
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
### Оценка по времени: O(n)
### Оценка по памяти: O(1)
### Описание решения
- проходимся циклом по двум строкам одновременно
- если текущего символа нет в s-словаре, добавляем s-символ как ключ, а t-символ как значение, аналогично для t-словаря, только ключ и значение нужно поменять местами
- если текущий символ есть  в s-словаре, сравниваем значение по этому ключу с текущим t-символом, если они не равны возращаем false, аналогично для t-словаря
- если цикл успешно пройден возращаем true