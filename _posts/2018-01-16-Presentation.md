---
layout     : post
title      : "Steering with Eyes Closed: mm-Wave Beam Steering without In-Band Measurement"
subtitle   : "Papers Study"
date       : 2018-01-16 12:00:00
author     : "Yung-Sheng Lu"
tags       : mmWave Beamforming
comments   : true
signature  : true
slides     : https://yungshenglu.github.io/slides/20180116_presentation.html
present    : https://slides.com/yungshenglu/20180116_presentation/live
github     :
link       :
---

> * Written by **Thomas Nitsche, Adriana B. Flores, Edward W. Knightly, and Joerg Widmer**.
> * Publish in [IEEE INFOCOMM 2015](http://ieeexplore.ieee.org/document/7218630/)

## Abstract

由於 mm-Wave 在傳遞的過程中衰減很快，所以目前在 mm-Wave 通訊是透過高度有向性的波束行程 (beamforming) 技術來增強訊號強度，以達到 multi-Gbps 的傳輸量，能克服傳輸過程中的 Pathloss 並能達到理想的訊號雜訊比 (SNR)。
但是，在建立通訊過程中，為了達到足夠窄的波束寬度 (beamwidth) 會相對需要一定的連結分析 (link budget)，而這些連結分析取決於天線之間搜尋波束的範圍大小，可能伴隨著使用裝置的移動性，還有傳送者與接收者之間波束解析 (beam resolution)，因此會產生相當大的成本。所以本篇論文提出一套架構 Blind Beam Steering (BBS) 來減少大量的成本。