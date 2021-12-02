---
title: Tailwind CSS - 壓縮 Utility 檔案大小 、安裝知能提示與最新版本須知
tags:
  - TailwindCSS
categories: TailwindCSS
description: 壓縮 CSS 大小，讓渲染更有效率
abbrlink: 2331513775
date: 2021-06-07 18:03:55
---

![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

## 為什麼要壓縮 CSS

Utility CSS 整包 CSS 整包檔案容量很大，會降低網頁效能，也是令人詬病的地方。
官方文件也表示 Tailwind CSS 為壓縮前的大小為 3566.2KB，但壓縮後就可以變成 289.2KB，也說雖然在開發者模式很肥大，但這是原先設計此框架的設計概念。是為了提升更有效率的開發體驗，共有上千種功能的 class，只是有可能一大部分根本不會使用到。

也可以把 Tailwind 想像成一大箱樂高，把這箱樂高「倒」出來後，再把需要的部分拿來組裝，組完後再把沒用到的樂高放回箱子裡。

所以 Tailwind 是可以壓縮的，可以去偵測到哪些 class 有被用到，把沒用到的移除，整體檔案容量就會減少很多喔！

這是初步匯出 Tailwind 的檔案大小，`3.46MB`。

![tailwind](https://i.imgur.com/GGkHtc0.png)

官方建議可以使用 `taiwind.config.js` 中的 `purge` 把專案中要編譯的檔案放進來，就只會去編譯我們指定的檔案，這樣就不會整包 CSS 匯出喔！超棒的！

基本用法：

首先在 purge 的選系下以陣列規範所有樣板檔案的路徑。

![purge](https://i.imgur.com/rZFJX6K.png)

那本篇範例我希望都可以一直被監測是壓縮，所以這裡使用手動模式：

![purge](https://i.imgur.com/V2mFSJm.png)

上面這個意思就是預設都是 enabled 狀態去做壓縮，然後要加縮的內容就是目前專案所有的 HTML 檔案。

### 舉例

我目前的 HTML 檔案只有一個。

![linkCSS](https://i.imgur.com/QOreTNn.png)

有使用到的 class 就只有這些，所以 Tailwind 會發現說我這支 HTML 裡面使用到的樣式只有這些，在我編譯的時候就會把其他的樣式刪除。

編譯可以輸入下方指令：

```cmd
npx tailwindcss -i ./src/tailwind.css -o ./dist/tailwind.css
```

編譯後就會看到 CSS 被壓縮到只剩下 10.58KB，是不是超棒的！

![complie](https://i.imgur.com/a6toAah.png)

使用此指令的話就是代表在 `production` 設定下才會做編譯，目前為了快速可以看到編譯效果，所以使用這段指令喔！更多設定指令的方式可以參考官方文件。

## Tailwind CSS 智能提示

官方有推薦 Visual Studio Code 套件可以使用，在套件區搜尋 Tailwind，就會找到此套件喔！

這樣就可以在打 class 名稱時使用智能提示，真的超級方便。

![](https://i.imgur.com/UBTMvLK.png)

如果無法使用 Tailwind 智能提示的話，資料夾裡面一定要要有 `tailwing.config.js` 以及在 `head` 裡面要放入編譯過後的 CSS 檔案喔！

## Tailwind CSS 升級須知

官方文件表示：不再支援 IE11 ~~(眾望所歸)~~

![](https://i.imgur.com/FbkAIrd.png)

中文的簡易意思就是說，之前官方為了維護 Tailwind 在 IE11 上可以運作，成本太高，所以只好放棄，但如果不幸專案上需要支援到 IE11，推薦使用 V1.9 版本，直到脫離 IE 後，就可以使用 V2.0 囉！

## 參考資料

- [Taiwind CSS 官方文件](https://tailwindcss.com/docs/installation)
- [【Tailwind CSS 教學 - 3 】別說 utility CSS 肥，壓縮起來連我自己都怕](https://ithelp.ithome.com.tw/articles/10243291)
