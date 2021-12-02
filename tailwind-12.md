---
title: Tailwind CSS - 元件相同時，把共同樣式拉出來
tags:
  - TailwindCSS
categories: TailwindCSS
description: 有多個相同樣式，可以再細分出來
abbrlink: 3362003898
date: 2021-06-27 19:33:29
---
![tailwindcss](https://tools.wingzero.tw/assets/upload/1611643654838_0.jpg)

## 單一按鈕樣式元件

[前篇](https://hsuchihting.github.io/TailwindCSS/20210627/2585108082/)有寫到單一按鈕，可以把樣式拆成元件來使用。如下：

```css
@layer components{
  .btn-green {
    @apply py-2 px-4 bg-green-500 text-white font-semibold rounded-lg shadow-md;
  }
  .btn-green:hover {
    @apply bg-green-700;
  }
  .btn-green:focus {
    @apply outline-none ring-2 ring-green-400 ring-opacity-75;
  }
}
```

如果今天我有兩個按鈕，一個綠色一個藍色，依照上述概念，似乎要寫成這樣：

```css
@layer components{
  .btn-green {
    @apply py-2 px-4 bg-green-500 text-white font-semibold rounded-lg shadow-md;
  }
  .btn-green:hover {
    @apply bg-green-700;
  }
  .btn-green:focus {
    @apply outline-none ring-2 ring-green-400 ring-opacity-75;
  }

  .btn-blue {
    @apply py-2 px-4 bg-blue-500 text-white font-semibold rounded-lg shadow-md;
  }
  .btn-blue:hover {
    @apply bg-blue-700;
  }
  .btn-blue:focus {
    @apply outline-none ring-2 ring-blue-400 ring-opacity-75;
  }
}
```

其實我就是複製同一串樣式，然後把顏色改掉，如此而已，當然畫面也是會有同樣效果啦...

![btn](https://i.imgur.com/zVLhF42.png)

可是如果今天畫面有五顆按鈕，那我顏色就要改五次，同樣的程式碼要複製五次，這樣如果樣式越來越多就越來越難維護跟閱讀。

## 元件中再抽共用元件

後來觀察，這跟 Bootstrap 有一點點異曲同工之妙，也就是可以再把按鈕的共同樣式拆出來，變成 `.btn` 去單獨處理按鈕，顏色之後再填上。

**template**

```html
    <button class="btn btn-green">Click me</button>
        <button class="btn btn-blue">Click me</button>
```

**style.css**

```css
@layer components {
    .btn {
        @apply py-2 px-4 text-white font-semibold rounded-lg shadow-md;
    }
    .btn:focus {
        @apply outline-none ring-2 ring-opacity-75;
    }
    .btn-green {
        @apply bg-green-500;
    }
    .btn-green:hover {
        @apply bg-green-700;
    }
    .btn-green:focus {
        @apply ring-green-400;
    }

    .btn-blue {
        @apply bg-blue-500;
    }
    .btn-blue:hover {
        @apply bg-blue-700;
    }
    .btn-blue:focus {
        @apply ring-blue-400;
    }
}
```

雖然看起來樣式變多了，可是細看會發現每個都單純管理自己的內容，這樣要修正相對好變動，不用擔心改錯了，其他也被影響到！

也順便檢查 `tailwind.css` 編譯後的 CSS 有沒有成功，看來是有成功編譯囉！

**tailwind.css**

```css
.btn {
  border-radius: 0.5rem;
  font-weight: 600;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  padding-left: 1rem;
  padding-right: 1rem;
  --tw-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  box-shadow: var(--tw-ring-offset-shadow, 0 0 #0000), var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow);
  --tw-text-opacity: 1;
  color: rgba(255, 255, 255, var(--tw-text-opacity));
}

.btn:focus {
  outline: 2px solid transparent;
  outline-offset: 2px;
  --tw-ring-offset-shadow: var(--tw-ring-inset) 0 0 0 var(--tw-ring-offset-width) var(--tw-ring-offset-color);
  --tw-ring-shadow: var(--tw-ring-inset) 0 0 0 calc(2px + var(--tw-ring-offset-width)) var(--tw-ring-color);
  box-shadow: var(--tw-ring-offset-shadow), var(--tw-ring-shadow), var(--tw-shadow, 0 0 #0000);
  --tw-ring-opacity: 0.75;
}

.btn-green {
  --tw-bg-opacity: 1;
  background-color: rgba(16, 185, 129, var(--tw-bg-opacity));
}

.btn-green:hover {
  --tw-bg-opacity: 1;
  background-color: rgba(4, 120, 87, var(--tw-bg-opacity));
}

.btn-green:focus {
  --tw-ring-opacity: 1;
  --tw-ring-color: rgba(52, 211, 153, var(--tw-ring-opacity));
}

.btn-blue {
  --tw-bg-opacity: 1;
  background-color: rgba(59, 130, 246, var(--tw-bg-opacity));
}

.btn-blue:hover {
  --tw-bg-opacity: 1;
  background-color: rgba(29, 78, 216, var(--tw-bg-opacity));
}

.btn-blue:focus {
  --tw-ring-opacity: 1;
  --tw-ring-color: rgba(96, 165, 250, var(--tw-ring-opacity));
}
```

畫面也有成功渲染！

![buttons](https://i.imgur.com/eIX75nR.png)