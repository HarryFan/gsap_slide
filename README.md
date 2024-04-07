# 輪播圖功能技術文件

## 概述

此技術文件旨在說明一個簡單的輪播圖功能，包括其基本結構、樣式和互動行為。該輪播圖功能支援通過上一張（Previous）和下一張（Next）按鈕來導覽圖片。

## HTML結構

```html
<div class="carousel-container">
    <div class="carousel">
        <div class="slide"><img src="1.jpg" alt="圖片說明 1"></div>
        <div class="slide"><img src="2.jpg" alt="圖片說明 2"></div>
        <div class="slide"><img src="3.jpg" alt="圖片說明 3"></div>
    </div>
</div>
<button class="pre">上一張</button>
<button class="next">下一張</button>
```

- `carousel-container`: 用於包含輪播圖的外部容器，設定了輪播圖的寬度和溢出行為。
- `carousel`: 包含所有幻燈片的容器，使用 flex 佈局使幻燈片橫向排列。
- `slide`: 個別幻燈片的容器，每個容器內包含一個 `img` 元素。
- `pre` 和 `next` 按鈕用於控制輪播圖的前後切換。

## CSS樣式

```css
.carousel-container {
    width: 100%;
    max-width: 600px;
    margin: auto;
    overflow: hidden;
}

.carousel {
    display: flex;
}

.slide {
    min-width: 100%;
    box-sizing: border-box;
}

img {
    width: 100%;
    height: auto;
    display: block;
}

.pre, .next {
    cursor: pointer;
}
```

- 輪播容器 (`carousel-container`) 設置了最大寬度和自動邊距，以置中顯示。
- 輪播元素 (`carousel`) 使用 flex 佈局來實現橫向排列的幻燈片。
- 每個幻燈片 (`slide`) 被設置為至少與輪播容器同寬。
- 圖片 (`img`) 設置為 100% 寬度，使其自適應容器大小。
- 上一張和下一張按鈕設置了指標光標，提高用戶體驗。

## JavaScript 互動

```javascript
let carouselIndex = 0;
const carousel = document.querySelector(".carousel");
const slides = document.querySelectorAll(".slide");
const slideWidth = slides[0].clientWidth;

function updateCarousel() {
    gsap.to(carousel, {duration: 0.5, x: -slideWidth * carouselIndex});
}

document.querySelector(".pre").addEventListener('click', () => {
    carouselIndex = carouselIndex === 0 ? slides.length - 1 : carouselIndex - 1;
    updateCarousel();
});

document.querySelector(".next").addEventListener('click', () => {
    carouselIndex = carouselIndex === slides.length - 1 ? 0 : carouselIndex + 1;
    updateCarousel();
});
```

- 使用 GSAP 函式庫來實現平滑的動畫效果。
- `carouselIndex` 用於追蹤目前顯示的幻燈片索引。
- `updateCarousel` 函數用於更新輪播圖的位置。
- 為 `pre` 和 `next` 按鈕新增點擊事件，用於更新 `carouselIndex` 並呼叫 `updateCarousel` 函數以切換幻燈片。

## 功能流程

1. 當使用者點擊「下一張」按鈕時，`carouselIndex` 增加，輪播圖移動到下一

張圖片。
2. 當使用者點擊「上一張」按鈕時，`carouselIndex` 減少，輪播圖移動到上一張圖片。
3. 輪播圖能夠循環播放，即從最後一張自動回到第一張，反之亦然。

## 結語

此技術文件描述了輪播圖的實現方式，包括其結構、樣式和互動功能。通過使用 HTML、CSS 和 JavaScript，我們建立了一個基本的輪播圖系統，能夠響應使用者的操作進行圖片切換。