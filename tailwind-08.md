---
title: Tailwind CSS - 偽類變體 Pseudo-Class Variants
tags:
  - TailwindCSS
categories: TailwindCSS
description: 好用的偽類變體，與響應式搭配效果超級便利
abbrlink: 1717980556
date: 2021-06-14 23:56:05
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

## 什麼是偽類變體

又來一個專有名詞，還沒學就心慌慌...

但是發現有一個熟悉名詞：**偽類**(看到這個我就放一半的心了)。在傳統 CSS 中，常常會使用偽元素，像是 `:hover`, `:active`, `:focus`...等等。以前如果要寫一個 `a` 連結，然後要 `hover` 效果會變色的話會寫：

<iframe height="265" style="width: 100%;" scrolling="no" title="css3 a href - TailwindCSS" src="https://codepen.io/hnzxewqw/embed/RwpqOzm?height=265&theme-id=light&default-tab=css,result"></iframe>

但使用 Tailwind 之後只要在想使用偽類效果的地方加上想用的偽類，就可以達到預期的效果，像是我我把上方範例改寫成 Tailwind 的方式的話，會是：

<iframe height="265" style="width: 100%;" scrolling="no" title="Tailwind a hover" src="https://codepen.io/hnzxewqw/embed/VwpVOwR?height=265&theme-id=light&default-tab=html,result"></iframe>

但其實 Tailwind 規劃偽類變體的方法跟傳統的 CSS 是不同的，當我滑鼠移到 `hover:text-red-500`，會出現提示訊息：

![tip](https://i.imgur.com/ZNC02Xq.png)

原來它是把 `hover` 包裝成一個 class，然後再去執行文字變色的效果有 `hover` 的偽類。

## 智能提示的方便之處

順便提一下智能提示有一個很方便的地方，也就是當我在打想要使用的 class 時，旁邊會跳出提示訊息，告訴我此 class 在編譯成 CSS 後會是什麼設定，這樣就不用一直去測試 Tailwind 的 class 效果是什麼囉！

![tips](https://i.imgur.com/7H8u3ji.png)

## 還有更多偽類變體可以使用

除了上方介紹的 hover 外，還有以下可以使用的偽類變體，都可以到[官方文件](https://tailwindcss.tw/docs/hover-focus-and-other-states)複製下來玩玩看。

- Hover
- Focus
- Active
- Group-hover
- Group-focus
- Focus-within
- Focus-visible
- Motion-safe
- Motion-reduce
- Disabled
- Visited
- Checked
- First-child
- Last-child
- Odd-child
- Even-child

## 偽類變體與響應式的合體技

[Tailwind CSS - 手機到桌上螢幕，所有的元素都能自適應](https://hsuchihting.github.io/TailwindCSS/20210612/1338142949/)有介紹過 Tailwind 自適應的強大之處，與偽類變體結合更是超強合體技！如下方範例，在解析度 375px 與超過 375px 時，可以讓按鈕在不同的解析度下有不同的 hover 效果喔！

<iframe height="265" style="width: 100%;" scrolling="no" title="Tailwind - pseudo x responsive" src="https://codepen.io/hnzxewqw/embed/yLMQWwq?height=265&theme-id=light&default-tab=html,result"></iframe>

## 參考資料

- [TailwindCSS - Hover, Focus, & Other States](https://tailwindcss.tw/docs/hover-focus-and-other-states)
- [【Tailwind CSS 教學 - 7】Pseudo-Class Variants 是 CSS 屆的偉大發明](https://ithelp.ithome.com.tw/articles/10246163)
