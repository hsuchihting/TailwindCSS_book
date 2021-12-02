---
title: TailwindCSS 筆記 - dark 深色模式
tags:
  - TailwindCSS
categories: TailwindCSS
description: 深色模式比你想得還要簡單！
abbrlink: 2562966958
date: 2021-09-08 22:46:31
---

![dark](https://images.unsplash.com/photo-1475070929565-c985b496cb9f?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80)

## 深色模式的原理

TailwindCSS 有趣的還有深色模式，可以透過 media 與 class 的方式啟動深色模式。
可以在配置檔 `tailwind.config.js` 中自行設定。

- media：讓裝置在深色模式的時候自動轉換。
- class：手動切換深色模式。

**tailwind.config.js**

```javascript
module.exports = {
  mode: "jit", //加在這裡
  purge: ["./**/*.html", "./src/**/*.css"],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {
      // ringWidth: ["active"], //加在這裡
    },
  },
  plugins: [],
};
```

裝置切換這邊就不需要特別說明，不管是電腦、平板或手機現在都能設定在某個時間就切換成深色模式。

這邊主要是介紹手動切換的練習。

## 起手式

首先先把深色模式設定成 class 的狀態。

**tailwind.config.js**

```javascript
module.exports = {
  mode: "jit",
  purge: ["./**/*.html", "./src/**/*.css"],
  darkMode: "class", //記得要是字串
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
};
```

## 實作背景切換深色模式

我這邊寫兩個按鈕，分別要去切換日間模式與夜間模式。

### Step 1 - 寫兩個按鈕

**HTML**

```html
<button
  id="light"
  class="px-4 py-2 rounded-full bg-white border-gray-400 border-2"
>
  日間模式 <i class="fas fa-sun text-yellow-500"></i>
</button>
<button
  id="dark"
  class="px-4 py-2 rounded-full bg-gray-700 border-gray-700 border-2 text-white"
>
  夜間模式<i class="fas fa-moon text-yellow-500"></i>
</button>
```

會得到下方畫面：

![button](https://i.imgur.com/6J1hQWP.png)

### Step 2 - 在 CSS 修改 base 的 body 樣式

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  body {
    @apply dark:bg-black;
  }
}
```

務必記得一定要在配置檔改成 class 或 media 狀態，不然 CSS 其實看不懂什麼是 `dark:bg-black` 的樣式。

### Step 3 - 寫入事件

引入 JS 於 `<body>` 之前，這應該不用贅述。

**HTML**

```html
<body>
  ...
  <script src="js/all.js"></script>
</body>
```

**JavaScript**

```javascript
let light = document.getElementById("light");
let dark = document.getElementById("dark");

light.addEventListener("click", function () {
  document.documentElement.classList.remove("dark");
});

dark.addEventListener("click", function () {
  document.documentElement.classList.add("dark");
});
```

我綁定兩個按鈕後，分別寫入在日間模式時就移除 `.dark` ，反之，在夜間模式就新增 `.dark` 啟動深色模式。

### 完成

**日間模式**

![light](https://i.imgur.com/DbIEBhT.png)

**夜間模式**

![dark](https://i.imgur.com/3GZQf2i.png)
