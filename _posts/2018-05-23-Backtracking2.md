---
layout     : post
title      : "回溯法 (Backtracking) - Part 2"
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

## 2.1 - Enumerate Permutations

* 所謂的「排列 (permutations)」是指將某集合內的數字，按照某些特定的順序列出。舉例來說：$${1, 2, 3}$$ 的所有排列情形有 $${1, 2, 3}$$、$${1, 3, 2}$$、$${2, 1, 3}$$、$${2, 3, 1}$$、$${3, 1, 2}$$、$${3, 2, 1}$$。
* 使用**回溯法**模擬「排列 (permutations) 的所有情形」，並以「字典順序」排序。以下範例為枚舉 $${0, 1, 2, 3}$$ 所有排列情形。

    ```cpp
    // 存放一組可能的答案
    int solution[4];
    // 記錄數字是否使用過
    bool isUsed[4];

    void backtracking(int n) {
        // Bound
        if (n == 5) {
            for (int i = 0; i < 4; ++i)
                printf("%d ", solution[i]);
            printf("\n");

            return 0;
        }

        for (int i = 0; i < 4; ++i) {
            if (!isUsed[i]) {
                isUsed[i] = true;

                solution[n] = i;
                backtracking(n + 1);

                isUsed[i] = false;
            }
        }
    }

    void enumerate_permutations() {
        for (int i = 0; i < 4; ++i)
            isUsed[i] = false;
        backtracking(0);
    }
    ```

* **字母排序問題**：以下為枚舉 $${a, b, c}$$ 的所有排列情形。

    ```cpp
    // 字串必須預先由小到大排序
    char alpha[3] = { 'a', 'b', 'c' };
    // 存放一組可能的答案
    char solution[3];
    // 記錄該字母是否使用過
    bool isUsed[3];
    
    void backtracking(int n, int N) {
        // Bound
        if (n == N) {
            for (int i = 0; i < N; ++i)
                printf("%c ", solution[i]);
            printf("\n");
            return;
        }
    
        // 枚舉所有字母，並各自遞迴。
        for (int i = 0; i < N; ++i) {
            if (!isUsed[i]) {
                isUsed[i] = true;
                // 填入字母
                solution[n] = alpha[i];
                backtracking(n + 1, N);

                isUsed[i] = false;
            }
        }
    }
    
    void enumerate_permutations() {
        for (int i = 0; i < 3; ++i)
            isUsed[i] = false;
    
        backtracking(0, 3);
    }
    ```

    * 在字母排序問題中，最常遇到就是當字母重複的時候，使用原本的回溯法會出現相同的排序情形。為了避免重複排列，在枚舉某一個位置的字母時，要避免重複填入相同的字母。
    * 如果將輸入的字串**「由小到大」**排序，字母會依照順序出現，相同的字母會相鄰出現，所以只需檢查「是否與上一步填入的字母相同」，即可避免填入相同的字母。

        ```cpp
        // 字串必須預先由小到大排序
        char alpha[3] = {'a', 'b', 'b'};
        char solution[3];
        bool isUsed[3];
        
        void backtracking(int n, int N) {
            // Bound
            if (n == N) {
                for (int i = 0; i < N; ++i)
                    printf("%c ", solution[i]);
                printf("\n");
                return;
            }
        
            char last_letter = '\0';
            for (int i = 0; i < N; ++i) {
                if (isUsed[i])
                    continue;

                // 避免枚舉一樣的字母
                if (s[i] == last_letter)
                    continue;
        
                // 記錄上一步使用過的字母
                last_letter = alpha[i];
                isUsed[i] = true;
        
                solution[n] = alpha[i];
                backtracking(n + 1, N);
        
                isUsed[i] = false;
            }
        }
        ```
    
    * 當字母**「重覆出現次數很多次」**，可以使用一個 $$128$$ 格的陣列，每一格分別存入每一個 ASCII 字元的出現次數，以簡化程式碼。

        ```cpp
        char alpha[3] = {'a', 'b', 'b'};
        char solution[3];
        // 分別紀錄每個 ASCII 字元的出現次數
        int ASCII[128];
        
        void backtracking(int n, int N) {
            if (n == N) {
                for (int i = 0; i < N; ++i)
                    printf("%c ", solution[i]);
                printf("\n");
                return;
            }
        
            // 枚舉每一個字母
            for (int i = 0; i < 128; ++i) {
                if (array[i] > 0) {
                    // 用掉一個字母
                    --array[i];
        
                    solution[n] = i;
                    backtracking(n + 1, N);
        
                    // 回收一個字母
                    ++array[i];
                }
            }
        }
        
        void enumerate_permutations() {
            for (int i = 0; i < 3; ++i)
                ASCII[i] = 0;

            // 統計每個字母出現的次數
            for (int i = 0; i < 3; ++i)
                ++ASCII[alpha[i]];
        
            backtracking(0, 3);
        }
        ```

---
## 2.2 - Enumerate Combinations

* 所謂的「組合 (combinations)」是指從某集合內的所有數字中，任意選取某些數字所形成的一個新集合。舉例來說：$${1, 2, 3}$$ 的所有組合情形有 $${ }$$、$${ 1 }$$、$${ 2 }$$、$${ 3 }$$、$${ 1, 2 }$$、$${ 1, 3 }$$、$${ 2, 3 }$$、$${ 1, 2, 3 }$$。
* 使用**回溯法**模擬「組合 (combinations) 的所有情形」
    * 以 $${0, 1, 2, 3, 4}$$ 為例，所有組合情形共 $$2^5$$ 種。以我們平常計數的概念，每個數字都是「取或不取」兩種情形，根據「乘法原理」，總共 $$2 \times 2 \times 2 \times 2 \times 2 = 2^5$$ 種情形。
    * 枚舉方式可以仿照「乘法原理」。建立一個陣列作為一個集合，以「布林值」表示該集合中「是否擁有該索引值元素」。觀念等同使用「Set 資料結構」進行索引存取 (indexed access)。
    * 因此在枚舉所有「組合」的情形時，我們只要依序針對每個位置，考慮「取或不取」兩種情形即可。

        ```cpp
        bool solution[5];
        
        void backtracking(int n) {
            // Bound
            if (n == 5) {
                for (int i = 0; i < 5; ++i) {
                    if (solution[i])
                        printf("%d ", i);
                }
                printf("\n");
                return;
            }
        
            // 選取數字 n 枚舉之後的位置。
            solution[n] = true;
            backtracking(n + 1);
        
            // 不取數字 n 枚舉之後的位置。
            solution[n] = false;
            backtracking(n + 1);
        }
        
        void enumerate_combinations() {
            backtracking(0);
        }
        ```

    * 除了使用「Set 資料結構」進行索引存取，亦可改為「循序存取 (sequential access)」

        ```cpp
        int subset[5];
 
        void backtracking(int n, int size) {
            // Bound
            if (n == 5) {
                for (int i = 0; i < size; ++i)
                    printf("%d ", subset[i]);
                printf("\n");
                return;
            }
        
            // 選取數字 n 枚舉剩下的數字。
            subset[size] = n;
            backtracking(n + 1, size + 1);
        
            // 不取數字 n 枚舉剩下的數字。
            backtracking(n + 1, size);
        }
        
        void enumerate_combinations() {
            backtracking(0, 0);
        }
        ```
    
* **範例：**枚舉 $${0, 1, 2, 3, 4}$$ 的所有組合情形。

    ```cpp
    bool solution[5];
 
    void backtracking1(int n) {
        // Bound
        for (int i = 0; i < 5; ++i)
            if (solution[i])
                printf("%d ", i);
        printf("\n");
    
        for (; n < 5; ++n) {
            // 選取數字 n
            solution[n] = true;
    
            // 枚舉後面的數字
            backtracking(n + 1);
    
            // 放回數字 n
            solution[n] = false;
        }
    }

    void backtracking2(int n, int size) {
        // Bound
        for (int i = 0; i < size; ++i)
            printf("%d ", subset[i]);
        printf("\n");
    
        for (; n < 5; ++n) {
            // 選取數字 n
            subset[size] = n;
    
            // 枚舉後面的數字
            backtracking2(n + 1, size + 1);
    
            // 不必放回數字 n，因為會覆蓋
        }
    }
    
    void enumerate_combinations() {
        backtracking1(0);
        backtracking2(0, 0);
    }
    ```

    * 若預先將數字**「由小至大」**排序，則回溯法的結果會按照「字典順序」排列。

---
## 2.3 - Enumerate Subset Sums

* 所謂的「子集和 (subset sums)」是指將某集合中的子集內所有元素的總和。舉例來說：$${1, 2, 8}$$ 的所有子集和情形有 $$0$$、$$1$$、$$2$$、$$8$$、$$1 + 2$$、$$1 + 8$$、$$2 + 8$$、$$1 + 2 + 8$$。直觀來說，可以枚舉所有子集，再分別求總和，最後排序完即是答案。
* 使用**回溯法**模擬「子集和 (subset sums) 的所有情形」
    * 使用具有「即時排序」特性的資料結構 (如：優先權佇列 (priority queue))，調整回溯法的枚舉順序。
    * 每個數字都是**「取」和「不取」**兩種選擇，放入資料結構中，由資料結構決定下一個枚舉的對象。
    * 為了簡單起見，假設數字都是正數。

    ```cpp
    const int N = 5;
    const int K = 6;
    int array[N] = {2, 4, 6, 7, 9};
    
    typedef struct pair {
        int n;
        int num;
    } Pair;
    
    bool operator<(Pair a, Pair b) {
        return a.num > b.num;
    }
    
    void enumerate_subsetsums() {
        printf("0");
    
        // 預先補入一個數，稍後再扣除回來。
        priority_queue<Pair> pq;
        pq.push({ 0, array[0] });
    
        for (int k = 1; k < K; ++k) {
            if (pq.empty()) break;
            int n = pq.top().n;
            int num = pq.top().num;
            pq.pop();
    
            printf("%d ", num);
    
            if (n + 1 < N) {
                // 取
                pq.push({ n + 1, num + array[n + 1] });
                // 不取
                pq.push({ n + 1, num - array[n] + array[n + 1] });
            }
        }
    }
    ```

---
## Practice

* **Online Judge UVa**
    * UVa-195 - Anagram
    * UVa-441 - Lotto
    * UVa-10063 - Knuth's Permutation
    * UVa-10098 - Generating Fast
    * UVa-10776 - Determine The Combination