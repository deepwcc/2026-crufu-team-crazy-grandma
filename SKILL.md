# SKILL.md — 北夸父網站設計規範

> 所有 HTML/CSS/JS 生成前，請先完整讀取此檔。

---

## 設計哲學

- **實用優先**：隊員在賽前、賽中用手機快速查找資訊，不是欣賞設計
- **清晰第一**：大字、高對比、少裝飾
- **零依賴**：不引入任何外部 JS 套件或 CSS 框架

---

## 色彩系統

### 語意色（亮色模式）

```css
:root {
  --color-bg:          #ffffff;
  --color-bg-secondary:#f5f5f0;
  --color-bg-card:     #ffffff;
  --color-border:      rgba(0,0,0,0.12);
  --color-text:        #1a1a1a;
  --color-text-muted:  #666666;

  /* 棒次難度語意色 */
  --color-easy:        #e8f5e9;  /* 清晨涼爽、第二天清晨 */
  --color-easy-text:   #2e7d32;
  --color-warn:        #fff3e0;  /* 開始熱、體力耗盡 */
  --color-warn-text:   #e65100;
  --color-danger:      #ffebee;  /* 正中午魔鬼區、難中之王 */
  --color-danger-text: #c62828;
  --color-night:       #ede7f6;  /* 夜間、跨夜路段 */
  --color-night-text:  #4527a0;

  /* 車組色 */
  --color-car-a:       #e3f2fd;
  --color-car-a-text:  #1565c0;
  --color-car-b:       #fce4ec;
  --color-car-b-text:  #880e4f;
}
```

### 深色模式

```css
@media (prefers-color-scheme: dark) {
  :root {
    --color-bg:          #121212;
    --color-bg-secondary:#1e1e1e;
    --color-bg-card:     #1e1e1e;
    --color-border:      rgba(255,255,255,0.12);
    --color-text:        #e8e8e8;
    --color-text-muted:  #999999;

    --color-easy:        #1b3a1c;
    --color-easy-text:   #81c784;
    --color-warn:        #3e2a00;
    --color-warn-text:   #ffb74d;
    --color-danger:      #3e1111;
    --color-danger-text: #ef9a9a;
    --color-night:       #1e1733;
    --color-night-text:  #b39ddb;

    --color-car-a:       #0d2137;
    --color-car-a-text:  #90caf9;
    --color-car-b:       #2d0a1a;
    --color-car-b-text:  #f48fb1;
  }
}
```

---

## 排版

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI",
               "PingFang TC", "Noto Sans TC", sans-serif;
  font-size: 16px;
  line-height: 1.6;
  color: var(--color-text);
  background: var(--color-bg);
}

/* 標題 */
h1 { font-size: 1.5rem; font-weight: 600; }
h2 { font-size: 1.2rem; font-weight: 600; }
h3 { font-size: 1rem;   font-weight: 600; }

/* 小標籤（棒次號、車組、難度） */
.badge {
  display: inline-block;
  font-size: 0.75rem;
  padding: 2px 8px;
  border-radius: 12px;
  font-weight: 500;
}
```

---

## 元件規範

### 導覽列（所有頁共用）

```html
<nav class="navbar">
  <a href="index.html" class="nav-brand">🏃 北夸父 2026</a>
  <div class="nav-links">
    <a href="legs.html">棒次表</a>
    <a href="runners.html">跑者</a>
    <a href="checklist.html">清單</a>
  </div>
</nav>
```

```css
.navbar {
  position: sticky;
  top: 0;
  z-index: 100;
  background: var(--color-bg);
  border-bottom: 1px solid var(--color-border);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.75rem 1rem;
}
.nav-links { display: flex; gap: 1rem; }
.nav-links a {
  font-size: 0.875rem;
  color: var(--color-text-muted);
  text-decoration: none;
}
.nav-links a.active { color: var(--color-text); font-weight: 600; }
```

### 棒次卡片

```html
<div class="leg-card feel-danger">
  <div class="leg-header">
    <span class="leg-no">棒13</span>
    <span class="runner-badge">溫泉</span>
    <span class="car-badge car-a">A車</span>
  </div>
  <div class="leg-stats">
    <span>6.6 km</span>
    <span>↑355 m</span>
    <span>↓188 m</span>
  </div>
  <div class="leg-meta">
    <span class="feel-badge">⚠️ 難中之王</span>
    <span class="time-badge">15:30–17:30</span>
  </div>
  <div class="leg-terrain">難中之王 / 照明 / 多彎 / 山景</div>
</div>
```

```css
.leg-card {
  background: var(--color-bg-card);
  border: 1px solid var(--color-border);
  border-radius: 12px;
  padding: 12px 14px;
  margin-bottom: 8px;
}
.leg-card.feel-easy   { border-left: 4px solid var(--color-easy-text); }
.leg-card.feel-warn   { border-left: 4px solid var(--color-warn-text); }
.leg-card.feel-danger { border-left: 4px solid var(--color-danger-text); }
.leg-card.feel-night  { border-left: 4px solid var(--color-night-text); }

.leg-header {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 6px;
}
.leg-no {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--color-text);
  min-width: 40px;
}
.leg-stats {
  display: flex;
  gap: 12px;
  font-size: 0.875rem;
  color: var(--color-text-muted);
  margin-bottom: 6px;
}
.leg-terrain {
  font-size: 0.8rem;
  color: var(--color-text-muted);
  margin-top: 4px;
}
```

### 跑者卡片

```html
<div class="runner-card">
  <div class="runner-avatar" style="background:var(--color-car-a);color:var(--color-car-a-text)">溫</div>
  <div class="runner-info">
    <div class="runner-name">溫泉 <span class="car-badge car-a">A車</span></div>
    <div class="runner-legs">棒 3、13、23</div>
  </div>
  <div class="runner-stats">
    <div><span class="stat-val">20.8</span><span class="stat-unit">km</span></div>
    <div><span class="stat-val">↑438</span><span class="stat-unit">m</span></div>
  </div>
</div>
```

### 清單項目

```html
<label class="cl-item">
  <input type="checkbox" class="cl-cb" data-key="reg-1">
  <div class="cl-check-box"></div>
  <div class="cl-item-body">
    <div class="cl-item-title">完成線上報名繳費</div>
    <div class="cl-item-desc">前往 focusline.com.tw/260411HC</div>
  </div>
</label>
```

---

## 棒次難度分類邏輯

```js
function feelClass(feel) {
  if (feel.includes('魔鬼') || feel.includes('難中之王') || feel.includes('正中午')) return 'danger';
  if (feel.includes('開始熱') || feel.includes('體力耗盡')) return 'warn';
  if (feel.includes('夜') || feel.includes('跨夜')) return 'night';
  return 'easy';
}
```

---

## RWD 斷點

```css
/* 手機（預設）：單欄 */
.grid { display: grid; grid-template-columns: 1fr; gap: 8px; }

/* 平板以上：雙欄 */
@media (min-width: 640px) {
  .grid { grid-template-columns: 1fr 1fr; }
}

/* 桌機：三欄 */
@media (min-width: 1024px) {
  .grid { grid-template-columns: 1fr 1fr 1fr; }
}
```

---

## index.html 主頁內容規格

主頁顯示以下區塊（由上到下）：

1. **Hero 區** — 隊名、活動日期、路線簡述
2. **總覽卡片** — 總里程 202km、30棒、10人、約30小時
3. **A車/B車分組** — 快速連結各跑者
4. **高難度警示** — 棒13/9/10/19/24/27 的紅色警告卡
5. **報名連結** — 按鈕連至 focusline.com.tw/260411HC

---

## checklist.html localStorage 規格

```js
const STORAGE_KEY = 'crufu_checklist_2026';

// 讀取
const saved = JSON.parse(localStorage.getItem(STORAGE_KEY) || '{}');

// 儲存（每次 checkbox 變動時）
function saveChecklist() {
  const state = {};
  document.querySelectorAll('.cl-cb').forEach(cb => {
    state[cb.dataset.key] = cb.checked;
  });
  localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
}
```
