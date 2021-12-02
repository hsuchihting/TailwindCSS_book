---
title: Tailwind CSS - 使用官方套件，以 typography 為例
tags:
  - TailwindCSS
categories: TailwindCSS
description: 懶得自己設定，那就用官方的吧！
abbrlink: 1327952700
date: 2021-06-29 23:52:09
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

除了可以把樣式元件化，功能模組化外，Tailwind 也提供自定義套件的方式給開發者使用，看個人習慣怎麼用，就怎麼用，不過我自己覺得是自定義套件比較會用在框架之中，如何使用就看個人囉！

## 自訂樣式套件起手式

自定義套件是寫在 `tailwind.config.js` 這支檔案中，並且要指定引入哪一個自定義套件，在 `plugins` 的陣列中使用函式來設定，函式用一個物件給與數個函式名稱，我自己常用的分別為：

- `addUtilities()`： 註冊新的功能樣式。
- `addComponents()`： 註冊新的元件樣式。
- `addBase()`： 註冊新的基本樣式。
- `addVariant()`： 註冊自定義變體。
- `theme()`： 找尋使用者在主題已配置的值。
- `variants()`： 找尋使用者在變體中已配置的值。

```javascript
const plugin = require("tailwindcss/plugin");

module.exports = {
  plugins: [
    plugin(function ({ addUtilities, addComponents, e, prefix, config }) {
      // Add your custom styles here
    }),
  ],
};
```

以上就針對我自己最近常用的幾個來做介紹。

## 使用官方套件

在介紹自定義套件之前，先介紹官方也有提供的套件與使用，官方文件表示：直接使用。只要在 `tailwind.config.js` 的 `plugins` 屬性中放入官方提供的套件，並且安裝其指令就可以使用。

## typography 排版

安裝指令：

```cmd
npm install @tailwindcss/typography
```

**tailwind.config.js**

```javascript
module.exports = {
  // ...
  plugins: [require("@tailwindcss/typography")],
};
```

**HTML**

使用時，要先輸入 `prose` 後面再繼續給 `prose-xl` 的樣式才吃得到喔！如下方所示，這個套件有支援響應式。

```html
<article class="prose sm:prose-xl">
  <h1>This is Title</h1>
  <p>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Impedit obcaecati
    temporibus delectus et eaque non enim, consequatur illum velit sapiente
    molestiae soluta voluptatibus omnis quasi dolores maxime officiis at vero!
  </p>
  <p>
    Lorem ipsum, dolor sit amet consectetur adipisicing elit. Aut dignissimos
    quasi pariatur nobis ipsa ullam! Commodi modi, saepe eveniet soluta numquam
    quasi ducimus, corrupti architecto distinctio dignissimos alias nesciunt
    doloribus?
  </p>
  <!-- ... -->
</article>
```

再打開瀏覽器就會看到套件設定的排版樣式。

![typography](https://i.imgur.com/OBIBMK2.png)

除了預設樣式外，也提供五種不同的排版樣式設定：

![prose](https://i.imgur.com/vAFQ1CV.png)

並且還提供七種顏色可以選擇，

![color](https://i.imgur.com/VkGRa2t.png)

## 自訂顏色與排版內容

官方提供一個範例，若想要自訂自己的排版內容，可以依照範本去設定自己喜歡的內容，兩種設定方式：

### extends 加入樣式

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      typography: {
        DEFAULT: {
          css: {
            color: "#333",
            a: {
              color: "#3182ce",
              "&:hover": {
                color: "#2c5282",
              },
            },
          },
        },
      },
    },
  },
  plugins: [
    require("@tailwindcss/typography"),
    // ...
  ],
};
```

### 包裝成函式

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      typography: (theme) => ({
        DEFAULT: {
          css: {
            color: theme("colors.gray.800"),

            // ...
          },
        },
      }),
    },
  },
  plugins: [
    require("@tailwindcss/typography"),
    // ...
  ],
};
```

還有更多設定方式可以參考[官方文件](https://github.com/tailwindlabs/tailwindcss-typography)，

其他官方套件如下：

- [Form](https://github.com/tailwindlabs/tailwindcss-forms)
- [Line-clamp](https://github.com/tailwindlabs/tailwindcss-line-clamp)
- [Aspect ratio](https://github.com/tailwindlabs/tailwindcss-aspect-ratio)

## 小結

透過使用官方套件知道一件事情，就是要先安裝套件，然後引入套件，並且可自行做設定。

## 參考資料

- [TailwindCSS - Plugins](https://tailwindcss.com/docs/plugins#official-plugins)
