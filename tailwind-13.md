---
title: Tailwind CSS - 新增自己的 Utility
tags:
  - TailwindCSS
categories: TailwindCSS
description: 預設沒有想要的功能，那我自己寫！
abbrlink: 2881787623
date: 2021-06-27 19:45:02
---
![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

除了可以新增元件外，也可以增加自訂義的功能。

雖然 TailwindCSS 已經提供非常多好用的 class，但還是會遇到需要自定義功能的情況，以下就介紹怎麼自訂義功能吧！

## 新增功能起手式

使用官方範例，可以看到跟新增元件的概念相似，告訴 `style.css` 要新增或覆寫哪一個圖層的內容，然後在裡面再撰寫想要的樣式內容。

**style.css**

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer utilities {
    .scroll-snap-none {
        scroll-snap-type: none;
    }
    .scroll-snap-x {
        scroll-snap-type: x;
    }
    .scroll-snap-y {
        scroll-snap-type: y;
    }
}
```

寫完後記得編譯，然後看一下 `tailwind.css` 是否有編譯成功。

**tailwind.css**

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer utilities {
    .scroll-snap-none {
        scroll-snap-type: none;
    }
    .scroll-snap-x {
        scroll-snap-type: x;
    }
    .scroll-snap-y {
        scroll-snap-type: y;
    }
}
```

> 這邊發現一個 bug，就是我在 HTML 沒有寫出對應的 class 時，似乎沒有辦法編譯成功在 `style.css` 自訂義的功能內容於 `tailwind.css` 的檔案中，所以要在 HTML 加上寫上此樣式的 class 名稱才能解決。

## 新增響應式功能

想要自響應式功能也非常方便，只要在圖層中加上 `@responsive` 就完成各種斷點，真是太狂了，如下方範例。

**style.css**

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer utilities {
    @variants responsive { /*加在這邊*/
      .scroll-snap-none {
        scroll-snap-type: none;
      }
      .scroll-snap-x {
        scroll-snap-type: x;
      }
      .scroll-snap-y {
        scroll-snap-type: y;
      }
    }
  }
```

在 HTML 也要寫上要使用的響應式斷點才能成功編譯，

**HTML**

```html
  <div class="scroll-snap-none sm:scroll-snap-x"></div>
```

**tailwind.css**

編譯後才會成功出現自訂義的內容，並且可以看到註解也會呈現在預設斷點的後方，代表有編譯成功。

```css
.scroll-snap-none {
  -ms-scroll-snap-type: none;
      scroll-snap-type: none;
}

@media (min-width: 640px) { /*加在這邊*/

  .sm\:scroll-snap-x {
    -ms-scroll-snap-type: x;
        scroll-snap-type: x;
  }
}

@media (min-width: 768px) { /*加在這邊*/
}

@media (min-width: 1024px) { /*加在這邊*/
}

@media (min-width: 1280px) { /*加在這邊*/
}

@media (min-width: 1536px) { /*加在這邊*/
}
```

## 新增偽類效果

之前有練習到可以在元件中建立偽類效果，那功能也會需要偽類效果，只要在 Utilites 裡面加上  `@variants hover, focus` 就可以了。

網頁最常出現就是按鈕滑鼠經過時會有個顏色轉換提示，下方練習為一個按鈕當我滑鼠經過時，會從紅色變為更深的紅色。

**HTML**

```html
 <button class="btn btn-red">click</button>
```

把想要新增的樣式寫在響應式裡面！讓我於響應式也可以吃到其效果。

**style.css**

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer utilities {
    @variants responsive {
        /*加在這邊*/
        @variants hover, focus {
            .btn {
                @apply px-4 py-2 rounded border-transparent text-white;
            }
            .btn-red {
                @apply bg-red-500 border-red-600 border-2;
            }
            .btn-hover {
                @apply bg-red-700;
            }
            .btn-focus {
                @apply border-red-400 border-2;
            }
        }
    }
}
```

編譯後就會看到 `tailwind.css` 也會有自訂義的樣式囉！

```css
.btn {
  border-color: transparent;
  border-radius: 0.25rem;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  padding-left: 1rem;
  padding-right: 1rem;
  --tw-text-opacity: 1;
  color: rgba(255, 255, 255, var(--tw-text-opacity));
}

.btn-red {
  --tw-bg-opacity: 1;
  background-color: rgba(239, 68, 68, var(--tw-bg-opacity));
  --tw-border-opacity: 1;
  border-color: rgba(220, 38, 38, var(--tw-border-opacity));
  border-width: 2px;
}

.hover\:btn-hover:hover {
  --tw-bg-opacity: 1;
  background-color: rgba(185, 28, 28, var(--tw-bg-opacity));
}

.focus\:btn-focus:focus {
  --tw-border-opacity: 1;
  border-color: rgba(248, 113, 113, var(--tw-border-opacity));
  border-width: 2px;
}
```

最後記得要把效果加回到按鈕的樣式中喔！

```html
 <button class="btn btn-red sm:hover:btn-hover focus:btn-focus">
            click
        </button>
```

**before hover**

![no hover](https://i.imgur.com/T6cik6m.png)

**after hover**

![after hover](https://i.imgur.com/V182y9G.png)

## 參考資料

* [TailwindCSS Adding New Utilities](https://tailwindcss.com/docs/adding-new-utilities)

* [【Tailwind CSS 教學 - 11】新增 Utilities 方式，讓您不缺各種 util CSS Class！](https://ithelp.ithome.com.tw/articles/10246240)