# GitHub Copilot Access：計價異動與主管決策摘要

## 一、核心結論

Copilot access 是可自願切換的新計價模式，不是強制調漲，也不是所有 AI 使用都免費。

- **已有 GitHub Enterprise Cloud 授權**：Copilot 額外席次費為零，需計量的 AI 用量另付費。相較 Copilot Business，平均每人每月低於 **1,900 AI Credits** 時較省；達到或超過後，依本文標準價格假設計算兩制同價。
- **沒有上述授權，採 Copilot Standalone**：每人每月固定費 US$10，需計量的 AI 用量另付費。平均每人每月低於 **900 AI Credits** 時較省；達到時同價，超過後 Business 較便宜。
- **混合授權企業**：應以整個 enterprise 的授權組合與總用量試算，不能只替低用量席次切換。

**建議核決方向：先完成企業整體成本試算，有明確節省再切換；若僅達同價，無須單純為省費而移轉。**

## 二、計價方式比較

| 計價模式 | 每人每月 Copilot 席次費 | 每月內含 AI Credits | 計量用量收費 |
|---|---:|---:|---|
| Copilot Business | US$19 | 每人 1,900，可彙集共用 | 超過內含額度後另計 |
| Copilot Enterprise | US$39 | 每人 3,900，可彙集共用 | 超過內含額度後另計 |
| Copilot access：已有 GitHub Enterprise Cloud 授權 | US$0 | 無 | 從第一次需計量的使用開始收費 |
| Copilot access：Standalone | US$10 | 無 | 從第一次需計量的使用開始收費 |

資料來源：[官方計價異動說明][1]。

### 用量計價的意義

- 1 AI Credit 相當於 US$0.01。
- 依模型及輸入、輸出、快取等 token 消耗計價，再換算為 AI Credits，不是每次提問固定扣一點。
- 程式碼補全與下一步編輯建議不以 AI Credits 計費；「從第一次使用收費」指需消耗 credits 的計量功能。
- US$0 僅指 Copilot 額外席次費為零，不代表 GitHub Enterprise Cloud 授權免費。

資料來源：[模型與定價][2]、[官方計價異動說明][1]。

## 三、損益平衡差異

以下以 Copilot Business 為比較基準，假設標準價格、相同用量與相同計量費率，不含稅與合約折扣，也不新增購買 GitHub Enterprise Cloud 授權。

| 比較項目 | 已有 GitHub Enterprise Cloud 授權 | Standalone |
|---|---|---|
| 新制固定費 | US$0／人／月 | US$10／人／月 |
| 新制月成本 | 用量 × US$0.01 | US$10＋用量 × US$0.01 |
| 損益平衡點 | 1,900 Credits／人／月 | 900 Credits／人／月 |
| 低於平衡點 | 新制較便宜 | 新制較便宜 |
| 等於平衡點 | 同價 | 同價 |
| 高於平衡點 | 依標準價格計算仍同價 | Business 較便宜 |
| 新制最高節省 | US$19／人／月，用量為零時 | US$9／人／月，用量為零時 |

### 計算方式

- 已有授權：US$19 ÷ US$0.01＝1,900 Credits。
- Standalone：(US$19－US$10) ÷ US$0.01＝900 Credits。
- 已有授權者超過 1,900 Credits 後，Business 的 US$19 固定費恰好等於內含額度的價值，因此加上超額費後與新制同價。
- Standalone 高用量時，Business 最多可比新制便宜 US$10／人／月。

以上為依[官方價格][1]與[Credit 換算][2]推導的結果，並非個別合約報價。

## 四、成本試算範例

**以下為假設性示意資料，並非公司實際使用資料。**

共同前提：100 人，Business 固定費為每月 US$1,900，內含合計 190,000 Credits，可彙集共用。所有金額為美元，不含稅、折扣及新增 GitHub Enterprise Cloud 授權成本。

### 範例一：100 人全部已有 GitHub Enterprise Cloud 授權

| 每人平均月用量 | 現制月成本 | 新制月成本 | 新制每月節省 |
|---:|---:|---:|---:|
| 500 Credits | US$1,900 | US$500 | US$1,400 |
| 1,500 Credits | US$1,900 | US$1,500 | US$400 |
| 1,900 Credits | US$1,900 | US$1,900 | US$0，同價 |
| 2,500 Credits | US$2,500 | US$2,500 | US$0，同價 |

**主管判讀：低用量時節省明顯；平均達 1,900 Credits 後，依標準價格計算兩制同價。**

### 範例二：100 人全部採 Standalone

| 每人平均月用量 | 現制月成本 | 新制月成本，含 US$1,000 固定費 | 新制相較現制 |
|---:|---:|---:|---|
| 500 Credits | US$1,900 | US$1,500 | 每月省 US$400 |
| 900 Credits | US$1,900 | US$1,900 | 同價 |
| 1,500 Credits | US$1,900 | US$2,500 | 每月多 US$600 |
| 2,500 Credits | US$2,500 | US$3,500 | 每月多 US$1,000 |

**主管判讀：Standalone 的固定費壓縮省費空間，平均用量超過 900 Credits，維持 Business 較划算。**

### 範例三：70 人已有授權，30 人採 Standalone

假設每人平均每月使用 1,000 Credits。

| 成本項目 | 現制 Business | 新制 |
|---|---:|---:|
| 固定席次費 | 100 × US$19＝US$1,900 | 30 × US$10＝US$300 |
| 另付用量費 | US$0，未超過內含額度 | 100 × 1,000 × US$0.01＝US$1,000 |
| 每月合計 | US$1,900 | US$1,300 |
| 節省金額 |  | 每月 US$600；相同用量維持一年可省 US$7,200 |

此組合的損益平衡點：

(US$1,900－US$300) ÷ US$0.01 ÷ 100 人＝**每人平均每月 1,600 Credits**。

- 低於 1,600 Credits：新制較省。
- 等於 1,600 Credits：同價。
- 超過 1,600 Credits：Business 較便宜。

## 五、企業整體試算公式

定義：

- N：目前 Business 席次數，也是試算切換後的總使用人數。
- S：切換後需使用 Standalone 的人數。
- U：企業每月總計量用量，單位為 AI Credits，包含目前由內含額度抵扣的用量。

在本文標準價格與相同使用範圍假設下：

```text
現制月成本＝19 × N＋max(0, U－1,900 × N) × 0.01
新制月成本＝10 × S＋U × 0.01
每月節省＝現制月成本－新制月成本
```

平均每人每月損益平衡用量：

```text
1,900－1,000 × (S ÷ N) AI Credits
```

此公式適用於 N > 0 且 0 ≤ S ≤ N。

- S＝0：門檻為 1,900 Credits；超過後同價。
- S＝N：門檻為 900 Credits；超過後 Business 較便宜。
- 0 < S < N：門檻介於 900 與 1,900 Credits；超過後 Business 較便宜。

## 六、適用條件與管理限制

### 不能逐席挑選新舊制

- 同一 enterprise 不能混用 Copilot access 與 Copilot Business／Enterprise，即使分屬不同 organization 也不行。
- 新制內可以混用「已有 GitHub Enterprise Cloud 授權」與「Standalone」兩種存取方式。
- Business 的額度可彙集共用，應以企業總用量或整體平均用量評估，不宜只看個別使用者。

### 功能與開通

- Copilot access 具備與 Copilot Enterprise 相同的功能與模型使用資格，仍受管理員政策與支出控制限制。
- 不會自動開通。即使已有 GitHub Enterprise Cloud 授權，管理員仍須指派 Copilot 席次。

### 開放與移轉

依本次對話所引用的官方頁面版本：

- 有 GitHub 或 Microsoft 客戶業務團隊服務的企業，自 2026 年 10 月 28 日起開放洽詢新建或移轉。
- Self-service 客戶尚未開放，將分階段推出；既有訂閱不受影響。
- GitHub Free／Team 組織及 self-service GitHub Enterprise Cloud 試用不適用。
- 移轉為自願，既有 Business／Enterprise 不會自動切換。
- 移轉於月份第一天生效，日期須與業務窗口確認；聯繫業務不代表立即變更計價或保證移轉日期。

資料來源：[官方計價異動說明][1]。開放狀態可能變動，申請前應確認最新公告及帳戶資格。

## 七、核准切換前檢查清單

- [ ] 使用相同月份、相同人數與相同使用範圍比較成本。
- [ ] 取得完整用量，包含目前由內含額度抵扣的部分，不只看超額費。
- [ ] 確認已有 GitHub Enterprise Cloud 授權及需 Standalone 的人數。
- [ ] 確認合約折扣、帳戶專屬價格、移轉條款與生效日。
- [ ] 設定預算及支出控制，納入人數與用量成長。
- [ ] 確認 AI Controls 中的 AI credits paid usage 政策保持啟用，讓使用者可使用消耗 credits 的功能。
- [ ] 檢查防火牆允許清單。若原本只允許 `*.business.githubcopilot.com`，須加入 `*.enterprise.githubcopilot.com`；Standalone 也適用。

管理要求依據：[官方計價異動說明][1]。

## 八、主管建議

1. **已有授權且用量偏低：優先評估切換。** 可減少閒置或低使用率席次的固定支出。
2. **Standalone 且用量偏高：傾向維持 Business。** 平均超過 900 Credits 即不具成本優勢。
3. **混合授權：以企業總成本核決。** 已有授權比例越高、平均用量越低，新制越有利。
4. **僅達同價：無須單純為省費而移轉。** 可另評估功能需求與管理影響。

以上為依計價結構提出的管理建議，不是官方省費保證。

## 參考資料

[1]: https://docs.github.com/en/enterprise-cloud@latest/copilot/get-started/whats-changing-with-github-enterprise-and-copilot
[2]: https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/copilot-billing/models-and-pricing

- [GitHub 官方：Enterprise 與 Copilot 計價異動][1]
- [GitHub 官方：Copilot 模型與定價][2]

本文整合本次對話中的官方資料摘要、成本推算與主管決策建議。試算為示意，實際費用應以帳戶合約、完整用量及官方最新規則為準。
