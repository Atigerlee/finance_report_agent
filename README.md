# AI 每日財經新聞與股市投資日報 (`AGENTS.md` 規則驅動專案)

本專案為「建立自己的 `AGENTS.md` / `CLAUDE.md`」課程作業成果。我們設計了一套**由規則驅動（Rule-Driven）、具備標準作業流程（SOP）的財經研究知識庫系統**，讓 AI Agent 能夠在不需要重新設計版面的情況下，每天持續蒐集真實市場數據、歸檔原始素材並發布風格一致的日報網頁。

---

## 📂 專案結構與檔案功能對照

```text
.
├── AGENTS.md                      # [核心規範] AI 員工手冊：定義角色、查核禁令、檔案命名、Markdown/HTML 範本與 4 步驟 SOP
├── skills/
│   └── report-generator.md        # [視覺規範] 定義單頁報告 6 大區塊、Tailwind CSS 樣式 Token 與台股紅漲綠跌語意表
├── index.html                     # [網站首頁] 內建 <!-- REPORT_CARDS_START --> 自動插入錨點、多空情緒篩選器與關鍵字搜尋
├── raw/                           # [原始數據存檔區] 存放每次網路搜尋查核後的結構化 Markdown 與新聞來源
│   ├── 2026-11-16-raw.md
│   └── 2026-11-13-raw.md
└── reports/                       # [正式日報網頁區] 存放依據 skills/ 規範生成的獨立單頁式 HTML 報告
    ├── 2026-11-16.html
    └── 2026-11-13.html
```

---

## 📝 作業繳交內容整理（可直接複製使用）

- **繳交標題格式**：`台大 [學號] [系級] [姓名] 每日財經新聞與股市投資日報`
- **GitHub Repository 連結**：`https://github.com/<你的GitHub帳號>/<你的Repo名稱>`
- **網頁連結 (GitHub Pages)**：`https://<你的GitHub帳號>.github.io/<你的Repo名稱>/`

### 1. 專案簡介
本專案建立了一個「AI 每日財經新聞與股市投資日報」自動化研究網站。不同於單次生成的靜態網頁，本專案透過 `AGENTS.md`（定義研究分析維度、真實數據查核規範、檔案命名與標準作業流程）搭配 `skills/report-generator.md`（定義單頁 HTML 視覺設計系統與台灣股市「紅漲綠跌」色彩語意），讓 AI 扮演「量化與總體財經研究助理」。每次只需對 AI 下達「請生成今日財經日報」，AI 便會自動上網檢索美股四大指數、台股加權指數、美債殖利率、黃金與重點財經新聞，依序產出原始查核記錄檔（`raw/YYYY-MM-DD-raw.md`）、獨立分析網頁（`reports/YYYY-MM-DD.html`），並自動在首頁（`index.html`）置頂插入最新日報卡片。

### 2. 簡短說明：如果之後要新增一個新的頁面或內容，你設計的規則可以如何幫助 AI 繼續完成？
當之後要新增任一交易日（例如 `2026-11-17`）的新日報頁面時，`AGENTS.md` 與 `skills/report-generator.md` 的規則能從以下四個層面幫助 AI 穩定、快速地接續開發：
1. **標準化 4 步驟流水線（SOP）與目錄分離**：`AGENTS.md` 明確規定「先搜尋查核存為 `raw/YYYY-MM-DD-raw.md` → 再讀取樣式規範生成 `reports/YYYY-MM-DD.html` → 最後更新 `index.html`」，讓 AI 清楚知道每次新增內容時要建立哪些檔案、放在哪個資料夾，不會遺漏步驟或破壞既有檔案。
2. **結構化資料範本與防幻覺限制**：`AGENTS.md` 定義了 `raw/` 的 YAML Frontmatter 與四大分析維度（跨資產市場總覽、3～5 則頭條新聞含一句話影響解讀、焦點產業個股、短中長線策略與風險），並強制要求透過網路搜尋取得真實數據與標註來源，確保新頁面內容品質與深度一致。
3. **模組化視覺與「台股紅漲綠跌」色彩規範**：`skills/report-generator.md` 統一規範了單頁報告的 6 大必備區塊、Tailwind CSS 卡片樣式、相對路徑規則（確保 GitHub Pages 相容）以及紅漲（`text-red-600`）、綠跌（`text-emerald-600`）、震盪（`text-amber-700`）的配色標準，讓新生成的頁面與舊頁面視覺風格完全統一，且自動串聯「前一交易日／下一交易日」雙向導覽按鈕。
4. **HTML 註解錨點（Anchor Comment）與首頁卡片模板**：`index.html` 中設有 `<!-- REPORT_CARDS_START -->` 標記，且 `AGENTS.md` 提供了包含 `data-sentiment="bullish|neutral|bearish"` 屬性的標準 `<article>` 卡片程式碼範本。AI 新增頁面後，只需在錨點正下方插入新卡片，即可讓新日報自動排在首頁最上方，並直接支援首頁的「偏多／震盪／偏空」即時篩選與關鍵字搜尋功能。
