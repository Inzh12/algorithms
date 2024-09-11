```cpp
#include <vector>
#include <unordered_map>
#include <iostream>

using namespace std;

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> answer;
        
        // ключ - число из вектора, занчение - индекс числа в векторе
        unordered_map<int, int> used;

        for (int index = 0; index < static_cast<int>(nums.size()); ++index) {
            int current_num = nums.at(index);
            auto possible_summand_it = used.find(target - current_num);

            if (possible_summand_it != used.end()) {
                answer.push_back(possible_summand_it->second);
                answer.push_back(index);

                return answer;
            } else {
                used.insert({current_num, index});
            }
        }

        return answer;
    }
};
```
### Оценка по времени: O(n)
### Оценка по памяти: O(n)
### Описание решения
Заполяем хеш-таблицу числами (ключи) и их индексами в векторе (значения) пока не найдём число, которое в сумме с предидущим числом даёт целевую сумму. Проверка существования такого предидущего чила выполяется поиском нужного ключа (целевая сумма минус текущее число) в хеш-таблице.
