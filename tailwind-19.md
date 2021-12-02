---
title: TailwindCSS 筆記 - 初探 Just in Time 模式 v2.2
tags:
  - TailwindCSS
categories: TailwindCSS
description: 不能不知道的 Just in Time 模式，用了就回不去了！
abbrlink: 2074616694
date: 2021-09-08 21:37:28
---
![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

## 關於 JIT 模式

JIT(Just in Time Mode) 是在 TailwindCSS v2.1 以後才出現的功能，未來此框架開發也會圍繞在這個功能上，如果有試玩的朋友就會發現這個功能真是相當酷炫，所以如果專案沒有特別要求要支援 IE 的話，建議都直接更新到最新版本，因為有用跟沒有差非常多，v2.1 以前的版本是沒有支援 JIT 模式，所以開發時這一點非常需要注意！

## 為什麼要使用 JIT 模式

練習至今有發現如果我修改很多 template 的東西，就會需要重新編譯專案，如果專案一大，編譯的時間就會很久，而在開發專案的過程必定會不斷地修改切版的內容，如果每次修改後都會因為編譯時間長而降低開發的效率，導致產出量能不佳，這樣原本這麼好用的切版框架，反而就變成不好用了。

## 使用 JIT 模式起手式

打開 `tailwind.config.js` 檔案，然後加上 `mode:'jit'`，這樣就可以了。

```cmd
module.exports = {
    purge: {
        enabled: true,
        content: ["./**/*.html"],
    },
    mode:'jit', //加在這裡
    darkMode: false, // or 'media' or 'class'
    theme: {
        extend: {},
    },
    variants: {
        extend: {
            ringWidth: ["active"],
        },
    },
    plugins: [],
};
```

### 直接看編譯速度

最有感覺就是在編譯的時候，這是沒有用 JIT 的編譯時間，共花了 2.6 秒左右。

![before jit](https://i.imgur.com/0Al5Q2V.png)

這是使用 JIT 之後，瞬間不到 1 秒就編譯完了！哇喔！

![used jit](https://i.imgur.com/JgRo4ze.png)

### 默認加入所有的狀態

使用 JIT 的好處其二，之前有看到有些樣式的狀態需要另外透過擴充的方式增加，但這樣變成再開發的時候，還要去確認哪一個有加上狀態，哪一個沒有加上狀態，以之前的練習為例，我在 `variants` 中擴充了一個 `ringWidth` 有 `active` 的狀態，但使用 JIT 模式後，這一段就不用加了，因為在此模式會默認所有狀態都加上去。

**tailwind.config.js**

```cmd
module.exports = {
    mode: "jit", //加在這裡
    purge: ["./**/*.html", "./src/**/*.css"],
    darkMode: false, // or 'media' or 'class'
    theme: {
        extend: {},
    },
    variants: {
        extend: {

        },
    },
    plugins: [],
};
```

雖然我已經把擴充的 ringWidth 刪除了，但我在 click 的時候依然會有 active 效果。

![active](https://i.imgur.com/28I60l1.png)

### 客製化樣式超省力

之前如果要客製化樣式，要回到配置檔的 theme 的內容去做客製，但如果在開發中會不斷需要增減樣式，其實是一件非常麻煩的事情，而且客製的內容只能使用 TailwindCSS 設定好的數值，如果要特別客製，可能就要寫成元件的方式，一兩頁可能還好，但當專案頁數一多，相依性也多的時候，就會非常的麻煩，但 JIT 幫我們解決這樣的問題。

以下方為例：

做一個寬高都相同為 `w-20` 的方形，

```html
<div class="container mx-auto mt-3">
  <div class="w-20 h-20 bg-blue-500 mt-4"></div>
</div>
```

![box](https://i.imgur.com/jXaWS3I.png)

如果使用 JIT 模式，我可以直接透過 `w-[...]` 的方式修改，就不用透過擴充的方式更改樣式囉！

```html
<div class="container mx-auto mt-3">
  <div class="w-[20px] h-20 bg-blue-500"></div>
</div>
```

![box fix](https://i.imgur.com/WVGCN0n.png)

打開開發人員工具也可以看到樣式的確被修改了。

![console](https://i.imgur.com/snMKec7.png)

當然顏色也可以這樣處理，方式也與剛剛修改寬度的方式相同，只要給予一個色票號碼即可。

```html
<div class="w-[20px] h-20 bg-[#f0f]"></div>
```

![pink](https://i.imgur.com/0BnzDUv.png)

![bg](https://i.imgur.com/1Fi07bu.png)

透過以上兩個簡單的練習，已經可以體驗到除了大幅降低編譯時間外，更重要的是可以客製化的彈性更大，當然還有很多內容可以參考官方文件。

## 參考資料

- [Just-in-Time ModeTailwind CSS version](https://tailwindcss.tw/docs/just-in-time-mode#troubleshooting)
