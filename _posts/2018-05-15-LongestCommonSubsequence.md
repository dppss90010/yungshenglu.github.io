---
layout     : post
title      : "最長共同子序列 (Longest Common Subsequence; LCS) - Part 1"
subtitle   : "演算法筆記 Algorithm Notes"
date       : 2018-05-15 12:00:00
author     : "Yung-Sheng Lu"
tags       : Algorithm DynamicProgramming LCS
comments   : true
signature  : true
slides     : 
present    :
github     : 
link       : 
---

## Longest Common Subsequence (LCS)

* 在多個序列中，出現在每一個序列 (亦即：每個序列都有的值) 且長度最為最長，該共同序列稱為「最常共同子序列 (Longest Common Subsequence; LCS)」。以下為例：
    * $$S_1$$ 和 $$S_2$$ 為以下二個序列，試求最長共同子序列。
        $$
        \begin{equation}
        S_1 = [ 2, 5, 7, 9, 4, 1, 3 ]\\
        S_2 = [ 3, 5, 4, 5, 7 ]\\
        \mathrm{LCS}(S_1, S_2) = [ 5, 4, 3 ]
        \end{equation}
        $$
    * $$S_1$$、$$S_2$$ 和 $$S_3$$ 為以下三個序列，試求最長共同子序列。
        $$
        \begin{equation}
        S_1 = [ a, b, c, d, b, c, e, e, a, ]\\
        S_2 = [ c, a, b, d, e, f, g, a ]\\
        S_3 = [ d, c, e, a ]\\
        \mathrm{LCS}(S_1, S_2, S_3) = { [ c, e, a ], [ d, e, a ] }
        \end{equation}
        $$
* 求解*一群數列*的「最長共同子序列 (Longest Common Subsequce; LCS)」為 NP-hard 問題，沒有快速的演算法。罪簡單的方式是「窮舉法」：窮舉 $$S_1$$ 的所有子序列，檢查 $$S_2$$，...，$$S_n$$ 是否都有該子序列。
    * 時間複雜度 (Time complexity)：$$O(s_1! \cdot (s_2 + ... + s_n))$$。
    * 求解*二個序列*的「最長共同子序列」為 P 問題。以下將介紹各種演算法。

---
## Longest Common Subsequence (LCS): Dynamic Programming

* 分割問題 (Partition)
    * 假設有二個序列為 $$S_1$$ 和 $$S_2$$，其「最長共同子序列 (LCS)」表示為：$$\mathrm{LCS}(S_1, S_2)$$。
    * 序列 $$S_1$$ 和 $$S_2$$ 的最後一個元素分別以 $$e_1$$ 與 $$e_2$$ 表示，剩餘部分以 $$\mathrm{sub}_1$$ 與 $$\mathrm{sub}_2$$ 表示，故可以將序列 $$S_1$$ 與 $$S_2$$ 表示如下：
        $$
        \begin{equation}
        S_1 = \mathrm{sub}_1 + e_1
        S_2 = \mathrm{sub}_2 + e_2
        \end{equation}
        $$
    * 由以上的二個式子，可以將 $$S_1$$ 與 $$S_2$$ 的「最長共同子序列 (LCS)」分為以下四種情形討論：
        1. LCS 包含 $$e_1$$ 但不含 $$e_2$$。
            此種情形對於 $$e_2$$ 沒有用處，若要找到 LCS 只需找 $$\mathrm{sub}_2$$ 即可。
            $$
            \begin{equation}
            \mathrm{LCS}(S_1, S_2) = \mathrm{LCS}(S_1, \mathrm{sub}_2)
            \end{equation}
            $$
        2. LCS 包含 $$e_2$$ 但不含 $$e_1$$。
            此種情形對於 $$e_1$$ 沒有用處，若要找到 LCS 只需找 $$\mathrm{sub}_1$$ 即可。
            $$
            \begin{equation}
            \mathrm{LCS}(S_1, S_2) = \mathrm{LCS}(\mathrm{sub}_1, S_2)
            \end{equation}
            $$
        3. LCS 不含 $$e_1$$ 且不含 $$e_2$$。
            此種情形對於 $$e_1$$ 與 $$e_2$$ 沒有用處，若要找到 LCS 需找到 $$\mathrm{sub}_1$$ 與 $$\mathrm{sub}_2$$。
            $$
            \begin{equation}
            \mathrm{LCS}(S_1, S_2) = \mathrm{LCS}(\mathrm{sub}_1, \mathrm{sub}_2)
            \end{equation}
            $$
        4. LCS 包含 $$e_1$$ 且包含 $$e_2$$。
            此種情形同時包含 $$e_1$$ 與 $$e_2$$ 且 $$e_1$$ 與 $$e_2$$ 都是二個序列的最後一個元素，故 LCS 的最後一個元素必定為 $$e_1$$ (同時也是 $$e_2$$)>
            $$
            \begin{equation}
            \mathrm{LCS}(S_1, S_2) = \mathrm{LCS}(\mathrm{sub}_1, \mathrm{sub}_2) + 1
            \end{equation}
            $$
    * 上述四種情形可以簡化為以下遞迴式：
        $$
        \begin{equation}
        \[ \mathrm{LCS}(S_1, S_2) =
        \begin{cases}
            \mathrm{max}( \mathrm{LCS}( \mathrm{sub}_1, S_2), \mathrm{LCS}(S_1, \mathrm{sub}_2) )       & \quad \text{if } n \text{ is even}\\
            \mathrm{LCS}(\mathrm{sub}_1, \mathrm{sub}_2) + e_1  & \quad \text{if } n \text{ is odd}
        \end{cases}
        \]
        \end{equation}
        $$
        * 當 $$s_1$$ 或 $$s_2$$ 為空集合，則 LCS 亦為空集合。
* 計算 Longest Common Subsequence (LCS) 的長度
    * `length[i][j]`：「 $$s_1$$ 前 $$i$$ 個元素」和「 $$s_2$$ 前 $$j$$ 個元素」的 LCS 長度。
    ~~~ cpp
    int s1[7] = {2, 5, 7, 9, 3, 1, 2};
    int s2[5] = {3, 5, 3, 2, 8};
    int length[8][6];

    void findLCS() {
        // Initialize
        for (int i = 0; i <= 7; ++i)
            length[i][0] = 0;
        for (int j = 0; j <= 5; ++j)
            length[0][j] = 0;
        
        // Start
        for (int i = 1; i <= 7; ++i) {
            for (int j = 1; j <= 7; ++j) {
                if (s1[i - 1] == s2[j - 1])
                    length[i][j] = length[i - 1][j - 1] + 1;
                else
                    length[i][j] = max(length[i - 1][j], length[i][j - 1]);
            }
        }

        // Print the result
        printf("LCS length: %d\n", length[7][5]);
    }
    ~~~

* 找出一個 Longest Common Subsequence (LCS)
    * `LCS[i][j]`：記錄每一格的結果是從哪一格而來。
    * 當某一格 `length[i][j]` 是由 `length[i-1][j-1] + 1` 而來，就印出 `s1[i]` （也是 `s2[j]`）。
    ~~~ cpp
    int s1[7] = {2, 5, 7, 9, 3, 1, 2};
    int s2[5] = {3, 5, 3, 2, 8};
    int length[8][6];
    int seq[5]

    void findLCS() {
        // Initialize
        for (int i = 0; i <= 7; ++i)
            length[i][0] = 0;
        for (int j = 0; j <= 5; ++j)
            length[0][j] = 0;
        
        // Start
        for (int i = 1; i <= 7; ++i) {
            for (int j = 1; j <= 7; ++j) {
                if (s1[i - 1] == s2[j - 1]) {
                    length[i][j] = length[i - 1][j - 1] + 1;
                    // LCS from the left-top
                    LCS[i][j] = 0
                }
                else {
                    length[i][j] = max(length[i - 1][j], length[i][j - 1]);
                    if (length[i - 1][j] < length[i][j - 1]) {
                        length[i][j] = length[i][j - 1];
                        // LCS from the left
                        LCS[i][j] = 1;
                    }
                    else {
                        length[i][j] = length[i - 1][j];
                        // LCS from the top
                        LCS[i][j] = 2;
                    }
                }
            }
        }

        // Print the result
        printf("LCS length: %d\n", length[7][5]);
        printf("LCS: ");
        printLCS(7, 5);
    }

    /* Loop version */
    void printLCS(int i, int j) {
        int len = length[i][j];

        while (len > 0) {
            if (LCS[i][j] == 0) {
                --len;
                seq[len] = s1[i];
            }
            else if (LCS[i][j] == 1)
                --j
            else
                --i;
        }

        len = length[i][j];
        for (int l = 0; l < len; ++l)
            printf("%d ", seq[l]);
    }

    /* Recursive version */
    void printLCS(int i, int j) {
        // End of null set
        if (i == 0 || j == 0)
            return;
        
        if (LCS[i][j] == 0) {
            printLCS(i - 1, j - 1);
            printf("%d ", s1[i]);
        }
        else if (LCS[i][j] == 1)
            printLCS(i, j - 1);
        else
            printLCS(i - 1, j);
    }
    ~~~

* 如何「找出所有的 Longest Common Subsequence (LCS)」？
    * 某一格的答案可以由上方、左方、左上方同時求得，因此可以將這些情形全部記錄下來。
    * 往回追溯的時候，可將所有情形追溯一遍，便可求出所有可能的 LCS。
    * 目前似乎無法在「線性時間內」找出所有的 LCS。
* 節省記憶體空間
    * 如果只想求出 LCS 的長度，而不需要求出 LCS：填陣列時，只需要填上方、左方、左上方的格子。
    * 計算順序：由左到右、再由上到下，陣列可以精簡成一行，然後暫存左上方的格子的值。

---
## Practice

* **Online Judge UVa**
    * UVa-111 - History Sorting
    * UVa-531 - Compromise
    * [UVa-10066 - The Twin Towers](https://yungshenglu.github.io/2018/04/21/UVA10066/)
    * UVa-10192 - Vacation
    * UVa-10405 - Longest Common Subsequence
    * UVa-10723 - Cyborg Genes