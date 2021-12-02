---
title: Tailwind CSS - 自訂 addBase 套件
tags:
  - TailwindCSS
categories: TailwindCSS
description: 打造屬於自己的基底樣式！
abbrlink: 1430341820
date: 2021-06-29 23:55:16
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

### 修改基底樣式 addBase

專案會使用到很多的標題樣式，在不同的頁面都會出現，那我就可以訂一個套件專門給標題使用。
此時就可以使用修改基底樣式的函式 `addBase()` 做修改，參照起手式的方式，我給三個標題不同的字體大小。

```javascript
const plugin = require("tailwindcss/plugin");

module.exports = {
  purge: {
    enabled: true,
    content: ["./*.html"],
  },
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [
    plugin(function ({ addBase, theme }) {
      addBase({
        h1: { fontSize: theme("fontSize.2xl") },
        h2: { fontSize: theme("fontSize.xl") },
        h3: { fontSize: theme("fontSize.lg") },
      });
    }),
  ],
};
```

在 `plugin` 的函式中帶入第一個參數是使用的方法，第二個參數是要修改的是什麼，我這邊要更換的是 `theme` 裡面的字體大小。

值得注意的地方是，要使用小數點作為連接，不是用連接符號（dash）喔！

重新編譯後可以得到下方結果。

![fontChange](https://i.imgur.com/zy7Y6s3.png)

打開開發人員工具可以看到，透過套件我已經把預設值改掉了。

**h1**

![h1](https://i.imgur.com/rCpQoOu.png)

**h2**

![h2](https://i.imgur.com/6GuL7Ph.png)

**h3**

![h3](https://i.imgur.com/yIyXxXb.png)

## 參考資料

- [TailwindCSS - Adding base styles](https://tailwindcss.com/docs/plugins#adding-base-styles)
