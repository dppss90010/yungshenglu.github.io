---
layout     : post
title      : "回溯法 (Backtracking) - Part 1"
subtitle   : "演算法筆記 Algorithm Notes"
date       : 2018-05-23 12:00:00
author     : "Yung-Sheng Lu"
tags       : Algorithm Backtracking
comments   : true
signature  : true
slides     : 
present    :
github     : 
link       : 
---

## 1.1 - Backtracking

* **回溯法 (Backtracking)** 是枚舉多維度數值的方法。使用**遞迴**的方式，依序窮舉各個維度的數值，並運算出所有可能的多維度數值，且在遞迴途中避免枚舉錯誤的多維度數值。以下為範例程式：

    ```cpp
    // Define a array for multi-dimensional value
    int solution[MAX_DIMENSION];
    
    void backtracking(int dimension) {
        /* Prune：在遞迴途中避免枚舉不正確的多維度數值 */
        if (solution[] will not be an answer)
            return;
    
        /* 使用多維度數值，並檢驗正不正確 */
        if (dimension == MAX_DIMENSION) {
            check and record solution[];
            return;
        }
    
        /* 窮舉這個維度的所有數值，並遞迴到下一個維度 */
        for (x = possible value of current dimension) {
            solution[dimension] = x;
            backtracking(dimension + 1);
        }
    }
    
    int main(void) {
        // 從第一個維度開始枚舉
        backtracking(0);
    }
    ```

* 當多維度數值只需要「唯一一組」，可以讓回溯法提早結束。以下為範例程式：

    ```cpp
    int solution[MAX_DIMENSION];
    // 隨時記錄是否已經找到正解
    bool find_answer = false;

    void backtracking(int dimension) {
        if (dimension == MAX_DIMENSION) {
            check and record solution;
            // 找到正解
            find_answer = true;
            return;
        }

        for (x = possible value of current dimension) {
            solution[dimension] = x;
            backtracking(dimension + 1);
            // 提早結束，跳出遞迴
            if (find_answer) 
                return;
        }
    }
    ```

* 評估多維度數值的優劣：隨時剔除劣的、保留優的。以下為範例程式：

    ```cpp
    int solution[MAX_DIMENSION];
    bool find_answer = false;
    // 代表多維度數值的優劣
    int best_cost;
    
    void backtracking(int dimension) {
        /* Bound：多維度數值太糟，不可能成為正解，可不必遞迴 */
        // 計算多維度數值的優劣
        int cost = cost of solution[];
        if (cost is far away from best_cost)
            return;
    
        if (dimension == MAX_DIMENSION) {
            check and record solution[];
    
            /* Bound：多維度數值太糟，不可能成為正解，可不必遞迴 */
            best_cost = cost;   // 記錄當前最佳結果
            if (cost is enough good)
                find_answer = true;
    
            return;
        }
    
        for (x = possible value of current dimension) {
            solution[dimension] = x;
            backtracking(dimension + 1);
            // 提早結束，跳出遞迴
            if (find_answer) return;
        }
    }
    ```

* **回溯法**的特色是隨時避免枚舉不正確的數值。一旦發現數值不正確，就不需要往下一層遞迴，而回溯至上一層，**可以節省時間**。此外，還可以調整維度先後順序，或是一個維度裡面的枚舉順序。如果安排得宜，可以更快找到正確的多維度數值。

---
## 1.2 - Enumerate Tuples

* 所謂的序對 (tuple)，其實就是**多維度的數值**。舉例來說：由 $$1$$、$$2$$、$$3$$ 所構成的序對有：$${1, 1, 1}$$、$${1, 1, 2}$$、$${1, 1, 3}$$、$${1, 2, 1}$$、......、$${3, 3, 3}$$。以下範例為枚舉「數字 $$1$$ 到 $$5$$ 選擇三次」全部可能的情形。
    * 使用一個陣列來存放所有可能的情形。陣列中不同的格子，即是不同的維度。

        ```cpp
        int solution[3];
        ```

    * 如果 `solution[0] = 4` 表示第一個抓到的數字是 $$4$$ ， `solution[2] = 1` 表示第二個抓到的數字是 $$1$$。

        ```cpp
        int solution[3];

        void backtracking(int n) {
            // Bound
            if (n == 3) {
                for (int i = 0; i < 3; ++i)
                    printf("%d ", solution[i]);
                printf("\n");
                return;
            }

            // 逐步枚舉數字 1 到 5，並且遞迴下去，枚舉之後的維度。
            for (int i = 1; i <= 5; ++i) {
                solution[n] = i;
                backtracking(n + 1);
            }
        }

        void enumerate_tuples() {
            backtracking(0);
        }
        ```

---
## Practice

* **Online Judge UVa**
    * UVa-129
    * UVa-140
    * UVa-165
    * UVa-193
    * UVa-222
    * UVa-259
    * UVa-291
    * UVa-301
    * UVa-331
    * UVa-399
    * UVa-435
    * UVa-524
    * UVa-539
    * UVa-565
    * UVa-574
    * UVa-598
    * UVa-628
    * UVa-656
    * UVa-732
    * UVa-10160
    * UVa-10186
    * UVa-10344
    * UVa-10364
    * UVa-10400
    * UVa-10419
    * UVa-10477
    * UVa-10501
    * UVa-10503
    * UVa-10513
    * UVa-10582
    * UVa-10605
    * UVa-10624
    * UVa-10637
    * UVa-10802