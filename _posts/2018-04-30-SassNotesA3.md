---
layout     : post
title      : "Sass 學習雜記 - A3. 字串函式"
subtitle   : "Web Programming Notes"
date       : 2018-04-30 14:00:00
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

## Appendix 3. 字串函式 (String Functios)

> * A3.1 - 引號函式
> * A3.2 - 字串屬性函式
> * A3.3 - 字串操作函式
> * A3.4 - 字串大寫小寫函式

---
### A3.1 - 引號函式

* **`unquote($string)`**：刪除字串中「最外層」的引號 (不論單引號或雙引號)。
    ```scss
    $string1: 'Hello Sass!';
    $content: unquote($string1);
    /* $content: Hello Sass! */
    $string2: "Hello Sass!";
    $content: unquote($string2);
    /* $content: Hello Sass! */
    $string3: "'Hello Sass!'";
    $content: unquote($string3);
    /* $content: 'Hello Sass!' */
    $string4: '"Hello Sass!"';
    $content: unquote($string4);
    /* $content: "Hello Sass!" */
    $string5: Hello Sass!;
    $content: unquote($string5);
    /* $content: Hello Sass! */
    ```
* **`quote($string)`**：增加字串中的「雙引號」，如果字串本身帶有單引號，則直接帶換為雙引號。注意：如果字串中間有單引號或空格時，需要使用「單引號」或「雙引號」刮起來，否則會編譯錯誤。
    ```scss
    $string1: 'Hello Sass!';
    $content: quote($string1);
    /* $content: "Hello Sass!" */
    $string2: "Hello Sass!";
    $content: quote($string2);
    /* $content: "Hello Sass!" */
    $string3: Hello Sass!;
    $content: quote($string3);
    /* Compile error - $string3: ("Hello" "Sass!") is not a string for `quote') */
    $string4: ' ';
    $content: quote($string4);
    /* $content: " " */
    ```

---
### A3.2 - 字串屬性函式

* **`str-length($string)`**：回傳字串 `$string` 的長度。
    ```scss
    $string: "Hello Sass!";
    $length: str-length($string);
    /* $length: 11 */
    ```
* **`str-index($string, $substring)`**：回傳子字串 `$substring` 在 `$string` 中的起始索引值，注意：Sass/SCSS 中的字串索引值起始為 `1`。若子字串 `$substring` 不存在於 `$string` 中，則回傳 `null`。
    ```scss
    $string: "Hello Sass!";
    $substring: "Sass";
    $index: str-index($string, $substring);
    /* $index: 7 */
    ```

---
### A3.3 - 字串操作函式

* **`str-insert($string, $insert, $index)`**：將字串 `$insert` 插入字串 `$string` 中的第 `$index` 的位置。
    ```scss
    $string: "Hello";
    $insert: "Sass!";
    $result: str-insert($string, $insert, 1);
    /* $result: "Sass!Hello" */
    $result: str-insert($string, $insert, 6);
    /* $result: "HelloSass!" */
    ```
* **`str-slice($string, $start, $end)`**：擷取字串 `$string` 中，起始索引為 `$start` 至索引為 `$end` 的字串。其中，`$end` 不一定要給定 (`$end` 預設值：`1`)。
    * **`$start`**：起始的索引；若為「負值」，則是從「字串的結尾」開始起算。
    * **`$end`**：結束的索引；若為「負值」，則是從「字串的結尾」開始起算，預設值為 `1`。
    ```scss
    $string: "Hello Sass!";
    $result: str-slice($string, 7, 10);
    /* $result: "Sass" */
    $result: str-slice($string, 7);
    /* $result: "Sass!" */
    $result: str-slice($string, -5, -2);
    /* $result: "Sass" */
    $result: str-slice($string, 7, -1);
    /* $result: "Sass!" */
    ```

---
### A3.4 - 字串大寫小寫函式

* **`to-upper-case($string)`**：將字串 `$string` 全部轉換為「大寫」。
    ```scss
    $string: "hello sass!";
    $upper: to-upper-case($string);
    /* $upper: "HELLO SASS!" */
    ```
* **`to-lower-case($string)`**：將字串 `$string` 全部轉換為「小寫」。
    ```scss
    $string: "HELLO SASS!";
    $upper: to-lower-case($string);
    /* $upper: "hello sass!" */
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