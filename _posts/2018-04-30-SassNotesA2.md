---
layout     : post
title      : "Sass 學習雜記 - A2. 顏色函式"
subtitle   : "Web Programming Notes"
date       : 2018-04-30 13:00:00
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

## Appendix 2. 顏色函式 (Color Functions)

> * A2.1 - RGB 顏色函式
> * A2.2 - HSL 顏色函式
> * A2.3 - 透明度調整
> * A2.4 - 其他顏色函式
> * A2.5 - 顏色運算

---
### A2.1 - RGB 顏色函式

* **`rgb($red, $green, $blue)`**：由紅、綠、藍建立一個十六進制的顏色碼。
    ```scss
    $color1: rgb(200, 40, 88);
    /* $color1: #c82858 */
    ```
* **`rgba($red, $green, $blue, $alpha)`**：由紅、綠、藍和透明度建立 RGBA 顏色。
    ```scss
    $color1: rgba(200, 40, 88, .65);
    /* $color1: rgba(200, 40, 88, .65) */
    ```
* **`rgba($color, $alpha)`**：由十六進制的顏色碼與透明度建立一個 RGBA 顏色。
    ```scss
    $color1: rgba(#c82858, .65);
    /* $color1: rgb(200, 40, 88, .65) */
    ```
* **`red($color)`**：由十六進制的顏色碼取出「紅色值」。
    ```scss
    $value: red(#c82858);
    /* $value: 200 */
    ```
* **`green($color)`**：由十六進制的顏色碼取出「綠色值」。
    ```scss
    $value: green(#c82858);
    /* $value: 40 */
    ```
* **`blue($color)`**：由十六進制的顏色碼取出「藍色值」。
    ```scss
    $value: blue(#c82858);
    /* $value: 88 */
    ```
* **`mix($color1, $color2, $proportion)`**：將 `$color1` 和 `$color2` 按照 `$proportion` 混合新的顏色。
    ```scss
    $color: mix(#c82858, rgba(200, 40, 80, .65), .3)
    /* $color: rgba(200, 40, 80, 0.65105) */
    ```

---
### A2.2 - HSL 顏色函式

* **`hsl($hue, $saturation, $lightness)`**：由色相 (hue)、飽和度 (saturation) 和亮度（lightness）的建立顏色。
    ```scss
    $color: hsl(200, 30%, 60%);
    /* $color: #7aa3b8 */
    ```
* **`hsla($hue, $saturation, $lightness, $alpha)`**：由色相、飽和度、亮度和透明度建立 RGBA 顏色。
    ```scss
    $color: hsl(200, 30%, 60%, .8);
    /* $color: rgba(122, 163, 184, .8) */
    ```
* **`hue($color)`**：由十六進制的顏色碼取出「色相值」。
    ```scss
    $value: hue(#7aa3b8);
    /* $value: 200 */
    ```
* **`saturation($color)`**：由十六進制的顏色碼取出「飽和度」。
    ```scss
    $value: saturation(#7aa3b8);
    /* $value: 30% */
    ```
* **`lightness($color)`**：由十六進制的顏色碼取出「亮度」。
    ```scss
    $value: saturation(#7aa3b8);
    /* $value: 60% */
    ```
* **`adjust-hue($color, $amount)`**：改變顏色的「色相值」並建立新的顏色。
    ```scss
    $color: adjust-hue(#ff3366, 150deg);
    /* $color: #33ff66 */
    ```
* **`lighten($color, $amount)`**：提高顏色的「亮度」並建立新的顏色。
    ```scss
    $color: lighten(#ff3366, 50%);
    /* $color: #ffffff */
    ```
* **`darken($color, $amount)`**：降低顏色的「亮度」並建立新點顏色。
    ```scss
    $color: darken(#ff3366, 50%);
    /* $color: #33000d */
    ```
* **`saturate($color, $amount)`**：提高顏色的「飽和度」並建立新點顏色。
    ```scss
    $color: saturate(#ff3366, 50%);
    /* $color: #ff3366 */
    ```
* **`desaturate($color, $amount)`**：降低顏色的「飽和度」並建立新點顏色。
    ```scss
    $color: desaturate(#ff3366, 50%);
    /* $color: #cc667f */
    ```
* **`grayscale($color)`**：建立 `$color` 的灰階色，相當於 `desaturate($color, 100%)`。
    ```scss
    $color: grayscale(#ff3366);
    /* $color: #999999 */
    ```
* **`complement($color)`**：建立 `$color` 的補色，相當於 `adjust-hue($color, 180deg)`。
    ```scss
    $color: complement(#ff3366);
    /* $color: #33ffcc */
    ```
* **`invert($color)`**：建立 `$color` 的反相色，即紅、綠、藍的值倒序，透明度不變。
    ```scss
    $color: invert(#ff3366);
    /* $color: 00cc99 */
    ```

---
### A2.3 - 透明度調整

* **`opacity($color)`** 或 **`alpha($color)`**：取出顏色的透明度。
    ```scss
    $value: opacity(red);
    /* $value: 1 */
    $value: alpha(red);
    /* $value: 1 */
    $value: opacity(rgba(red, .8));
    /* $value: 0.8 */
    $value: alpha(rgba(red, .8));
    /* $value: 0.8 */
    ```
* **`fade-out($color, $amount)`** 或 **`transparentize($color, $amount)`**：藉由數值 `0` 至 `1` 作爲 **減少透明度** 的表示方式。
    ```scss
    $color1: rgba(39, 39, 39, 0.5);
    $amount: 0.1;
    /* rgba(39, 39, 39, 0.4) */
    $color2: fade-out($color, $amount);
    ```
* **`fade-in($color, $amount)`** 或 **`opacify($color, $amount)`**：藉由數值 `0` 至 `1` 作爲 **增加透明度** 的表示方式。
    ```scss
    $color1: rgba(39, 39, 39, 0.5);
    $amount: 0.1;
    /* rgba(39, 39, 39, 0.6) */
    $color2: fade-in($color, $amount);
    ```

---
### A2.4 - 其他顏色函式

* **`adjust-color($color, [$red], [$green], [$blue], [$hue], [$saturation], [$lightness], [$alpha])`**：可以設置多個顏色參數，也可以同時不設置，並建立新的顏色。
    ```scss
    $color: adjust-color(hsl(25, 100%, 80%), $lightness: -30%, $alpha: -0.4);
    /* rgba(255, 106, 0, 0.6); */
    ```
* **`scale-color($color, [$red], [$green], [$blue], [$saturation], [$lightness], [$alpha])`**：語法和 `adjust-color` 相同，可以同時設置多個顏色參數，並建立新的顏色。
    ```scss
    $color: scale-color(hsl(200, 70%, 80%), $saturation: -90%, $alpha: -30%);
    /* $color: rgba(200, 205, 208, 0.7) */
    ```
* **`change-color($color, [$red], [$green], [$blue], [$hue], [$saturation], [$lightness], [$alpha])`**：改變顏色參數，並建立新的顏色。
    ```scss
    $color: change-color(hsl(25, 100%, 80%), $lightness: 40%, $alpha: 0.8);
    /* $color: rgba(204, 85, 0, 0.8) */
    ```

---
### A2.5 顏色運算

* 除了上述 Sass 所提供的函式，Sass 也支援數學函式提供數值上的計算結果。
    * 以下以 *顏色運算* 作爲說例。
        ```scss
        $color: #010203 + #040506;
        ```
    * 上述程式中，顏色運算將個別對 *紅色*，*綠色* 與 *藍色* 進行計算，因此將 *每二個數值爲一組* 分別計算，如下所示：
        ```scss
        01 + 04 = 05
        02 + 05 = 07
        03 + 06 = 09
        ```
    * 最後顏色計算結果如下所示：
        ```scss
        $color: #050709;
        ```
* Sass 同時支援 `rgba()`，`hsla()` 與字串表示 (如：`red` 或 `blue`) 的顏色計算。

> **補充**
> * [線上 Sass 顏色工具](http://jim-nielsen.com/sassme)

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