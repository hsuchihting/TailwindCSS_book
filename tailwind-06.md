---
title: Tailwind CSS - 手機到桌上螢幕，所有的元素都能自適應
tags:
  - TailwindCSS
categories: TailwindCSS
description: 通通給我 RWD 起來！
abbrlink: 1338142949
date: 2021-06-12 22:03:50
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

跟 Bootstrap 一樣也是手機優先的響應式斷點設計，官方文件也提供尺寸對照：

![rwd](https://i.imgur.com/R0sWHIH.png)

讓前端在開發輕鬆在 HTML 上寫斷點，不用特別去 CSS 撰寫了。

## 直觀又好懂的斷點寫法

我可以透過 `斷點:條件` 的方式來撰寫斷點，例如：

```html
<img class="w-16 md:w-32 lg:w-48" src="..." />
```

這一段是表示：

- 手機圖片寬度為 `16px`
- 平板圖片寬度為 `32px`
- 桌機圖片寬度為 `48px`

<iframe height="265" style="width: 100%;" scrolling="no" title="Tailwind breakpoint" src="https://codepen.io/hnzxewqw/embed/XWMPEZp?height=265&theme-id=light&default-tab=html,result" ></iframe>

官方推薦是從小到大的斷點依序撰寫，好讀又直觀，當然想要隨意換順序也可以，但為了以後維護，還是有順序的寫會比較好。

## 不只單元素，合體技也可以

<iframe height="600" style="width: 100%;" scrolling="no" title="tailwind breapoint2" src="https://codepen.io/hnzxewqw/embed/WNpgzgb?height=265&theme-id=light&default-tab=html,result"></iframe>

Tailwind 因為可以自由控制元素達到響應式的效果，所以上方範例手機板看起來是一張卡片，但手機板以上就會成橫幅的排版，這時候就可以看得出來此彈性的優勢別於元件型框架的差別。可以自由地做成任何想要的排版，我覺得這部份真的非常棒，不用受限於元件庫的限制了。

想要做卡片、彈窗，還是其他常見的元件，似乎都可以透過 Utility-First 來完成。

## 不需要針對手機板使用斷點

有提到 Tailwind 是手機優先開始撰寫，所以手機板不需要使用前綴詞，不要誤用 sm 是手機螢幕大小，sm 的預設斷點為 640px 喔！官方範例為：

```html
<div class="sm:text-center"></div>
```

正確的寫法為：

```html
<div class="text-center sm:text-left">這是一段文字</div>
```

上方的寫法意思是，在手機板的時候文字居中，解析度 `640px` 以上時，文字靠左。

<iframe height="265" style="width: 100%;" scrolling="no" title="Tailwind breakpoint3" src="https://codepen.io/hnzxewqw/embed/PopdRvr?height=265&theme-id=light&default-tab=html,result"></iframe>

## 單一斷點導向

Tailwind 的斷點只有 `min-width`，沒有 `max-width` ，這代表我都是要從手機板出發來寫斷點，如果我只想在某個元素使用斷點，我只需要在更大的斷點上寫我要的內容，就會覆蓋前一個斷點的內容，比如說下方範例：

<iframe height="265" style="width: 100%;" scrolling="no" title="Tailwind breakpoint4" src="https://codepen.io/hnzxewqw/embed/QWpVmeN?height=265&theme-id=light&default-tab=html,result" ></iframe>

我有一個方塊，在手機板的時候要靠左，並且是蜜桃色的，但隨著螢幕尺寸的變化，會慢慢變成不同的顏色，甚至到最大的斷點時，可以設定讓方塊靠右對齊。

透過斷點達到想呈現的效果就是這麼容易。

## 客製化斷點

Tailwind 的優點就是可以自由的客製化，假如預設的斷點比較不符專案使用，也可以透過 `tailwind.config.js` 去設定想要的斷點喔！斷點的前綴詞可以自訂義。

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    screens: {
      'tablet': '640px',
      // => @media (min-width: 640px) { ... }

      'laptop': '1024px',
      // => @media (min-width: 1024px) { ... }

      'desktop': '1280px',
      // => @media (min-width: 1280px) { ... }
    },
  }
}
```

## 參考資料

- [Tailwind CSS - Breakpoints](https://tailwindcss.tw/docs/breakpoints)
