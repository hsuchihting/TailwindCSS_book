---
title: TailwindCSS 筆記 - 價目表卡片實戰 - 進階卡片樣式
tags:
  - TailwindCSS
categories: TailwindCSS
description: 卡片互動效果、RWD 顯示、使用 JavaScript 迴圈產生列表內容
abbrlink: 854832424
date: 2021-09-13 22:50:34
---

![card](https://i.imgur.com/nxwdr4q.png)

前篇已經將基本的卡片樣式完成，要繼續完成幾個互動效果，會有以下內容：

1. 滑鼠經過卡片會有放大效果。
2. RWD 效果，PC 版卡片為三欄。
3. 透過 JS 迴圈方式產生新的卡片。

## 增加 hover 的互動效果

在卡片外層加上以下 class，卡片的程式碼可以參考上一篇內容。
因為我要在滑鼠過時卡片有放大效果，所以要使用 hover，並且使用 transition 屬性底下的 scale 縮放效果，這邊選擇 110，也就是 110%，並且加上效果時間，這樣就完成了。

```html
<div class="hover:scale-110 duration-300 ">...card code...</div>
```

原本樣式：可以看到左右有明顯間距。

![before hover](https://i.imgur.com/huPXw2D.png)

滑鼠經過後：間距變小了。

![hover card](https://i.imgur.com/8Oszqzw.png)

## RWD 三欄效果

TailwindCSS 是單一斷點的手機優先 CSS 框架，所以一開始建構就是手機版，而今天要在 PC 版本實呈現三欄的內容，這時就要在卡片的最外層加上 lg 的尺寸來定義各種 RWD 的效果樣式。

也就是這邊要往後加上 PC 版樣式的內容。

```html
<div class="mt-8">... card code...</div>
```

加上以下 class，前面都要加上 lg 的尺寸樣式喔！

```html
<div
  class="mt-8 lg:grid lg:grid-cols-3 lg:justify-evenly lg:gap-8 lg:w-[1280px] lg:mx-auto"
></div>
```

- grid：值得一提的是這個 class，也就是使用網格系統，透過官網介紹可以透過網格系統的方式直接定義樣式，省去計算的時間。這邊是使用 [Grid Template Columns](https://tailwindcss.com/docs/grid-template-columns) 的樣式去定義三欄效果。

用法很簡單，官方文件示範如下：

![grid](https://i.imgur.com/iPTBB41.png)

使用這個語法 `grid-cols-{n}`，放入想要分幾欄即可，非常簡單且易懂。

> 前面要先定義 grid 的樣式才能使用。

- justify-evenly：讓卡片等距。
- gap-8：間隔有 2rem。

![gap](https://i.imgur.com/Z7a0GPi.png)

最後限制寬度為 1280px，並且置中對齊。

## 透過 JS 迴圈來跑出複數卡片

這次透過一個簡單的迴圈方式來渲染可用內容的列表內容，因正式卡片的內容可能數量有多有少，如果少的話做苦工就算了，但如果資料量很大，就不是手工可以解決的事情。

### 引入 js 檔案

這應該不用在贅述。

```html
<body>
  ...code...
  <script src="js/all.js"></script>
</body>
```

**js**

建立一個函式，並且先預設呼叫有三個參數，分別是列表一到三，

```javascript
function renderList() {}

renderList("list1");
renderList("list2");
renderList("list3");
```

此時也在 template 的 `ul` 上各加上 `id`，分別為 `list1`， `list2` 和 `list3`。

**html**

```html
<ul id="list1" class="...">
  ...
</ul>
```

### 再把要執行的內容寫在函式內

1. 因執行函式已經有指定其參數，而這個參數為 id 的值，故透過 getElementById 的方式接收參數。
2. 再用一個變數來存模板語法，就是把 li 的內容複製到這裡來。
3. 最後再用迴圈組字串。

```javascript
function renderList(id) {
  const listUl = document.getElementById(id);
  const templateLi = `
      <li class="flex items-center mt-4">
        <i class="far fa-check-circle text-green-400"></i>
         <span
             class=" pl-3 text-gray-800 tracking-wide">免費使用</span>
      </li>
  `;

  let str = "";
  for (let i = 0; i < 5; i++) {
    str = str + templateLi;
  }
  listUl.innerHTML = str;
}

renderList("list1");
renderList("list2");
renderList("list3");
```

### 在配置檔加上 js 路徑

因為有寫模板語法在 js 檔案裡，所以要記得加上 js 檔案在配置檔。

**tailwind.config.js**

```javascript
module.exports = {
  mode: "jit",
  purge: ["./**/*.html", "./src/**/*.css", "./js/**/*.js"], //要加上 JS 的路徑
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
};
```

![render](https://i.imgur.com/UqGmrau.png)

這樣就可以跑出列表了。

### 加入判斷微調畫面

但有發現背景為紫色的卡片中的列表文字是黑色的，這樣看不清楚，所以要加一個判斷讓其變成白色，可以加在模板語法上方。

```javascript
function renderList(id) {
  const listUl = document.getElementById(id);
  let originColor = "text-green-400";
  if (id === "list2") {
    originColor = "text-white";
  }
  const templateLi = `
      <li class="flex items-center mt-4">
        <i class="far fa-check-circle ${originColor}"></i>
         <span
             class=" pl-3 ${originColor} tracking-wide">免費使用</span>
      </li>
  `;

  let str = "";
  for (let i = 0; i < 5; i++) {
    str = str + templateLi;
  }
  listUl.innerHTML = str;
}
```

- 設定一個變數存取原本的顏色。
- 在寫入判斷當 `id` 等於 `list2` 的時候，顏色就改變為白色。
- 透過模板語法中帶變數的方式 `${param}` 的方式帶入原本顏色的位置。

這樣就完成透過判斷來改變列表內容的文字囉！

![js](https://i.imgur.com/yDstLla.png)
