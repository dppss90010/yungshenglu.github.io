---
layout     : post
title      : "Sass 學習雜記 - A1. 數學函式"
subtitle   : "Web Programming Notes"
date       : 2018-04-30 12:00:00
author     : "Yung-Sheng Lu"
tags       : Sass WebProgramming
comments   : true
signature  : true
slides     : 
present    : 
github     :
link       :
---

![Sass](https://i.imgur.com/7vx71Hx.png)

## Appendix 1. 數學函式 (Math Functions)

> * A1.1 - 運算函式
> * A1.2 - 進位函式

---
### A1.1 - 運算函式

* **`percentage($value)`**：將一個「單位相同」的數值轉換為百分比。
    ```scss
    $value1: .2;
    $perc = percentage($value1);
    /* $perc: 20% */
    $value2: 2px / 10em;
    $perc = percentage($value2);
    /* Compile error - $value2: 0.2px/em is not a unitless number for `percentage' */
    $value3: 2em / 10em;
    $perc = percentage($value3);
    /* $perc: 20% */
    ```
* **`abs($value)`**：絕對值運算，若 `$value` 為數學式，則「單位要相同」。
    ```scss
    $value1: -10;
    $result: abs($value1);
    /* $result: 10 */
    $value2: -10px;
    $result: abs($value2);
    /* $result: 10px */
    $value3: -.6%;
    $result: abs($value3);
    /* $result: 0.6% */
    $value4: -1px / 2px;
    $result: abs($value4);
    /* $result: 0.5 */
    ```
* **`min($value1, $value2, ...)`**：由 `$value1`、`$value2`、...等「單位相同」的數字中找出最小值。
    ```scss
    $valueList1: 1, 2, 1%, 3, 300%;
    $minValue: min($valueList1);
    /* $minValue: 1% */
    $valueList2: 1px, 2, 3px;
    $minValue: min($valueList2);
    /* $minValue: 1px */
    $valueList3: 1px, 1em;
    $minValue: min($valueList3);
    /* Compile error - SyntaxError: Incompatible units: 'em' and 'px'. */
    $valueList4: 1em, 2em, 6em;
    $minValue: min($valueList4);
    /* $minValue: 1em */
    ```
* **`max($value1, $value2, ...)`**：由 `$value1`、`$value2`、...等「單位相同」的數字中找出最大值。
    ```scss
    $valueList1: 1, 6;
    $maxValue: min($valueList1);
    /* $maxValue: 6 */
    $valueList2: 1, 3px, 6%, 9;
    $maxValue: min($valueList2);
    /* Compile error - SyntaxError: Incompatible units: '%' and 'px'. */
    $valueList3: 1px, 6px;
    $maxValue: min($valueList3);
    /* $maxValue: 6px */
    ```
* **`random($value)`**：由 1 - `$value` 隨機產生一個數字，若無給定 `$value`，則預設為 `100`。
    ```scss
    $number: random() + px;
    /* $number: random a number from 1 to 100 with px as unit */
    $value: 300;
    $number: random($value) + px;
    /* $number: random a number from 1 to 300 with px as unit */
    ```

---
### A1.2 - 進位函式

* **`round($value)`**：四捨五入運算，若 `$value` 為數學式，則「單位要相同」。
    ```scss
    $value1: 12.3;
    $result: round($value1);
    /* $result: 12 */
    $value2: 14.9999;
    $result: round($value2);
    /* $result: 15 */
    $value3: 2.2%;
    $result: round($value3);
    /* $result: 2% */
    $value4: 3.9em;
    $result: round($value4);
    /* $result: 4em */
    $value5: 2px / 3px;
    $result: round($value5);
    /* $result: 1 */
    ```
* **`ceil($value)`**：無條件進位運算，若 `$value` 為數學式，則「單位要相同」。
    ```scss
    $value1: 12.3;
    $result: ceil($value1);
    /* $result: 13 */
    $value2: 14.1111;
    $result: ceil($value2);
    /* $result: 15 */
    $value3: 2.3%;
    $result: ceil($value3);
    /* $result: 3% */
    $value4: 3.5em;
    $result: ceil($value4);
    /* $result: 5em */
    $value5: 2px / 3px;
    $result: ceil($value5);
    /* $result: 1 */
    ```
* **`floor($value)`**：無條件捨去運算，若 `$value` 為數學式，則「單位要相同」。
    ```scss
    $value1: 12.8;
    $result: floor($value1);
    /* $result: 12 */
    $value2: 14.8888;
    $result: floor($value2);
    /* $result: 14 */
    $value3: 2.8%;
    $result: floor($value3);
    /* $result: 2% */
    $value4: 3.5em;
    $result: floor($value4);
    /* $result: 3em */
    $value5: 2px / 3px;
    $result: floor($value5);
    /* $result: 0 */
    ```

---
## 【Sass 學習雜記】系列

* [Sass 學習雜記 - Part 1. 簡介](https://yungshenglu.github.io/2017/12/19/SassNotes1/)
* [Sass 學習雜記 - Part 2. 變數表示](https://yungshenglu.github.io/2017/12/20/SassNotes2/)
* [Sass 學習雜記 - Part 3. 巢狀表示](https://yungshenglu.github.io/2017/12/21/SassNotes3/)
* [Sass 學習雜記 - Part 4. 組合表示](https://yungshenglu.github.io/2017/12/22/SassNotes4/)
* [Sass 學習雜記 - Part 5. 函式與運算](https://yungshenglu.github.io/2017/12/23/SassNotes5/)
* [Sass 學習雜記 - Part 6. 條件與迴圈](https://yungshenglu.github.io/2017/12/24/SassNotes6/)
* [Sass 學習雜記 - Part 7. 常見的編譯錯誤](https://yungshenglu.github.io/2017/12/24/SassNotes7/)
* [Sass 學習雜記 - Part 8. 開發架構與檔案切割](https://yungshenglu.github.io/2017/12/25/SassNotes8/)
* [Sass 學習雜記 - Part 9. 合併樣式](https://yungshenglu.github.io/2017/12/26/SassNotes9/)

> 如果你有任何建議與指教，歡迎於下方留言一起討論喔！