---
title: Tailwind CSS - 增加 Base 樣式
tags:
  - TailwindCSS
categories: TailwindCSS
description: 客製化自己的樣式
abbrlink: 1455247132
date: 2021-06-14 16:15:29
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

## 什麼是 Base 樣式

概念有點像是 CSSreset，現在網頁基本上都會使用 CSS reset，有寫過網頁一段時間都不陌生，而 Tailwind 有提供一組基底樣式，稱為 [Preflight](https://tailwindcss.tw/docs/preflight)，基本上就是採用 [modern-normalize](https://github.com/sindresorhus/modern-normalize) 啦！

以前一開始學網頁是用 [CSS reset](https://meyerweb.com/eric/tools/css/reset/) ，後來就都用 [Nomalize](https://necolas.github.io/normalize.css/) 了。

> 延伸閱讀：[Day21：小事之 CSS Reset 與 CSS normalize](https://ithelp.ithome.com.tw/articles/10196528)。

然後官網有說到基底預設樣式為 [box-sizing-reset](https://www.paulirish.com/2012/box-sizing-border-box-ftw/)，為什麼特別提這個呢？

因為預設其實是 `box-sizing:content-box`，那 `border-box` 跟 `content-box` 的差別是什麼?

簡單來說，`border-box` 就是我指定的寬度或高度是多少，網頁就會呈現該數值，但如果是 `content-box` 就會另外加上 border(邊框) 的寬度，結果跟預期的結果不同。

從範例可以看到兩者不同的在尺寸上不同的變化。

<iframe height="265" style="width: 100%;" scrolling="no" title="Tailwind base" src="https://codepen.io/hnzxewqw/embed/dyvgrbO?height=265&theme-id=light&default-tab=css,result" ></iframe>

Tailwind 跟 Bootstrap 5 都有加上這個屬性。

## 覆蓋原本 base 的設定

在一開始安裝 Tailwind 的時候有一個主要的 CSS 檔案 `style.css`，裡面會放 Tailwind 三個基本設定內容

**style.css**

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

如果專案的需求是改變 h1 的預設大小，那可以把要改變的內容直接寫在 `style.css` 這隻檔案內，然後使用 `@layer base`，再把要更改的屬性與值寫在裡面。如下方範例：

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  h1 {
    @apply text-6xl text-red-500 my-5;
  }
}
```

這段意思是，我使用 `@layer` 圖層的語法，把 base 的 `h1` 樣式改掉，並且使用 `@apply` 允許修改整個 `h1` 的內容， `@apply` 有點像是把想要的樣式合併起來，類似拆模組的概念。

下圖為原本的 `h1` 樣式，

![origin](https://i.imgur.com/poFwTnK.png)

此圖為修改後的樣式，改變樣式後記得要重新編譯。

![change](https://i.imgur.com/EXHx13W.png)

## 覆蓋預設文字樣式

跟覆蓋 base 樣式的方法一樣，專案需求如果要覆蓋樣式，官網也提供範例可以參考，而覆蓋字體是使用 `@font-face` 語法，並把相關內容寫在其中。

**style.css**

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  h1 {
    @apply text-6xl text-red-500 my-5;
  }
  @font-face {
    font-family: Proxima Nova;
    font-weight: 400;
    src: url(/fonts/proxima-nova/400-regular.woff) format("woff");
  }
  @font-face {
    font-family: Proxima Nova;
    font-weight: 500;
    src: url(/fonts/proxima-nova/500-medium.woff) format("woff");
  }
}
```

如此我就新增了一種字型的粗細度。

## 使用套件新增字型

官方也提供了另一種方法，如同之前響應式一樣，可以直接寫在 `tailwind.config.js` 裡面，當作套件來新增。

如果要自訂義套件使用，要使用 `addBase` 這個方法，才能做使用喔！並且所有有使用 `addBase` 產生的樣式，都會被加到 `base` 的樣式中。下方範例就是將自訂義 `h1`~`h3` 字體大小。

使用方法：

- 在 plugins 的陣列中加上套件的方法，此範例稱作 `plugin()`，此名稱可自訂義。
- 裡面使用一個函式，並給予一個物件，兩個屬性， `addBase`,`theme`。
- 函式裡面需用 `addBase()` 這個方法，並且塞入物件，此物件就是要修改的文字屬性內容。

**tailwind.config.js**

```javascript
//引入剛剛新增的字型 plugin
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

完成後，就設定好文字的套件囉！

## 參考資料

- [Tailwind CSS - Adding Base Styles](https://tailwindcss.com/docs/adding-base-styles)
- [【Tailwind CSS 教學 - 6】我知道你懂 CSS Reset，但你懂 base 全站樣式設定嗎？](https://ithelp.ithome.com.tw/articles/10244972)
