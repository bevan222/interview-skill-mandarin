# Interview Skill Mandarin

這個 repo 收錄一個 Codex skill：`tailor-interview-questions`。

它適合用在中文面試準備情境，能根據使用者提供的 JD 與履歷，從面試官角度產生面試問題；也能在使用者回答題目後，針對回答進行評分、分析，並輸出可閱讀的 HTML 報告。

## Skill 功能

### 1. 產生面試問題

當使用者提供：

- JD / 職缺描述
- 履歷、CV、LinkedIn、作品集或候選人背景
- 特別想準備的方向，例如策略、MVP、TPM、技術架構、產品風控

skill 會：

- 萃取 JD 的核心招募訊號
- 萃取履歷中的專案、經歷、技能、成果與潛在缺口
- 盡可能覆蓋 JD 與履歷中的重要內容
- 從面試官視角產生至少 10 題面試問題
- 將有前後關係的問題放在同一組 interview thread，不會零散排列
- 標示每題的觀察點與依據

### 2. 分析使用者答題

當使用者針對題目回答，例如：

```text
1. 我的回答是...
2. 我的回答是...
```

skill 會逐題分析：

- 顯示原始問題與使用者回答
- 針對 `Logic Consistency` 評分，0 到 100 分
- 針對 `Conciseness` 評分，0 到 100 分
- 給出 `Overall Score`
- 從 Expert Perspective 分析回答好在哪裡、缺了什麼
- 提供 Strategic Framework，告訴使用者應該用什麼結構回答
- 提供 Ideal Logic Roadmap，拆解滿分回答應該包含的關鍵點
- 提供 Standard Professional Answer，示範一個具體、有邏輯、但不會過度文鄒鄒的面試回答
- 輸出靜態 HTML 報告，讓使用者可以切換每一題閱讀分析

## 安裝方式

將 skill 資料夾複製到 Codex skills 目錄：

```bash
git clone https://github.com/bevan222/interview-skill-mandarin.git
mkdir -p ~/.codex/skills
cp -R interview-skill-mandarin/tailor-interview-questions ~/.codex/skills/
```

安裝後，skill 路徑應該像這樣：

```text
~/.codex/skills/tailor-interview-questions/SKILL.md
~/.codex/skills/tailor-interview-questions/agents/openai.yaml
```

重新開啟或刷新 Codex 後，就可以使用：

```text
$tailor-interview-questions
```

## 使用範例

### 範例 1：根據 JD 與履歷產生面試題

```text
$tailor-interview-questions

請根據以下 JD 與我的履歷，從面試官角度產生面試問題。

JD:
...

履歷:
...

我特別想準備策略、MVP、TPM、交易系統風控相關題目。
```

預期輸出會包含：

- Target role focus
- Resume-based interview angles
- 分組後的 interview threads
- 每題的問題、追問關係、觀察點與依據

### 範例 2：分析使用者回答

```text
$tailor-interview-questions

請分析我以下答題：

1. 馬丁格爾本身不是保證獲利的機制...
2. 如果銀行要變成交易所，我會先從...
```

預期輸出：

- 產生一個靜態 HTML 檔案
- 每題都包含：
  - Question & User Answer
  - Expert Perspective
  - Strategic Framework
  - Ideal Logic Roadmap
  - Standard Professional Answer
- 每題都有 Logic Consistency、Conciseness、Overall Score

## 專業回答的風格

這個 skill 對「專業」的定義不是堆疊專有名詞，而是回答能不能讓面試官清楚看到你的判斷邏輯。

好的回答應該：

- 用一般人能自然說出口的語氣回答
- 先講清楚問題本質，再講自己的處理方式
- 把抽象概念轉成具體行動，例如要檢查什麼、限制什麼、觀察什麼指標
- 說明因果關係，例如「因為有這個風險，所以我會做這個限制」
- 必要時才使用專有名詞，而且要用具體例子補足
- 避免只說「強化風控」、「提升穩定性」、「設計 scalable architecture」這種聽起來專業但不夠具體的句子

例如：

```text
較弱：我會強化風控和監控機制。

較好：我會先限制最大加碼次數，設定單日虧損上限，並且在交易所 API 回傳訂單狀態不一致時暫停策略，避免系統因為重複下單把虧損放大。
```

## 評分標準

### Logic Consistency

評估回答是否：

- 直接回答問題
- 推理鏈清楚
- 沒有前後矛盾
- 能說明原因、取捨與風險
- 能連結 JD、履歷或自身經驗

### Conciseness

評估回答是否：

- 聚焦在最重要的內容
- 避免過多背景鋪陳
- 避免重複或語意模糊
- 有清楚的段落或邏輯順序
- 能在有限時間內讓面試官抓到重點

## Repo 結構

```text
interview-skill-mandarin/
├── README.md
└── tailor-interview-questions/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

## 適合使用情境

- 準備中文面試
- 需要根據 JD 與履歷客製化面試題
- 想從面試官角度找出履歷風險與追問點
- 想練習策略題、技術題、產品題、TPM 題
- 想針對自己的回答取得結構化評分與改寫示範
