## Костыльный, но рабочий способ без написания собственного хэша для пары
```cpp
#include <vector>
#include <unordered_set>
#include <string>

using namespace std;

class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        unordered_set<string> rows;
        unordered_set<string> cols;
        unordered_set<string> blocks;
        
        for (int row = 0; row < 9; ++row) {
            for (int col = 0; col < 9; ++col) {
                char symbol = board[row][col];
                
                if (symbol == '.') {
                    continue;
                }
                
                int block = row / 3 * 3 + col / 3;
                
                string row_and_symbol = to_string(row) + symbol;
                if (rows.find(row_and_symbol) != rows.end()) {
                    return false;
                } else {
                    rows.insert(row_and_symbol);
                }
                
                string col_and_symbol = to_string(col) + symbol;
                if (cols.find(col_and_symbol) != cols.end()) {
                    return false;
                } else {
                    cols.insert(col_and_symbol);
                }
                
                string block_and_symbol = to_string(block) + symbol;
                if (blocks.find(block_and_symbol) != blocks.end()) {
                    return false;
                } else {
                    blocks.insert(block_and_symbol);
                }
            }
        }
        
        return true;
    }
};
```
## Метод с собственной хеш-функцией
```cpp
#include <vector>
#include <unordered_set>
#include <utility>

using namespace std;

class Solution {
private:
    struct pairHash {
        template <class T1, class T2>
        size_t operator()(const pair<T1, T2>& p) const {
            return hash<T1>()(p.first) ^ hash<T2>()(p.second);
        }
    };
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        unordered_set<pair<int, char>, pairHash> rows;
        unordered_set<pair<int, char>, pairHash> cols;
        unordered_set<pair<int, char>, pairHash> blocks;
		
        for (int row = 0; row < 9; ++row) {
            for (int col = 0; col < 9; ++col) {
                char symbol = board[row][col];
				
                if (symbol == '.') {
                    continue;
                }
				
                int block = row / 3 * 3 + col / 3;
				
                if (rows.find({row, symbol}) != rows.end()) {
                    return false;
                } else {
                    rows.insert({row, symbol});
                }
				
                if (cols.find({col, symbol}) != cols.end()) {
                    return false;
                } else {
                    cols.insert({col, symbol});
                }
				
                if (blocks.find({block, symbol}) != blocks.end()) {
                    return false;
                } else {
                    blocks.insert({block, symbol});
                }
            }
        }
		
        return true;
    }
};

```
### Оценка по времени: O(1)
### Оценка по памяти: O(1)
