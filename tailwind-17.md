---
title: TailwindCSS 筆記 - 認識 PostCSS
tags:
  - TailwindCSS
categories: TailwindCSS
description: 我知道你知道預處理器，那後處理器呢?
abbrlink: 1114276106
date: 2021-09-08 21:32:36
---

![postcss](https://cythilya.github.io/assets/css/postcss-cover-small.png)

前面有提到安裝 TailwindCSS 推薦使用 PostCSS，前面練習的都是沒有相依 PostCSS 來練習，但該面對的總是要面對，先來認識一下關於 CSS 的處理，就以一般前端常用的 SCSS 為例。

## 關於預處理器與後處理器

從字面上可以得知，CSS 的處理可以分為預處理跟後處理 ~~(廢話)~~，相信有切版一段時間的前端工程師都享受到預處理器的方便之處，可以統一命名變數整理關於字型顏色、大小或是各種共用的屬性，避免不斷輸入一樣的色碼，甚至在大幅修改的時候，可以透過變數免去修改的時間。

### 預處理器

> 寫的內容瀏覽器並看不懂，但透過 build 之後編譯成瀏覽器看得懂的 CSS 語法。

像是今天要寫一個圓角，可以透過變數撰寫顏色，並且可以用 & 延續要做 `:hover` 效果，不必重新寫一次 class 的動作。

<iframe height="300" style="width: 100%;" scrolling="no" title="scss" src="https://codepen.io/hnzxewqw/embed/YzQXvVq?default-tab=html%2Cresult">
</iframe>

**SCSS**

```css
$bg-primary: red;
$bg-hover: orange;

.box {
  width: 100px;
  height: 100px;
  border-radius: 10px;
  background-color: $bg-primary;
  &:hover {
    background-color: $bg-hover;
  }
}
```

編譯成 CSS 後

**CSS**

```css
.box {
  width: 100px;
  height: 100px;
  border-radius: 10px;
  background-color: red;
}
.box:hover {
  background-color: orange;
}
```

是不是超方便，但 SCSS 有一個要注意的地方，如果要使用預處理器，就要使用他所有的包含的內容，不能自行刪減，就算你這個專案用不到，但還是需要整個使用。

## 後處理器

既然能預處理也可以後處理，而 PostCSS 就是屬於後處理器，其中方便之處是可以自行增減自己需要的編譯的部分，最常用的就是個瀏覽器的前綴詞。套件是這個 [autoprefixer](https://www.npmjs.com/package/autoprefixer)

### 後處理器

直接先看官方範例，下方是要寫的樣式，

```css
.my-class,
#my-id {
  border-radius: 1em;
  transition: all 1s ease;
  box-shadow: #123456 0 0 10px;
}
```

但如果要自行加上各瀏覽器的前綴詞會變這樣，

```css
.my-class,
#my-id {
  -moz-border-radius: 1em;
  -webkit-border-radius: 1em;
  border-radius: 1em;
  -moz-transition: all 1s ease;
  -o-transition: all 1s ease;
  -webkit-transition: all 1s ease;
  transition: all 1s ease;
  -moz-box-shadow: #123456 0 0 10px;
  -webkit-box-shadow: #123456 0 0 10px;
  box-shadow: #123456 0 0 10px;
}
```

光是去找相符的瀏覽器就搞死自己，但是透過後處理器編譯後，就可以直接這樣了，當然預處理器也可以辦到。

### 那幹嘛用後處理器

1. 可以建立自己的套件(plugins)。
2. 使用標準的 CSS 語法。

## PostCSS 起手式

- 安裝 PostCSS 與其插件。

```cmd
npm install postcss postcss-loader autoprefixer precss --save-dev
```

這邊有安裝剛剛提到的前綴詞插件 `autoprefixer`。

- 安裝完後會有一個 `postcss.config.js` 檔案，加入需要用到的 press 與 autoprefixer 套件即可。
  > 所有想要用的擴充套件都要在 `postcss.config.js` 設定檔才行。當然用在 `tailwind` 的時候就是要在 `tailwind.config.js` 裡面設定。

```cmd
module.exports = {
  plugins: {
    precss: {}, // 使用類似 SASS 的功能，例如：變數
    autoprefixer: {
      // 加入各家瀏覽器的前綴詞
      browsers: [
        // 指定支援的瀏覽器版本
        'Chrome >= 52',
        'FireFox >= 44',
        'Safari >= 7',
        'Explorer >= 11',
        'last 2 Edge versions',
      ],
    },
  },
};
```

這樣就可以使用 `autoprefixer` 的套件了。

## 參考資料

- [PostCSS](https://cythilya.github.io/2018/08/10/postcss/)
- [[心得] 什麼是 postcss?](http://huli.logdown.com/posts/262723-experiences-what-is-postcss)
- [DAY13 - Postprocessor - PostCss 基本介紹](https://ithelp.ithome.com.tw/articles/10245594)
