---
title: Tailwind CSS - 每個 Utility class 都支援響應式與偽類
tags:
  - TailwindCSS
categories: TailwindCSS
description: Tailwind CSS 的最大優勢之一
abbrlink: 2095338064
date: 2021-06-07 22:57:00
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

手刻響應式網站，對我來說其實沒有到很困難，但如果頁面一多，時程又趕，就會很麻煩，而 Tailwind 有一個令人心動的特點就是，所有的 Utility class 都支援響應式。

## 怎麼寫響應式斷點

手刻響應式會使用下面的方式撰寫：

```cmd
@media query(max-width:XXXpx){
/** 響應式內容 */
}
```

甚至後來學 SCSS 的時候因為懶惰就另外寫了一個元件，每次只要引入元件，在使用 `@include` 想要的尺寸就好，可是前端的世界沒這麼好過，看看現在手機已經都快不像手機，都跟小電視一樣，尺寸亂七八糟什麼都有，各家手機也都規則不一。

### 使用 Bootstrap 設定響應式

後來學了 Bootstrap 後，算是在響應式有得到一點救贖，只在響應式不用去想斷點，只要專心切板就好，我最常用的就是惱人的 [table](https://bootstrap5.hexschool.com/docs/5.0/content/tables/) 了。

<iframe height="265" style="width: 100%;" scrolling="no" title="Tailwind CSS example BS table" src="https://codepen.io/hnzxewqw/embed/oNZyWKd?height=265&theme-id=light&default-tab=html,result"></iframe>

個人覺得 `table` 的部分算是已經夠好用了，也算是清楚，但還是要相依在該規範中。

其他元件就要整個元件程式碼完整架構，如：卡片

```html
<div class="card" style="width: 18rem;">
  <img src="..." class="card-img-top" alt="..." />
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">
      Some quick example text to build on the card title and make up the bulk of
      the card's content.
    </p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
</div>
```

<iframe height="265" style="width: 100%;" scrolling="no" title="BS card" src="https://codepen.io/hnzxewqw/embed/jOBKwPW?height=265&theme-id=light&default-tab=html,result"></iframe>

可以看到又出現跟之前說明的狀況一樣，因為 Bootstrap 是以定義好的元件方式載入畫面，所以會需要依賴該框架的元件定義，才能完整呈現想要的畫面。

如果要多張卡片呈現在畫面的時候，就變成要外面再包更多的標籤。

```html
<div class="row">
  <div class="col-md-3">...</div>
</div>
```

如果畫面單純就還好，可是如果今天畫面越來越複雜的時候，在維護時光是找標籤收尾可能都滿難找到的。

## Tailwind 是手機優先斷點寫法

跟 Bootstrap 一樣是從手機優先來規劃斷點的，以卡片為例，今天透過 Utility-first 的方式來撰寫三張卡片並排且加入斷點。Tailwind 不需要相依在元件之下，就可以寫出卡片效果以及斷點。

![rwd](https://i.imgur.com/9RtP50g.png)

官方也提供明確的斷點寫法，只要在想要做斷點的前面加上斷點縮寫即可，例如：

```html
<img class="w-16 md:w-32 lg:w-48" src="...">
```

是不是跟 Bootstrap 有異曲同工之妙，但是我只要加在想要的 `element` 上面就好了，也不用加了很多 `.row` 跟 `.col`。

## 偽類也是一樣的方法

通常我們想要按鈕有點互動效果，一般 CSS 也會寫成：

```css
h1 {
  color: red;
}

h1:hover {
  color: blue;
}
```

但我使用 Tailwind 就只要寫成

```html
<h1 class="text-red-500 hover:text-blue-500">this is title</h1>
```

**DEMO**

<iframe height="265" style="width: 100%;" scrolling="no" title="Tailwind CSS hover" src="https://codepen.io/hnzxewqw/embed/VwpdzYw?height=265&theme-id=light&default-tab=html,result"></iframe>

直觀又好理解！

## 最後綜合一個響應式卡片與有偽類效果的練習

點選右側的 CodePen 可以看見響應式的效果喔！

<iframe height="800" style="width: 100%;" scrolling="no" title="Tailwind RWD &amp; hover" src="https://codepen.io/hnzxewqw/embed/dyvKzMy?height=265&theme-id=light&default-tab=html,result"></iframe>

## 參考資料

- [TailwindCSS - Hover, Focus, & Other States ](https://tailwindcss.com/docs/hover-focus-and-other-states)
