---
layout     : post
title      : "最長共同子序列 (Longest Common Subsequence; LCS)"
subtitle   : "演算法筆記 Algorithm Notes"
date       : 2018-04-21 12:00:00
author     : "Yung-Sheng Lu"
tags       : Algorithm DynamicProgramming LCS
comments   : true
signature  : true
slides     : 
present    :
github     : 
link       : 
---

# 最長共同子序列 (Longest Common Subsequence; LCS)

* 在多個序列中，出現在每一個序列 (亦即：每個序列都有的值) 且長度最為最長，該共同序列稱為「最常共同子序列 (Longest Common Subsequence; LCS)」。以下為例：
    * $$S_1$$ 和 $$S_2$$ 為以下二個序列，試求最長共同子序列。
        $$
        \begin{equation}
        S_1 = [ 2, 5, 7, 9, 4, 1, 3 ]
        S_2 = [ 3, 5, 4, 5, 7 ]
        \mathrm{LCS}(S_1, S_2) = [ 5, 4, 3 ]
        \end{equation}
        $$
    * $$S_1$$、$$S_2$$ 和 $$S_3$$ 為以下三個序列，試求最長共同子序列。
        $$
        \begin{equation}
        S_1 = [ a, b, c, d, b, c, e, e, a, ]
        S_2 = [ c, a, b, d, e, f, g, a ]
        S_3 = [ d, c, e, a ]
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
        \[ \mathem{LCS}(S_1, S_2) =
        \begin{cases}
            \mathrm{max}( \mathrm{LCS}( \mathrm{sub}_1, S_2), \mathrm{LCS}(S_1, \mathrm{sub}_2) )       & \quad \text{if } n \text{ is even}\\
            \mathrm{LCS}(\mathrm{sub}_1, \mathrm{sub}_2) + e_1  & \quad \text{if } n \text{ is odd}
        \end{cases}
        \]
        \end{equation}
        $$