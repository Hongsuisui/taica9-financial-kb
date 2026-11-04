# AGENTS.md — 個人財金知識庫 (Financial Knowledge Base) 自動化運作規範手冊

本文件為「個人財金知識庫」網站之 AI 開發助手（AI Agent）作業規範。
當使用者提供每日 Podcast 逐字稿、新聞文字或個股動態時，AI Agent 必須嚴格遵循本規範進行內容萃取、HTML 報告生成以及 index.html 首頁更新。

---

## 1. 專案核心範疇與定位

1. **泰鼎-KY (4927)**：PCB 產業動態、泰國廠產能、季度與月度營收追蹤、毛利率與財務指標。
2. **游庭皓的財經皓角**：每日總體經濟分析、聯準會政策、通膨指標、總經趨勢解讀。
3. **股癌 Gooaye**：市場心法、個股消息面、產業觀察、投資情緒與風險控管。

---

## 2. AI 產出任務工作流 (Workflow)

當收到新輸入資料（逐字稿/新聞）時，AI Agent 需執行以下三階段任務：

### 階段一：內容深度萃取與交會點分析 (Daily Insight Synthesis)
- **總經重點**：萃取「財經皓角」之總經關鍵趨勢。
- **個股心法**：萃取「股癌」之操作心法與個股觀察。
- **泰鼎-KY 關聯**：若有相關 PCB 或供應鏈消息，進行深度對齊；若無，則更新最新營收或籌碼數據。
- **總經 x 心法交會點**：強制撰寫一段 100~150 字的「總經環境與個股操作心法之交叉驗證與策略總結」。

### 階段二：生成獨立單篇報告 (`reports/YYYY-MM-DD-report.html`)
- 檔名規範：`reports/YYYY-MM-DD-report.html` (例：`reports/2026-11-04-report.html`)。
- 視覺風格：日系簡潔雜誌風格 (Minimalist Japanese Tech-Journal Standard)，使用 Tailwind CSS CDNs，搭配乾淨白灰底、深灰文字與優雅的靛藍/木質調配色。
- 報告結構必須包含：
  1. 頁首（報告日期、主題標籤、返回首頁按鈕）
  2. 今日交會點摘要 (Daily Insight Synthesis)
  3. 泰鼎-KY (4927) 專題卡片
  4. 游庭皓每日總經解析
  5. 股癌市場心法與產業觀察
  6. LLM Wiki 財經專有名詞小卡（至少 2 個名詞解釋，含定義與實務應用）

### 階段三：提供首頁 (`index.html`) 更新程式碼片段
- 提供一段待插入 `index.html` 的 HTML 卡片片段，包含：
  - 日期、標題、摘要（100字內）
  - 相關標籤（#PODCAST, #泰鼎KY, #每日總經, #心法）
  - 連向該篇報告的超連結 `reports/YYYY-MM-DD-report.html`

---

## 3. 標籤與分類系統規範

所有報告與首頁卡片必須精準使用以下標籤：
- `#PODCAST`：包含 游庭皓 或 股癌 內容時必帶。
- `#泰鼎KY`：包含 泰鼎-KY (4927) 個股或 PCB 產業分析時必帶。
- `#每日總經`：包含 總體經濟、利率、通膨、央行政策 時必帶。
- `#心法`：包含 投資心法、風險控管、心理素質 時必帶。

---

## 4. LLM Wiki 財經字典標準格式

每篇報告末尾必須包含 2~3 個專有名詞卡片，格式如下：
```html
<div class="border-l-4 border-indigo-500 bg-slate-50 p-4 rounded-r shadow-sm">
  <h4 class="font-bold text-slate-800 text-base mb-1">【名詞名稱】英文/縮寫</h4>
  <p class="text-xs text-slate-600 mb-2"><strong>定義：</strong>簡單白話解釋。</p>
  <p class="text-xs text-slate-600"><strong>實務應用：</strong>在此次分析中代表的意義與觀測指標。</p>
</div>