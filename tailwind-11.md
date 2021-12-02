---
title: Tailwind CSS - 把重複使用的功能變成元件
tags:
  - TailwindCSS
categories: TailwindCSS
description: 把常用的樣式模組化
abbrlink: 2585108082
date: 2021-06-27 19:31:08
---
![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

Utility-first 固然方便，也是有缺點的，雖然免除了定義 class 名稱的困擾，但換來的是滿滿的樣式名稱，像是如果要做一張圖文卡片，就會變成這樣。

<iframe height="550" style="width: 100%;" scrolling="no" title="TailwindCSS card" src="https://codepen.io/hnzxewqw/embed/gOmNGVB?defaultTab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true"></iframe>

說實在要維護起來真的滿困難的，如果剛好接手的又對 TailwindCSS 不熟，那就會花費很多時間。

## 包裝成元件

雖然 Utility-first 的特性就是會有滿滿的樣式名稱，的確是令人詬病的，但 TailwindCSS 貼心的讓開發者可以對於重複使用的元件同一功能且可重複使用的方法。

例如：我今天開發了一個按鈕樣式

<iframe height="300" style="width: 100%;" scrolling="no" title="TailwindCSS button" src="https://codepen.io/hnzxewqw/embed/wvJLPBZ?defaultTab=html%2Cresult" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true"></iframe>

但一個網頁一定不只一顆按鈕，總不能每次做按鈕，都要打這麼多 class 吧? 就算是複製，也是會花滿多時間，而且可能貼錯。

### 使用 @apply 語法組成匯重複使用的 class

像這個按鈕可能會很多頁面都會用到，如果一開始接觸 TailwindCSS，光是要找按鈕在哪裡，就會花點時間，官方建議使用 `@layer` 圖層的屬性，去告訴框架，我是要在 component 的裡面去更新或覆寫預設樣式，再來可以把原本按鈕的樣式名稱用 `@apply` 包裝，寫在 TailwindCSS 預設的 `style.css` 裡面。

> 如果也是跟我一樣是平面設計轉職的朋友，相信用圖層的方式去理解應該滿快速的。

**style.css**

```css
/* ./your-css-folder/styles.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer components{
  .btn-green {
    @apply py-2 px-4 bg-green-500 text-white font-semibold rounded-lg shadow-md;
  }
  .btn-green:hover {
    @apply bg-green-700;
  }
  .btn-green:focus {
    @apply outline-none ring-2 ring-green-400 ring-opacity-75;
  }
}
```

再來把 HTML 的按鈕樣式改成包裝好的樣式名稱 `btn-green`，

**template**

```html
  <button class="btn-green">Click me</button>
```

完成後，進行編譯，編譯完後就可以出現效果。

如果還不放心，可以到 `tailwindcss.css` 檔案中找一下剛剛內容做重複的檢查，就會看到編譯過後的樣式囉！

**tailwindcss.css**

```css
.btn-green {
  --tw-bg-opacity: 1;
  background-color: rgba(16, 185, 129, var(--tw-bg-opacity));
  border-radius: 0.5rem;
  font-weight: 600;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  padding-left: 1rem;
  padding-right: 1rem;
  --tw-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  box-shadow: var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow);
  --tw-text-opacity: 1;
  color: rgba(255, 255, 255, var(--tw-text-opacity));
}

.btn-green:hover {
  --tw-bg-opacity: 1;
  background-color: rgba(4, 120, 87, var(--tw-bg-opacity));
}

.btn-green:focus {
  outline: 2px solid transparent;
  outline-offset: 2px;
  --tw-ring-offset-shadow: var(--tw-ring-inset) 0 0 0 var(--tw-ring-offset-width) var(--tw-ring-offset-color);
  --tw-ring-shadow: var(--tw-ring-inset) 0 0 0 calc(2px + var(--tw-ring-offset-width)) var(--tw-ring-color);
  box-shadow: var(--tw-ring-offset-shadow), var(--tw-ring-shadow), var(--tw-shadow, 0 0 #0000);
  --tw-ring-opacity: 1;
  --tw-ring-color: rgba(52, 211, 153, var(--tw-ring-opacity));
  --tw-ring-opacity: 0.75;
}
```

如此就可以完成跟上方寫的按鈕相同的樣式囉！

## 參考資料

* [TailwindCSS - Extracting Components](https://tailwindcss.com/docs/extracting-components)