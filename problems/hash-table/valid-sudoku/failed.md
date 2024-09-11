## Попытка 1
```cpp
#include <vector>
#include <unordered_set>
#include <utility>

using namespace std;

class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        unordered_set<pair<int, char>> rows;
        unordered_set<pair<int, char>> cols;
        unordered_set<pair<int, char>> blocks;
        
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
### Описание ошибки
std::hash не определён для std::pair