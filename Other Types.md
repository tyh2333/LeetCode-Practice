# Other Types:



#### [189. Rotate Array](https://leetcode-cn.com/problems/rotate-array/)

Given an array, rotate the array to the right by `k` steps, where `k` is non-negative.

**Example 1:**

```
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        reverse(nums.begin(), nums.end() - k % nums.size());
        reverse(nums.end() - k % nums.size(), nums.end());
        reverse(nums.begin(), nums.end());
    }
};
```



#### [73. Set Matrix Zeroes](https://leetcode-cn.com/problems/set-matrix-zeroes/)

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s, and return *the matrix*.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```



```c++
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        bool rowFlag = false;
        // (1) check if the first row or first col should be set to 0
        for (int i = 0; i < matrix[0].size(); i++) {
            // the first row should be set to 0:
            if (matrix[0][i] == 0) {
                rowFlag = true;
                break;
            }
        }
        bool colFlag = false;
        for (int i = 0; i < matrix.size(); i++) {
            // the second col should be set to 0:
            if (matrix[i][0] == 0) {
                colFlag = true;
                break;
            }
        }
        // (2) modify first row and first col by checking 0s:

        for (int i = 1; i < matrix.size(); i++) {
            for (int j = 1; j < matrix[0].size(); j++) {
                // if [i][j] is 0: set the [i][0] and [0][j] to 0; 
                if (matrix[i][j] == 0){
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        // (3) set 0s:
        // check 0s in the first row then set all according column:
        for (int i = 1; i < matrix[0].size(); i++) {
            if (matrix[0][i] == 0) {
                for (int j = 0; j < matrix.size(); j++) {
                    matrix[j][i] = 0;
                }
            }
        }
        // check 0s in the first col then set all according row:
        for (int i = 1; i < matrix.size(); i++) {
            if (matrix[i][0] == 0) {
                for (int j = 0; j < matrix[0].size(); j++) {
                    matrix[i][j] = 0;
                }
            }
        }
        // (4) deal with the first row and col:
        if (rowFlag){
            for (int i = 0; i < matrix[0].size(); i++) {
                matrix[0][i] = 0;
            }
        }
        if (colFlag){
            for (int i = 0; i < matrix.size(); i++) {
                matrix[i][0] = 0;
            }
        }
    }
};
```

