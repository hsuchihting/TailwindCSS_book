---
title: Tailwind CSS - 讓 Variants 成為偽類的強大神器
tags:
  - TailwindCSS
categories: TailwindCSS
description: 彈性超高的 Variants 設定
abbrlink: 2922303441
date: 2021-06-22 23:31:01
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

除了 [Tailwind CSS - 設定自己想要的 TailwindCSS 樣式 Variant](https://hsuchihting.github.io/TailwindCSS/20210620/961026179/) 提到可以自訂 `hover` 在想要的樣式裡外，此框架的作者還很貼心的寫了一個效果， [Group-hover](https://tailwindcss.com/docs/hover-focus-and-other-states#group-hover)

## Group-hover

在介紹 Group-hover 前，先講一下，如果是傳統寫 CSS 的話是什麼狀況。

先給個情境，規格書來個需求說：

1. 要有張卡片。
2. 滑鼠經過時，卡片背景色與卡片標題要變色。

所以傳統的 CSS 就會變成：

<iframe height="300" style="width: 100%;" scrolling="no" title="tradition CSS" src="https://codepen.io/hnzxewqw/embed/bGqyORr?height=265&theme-id=light&default-tab=html,result"></iframe>

當然對於切版熟手或許這個沒什麼問題，但還是回到原本的困擾，要想命名，要分層去寫效果進去，如果今天拆分元件，可能也無法所有的樣式都共用。

如果遇到會有群組型的 `hover` 樣式，透過 TailwindCSS 可以這樣寫：

```html
<div
  class="
      group
      px-6
      py-5
      w-72
      rounded
      space-y-1
      bg-gray-200
      hover:bg-yellow-200
      "
>
  <div
    class="
      text-2xl text-gray-700
      group-hover:text-blue-800 group-hover:text-4xl
      "
  >
    Card Title
  </div>
  <p>
    Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quisquam
    repellendus error, qui natus ea quas, aut, ipsa illo cupiditate corrupti in
    quaerat enim. Iusto, impedit? Est saepe ratione dolorum officiis?
  </p>
</div>
```

只要加上想要呈現的 class，一行 CSS 都不用寫，而且也不用想命名，真是太方便了！

但是發現一件事情，為什麼改用 TailwindCSS 寫完後文字不會再 hover 的時候改變樣式呢?

<iframe height="265" style="width: 100%;" scrolling="no" title="TailwindCSS-card" src="https://codepen.io/hnzxewqw/embed/LYWoMgp?height=265&theme-id=light&default-tab=html,result"></iframe>

原因是預設設定檔，沒有加入 `group-hover` 的樣式，所以要手動加入，在 `tailwindcss.config.js` 設定檔更新如下：

**tailwindcss.config.js**

```cmd
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
        extend: {
            borderStyle: ["responsive", "hover"],
            fontSize: ['responsive',"group-hover"], //加入 group-hover
        },
    },
    plugins: [],
};
```

**hover**

![hover](https://i.imgur.com/P1juNTL.png)

> 因為 CodePen 無法載入 `tailwind.config.js` 的內容，所以要在本地端時做才會有效果喔！

## 還有更多偽類變體可以使用

除了 `Group-hover` 外，還有其他效果，可以看 [Tailwind CSS - 偽類變體 Pseudo-Class Variants](https://hsuchihting.github.io/TailwindCSS/20210614/1717980556/) 有介紹與響應式的合體技喔！

## 客製化自己的 Variants

如果覺得每次要去改預設設定檔很麻煩，那就自己弄一個專屬此案件的 `variants` 吧！

首先我想設定一個香蕉的 `variants` 來用，就在一開始預設的 `style.css` 檔案中加入我要的樣式。

![style](https://i.imgur.com/p3VDp97.png)

記得儲存加編譯，我知道你也忘記了，編譯指令如下：

```cmd
npx tailwindcss -i ./src/tailwind.css -o ./dist/tailwind.css
```

編譯結束後怎麼知道有沒有成功？

這時就可以到編譯後的 `tailwind.css` 搜尋 `banana`，然後就會看到自定義的 `banana` 樣式出現在裡面囉！

![banana](https://i.imgur.com/SIZB6AI.png)

寫到這邊真的覺得 TailwindCSS 真的很便利於開發呢！

## 參考資料

- [【Tailwind CSS 教學 - 9】強大 Variant 讓你寫 CSS 偽元素不卡卡](https://ithelp.ithome.com.tw/articles/10246237)
- [TailwindCSS - Group-hover](https://tailwindcss.com/docs/hover-focus-and-other-states#group-hover)
