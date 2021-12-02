---
title: TailwindCSS 筆記 - 切一個響應式留言按鈕畫面
tags:
  - TailwindCSS
categories: TailwindCSS
description: 小試身手，切一個響應式留言按鈕
abbrlink: 1511158673
date: 2021-09-08 21:35:18
---

![rwd button](https://i.imgur.com/WgHixfe.png)

前面了解基礎的使用後，來實戰一個簡單的留言按鈕與如何變成響應式的呈現。

## 基礎架構

- 有大頭照
- 有留言區按鈕

## 進行切版

1. 跟 Bootstrap 有點像，最外層使用 `.container` 訂調介面為滿版。
2. 制定灰色底色區塊，並且要符合整個頁面寬，使用 `.w-full` 語法，透過提示工具可以看到 `.w-full = width:100%`，為了要讓大頭照跟留言按鈕橫向呈現，在給予一個 `.flex` 語法。
3. 大頭照部分使用 [picsum](https://picsum.photos/) 的隨機圖片，並且設定外層有白框，使用 `.border-white .border-2` 兩個語法。
4. 按鈕部分使用 `.flex-1`，其作用是讓按鈕自適應縮放，不受初始大小影響。
5. 按鈕加上當有 hover 時，背景色可以變換，只要寫上 `hover:bg-gray-300` 就可以囉！

```html
<div class="container mx-auto mt-3">
  <h1 class="block text-gray-800 text-xl py-5 font-bold">寫一個留言按鈕</h1>
  <div class="w-full px-4 py-3 flex box-border rounded-lg bg-gray-400">
    <div
      class="w-12 mr-3 flex-shrink-0 rounded-full border-white border-2 overflow-hidden"
    >
      <img src="https://picsum.photos/200/200?random=1" alt="" />
    </div>
    <button class="flex-1 bg-gray-200 rounded-full hover:bg-gray-300">
      <p class="text-left pl-3 text-gray-600  text-md">在想些什麼...</p>
    </button>
  </div>
</div>
```

這樣就切完了，滿單純也簡單，而且可以快速的達到想要的效果。

## 加上自訂義的屬性

雖然 TailwindCSS 已經有預設一些樣式的狀態，但並不是每個都有支援，假設現在 PM 說：客戶想要在按鈕外面加上外框，並且要在點擊時出現。

這時候我就要去找 `variants` 預設中這個 `ringWidth` 的 Utility，然後發現初始設定並沒有 active 這個屬性。

```cmd
ringWidth: ['responsive', 'focus-within', 'focus'],
```

這時候就可以自行擴增其屬性，可以到 tailwind.config.js 中的 extends，加上這個屬性，

```javascript
module.exports = {
  purge: ["./**/*.html"],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {
      ringWidth: ["active"], //加在這裡
    },
  },
  plugins: [],
};
```

加好之後記得要重新編譯 TailwindCSS。

此時，就會看到我只有打 ac，就會出現對應的選項。

![active](https://i.imgur.com/XLlMqaq.png)

再來就只要加上 active 後，ring 的寬度即可。

```html
<button class="flex-1 bg-gray-200 rounded-full hover:bg-gray-300 active:ring-4">
  <p class="text-left pl-3 text-gray-600  text-md">在想些什麼...</p>
</button>
```

然後加好之後，在滑鼠點擊時，就會出現外框了。

![ring](https://i.imgur.com/fw4DY7X.png)

## 加上響應式

前面有提到 TailwindCSS 任何的 Utility 都可以加上響應式。假設我在不同斷點要呈現外框都是不同顏色，可以這樣寫

```html
<div class="container mx-auto mt-3">
  <h1 class="block text-gray-800 text-xl py-5 font-bold">寫一個留言按鈕</h1>
  <div
    class="w-full px-4 py-3 flex box-border rounded-lg bg-gray-400 sm:bg-red-400 md:bg-yellow-400 lg:bg-green-400 xl:bg-blue-400"
  >
    ...
  </div>
</div>
```

然後就會看到當解析度不同的時候會呈現不同的顏色。

### screen < sm(640px)

![phone](https://i.imgur.com/5To5HI2.png)

### screen > sm(640px)

![sm](https://i.imgur.com/D7bi6sy.png)

### screen > md(768px)

![md](https://i.imgur.com/u29R6Kt.png)

### screen > lg(1024px)

![lg](https://i.imgur.com/XQ8LVS6.png)

### screen > xl(1280px)

![xl](https://i.imgur.com/9vaScav.png)

寫到這邊完全沒有寫到任何一行 CSS，但卻可以實現樣式與響應式功能，真是非常棒呢！
