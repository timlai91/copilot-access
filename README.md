# Copilot access 費用試算 / Pricing Calculator

[繁體中文](#繁體中文) | [English](#english)

## 繁體中文

支援繁體中文（zh-TW）與 English 的互動式靜態頁面，協助企業比較 **Copilot Business** 與 **Copilot access** 的費用差異。調整使用人數、授權組合與 AI Credits 用量，即可查看月費、年度差額及損益平衡點。

內容依據 [計價異動與主管決策摘要](copilot-access.md) 建立。這是**非官方試算工具**，不是帳單、個別合約報價或官方省費保證。

### 快速開始

下載 [copilot-access.html](copilot-access.html)，以已啟用 JavaScript 的現代瀏覽器直接開啟即可使用。GitHub 的檔案頁僅供檢視原始碼，請先下載到本機再開啟。

也可以在 Windows PowerShell 執行：

```powershell
git clone https://github.com/timlai91/copilot-access.git
Set-Location .\copilot-access
Start-Process .\copilot-access.html
```

不需安裝套件、編譯或啟動伺服器。HTML 已內含樣式、互動邏輯與圖示，可離線試算；輸入數字不會由頁面上傳至伺服器。

### 使用方式

預設顯示繁體中文，可使用畫面右上角的「中文／English」切換語系。切換會同步更新說明、圖表、錯誤提示及試算結果文字，不會重設輸入數字或切換用量模式。

1. 輸入企業總使用人數，也就是目前 Business 席次數及切換後總人數。
2. 輸入其中需要 Standalone 的人數；其餘人數視為已有 GitHub Enterprise Cloud 授權。
3. 輸入每人平均月用量，或切換為企業每月總用量；也可使用滑桿調整平均用量。
4. 比較兩制固定費、另付用量費、每人平均月費與總差額，再查看費用曲線及平衡點。

**用量必須包含目前由內含額度抵扣的部分，不能只填超額用量。** 頁面提供「全部已有授權」、「全 Standalone」及「混合 70／30」三個文件範例，也可按「重設」回到預設混合情境。

總人數須為 1 至 1,000,000 的整數，Standalone 人數須介於 0 與總人數之間；企業每月總用量上限為 1 兆 AI Credits。輸入無效時，頁面會提示原因並暫停顯示試算結果。

### 計價邏輯

本頁以 **Copilot Business 的標準價格**為比較基準，不是 Copilot Enterprise 費用試算。

| 模式 | 每人每月 Copilot 席次費 | 每月內含 AI Credits | 另付用量費 |
|---|---:|---:|---|
| Copilot Business | US$19 | 每人 1,900，可彙集共用 | 超過共用額度的部分另計 |
| access：已有 GitHub Enterprise Cloud 授權 | US$0 | 無 | 全部需計量用量另計 |
| access：Standalone | US$10 | 無 | 全部需計量用量另計 |

1 AI Credit＝US$0.01。Credits 依模型及輸入、輸出、快取等 token 消耗計算，**不是提問次數**；程式碼補全與下一步編輯建議不以 AI Credits 計費。

#### 企業整體公式

`N` 為總人數，`S` 為需 Standalone 的人數，`U` 為企業每月總計量用量（AI Credits）。適用條件為 `N > 0` 且 `0 ≤ S ≤ N`。

```text
Business 月成本 = 19 × N + max(0, U − 1,900 × N) × 0.01
access 月成本   = 10 × S + U × 0.01
每月節省        = Business 月成本 − access 月成本

每人平均損益平衡用量 = 1,900 − 1,000 × (S ÷ N) AI Credits
```

| 授權組合 | 每人平均月用量平衡點 | 超過平衡點後 |
|---|---:|---|
| 全部已有 Enterprise Cloud 授權 | 1,900 Credits | 依標準價格計算，兩制仍同價 |
| 全部採 Standalone | 900 Credits | Business 較便宜 |
| 混合授權 | 介於 900 與 1,900 Credits | Business 較便宜 |

低於各組合的平衡點時，access 較省；等於精確平衡點時同價。圖表與顯示金額可能四捨五入。

#### 預設試算範例

假設共 100 人，其中 70 人已有 Enterprise Cloud 授權、30 人需 Standalone，每人平均每月使用 1,000 Credits，企業總用量為 100,000 Credits。

| 費用項目 | Business | access |
|---|---:|---:|
| 固定席次費 | US$1,900 | US$300 |
| 另付用量費 | US$0 | US$1,000 |
| 每月合計 | US$1,900 | US$1,300 |

此情境每月可省 **US$600**；相同人數與用量維持 12 個月可省 **US$7,200**，每人平均平衡點為 **1,600 Credits／月**。這是假設性示例，並非公司實際使用資料。

### 判讀與移轉注意事項

- **US$0 僅指 Copilot 額外席次費。** 不代表 GitHub Enterprise Cloud 授權免費，也不代表所有 AI 使用免費。
- **必須比較整個 enterprise。** 同一 enterprise 不能混用 access 與 Business／Enterprise，即使分屬不同 organization 也不行；access 內可以混用既有授權與 Standalone 存取方式。
- **試算不含稅、合約折扣及新增 Enterprise Cloud 授權成本。** 兩制假設使用範圍、用量及計量費率相同，年差額只將同一月情境乘以 12，不是成長預測。
- **移轉是自願選擇，不會自動切換或開通。** 管理員仍須指派 Copilot 席次，並確認帳戶資格、預算、政策及移轉生效日。

頁面另附可展開的計算公式、功能與開通說明、申請資格，以及預算、AI Controls 政策與防火牆設定檢查清單。完整背景請參考 [copilot-access.md](copilot-access.md)。

### 專案內容

| 檔案 | 用途 |
|---|---|
| [copilot-access.html](copilot-access.html) | 單一檔案的互動式費用試算頁面，支援桌面與手機版面 |
| [copilot-access.md](copilot-access.md) | 計價異動、公式推導、試算範例與主管決策摘要 |
| `.gitignore` | 排除本機設計初稿資料夾 `design-demos` |

正式頁面不依賴 `design-demos`。修改計價規則時，應同步更新 HTML 中的計算邏輯、說明文字、範例與相關文件。

### 資料來源

現有頁面的價格及開放狀態核對日期為 **2026-11-05**。規則與申請資格可能變動，決策前請確認官方最新公告、完整用量及帳戶合約。

- [GitHub 官方：Enterprise 與 Copilot 計價異動](https://docs.github.com/en/enterprise-cloud@latest/copilot/get-started/whats-changing-with-github-enterprise-and-copilot)
- [GitHub 官方：Copilot 模型與 Credits 定價](https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/copilot-billing/models-and-pricing)

## English

[繁體中文](#繁體中文) | [English](#english)

An interactive static page in Traditional Chinese (zh-TW) and English that helps enterprises compare **Copilot Business** and **Copilot access** costs. Adjust user counts, licensing mix, and AI Credits usage to see monthly costs, annual differences, and the break-even point.

Based on the [pricing changes and management decision summary (Traditional Chinese)](copilot-access.md). This is an **unofficial calculator**, not a bill, an individual contract quote, or an official guarantee of savings.

### Quick start

Download [copilot-access.html](copilot-access.html) and open it directly in a modern browser with JavaScript enabled. GitHub's file viewer displays source code only; download the file before opening it locally.

Alternatively, run these commands in Windows PowerShell:

```powershell
git clone https://github.com/timlai91/copilot-access.git
Set-Location .\copilot-access
Start-Process .\copilot-access.html
```

No package installation, build, or server is required. The HTML includes all styles, interaction logic, and icons, so calculations work offline. The page does not upload your inputs to a server.

### Usage

The page opens in Traditional Chinese by default. Use the "中文 / English" switch in the top-right corner to change languages. Explanations, charts, validation messages, and result text update together without resetting your inputs or changing the usage mode.

1. Enter the enterprise's total user count: the current number of Business seats and the total users after switching.
2. Enter how many of those users require Standalone access. The remaining users are assumed to already have GitHub Enterprise Cloud licenses.
3. Enter average monthly usage per person, or switch to total monthly enterprise usage. You can also use the slider to adjust average usage.
4. Compare fixed seat fees, additional usage charges, average monthly cost per person, and total cost differences, then review the cost curves and break-even point.

**Usage must include the portion currently covered by included allowances, not just overage usage.** The page provides three documented presets: all users already licensed, all Standalone, and a 70/30 mix. Use Reset to return to the default mixed scenario.

The total user count must be an integer from 1 to 1,000,000, and the Standalone count must be between zero and the total user count. Total monthly enterprise usage is capped at 1 trillion AI Credits. Invalid input displays an explanation and hides calculation results until corrected.

### Pricing model

The comparison uses **standard Copilot Business pricing** as its baseline. It is not a Copilot Enterprise cost calculator.

| Model | Monthly Copilot seat fee per person | Included monthly AI Credits | Additional usage charges |
|---|---:|---|---|
| Copilot Business | US$19 | 1,900 per person, pooled across users | Usage above the pooled allowance |
| access: existing GitHub Enterprise Cloud license | US$0 | None | All metered usage |
| access: Standalone | US$10 | None | All metered usage |

1 AI Credit = US$0.01. Credits depend on the model and token consumption, including input, output, and caching; **they are not a count of prompts**. Code completions and next edit suggestions are not billed in AI Credits.

#### Enterprise-wide formulas

`N` is the total user count, `S` is the number of users requiring Standalone, and `U` is total monthly enterprise metered usage in AI Credits. These formulas require `N > 0` and `0 ≤ S ≤ N`.

```text
Business monthly cost = 19 × N + max(0, U − 1,900 × N) × 0.01
access monthly cost   = 10 × S + U × 0.01
Monthly savings       = Business monthly cost − access monthly cost

Average break-even usage per person = 1,900 − 1,000 × (S ÷ N) AI Credits
```

| Licensing mix | Average monthly break-even usage per person | Above the break-even point |
|---|---:|---|
| All users already have Enterprise Cloud licenses | 1,900 Credits | Both models remain equal at standard prices |
| All users use Standalone | 900 Credits | Business is cheaper |
| Mixed licensing | Between 900 and 1,900 Credits | Business is cheaper |

access is cheaper below each mix's break-even point; costs are equal at the exact break-even point. Chart labels and displayed amounts may be rounded.

#### Default example

Assume 100 users: 70 already have Enterprise Cloud licenses and 30 require Standalone. Each person uses an average of 1,000 Credits per month, totaling 100,000 Credits for the enterprise.

| Cost component | Business | access |
|---|---:|---:|
| Fixed seat fees | US$1,900 | US$300 |
| Additional usage charges | US$0 | US$1,000 |
| Monthly total | US$1,900 | US$1,300 |

This scenario saves **US$600 per month**, or **US$7,200** if the same user counts and usage continue for 12 months. The average break-even point is **1,600 Credits per person per month**. This is a hypothetical example, not actual company usage data.

### Interpretation and migration notes

- **US$0 refers only to the additional Copilot seat fee.** It does not mean GitHub Enterprise Cloud licenses or all AI usage are free.
- **Compare the entire enterprise.** A single enterprise cannot mix access with Business or Enterprise, even across different organizations. Within access, users with existing licenses and Standalone users can coexist.
- **Estimates exclude taxes, contract discounts, and new Enterprise Cloud license costs.** Both models assume the same usage scope, volume, and metered rates. Annual differences multiply the same monthly scenario by 12; they are not growth forecasts.
- **Migration is optional, not automatic activation or switching.** Administrators must still assign Copilot seats and confirm account eligibility, budgets, policies, and the migration effective date.

The page also includes expandable formulas, feature and activation guidance, eligibility details, and a checklist covering budgets, AI Controls policies, and firewall settings. For full background, see [copilot-access.md (Traditional Chinese)](copilot-access.md).

### Project files

| File | Purpose |
|---|---|
| [copilot-access.html](copilot-access.html) | Single-file interactive pricing calculator with desktop and mobile layouts |
| [copilot-access.md](copilot-access.md) | Pricing changes, formula derivations, examples, and management decision summary in Traditional Chinese |
| `.gitignore` | Excludes the local `design-demos` draft folder |

The final page does not depend on `design-demos`. When changing pricing rules, update the HTML's calculation logic, explanatory text, examples, and related documentation together.

### Sources

The existing page's pricing and availability were checked on **2026-11-05**. Rules and eligibility may change. Before making a decision, confirm the latest official announcements, complete usage data, and your account's contract terms.

- [GitHub: What's changing with GitHub Enterprise and Copilot](https://docs.github.com/en/enterprise-cloud@latest/copilot/get-started/whats-changing-with-github-enterprise-and-copilot)
- [GitHub: Copilot models and pricing](https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/copilot-billing/models-and-pricing)
