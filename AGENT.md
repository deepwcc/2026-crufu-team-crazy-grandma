# AGENT.md — Claude Code Agent 任務分工

> Claude Code 請依序執行以下 Agent 任務。每個 agent 完成後才進行下一個。

---

## 執行順序

```
1. data-agent    → 生成 data.js（所有資料，其他 agent 依賴此檔）
2. style-agent   → 生成 style.css
3. page-agent    → 生成 index.html
4. legs-agent    → 生成 legs.html
5. runner-agent  → 生成 runners.html
6. check-agent   → 生成 checklist.html
7. deploy-agent  → 生成 README.md，輸出部署指令
```

---

## Agent 1：data-agent

**任務：** 生成 `data.js`，包含網站所需的全部資料。

**輸出：** `data.js`

**規格：**

```js
// data.js — 北夸父2026 所有資料

const RUNNERS = [
  { name:"崧",   car:"A", legs:[1,11,21], km:20.7, up:277, dn:222 },
  { name:"宜臻", car:"A", legs:[2,12,22], km:21.0, up:419, dn:174 },
  { name:"溫泉", car:"A", legs:[3,13,23], km:20.8, up:438, dn:513 },
  { name:"勳",   car:"A", legs:[4,14,24], km:22.3, up:426, dn:378 },
  { name:"浩安", car:"A", legs:[5,15,25], km:21.5, up:153, dn:435 },
  { name:"June", car:"B", legs:[6,20,28], km:20.0, up:148, dn:636 },
  { name:"Dean", car:"B", legs:[7,17,26], km:19.9, up:231, dn:227 },
  { name:"鍾誠", car:"B", legs:[8,19,29], km:22.5, up:396, dn:173 },
  { name:"凱欣", car:"B", legs:[9,18,30], km:19.5, up:199, dn:239 },
  { name:"凱",   car:"B", legs:[10,16,27],km:21.2, up:481, dn:192 },
];

const LEGS = [
  { no:1,  km:6.7, up:67,  dn:87,  terrain:"wc / 白天",                    time:"06:00-10:00", feel:"清晨涼爽",       runner:"崧",   car:"A" },
  { no:2,  km:7.7, up:23,  dn:29,  terrain:"加油站/餐廳/wc/白天",           time:"06:00-10:00", feel:"清晨涼爽",       runner:"宜臻", car:"A" },
  { no:3,  km:6.6, up:19,  dn:19,  terrain:"路橋/加油站/wc/白天",           time:"06:00-10:00", feel:"清晨涼爽",       runner:"溫泉", car:"A" },
  { no:4,  km:7.1, up:24,  dn:25,  terrain:"wc / 白天",                    time:"06:00-10:00", feel:"清晨涼爽",       runner:"勳",   car:"A" },
  { no:5,  km:7.7, up:37,  dn:36,  terrain:"wc/海景/餐廳/白天",             time:"06:00-10:00", feel:"清晨涼爽",       runner:"浩安", car:"A" },
  { no:6,  km:6.2, up:38,  dn:36,  terrain:"wc/海景/餐廳/白天",             time:"10:00-12:30", feel:"開始熱了",       runner:"June", car:"B" },
  { no:7,  km:6.2, up:39,  dn:39,  terrain:"加油站/海景/wc/白天",           time:"10:00-12:30", feel:"開始熱了",       runner:"Dean", car:"B" },
  { no:8,  km:7.2, up:67,  dn:49,  terrain:"加油站/海景/白天",              time:"10:00-12:30", feel:"開始熱了",       runner:"鍾誠", car:"B" },
  { no:9,  km:6.8, up:82,  dn:81,  terrain:"海景 / 白天",                  time:"12:30-15:30", feel:"正中午魔鬼區",   runner:"凱欣", car:"B" },
  { no:10, km:8.2, up:75,  dn:96,  terrain:"海景/wc/餐廳/白天",             time:"12:30-15:30", feel:"正中午魔鬼區",   runner:"凱",   car:"B" },
  { no:11, km:7.4, up:108, dn:94,  terrain:"餐廳/wc/白天",                  time:"12:30-15:30", feel:"正中午魔鬼區",   runner:"崧",   car:"A" },
  { no:12, km:6.4, up:112, dn:43,  terrain:"wc / 白天",                    time:"15:30-17:30", feel:"接近傍晚",       runner:"宜臻", car:"A" },
  { no:13, km:6.6, up:355, dn:188, terrain:"難中之王/照明/多彎/山景",        time:"15:30-17:30", feel:"難中之王",       runner:"溫泉", car:"A" },
  { no:14, km:8.2, up:107, dn:303, terrain:"照明/車多/夜間",                time:"17:30-22:30", feel:"入夜涼爽",       runner:"勳",   car:"A" },
  { no:15, km:6.7, up:66,  dn:107, terrain:"wc/海景/車多/夜間",             time:"17:30-22:30", feel:"入夜涼爽",       runner:"浩安", car:"A" },
  { no:16, km:5.4, up:87,  dn:85,  terrain:"照明/wc/夜間",                  time:"17:30-22:30", feel:"入夜涼爽",       runner:"凱",   car:"B" },
  { no:17, km:6.7, up:97,  dn:90,  terrain:"多彎/加油站/wc/夜間",           time:"17:30-22:30", feel:"入夜涼爽",       runner:"Dean", car:"B" },
  { no:18, km:7.3, up:98,  dn:107, terrain:"加油站/照明/餐廳/wc/夜間",      time:"17:30-22:30", feel:"入夜涼爽",       runner:"凱欣", car:"B" },
  { no:19, km:6.6, up:208, dn:39,  terrain:"多彎/山景/照明/夜間",           time:"22:30-06:30", feel:"深夜跨夜路段",   runner:"鍾誠", car:"B" },
  { no:20, km:7.1, up:106, dn:286, terrain:"多彎 / 夜間",                   time:"22:30-06:30", feel:"深夜跨夜路段",   runner:"June", car:"B" },
  { no:21, km:6.6, up:102, dn:41,  terrain:"照明/海景/夜間",                time:"22:30-06:30", feel:"深夜跨夜路段",   runner:"崧",   car:"A" },
  { no:22, km:6.9, up:284, dn:102, terrain:"多彎/山景/夜間",                time:"22:30-06:30", feel:"深夜跨夜路段",   runner:"宜臻", car:"A" },
  { no:23, km:7.6, up:64,  dn:306, terrain:"多彎/照明/加油站/夜間",         time:"22:30-06:30", feel:"深夜跨夜路段",   runner:"溫泉", car:"A" },
  { no:24, km:7.0, up:295, dn:50,  terrain:"多彎/山景/車多/夜間",           time:"22:30-06:30", feel:"深夜跨夜路段",   runner:"勳",   car:"A" },
  { no:25, km:7.1, up:50,  dn:292, terrain:"海景/wc/夜間",                  time:"22:30-06:30", feel:"深夜跨夜路段",   runner:"浩安", car:"A" },
  { no:26, km:7.0, up:95,  dn:98,  terrain:"加油站/海景/餐廳/白天",         time:"06:30-07:45", feel:"第二天清晨",     runner:"Dean", car:"B" },
  { no:27, km:7.6, up:319, dn:11,  terrain:"加油站/山景/白天",              time:"07:45-10:15", feel:"體力耗盡開始熱", runner:"凱",   car:"B" },
  { no:28, km:6.7, up:4,   dn:314, terrain:"海景/wc/白天",                  time:"07:45-10:15", feel:"體力耗盡開始熱", runner:"June", car:"B" },
  { no:29, km:8.7, up:121, dn:85,  terrain:"加油站/餐廳/車多/白天",         time:"10:15-12:30", feel:"第二天正中午",   runner:"鍾誠", car:"B" },
  { no:30, km:5.4, up:19,  dn:51,  terrain:"wc/海景/白天",                  time:"10:15-12:30", feel:"第二天正中午",   runner:"凱欣", car:"B" },
];

const HIGH_RISK_LEGS = [13, 9, 10, 19, 24, 27];

const CHECKLIST = [
  {
    id: "reg",
    icon: "📋",
    title: "報名 & 費用",
    items: [
      { key:"reg-1", title:"確認10人名單正確", desc:"崧/宜臻/溫泉/勳/浩安/June/Dean/鍾誠/凱欣/凱" },
      { key:"reg-2", title:"完成線上報名繳費", desc:"focusline.com.tw/260411HC" },
      { key:"reg-3", title:"確認衣服尺寸", desc:"10人各自提交尺寸" },
      { key:"reg-4", title:"決定隊名", desc:"填入報名表" },
    ]
  },
  {
    id: "car",
    icon: "🚗",
    title: "車輛安排",
    items: [
      { key:"car-1", title:"A車：崧/宜臻/溫泉/勳/浩安", desc:"確認司機（至少1位有駕照）" },
      { key:"car-2", title:"B車：June/Dean/鍾誠/凱欣/凱", desc:"確認司機（至少1位有駕照）" },
      { key:"car-3", title:"下載離線地圖", desc:"宜蘭→淡水濱海路線30接力點" },
      { key:"car-4", title:"建立A/B車即時通訊群", desc:"兩車隨時保持聯繫" },
    ]
  },
  {
    id: "gear",
    icon: "🎒",
    title: "裝備 & 補給",
    items: [
      { key:"gear-1", title:"頭燈 & 備用電池（全員）", desc:"棒14–25均為夜間路段" },
      { key:"gear-2", title:"反光背心（夜間跑者）", desc:"夜間車多路段強制穿著" },
      { key:"gear-3", title:"食物 & 飲水補給（2日份）", desc:"兩輛車各備充足補給" },
      { key:"gear-4", title:"急救包 / 肌貼 / 防曬乳", desc:"OK繃、止痛藥、運動貼布" },
      { key:"gear-5", title:"保暖外套（跨夜備用）", desc:"凌晨氣溫偏低" },
      { key:"gear-6", title:"行動電源", desc:"賽程約30小時，手機滿電出發" },
    ]
  },
  {
    id: "stay",
    icon: "🏨",
    title: "住宿安排",
    items: [
      { key:"stay-1", title:"預訂 4/10 晚宜蘭住宿", desc:"靠近起點武荖坑風景區" },
      { key:"stay-2", title:"預訂完賽慶功餐廳", desc:"淡水老街附近，4/12 中午後" },
    ]
  },
  {
    id: "race",
    icon: "🏃",
    title: "賽前確認",
    items: [
      { key:"race-1", title:"攜帶身分證 & 健保卡", desc:"報到時需出示身分證明" },
      { key:"race-2", title:"確認報到時間地點", desc:"起跑前至少1小時到達宜蘭武荖坑" },
      { key:"race-3", title:"棒次跑序最終確認", desc:"10人30棒分工，以本檔資料為準" },
      { key:"race-4", title:"各自完成賽前訓練", desc:"建議各自先跑10km以上" },
    ]
  },
];
```

---

## Agent 2：style-agent

**任務：** 生成 `style.css`

**規格：**
- 完整實作 SKILL.md 的色彩系統（含深色模式）
- 實作所有元件：navbar、leg-card、runner-card、cl-item、badge
- mobile-first，包含 640px / 1024px 斷點
- 無任何外部依賴

---

## Agent 3：page-agent

**任務：** 生成 `index.html`（主頁）

**頁面結構：**
1. `<head>` — charset UTF-8、viewport、title「北夸父2026 | 夸父追日接力賽」、link style.css + data.js
2. 導覽列（active: 首頁）
3. Hero 區 — 大標題、活動日期「2026/4/11–12」、路線「宜蘭 → 淡水｜202km｜30棒」
4. 總覽卡片列（4張：總里程、總棒次、隊員、預計時長）
5. 高難度警示區塊（從 `HIGH_RISK_LEGS` 動態渲染）
6. A車/B車跑者快速總覽（小卡片，點擊跳至 runners.html#跑者名）
7. Footer：報名連結按鈕 + 大會網站連結

**JS 邏輯：** 從 `data.js` 讀取 `RUNNERS`、`LEGS`、`HIGH_RISK_LEGS` 動態渲染，不硬編碼 HTML

---

## Agent 4：legs-agent

**任務：** 生成 `legs.html`（30棒次詳細表）

**頁面結構：**
1. 導覽列（active: 棒次表）
2. 篩選列：
   - 全部 / A車 / B車（按車組篩選）
   - 下拉選單：依跑者篩選（從 RUNNERS 動態生成選項）
   - 難度篩選：全部 / 清晨好跑 / 注意 / 危險 / 夜間
3. 棒次卡片列表（從 `LEGS` 動態渲染，套用 `feelClass()` 對應樣式）
4. 每張卡片點擊展開「注意事項」（高難度棒次顯示額外提示文字）

**JS 邏輯：**
- 篩選邏輯純前端，不需要 fetch
- 篩選後即時更新顯示數量「顯示 X / 30 棒」

---

## Agent 5：runner-agent

**任務：** 生成 `runners.html`（10人跑者資訊）

**頁面結構：**
1. 導覽列（active: 跑者）
2. A車 / B車 分區標題
3. 每位跑者一張完整卡片，含：
   - 名字 + 車組標籤
   - 總里程、總爬升、總下降
   - 3個棒次的詳細資訊（距離、時段、地形、難度標籤）
   - 高難度棒次以紅色邊框警示
4. 每張卡片有 `id="runner-{name}"` 供 index.html 錨點連結

---

## Agent 6：check-agent

**任務：** 生成 `checklist.html`（籌備清單）

**頁面結構：**
1. 導覽列（active: 清單）
2. 進度條（已完成 N / 總項目 M）
3. 各分類清單（從 `CHECKLIST` 動態渲染）
4. 「全部重置」按鈕

**JS 規格：**
- 使用 `localStorage`（key: `crufu_checklist_2026`）
- 頁面載入時恢復上次勾選狀態
- 每次勾選立即儲存

---

## Agent 7：deploy-agent

**任務：** 生成 `README.md`，並在 terminal 輸出部署指令

**README.md 內容：**

```markdown
# 北夸父2026 — 隊員網站

CRUFU RUN 夸父追日跨夜接力賽（北臺灣站）隊伍資訊網站。

## 本地預覽

```bash
npx serve .
# 或
python3 -m http.server 8080
```

## 部署到 GitHub Pages

```bash
git init
git add .
git commit -m "init: 北夸父2026隊伍網站"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/crufu-run-2026.git
git push -u origin main
```

然後到 GitHub repo → Settings → Pages → Branch: main / (root) → Save

網站將在幾分鐘後上線：`https://YOUR_USERNAME.github.io/crufu-run-2026/`

## 頁面說明

| 頁面 | 功能 |
|------|------|
| index.html | 首頁總覽、高難度警示、A/B車分組 |
| legs.html | 30棒次詳細表，可篩選 |
| runners.html | 10位跑者各自棒次資訊 |
| checklist.html | 籌備清單，狀態自動儲存 |
```

**部署指令（直接執行）：**

```bash
# deploy-agent 執行以下指令
git add .
git status
echo "✅ 檔案確認完畢，請執行以下指令部署："
echo "git commit -m 'init: 北夸父2026隊伍網站'"
echo "git push -u origin main"
```

---

## 注意事項

- 所有 agent 完成後，執行 `npx serve .` 本地預覽，確認無 console error
- 每個 `.html` 必須引入 `style.css` 和 `data.js`（`<script src="data.js"></script>` 放 `</body>` 前）
- 不允許內嵌任何硬編碼跑者/棒次資料，一律從 `data.js` 讀取
- 棒次13（溫泉）的注意事項展開文字：「爬升355m，全程最高難度路段。出發前充分熱身，全程控速，每30分鐘補水一次。」
