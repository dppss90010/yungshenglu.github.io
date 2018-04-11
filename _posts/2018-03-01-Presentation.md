---
layout     : post
title      : "MUSIC and Improved MUSIC algorithm to Estimate Direction Arrival"
subtitle   : "Papers Study"
date       : 2018-03-01 18:00:00
author     : "Yung-Sheng Lu"
tags       : MUSIC Algorithm DOA
comments   : true
signature  : true
slides     : https://yungshenglu.github.io/slides/20180301_presentation.html
present    : https://slides.com/yungshenglu/20180301_presentation/live
github     :
link       :
---

> * Written by **Pooja Gupta, S. P. Kar**.
> * Publish in [IEEE ICCSP 2015](http://ieeexplore.ieee.org/document/7322593/)

## Abstract

MUSIC 演算法是一種基於 **矩陣特徵空間分解的方法**。從幾何角度講，訊號處理的觀測空間可以分解為訊號子空間和雜訊子空間，顯然這兩個空間是正交的。訊號子空間由陣列接收到的數據協方差 (covariance) 矩陣中與訊號對應的特徵向量組成，雜訊子空間則由協方差矩陣中所有最小特徵值（雜訊方差）對應的特徵向量組成。MUSIC 演算法就是利用這 **兩個互補空間之間的正交特性** 來估計空間訊號的方位。MUSIC 演算法大大提高了測向解析度，同時適應於 **任意形狀的天線陣列**，但是原型 MUSIC 演算法要求接收訊號是 **非相干性 (non-coherent)** 的，因此本篇論文將原本的 MUSIC 演算法進行改良，提出改良版本的 MUSIC 演算法，能處理接收訊號為 **相干性的訊號 (coherent signal)**。
