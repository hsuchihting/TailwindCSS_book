---
title: TailwindCSS 筆記 - 價目表卡片實戰 - 首頁標題樣式
tags:
  - TailwindCSS
categories: TailwindCSS
description: 首頁標題實戰練習
abbrlink: 1037863192
date: 2021-09-12 20:22:03
---

![title](https://i.imgur.com/sexi49o.png)

前面講了這麼多簡單的觀念與使用方法，接下來的幾篇都會是搭配 JIT 模式的實作練習，就來做一個簡易的價目表卡片吧！

## 建立專案架構

- 設定 `body` 背景色，使用自定義的方式來寫，`bg-[#colorCode]`。
- 在 `body` 的下層使用一個區塊元素定義整個標題的架構。
- 使用 `flex` 屬性包住標題與按鈕，使其橫向並排，用 `justify-between` 與 `item-start` 屬性使其兩個元素向上又左右對齊。
- 在 `1280px` 以上螢幕使用最大寬度為 `1280px`，原因是人眼的角度為 120 度，若頁面太寬，是不好瀏覽的。
- 並且 h1 的樣式給了一個 `letter spacing` 的屬性，讓標題文字寬度可以變寬，顯得更顯眼也好比較好閱讀。

```html
<body class=" bg-[#eee]">
  <div class="p-4 h-screen lg:p-8">
    <div class="flex justify-between items-start lg:max-w-[1280px] lg:mx-auto">
      <h1 class="text-gray-800 text-4xl tracking-wide">this is title</h1>
      <button>login</button>
    </div>
  </div>
</body>
```

這時就會得到以下結果，

![h1](https://i.imgur.com/Rj9zg83.png)

> 有發現到 `button` 在 TailwindCSS 樣式跟傳統 CSS 的樣式不太一樣，是沒有預設樣式的。

## 按鈕樣式

前面有提到 JIT 模式的好處，不需要看額外配置檔的預設樣式有哪些偽類或偽元素沒有新增，而是直接加上去就可以了。

除了最簡單的背景基本樣式以及 `active` 樣式外，這邊比較特別的是有加上一個 `duration` 的樣式，如果沒有 JIT 的話，前面要加上 `transition` 這個屬性，才會知道要用此樣式，但在 JIT 模式後，就會知道要使用 `transition` 這個效果，不需要另外寫。

```html
<button
  id="login"
  class=" bg-purple-500 text-white py-2 px-4 rounded-md hover:bg-purple-600 tracking-wide active:bg-purple-900 active:ring-2 duration-200"
>
  login
</button>
```

![button](https://i.imgur.com/gBuKlb5.png)
