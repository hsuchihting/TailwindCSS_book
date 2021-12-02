---
title: Tailwind CSS - 選擇該框架的原因
tags:
  - TailwindCSS
categories: TailwindCSS
description: CSS 框架新選擇
abbrlink: 1705808851
date: 2021-06-05 20:45:00
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

## 什麼是 TailWind CSS

近年竄起的 CSS 框架，有別於老牌 Bootstrap、Material...等以元件構成的框架，是一套純粹以 Utility-First CSS，用許多的 class 就可以構成畫面，非常適合快速切版，並且因高彈性的關係，可以達到客製化的效果。

## 什麼是 Utility-First CSS

說到 Utility-First CSS，先回過頭介紹一般常見的 CSS framework，對於大家熟悉的 Bootstrap、Material UI...等，把 Component 都定義好，想要什麼元件就抓來用，湊起來就可以完成一個網站的 framework 不陌生。

要 navbar 或是 button，甚至 table 都可以完成，實在是非常方便。

不過，使用這些 framework 就會遇到一個問題，會聽到一些客戶說：「你的網站看起來好 Bootstrap 喔！」這就算了，因為已經定義好元件的內容，要客製化的話，後續會遇到維護的麻煩與困擾。

### 使用元件框架會遇到哪些麻煩與困擾

#### 最不好的方式：覆蓋 CSS

因原本的定義好的框架比較沒有客製化的方式，或是有些網路上找到的套件很難去客製成自己的想要的樣式，只好用各種覆蓋的方式去改動 CSS，如果沒事就沒事，改完後續又要修改，就還需要花很多時間去找原本框架或套件定義的 CSS 寫在哪裡。但這種方式很容易把東西改壞。

#### 下載定義好的程式碼

有些框架有提供自訂義的彈性，可以把相對的地方修改後再把程式碼下載下來，一開始看起來會覺得這樣也很好耶！可是，當以後這個專案交給其他人接手，甚至是完全沒碰過這個專案的同事時，可能會發現同事怎麼改個程式碼，拳頭越來越硬了呢? 因為根本不知道哪些地方被改動了。

#### 引入後再覆寫 Sass

這是比較好的情況，可以引入框架的 Sass，但又覆寫部分的 Sass 變數，可以調整設定，也比較不容易造成後續管理以及維護的問題，Bootstrap 就是這樣。可是，如果框架已經把 UI 都定義好了，可以調整的範圍就會受到不少限制。

## 小結

回過頭來說，使用 Utility-First CSS 的時候，因是使用 class 建構出來的畫面，所以要更動相對容易與方便，因為每個元件都是自己刻出來的，哪裡不滿意、不符需求，都可以在 Utility class 增減中完成，是相當具有彈性的。

## 參考資料

- [還在跟複雜的 CSS 的設定奮鬥嗎？用 Tailwind 來幫你實現真正的高效整潔！](https://5xruby.tw/posts/tailwind-css-plugin)
- [Tailwind CSS 官網](https://tailwindcss.com/)
