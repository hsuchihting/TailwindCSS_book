---
title: Tailwind CSS - 設定自己想要的 TailwindCSS 樣式 Variant
tags:
  - TailwindCSS
categories: TailwindCSS
description: 如果預設樣式沒有可以使用的，就自己客製吧！
abbrlink: 961026179
date: 2021-06-20 23:53:22
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

前面有提到 TailwindCSS 在所有的 DOM 元素前面幾乎都可以使用偽類變體來控制，但幾乎也就代表了沒有全部的元素都可以這樣做，那如果專案需要設定效果，但 TailwindCSS 沒有支援怎麼辦。

> ~~那就自己用 CSS 刻阿！然後這篇就到這裡結束了(被揍)~~

貼心的 TailwindCSS 也提供可以客製化的方式給開發者。

## 使用 Variant 來設定自己想要的樣式

基本上許多常用的效果 TailwindCSS 都已經幫開發者設定好，那為什麼要可以自訂呢?

因為還是有許多較少使用的樣式，沒有被設定。因為較少使用，所以要用到的時候，會發現我打了樣式，卻沒有出現效果...

例如：

我想在 `hover` 效果的時候使用 `border-dashed` 虛線效果，可是沒有出現。

<iframe height="265" style="width: 100%;" scrolling="no" title="TailwindCSS no border-dashed style" src="https://codepen.io/hnzxewqw/embed/poeBpoK?height=265&theme-id=light&default-tab=html,result"></iframe>

雖然我也可以每次要用的時候再去翻文件就好，但就是每次要寫就要去找一次，有點麻煩。

> 可能常寫也會記得啦！~~但如果可以都不要寫不是更好(誤)~~...

## 建構屬於自己的設定檔

### 預設設定檔

在文件中有一個指令

```cmd
npx tailwindcss init
```

會將專案根目錄建立一個最基本的 `tailwind.config.js` 檔案，也就是一開始安裝的時候出現的那支，會看到內容都是空的。

```javascript
// tailwind.config.js
module.exports = {
  purge: [],
  darkMode: false, // 或 'media' 或 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
};
```

## 完整的設定檔

如果想看到 TailwindCSS 完整的設定檔，可以輸入指令

```cmd
npx tailwindcss init --full
```

這時候就會看到 TailwindCSS 完整的[預設配置檔](<[https://](https://unpkg.com/browse/tailwindcss@2.2.2/stubs/defaultConfig.stub.js)>)，因礙於篇幅關係就不再放到文章中，可點選連結查看。

### 建議覆蓋預設配置檔的內容

雖然得到完整的預設配置檔，可以改成專案需求的樣式，但官方文件建議只在需要客製化地方，使用覆蓋的方式去取代原本預設的樣式，會是比較推薦的做法，避免一次引入太多沒使用到的樣式，讓 CSS 變得很肥。

官方有給一個使用覆蓋預設樣式的範例：

```javascript
// `tailwind.config.js` 範例檔案
const colors = require("tailwindcss/colors");

module.exports = {
  theme: {
    colors: {
      gray: colors.coolGray,
      blue: colors.lightBlue,
      red: colors.rose,
      pink: colors.fuchsia,
    },
    fontFamily: {
      sans: ["Graphik", "sans-serif"],
      serif: ["Merriweather", "serif"],
    },
    extend: {
      spacing: {
        128: "32rem",
        144: "36rem",
      },
      borderRadius: {
        "4xl": "2rem",
      },
    },
  },
  variants: {
    extend: {
      borderColor: ["focus-visible"],
      opacity: ["disabled"],
    },
  },
};
```

可以看見此範例覆蓋了以下幾個內容：

1. 主題 `theme` 下有兩個子項目：字型 `fontFamily` 與延伸區塊 `extend` 改變 **間距 `spacing`** 以及 **邊框弧度 `borderRadius`**。
2. 變化模式 **variants** 的項目：**邊框線條 `borderColor`** 與 **透明度 `opacity`**。

## 更改 tailwind.config.js 的 Variants 內容

本篇重點在 `variants` 區塊，超級多屬性!!

**tailwind.config.js**

```javascript
variants: {
    accessibility: ['responsive', 'focus-within', 'focus'],
    alignContent: ['responsive'],
    alignItems: ['responsive'],
    alignSelf: ['responsive'],
    animation: ['responsive'],
    appearance: ['responsive'],
    backdropBlur: ['responsive'],
    backdropBrightness: ['responsive'],
    backdropContrast: ['responsive'],
    backdropDropShadow: ['responsive'],
    backdropFilter: ['responsive'],
    backdropGrayscale: ['responsive'],
    backdropHueRotate: ['responsive'],
    backdropInvert: ['responsive'],
    backdropSaturate: ['responsive'],
    backdropSepia: ['responsive'],
    backgroundAttachment: ['responsive'],
    backgroundBlendMode: ['responsive'],
    backgroundClip: ['responsive'],
    backgroundColor: ['responsive', 'dark', 'group-hover', 'focus-within', 'hover', 'focus'],
    backgroundImage: ['responsive'],
    backgroundOpacity: ['responsive', 'dark', 'group-hover', 'focus-within', 'hover', 'focus'],
    backgroundPosition: ['responsive'],
    backgroundRepeat: ['responsive'],
    backgroundSize: ['responsive'],
    blur: ['responsive'],
    borderCollapse: ['responsive'],
    borderColor: ['responsive', 'dark', 'group-hover', 'focus-within', 'hover', 'focus'],
    borderOpacity: ['responsive', 'dark', 'group-hover', 'focus-within', 'hover', 'focus'],
    borderRadius: ['responsive'],
    borderStyle: ['responsive'],
    borderWidth: ['responsive'],
    boxDecorationBreak: ['responsive'],
    boxShadow: ['responsive', 'group-hover', 'focus-within', 'hover', 'focus'],
    boxSizing: ['responsive'],
    brightness: ['responsive'],
    clear: ['responsive'],
    container: ['responsive'],
    contrast: ['responsive'],
    cursor: ['responsive'],
    display: ['responsive'],
    divideColor: ['responsive', 'dark'],
    divideOpacity: ['responsive', 'dark'],
    divideStyle: ['responsive'],
    divideWidth: ['responsive'],
    dropShadow: ['responsive'],
    fill: ['responsive'],
    filter: ['responsive'],
    flex: ['responsive'],
    flexDirection: ['responsive'],
    flexGrow: ['responsive'],
    flexShrink: ['responsive'],
    flexWrap: ['responsive'],
    float: ['responsive'],
    fontFamily: ['responsive'],
    fontSize: ['responsive'],
    fontSmoothing: ['responsive'],
    fontStyle: ['responsive'],
    fontVariantNumeric: ['responsive'],
    fontWeight: ['responsive'],
    gap: ['responsive'],
    gradientColorStops: ['responsive', 'dark', 'hover', 'focus'],
    grayscale: ['responsive'],
    gridAutoColumns: ['responsive'],
    gridAutoFlow: ['responsive'],
    gridAutoRows: ['responsive'],
    gridColumn: ['responsive'],
    gridColumnEnd: ['responsive'],
    gridColumnStart: ['responsive'],
    gridRow: ['responsive'],
    gridRowEnd: ['responsive'],
    gridRowStart: ['responsive'],
    gridTemplateColumns: ['responsive'],
    gridTemplateRows: ['responsive'],
    height: ['responsive'],
    hueRotate: ['responsive'],
    inset: ['responsive'],
    invert: ['responsive'],
    isolation: ['responsive'],
    justifyContent: ['responsive'],
    justifyItems: ['responsive'],
    justifySelf: ['responsive'],
    letterSpacing: ['responsive'],
    lineHeight: ['responsive'],
    listStylePosition: ['responsive'],
    listStyleType: ['responsive'],
    margin: ['responsive'],
    maxHeight: ['responsive'],
    maxWidth: ['responsive'],
    minHeight: ['responsive'],
    minWidth: ['responsive'],
    mixBlendMode: ['responsive'],
    objectFit: ['responsive'],
    objectPosition: ['responsive'],
    opacity: ['responsive', 'group-hover', 'focus-within', 'hover', 'focus'],
    order: ['responsive'],
    outline: ['responsive', 'focus-within', 'focus'],
    overflow: ['responsive'],
    overscrollBehavior: ['responsive'],
    padding: ['responsive'],
    placeContent: ['responsive'],
    placeItems: ['responsive'],
    placeSelf: ['responsive'],
    placeholderColor: ['responsive', 'dark', 'focus'],
    placeholderOpacity: ['responsive', 'dark', 'focus'],
    pointerEvents: ['responsive'],
    position: ['responsive'],
    resize: ['responsive'],
    ringColor: ['responsive', 'dark', 'focus-within', 'focus'],
    ringOffsetColor: ['responsive', 'dark', 'focus-within', 'focus'],
    ringOffsetWidth: ['responsive', 'focus-within', 'focus'],
    ringOpacity: ['responsive', 'dark', 'focus-within', 'focus'],
    ringWidth: ['responsive', 'focus-within', 'focus'],
    rotate: ['responsive', 'hover', 'focus'],
    saturate: ['responsive'],
    scale: ['responsive', 'hover', 'focus'],
    sepia: ['responsive'],
    skew: ['responsive', 'hover', 'focus'],
    space: ['responsive'],
    stroke: ['responsive'],
    strokeWidth: ['responsive'],
    tableLayout: ['responsive'],
    textAlign: ['responsive'],
    textColor: ['responsive', 'dark', 'group-hover', 'focus-within', 'hover', 'focus'],
    textDecoration: ['responsive', 'group-hover', 'focus-within', 'hover', 'focus'],
    textOpacity: ['responsive', 'dark', 'group-hover', 'focus-within', 'hover', 'focus'],
    textOverflow: ['responsive'],
    textTransform: ['responsive'],
    transform: ['responsive'],
    transformOrigin: ['responsive'],
    transitionDelay: ['responsive'],
    transitionDuration: ['responsive'],
    transitionProperty: ['responsive'],
    transitionTimingFunction: ['responsive'],
    translate: ['responsive', 'hover', 'focus'],
    userSelect: ['responsive'],
    verticalAlign: ['responsive'],
    visibility: ['responsive'],
    whitespace: ['responsive'],
    width: ['responsive'],
    wordBreak: ['responsive'],
    zIndex: ['responsive', 'focus-within', 'focus'],
  },
```

找到 `borderStyle` 屬性，因為剛剛我想在 `hover` 時使用 `border-dashed`，但此屬性預設，沒有這 `hover` 效果。預設如下：

```javascript
borderStyle: ['responsive'],
```

又看到其他屬性有加上 `hover` 與 `focus` 的偽類值，所以我也照樣照句，把 `hover` 加入到 `borderStyle` 中。

新增後會變這樣：

```javascript
borderStyle: ['responsive','hover'],
```

這時候再回到 HTML 上就會發現智能提示會出現之前想要設定的 `border-dashed` 樣式！

![html](https://i.imgur.com/P7CoauK.png)

**HTML**

```html
<div class="container sm:mx-auto">
  <button
    class="
        flex
        sm:mx-auto
        rounded
        py-2
        px-3
        m-2
        bg-yellow-300
        text-black
        hover:text-white
        hover:bg-green-500
        focus:outline-none
        border-black border-2
        hover:border-red-900 hover:border-dashed hover:border-8
        "
  >
    Click Me
  </button>
  <br />
  <p class="text-center">
    <code class="bg-pink-200 p-2 text-red-500">border-dashed</code>沒有效果
  </p>
</div>
```

重新編譯後，滑鼠移動到畫面上，也會出現一樣的效果。

**no hover**

![before](https://i.imgur.com/D9fGXNk.png)

**hover**

![after](https://i.imgur.com/V5avGUd.png)

如果要用覆蓋的方式，可以寫在 `variants` 屬性內，也會達到一樣的效果。

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
    extend: {
      borderStyle: ["responsive", "hover"],
    },
  },
  plugins: [],
};
```

以上筆記客製化 `variants` 變化模式如何新增效果在預設設定檔中，或是覆蓋想要改變的樣式，自己一開始用會全部展開修改，因為太多屬性，還要去翻找文件有時候滿麻煩的，但相信未來熟稔之後，應該就可以用覆蓋的方式來寫了。

## 參考資料

- [TailwindCSS - Configuration](https://tailwindcss.com/docs/configuration)
- [【Tailwind CSS 教學 - 8】詳解 Variant Tailwind config 設定方式](https://ithelp.ithome.com.tw/articles/10246236)
