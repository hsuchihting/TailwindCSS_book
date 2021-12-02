---
title: TailwindCSS 筆記 - Just In Time 模式的有趣功能
tags:
  - TailwindCSS
categories: TailwindCSS
description: JIT 模式太神啦！
abbrlink: 3644739138
date: 2021-09-08 21:39:19
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

## 未來更新趨勢

從官方文件可以看到在 JIT 模式中的 CSS 寫法可以非常的多樣且直覺，而未來 TailwindCSS 更新的核心與發展都會圍繞著 JIT 模式來開發。

## 在 JIT 底下有趣的功能

除了上篇說到的改尺寸跟顏色的寫法外，還有支持很多種原本要另外自己制定樣式的樣式，但在 TailwindCSS 中可以透過幾個 class 就能達成。

### 對於偽元素的支持

在傳統寫 CSS 使用偽元素可以完成許多樣式的設定，例如：

<iframe height="300" style="width: 100%;" scrolling="no" title="偽元素 CSS" src="https://codepen.io/hnzxewqw/embed/WNOoRrw?default-tab=html%2Cresult" frameborder="no">
</iframe>

使用 TailwindCSS 可以這樣寫：

```html
<div
  class="
                    text-gray-700
                    before:text-white
                    after:text-white
                    before:p-2
                    after:p-2
                    before:content-['before'] before:block before:bg-blue-500
                    after:flex after:bg-pink-300 after:content-['after']
                "
>
  ----
</div>
```

畫面呈現會是：

![fake](https://i.imgur.com/RHX8j5T.png)

而官方文件也提供以下偽元素可以使用的 variants

![pseudo variants](https://i.imgur.com/LCCinHY.png)

## 透明度

在沒有使用 JIT 模式下，如果要設定一個背景透明度要這樣寫，

```html
<div
  class="bg-red-500 bg-opacity-25 w-20 h-20 flex justify-center items-center"
>
  透明度
</div>
```

但如果有使用 JIT 模式的話，可以這樣寫，效果也相同，直接在顏色上算數學，把設定的顏色直接去除想要的透明度數值，這點真是超方便的。

```html
<div class="bg-red-500/25 w-20 h-20 flex justify-center items-center">
  透明度
</div>
```

![opacity](https://i.imgur.com/t5ATx50.png)

## 使用變數來變更字體、顏色或是任何屬性值

這邊很有趣，有點像是 SCSS 可以命名變數的方式，但又更加彈性，有兩種可以改變樣式的方法。

### 定義變數並直接使用在 template 上

在 `tailwind.css` 的 base 上方，先給一個 `:root{}` 的區塊，並且可以自訂義樣式名稱與值，比如說我要自訂字體大小、背景與顏色，可以這樣寫。

**tailwind.css**

```css
:root {
  --color: #fff;
  --bgc: #3e3e3e;
  --fontSize: 24px;
}

@tailwind base;
@tailwind components;
@tailwind utilities;

.title {
  color: var(--color);
  background-color: var(--bgc);
  font-size: var(--fontSize);
}
```

**html**

```html
<h2 class="title">使用變數</h2>
```

> 變數前面要使用 `--`，沒辦法使用 `$` 或是 `_` 等符號，會無法成功命名變數。

完成效果：

![var](https://i.imgur.com/QVBMVjq.png)

### 直接在 template 上使用變數

還有另一個方式是使用定義好的變數，因為 template 無法直接知道變數是什麼東西，所以在不同屬性的變數前面，要加上以下的類型。

![type](https://i.imgur.com/c19Ivry.png)

以原本的變數為例，直接使用在 template 上可以這樣寫，

```html
<h2
  class="bg-[color:var(--bgc)] text-[color:var(--color)] text-[length:var(--fontSize)]"
>
  使用變數2
</h2>
```

如同前面有提到可以自訂樣式的寫法，但這邊是使用 color 的類型去指定顏色相關的樣式，文字就要使用 length 的類型，並且後面再加上定義好的變數樣式，就可以直接使用了。

得到的效果會與第一個相同。

![var2](https://i.imgur.com/RoaFGcf.png)

雖然看起來比較麻煩，但好處是，當今天接手前人專案，當今天專案又大樣式又深的時候，沒時間研究的話，可以使用第二種方式達到修改樣式的效果喔！

至於哪一種比較好用就見仁見智了。

## 修改 input 游標

`<input>` 標籤不管在前後台都會頻繁使用的標籤，預設就是萬年不變的黑色閃爍游標

<iframe height="300" style="width: 100%;" scrolling="no" title="input" src="https://codepen.io/hnzxewqw/embed/mdwOWEO?default-tab=html%2Cresult" >
</iframe>

而 TailwindCSS 可以透過 JIT 模式去修改其游標樣式。

```html
<input
  type="text"
  class="caret-red-400 p-2 border-2 focus:border-blue-300 focus:outline-none"
/>
```

![input](https://i.imgur.com/XcLz5eT.png)

## 小結

本篇就是紀錄一些在 JIT 模式中新增以及有趣的功能，跟著官方的示範跟練習，真的覺得 JIT 模式相當強大，也節省非常多的時間，真是太厲害了！

## 參考資料

- [Just-in-Time Mode](https://tailwindcss.com/docs/just-in-time-mode)
