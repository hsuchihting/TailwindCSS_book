---
title: Tailwind CSS - 如何在 Angular 中使用 TailwindCSS
tags:
  - TailwindCSS
  - Angular
categories: TailwindCSS
description: 在 Angular 使用 TailwindCSS 就是爽！
abbrlink: 3640682418
date: 2021-07-02 22:07:32
---

![TA](https://miro.medium.com/max/1400/1*5H42UPUpAiZZiKakeGVB8g.png)

## 安裝說明

### 安裝環境

- Angualr 11.2.6
- node.js v14.17.0

### 建立一個 Angular CLI

可以參考這一篇 [Angular 筆記 - Angular CLI 安裝與基本認識](https://hsuchihting.github.io/angular/20200818/419544592/)，這裡就不在說明。

### 安裝 TailwindCSS

輸入指令就會自動安裝 TailwindCSS 最新版本，PostCSS 以及 autoprefixer，詳細說明可以看[此篇](https://hsuchihting.github.io/TailwindCSS/20210605/3452359063/)或[中文版官方文件](https://tailwindcss.tw/docs/installation)。

```cmd
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
```

### 產生 TailwindCSS 配置檔

輸入指令：

```cmd
npx tailwindcss init
```

安裝完成就會看到跟目錄有一個 `tailwind.config.js` 的設定檔案，點開內容如下：

**tailwind.config.js**

```javascript
module.exports = {
  purge: [],
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

### 引入基礎樣式

#### CSS

如果是用 CSS 格式，引入的話要這樣，並且每次都要編譯。

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

編譯指令：

```cmde
npx tailwindcss build style.css -o tailwind.css
```

#### SCSS

如果是 SCSS 的話，引入要用 @import，因為有裝 PostCSS 所以不用每次都編譯。

```css
@import "tailwindcss/base";
@import "tailwindcss/components";
@import "tailwindcss/utilities";
```

## 移除不必要的樣式

因為 TailwindCSS 是 Utility-First，就是一大包檔案，為了避免有太多無用的樣式導致專案肥大，所以可以設定什麼檔案才要留樣式，像是 Angular 設定大概就是 `.html` 跟 `.scss` 以及 `.ts` 檔案了，在 purge 中設定如下：

**tailwind.config.js**

```javascript=
module.exports = {
  purge: {
    enabled: true,
    content: ["./src/**/*.html", "./src/**/*.scss"],
  },
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

## 安裝智能套件 Tailwind CSS IntelliSense

![tailwind plugin](https://i.imgur.com/gfdWdEz.png)

一定要安裝智能套件，[套件傳送門](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)，使用說明可參照[這裡](https://hsuchihting.github.io/TailwindCSS/20210607/2331513775/)。

## 智能套件故障排除

![stylelint](https://i.imgur.com/XLaC4n0.png)

要安裝 stylelint 智能套件故障排除的套件，因為 VSCode 看不懂 `@tailwindcss` 的標籤，並且要取消**工作區**的 CSS 與 SCSS Validate 的設定。

**CSS Validate**

![css validate](https://i.imgur.com/AZUoSmu.png)

**SCSS Validate**

![scss](https://i.imgur.com/OaojgS5.png)

最後在設定檔 `setting.json` 裡面貼上這一段

```cmd
{
  "stylelint.config": {
    "rules": {
      "at-rule-no-unknown": [true, {
        "ignoreAtRules": [
          "tailwind",
          "apply",
          "layer",
          "variants",
          "responsive",
          "screen"
        ]
      }],
      "declaration-block-trailing-semicolon": null,
      "no-descending-specificity": null
    }
  },
  "css.validate": false,
  "scss.validate": false
}
```

## 做一張簡單的圖文介紹卡片

<iframe height="700" style="width: 100%;" scrolling="no" title="TailwindCSS reponsive card" src="https://codepen.io/hnzxewqw/embed/OJmVpyE?defaultTab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true"></iframe>

## 在 Angular 使用 TailwindCSS JIT 模式

從 Angular12 有完整支援 TailwindCSS JIT 模式，所以專案若沒有向下兼容的需要，建議可以升級到 v.12 以上喔！

## 參考資料

- [Install Tailwind CSS in an Angular project](https://javascript.plainenglish.io/install-tailwind-css-in-an-angular-project-54a189b53db2)
- [安裝 IntelliSense 套件故障排除](https://ithelp.ithome.com.tw/articles/10243291)
- [TailwindCSS - Install](https://tailwindcss.tw/docs/installation)
- [Tailwind CSS with Angular V12- What You Need to Know](https://dev.to/bitovi/tailwind-css-with-angular-v12-what-you-need-to-know-2h9b)
