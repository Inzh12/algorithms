```cpp
#include <vector>
#include <unordered_map>

using namespace std;

class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> map;
        vector<vector<int>> freqs(nums.size() + 1);
        vector<int> result;
        
        for (int num : nums) {
            ++map[num];
        }
        
        for (const auto& [k, v] : map) {
            freqs.at(v).push_back(k);
        }
        
        for (size_t i = freqs.size() - 1; i > 0; --i) {
            for (int num : freqs.at(i)) {
                result.push_back(num);
                if (result.size() == k) {
                    return result;
                }
            }
        }
        
        return result;
    }
};
```
### Оценка по времени: O(n)
### Оценка по памяти: O(n)
### Описание решения
- заполняем хэш-таблицу числами (ключи) и их частотой (значения)
- составляем из хэш-таблицы вектор векторов чисел, где индекс внешнего вектора - частота числа, а внутренние векторы - числа с соответствующей частотой
- проходимся циклом по внешнему вектору в обратном направлении и заполняем вектор результатов числами из внутренних векторов, пока размер вектора результатов не достигнет k
- возращаем результат