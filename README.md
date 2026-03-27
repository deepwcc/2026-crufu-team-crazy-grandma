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
