---
title: Tailwind CSS - 起手式
tags:
  - TailwindCSS
categories: TailwindCSS
description: 如何使用 Tailwind CSS
abbrlink: 3452359063
date: 2021-06-05 20:47:03
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

## 使用 CDN 載入 Tailwind CSS

如果想快速使用與把玩一下 Tailwind CSS，官方有提供一個 CDN，直接放到 `link` 就可以了。

```cmd
<link href="https://unpkg.com/tailwindcss@^2/dist/tailwind.min.css" rel="stylesheet">
```

但官方其實不太推薦這種用法，原因如下：

![use cdn](https://i.imgur.com/KarsOIk.png)

1. 不能自訂義 Tailwind 的預設主題。
2. 不能使用任何指令，像是 `@apply`，`@variants`...等。
3. 不能啟用其他的 variants，像是 `group-focus`。
4. 不能安裝第三方套件。
5. 不能 tree-shake 未使用到的樣式。

好的！官方都說五個不能了，如果只想匯入 CDN 這條路應該就僅限於不想客製化網站一途了，那這樣就失去使用 Tailwind 的意義。

## 安裝 Tailwind

[官方文件](https://tailwindcss.com/docs/installation)中在不能五大理由下方還有提到一句話：

![](https://i.imgur.com/lcHM6lM.png)

如果要使用更多 Tailwind，應該要安裝 PostCSS 套件。

### 使用 NPM 安裝

首先先進入開啟好專案的資料夾，然後點選右鍵開啟終端機，這時候會看到路徑已經在自己的資料夾中，

![terminal](https://i.imgur.com/2Q2M5z4.png)

官方教學使用 NPM 來安裝 Tailwind CSS、PostCSS，還有 autoprefixer 這三個檔案。

```cmd
npm install tailwindcss@latest postcss@latest autoprefixer@latest
```

**安裝原因：**

> Tailwind 不會自動加上瀏覽器前缀詞到產生的 CSS 中，所以瀏覽器無法讀取 CSS，要加上 autoprefixer 這個套件去處理此問題，所以一行指令就三個安裝玩了，輕鬆愉快。

還有提到一個錯誤，但是 v2.0 版本的 Tailwind 依賴於 PostCSS 8，若將 Tailwind 與舊版本的 PostCSS 混合使用，可能會看到以下跳錯訊息：

`Error: PostCSS plugin tailwindcss requires PostCSS 8.`

這時請安裝 [PostCSS 7](https://www.tailwindcss.cn/docs/installation#post-css-7) 版本，才能兼容。

**安裝 PostCSS 7**

```cmd
npm uninstall tailwindcss
npm install tailwindcss@npm:@tailwindcss/postcss7-compat
```

這時候打開 IDE，會看到目錄中有一個 `package.json` 檔案，就會看到剛剛裝好的三個套件。

**package.json**

```cmd
{
  "dependencies": {
    "autoprefixer": "^10.2.6",
    "postcss": "^8.3.0",
    "tailwindcss": "^2.1.4"
  }
}
```

## 建立 tailwindcss.config 檔案

因為我想要自訂義未來 Tailwind 的安裝內容，可以使用 Tailwind 工具生成一份配置文件，此命令工具已經包含在 tailwindcss 內。

在終端機輸入指令

```cmd
npx tailwindcss init
```

![tailwindcss init](https://i.imgur.com/WNHP5Zo.png)

安裝完成後就會看到有一個 tailwind.config.js 的檔案在目錄底下。

![menu](https://i.imgur.com/UXDIzZn.png)

點進檔案後就會看到預設的配置內容。

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

## 新增 Tailwind 到 CSS 中

在 VSCode 中新增一個 CSS 檔案，命名就如官方推薦的 `style.css`。(依照專案可自訂義此名字)

再把 Tailwind 的三個核心複製貼到剛剛新建的 CSS 檔案中。

```cmd
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### 不依賴 PostCSS 使用 Tailwind

雖然官方強力推薦要搭配 PostCSS，但因為還要去了解 PostCSS 沒有那麼容易，所以為了達到比較無障礙的使用，就不依賴 PostCSS 來使用，可以輸入下方指令，就可以將 Tailwind 編譯成瀏覽器看得懂的 CSS，完成後就可以直接使用 Tailwind 了！

```cmd
npx tailwindcss -i ./src/tailwind.css -o ./dist/tailwind.css
```

看到上方畫面就代表成功囉！

## 幫 CSS 瘦身

承上所示，Tailwind 因為是 Utility 的關係，會把整包檔案匯入，但我可能這次專案沒有用到這麼多的 Utility，如果整包檔案要選染於網頁，效能就會低落，Tailwind 官方文件很貼心也提供可以瘦身的方法，選到 `tailwind.config.js` 檔案，將我可能會使用到的內容寫在 `purge` 屬性內，就可以去監聽我哪支檔案有使用到，只會編譯使用的檔案，真的很貼心呢！

**tailwind.config.js**

```javascript
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
  plugins: [],
};
```

## 參考資料

- [Tailwind 官方文件](https://tailwindcss.com/docs/installation)
