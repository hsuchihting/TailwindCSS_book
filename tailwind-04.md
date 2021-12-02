---
title: Tailwind CSS - CSS 傳統撰寫方式與功能優先的差異
tags:
  - TailwindCSS
categories: TailwindCSS
description: 使用 Tailwind CSS 撰寫之優勢
abbrlink: 1535452451
date: 2021-06-07 18:06:24
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

## Utility First 功能優先

官方文件給的定義

> 從組合過的原生功能，來建立起複雜的元件。

### 傳統的 CSS 撰寫方式

在介紹 Utility First 之前，先來看一下傳統 CSS 怎麼寫。

假設我今天要切一個下方畫面：

![chat](https://i.imgur.com/ruqeK9M.png)

相信一開始沒有任何網頁前端背景的人，應該是跟我一樣，從 HTML + CSS 寫出一個所見即所得的靜態網頁，而一開始寫 CSS 會建議使用語意化來命名 `class name`，然後就會向下方的範例程式碼一樣，

**HTML**

```html
<div class="chat-notification">
  <div class="chat-notification-logo-wrapper">
    <img
      class="chat-notification-logo"
      src="/img/logo.svg"
      alt="ChitChat Logo"
    />
  </div>
  <div class="chat-notification-content">
    <h4 class="chat-notification-title">ChitChat</h4>
    <p class="chat-notification-message">你有一則新訊息</p>
  </div>
</div>
```

**CSS**

```css
.chat-notification {
  display: flex;
  max-width: 24rem;
  margin: 0 auto;
  padding: 1.5rem;
  border-radius: 0.5rem;
  background-color: #fff;
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
}
.chat-notification-logo-wrapper {
  flex-shrink: 0;
}
.chat-notification-logo {
  height: 3rem;
  width: 3rem;
}
.chat-notification-content {
  margin-left: 1.5rem;
  padding-top: 0.25rem;
}
.chat-notification-title {
  color: #1a202c;
  font-size: 1.25rem;
  line-height: 1.25;
}
.chat-notification-message {
  color: #718096;
  font-size: 1rem;
  line-height: 1.5;
}
```

看得出來所有的東西都跟 chat 有關，但是只要階層一多， class 的名稱就會越來越長，慢慢的第一時間也越來越難分辨這段是什麼?

另外，要想命名也是非常頭痛的事情，如果用 Tailwind 改寫會變成如何？

```html
<div
  class="p-6 max-w-sm mx-auto bg-white rounded-xl shadow-md flex items-center space-x-4"
>
  <div class="flex-shrink-0">
    <img class="h-12 w-12" src="/img/logo.svg" alt="ChitChat Logo" />
  </div>
  <div>
    <div class="text-xl font-medium text-black">ChitChat</div>
    <p class="text-gray-500">你有一則新訊息</p>
  </div>
</div>
```

看起來的確有精簡一點，雖然最外層的 class 好像變得更長了，可是我卻一行 CSS 都不用寫！原本要在 CSS 的定義的內容，全部透過 Tailwind 的 Utility-First 的方式呈現在畫面上了！

當我第一次接觸 Tailwind 的時候，也覺得這樣也沒有比較好啊！而且變得更繁瑣，的確是這樣沒錯，但開始寫了以後會發現以下優點：

- **我不必為了命名 class 而傷腦筋**，不需要只是要添加某些樣式就硬要寫類似 `.side-wrap` 這種為了命名而命名的 class name。
- **CSS 檔案不會再變多了**，傳統撰寫方式，是每當新增功能的時候，CSS 樣式都會變多，使用 Utility- First 的方式，都是可以重用的 class name，幾乎不用編寫新的 CSS，而且因為共用了 class，就算頁面非常多，但因為 class 內容相同，所以 CSS 檔案也不會變肥，渲染畫面效果更好！
- **不用擔心更改後畫面壞掉**，因為 CSS 是全域的，每次要改一些樣式，都會怕整個畫面壞掉，因為我修改的地方是 HTML，所以只要專注在我要修改的部分，不用擔心會影響到其他樣式。

**Demo**

<iframe height="265" style="width: 100%;" scrolling="no" title="Tailwind CSS example chat" src="https://codepen.io/hnzxewqw/embed/RwpJGwW?height=265&theme-id=light&default-tab=html,result"></iframe>

> 官方文件是用絕對路徑引入圖片，因我沒有該圖片，所以就直接去複製網頁中的 SVG 檔案。

## 寫這麼多 class，為什麼不寫 inline style

inline style 就是在 HTML 上面寫上樣式，

```html
<h1 style="color: red;font-size: 24px; padding: 10px 0;">title</h1>
```

但這樣會有一個問題，這只有針對這個 tag 就是 inline style 的權重較高，未來若要修改樣式，則需要找到該 tag，而使用 Tailwind 可以透過 class 定義的關係，能夠 `tailwind.config.js` 輕易修改多個樣式。

## 參考資料

- [Tailwind CSS - Utility-First](https://tailwindcss.com/docs/utility-first)
