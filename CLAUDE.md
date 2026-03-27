# CLAUDE.md — 北夸父隊 GitHub Pages 專案指引

> Claude Code 啟動時請先讀取此檔，再讀取 SKILL.md 與 AGENT.md。

---

## 專案概述

**目標：** 建立一個靜態 GitHub Pages 網站，供北夸父路跑隊 10 位隊員賽前查看棒次、補給、裝備資訊。  
**活動：** 2026/4/11–12 CRUFU RUN 夸父追日跨夜接力賽（北臺灣站）  
**路線：** 宜蘭武荖坑風景區 → 淡水（約 202 km，30 棒）  
**隊員：** 崧、宜臻、溫泉、勳、浩安（A車）／June、Dean、鍾誠、凱欣、凱（B車）

---

## 技術規格

- **框架：** 純 HTML + CSS + 原生 JS（無 build step，直接 `git push` 即部署）
- **部署：** GitHub Pages（`gh-pages` branch 或 `docs/` 資料夾）
- **入口：** `index.html`
- **樣式：** 單一 `style.css`，mobile-first，支援深色模式（`prefers-color-scheme`）
- **字體：** 系統字體堆疊（無需外部載入）
- **禁止：** 不使用任何需要 build 的框架（React、Vue、Next.js 等）

## 檔案結構

```
/
├── index.html          # 主頁（總覽）
├── style.css           # 全站樣式
├── data.js             # 所有資料（棒次、跑者、清單）
├── legs.html           # 30棒次詳細表
├── runners.html        # 10人跑者資訊
├── checklist.html      # 籌備清單（可打勾，localStorage 儲存）
└── README.md           # 部署說明
```

---

## 資料來源（北夸父_.csv 整理後）

### 跑者與棒次分配

| 跑者 | 車組 | 負責棒次 | 總里程(km) | 總爬升(m) | 總下降(m) |
|------|------|----------|-----------|----------|----------|
| 崧   | A    | 1, 11, 21 | 20.7 | 277 | 222 |
| 宜臻 | A    | 2, 12, 22 | 21.0 | 419 | 174 |
| 溫泉 | A    | 3, 13, 23 | 20.8 | 438 | 513 |
| 勳   | A    | 4, 14, 24 | 22.3 | 426 | 378 |
| 浩安 | A    | 5, 15, 25 | 21.5 | 153 | 435 |
| June | B    | 6, 20, 28 | 20.0 | 148 | 636 |
| Dean | B    | 7, 17, 26 | 19.9 | 231 | 227 |
| 鍾誠 | B    | 8, 19, 29 | 22.5 | 396 | 173 |
| 凱欣 | B    | 9, 18, 30 | 19.5 | 199 | 239 |
| 凱   | B    | 10, 16, 27 | 21.2 | 481 | 192 |

### 30 棒次資料（完整）

```js
// 詳見 data.js — legs 陣列
// 欄位：no, km, up, dn, terrain, time, feel, runner, car
```

見 `data.js` 中的 `LEGS` 陣列（由 AGENT.md 的 data-agent 生成）。

---

## 重要警示棒次

| 棒次 | 跑者 | 原因 | 注意事項 |
|------|------|------|----------|
| 棒13 | 溫泉 | 爬升355m，難中之王 | 充分熱身、多帶水 |
| 棒9  | 凱欣 | 正中午魔鬼區 | 防曬、帽子、補水 |
| 棒10 | 凱   | 正中午魔鬼區 | 同上 |
| 棒19 | 鍾誠 | 深夜，爬升208m | 頭燈、反光背心 |
| 棒24 | 勳   | 深夜，爬升295m | 頭燈、保暖 |
| 棒27 | 凱   | 第二天體力耗盡，爬升319m | 肌貼、補給充足 |

---

## 開發規範

1. **所有文字使用繁體中文**，專有名詞（GitHub、CSS 等）保留英文
2. **mobile-first**：主要使用者在手機上查看
3. **離線友善**：不依賴外部 CDN（字體、框架均本地或系統）
4. **localStorage** 用於 checklist 狀態儲存（key: `crufu_checklist`）
5. 每頁頂部固定導覽列，底部顯示「A車 | B車」分組標籤

---

## 快速開始（給 Claude Code）

```bash
# 1. 初始化
git init crufu-run-2026
cd crufu-run-2026

# 2. 建立所有檔案（參照 AGENT.md 分工）
# agent: data-agent → 生成 data.js
# agent: ui-agent   → 生成 index.html, style.css
# agent: page-agent → 生成 legs.html, runners.html, checklist.html

# 3. 部署
git add .
git commit -m "init: 北夸父2026隊伍網站"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/crufu-run-2026.git
git push -u origin main
# 然後在 GitHub repo Settings → Pages → Source: main / (root)
```

---

## 完成標準

- [ ] 手機上所有頁面可正常瀏覽
- [ ] 棒次表可依「跑者」篩選
- [ ] checklist 打勾狀態重整後仍保留
- [ ] 高難度棒次有紅色警示標籤
- [ ] 深色模式自動切換
