# Slack 開發協作流程（第一版）

更新日期：2026-10-05

這份文件記錄協作方式與產品功能。它不是生效規則，也不會建立訂閱、啟動 AI 或改變權限；自訂規則仍以帳號目前設定為準。

## 討論、決策與交接

1. 工作已有使用者指定用途及接收對象的 Slack 對話時，在該處討論、回報與交接；沒有明確對應對話時，先在目前對話處理
2. 把目標、已確認決策、目前進度、測試結果、阻礙及下一步整理在同一工作串，區分已驗證事實與待確認事項
3. 交接附上可核對的來源，例如相關訊息、issue、PR、commit 或測試結果；先確認內容仍適用，避免沿用過期決策
4. 交接至少包含目標、repo／工作目錄、允許修改範圍、完成條件與下一步。新的交接串應連回已授權的來源；在缺少授權或資訊時先確認
5. 只向已指定的接收對象分享該工作允許公開的資訊，不轉貼秘密、登入連結或未授權私人資訊。公開 Git 文件只放通用流程，不收錄私人工作串或專案執行證據

## GitHub 通知與驗證

[GitHub 的 Slack 整合](https://docs.github.com/en/integrations/how-tos/slack/use-github-in-slack)可以訂閱 repo 活動、在 Slack 查看 issue／PR 更新及分享 GitHub 連結。以下是供人工設定的範例，不代表任何工作區已經設定完成：

```text
/github subscribe OWNER/REPO pulls reviews workflows:{event:"pull_request","push" branch:"main"}
/github subscribe list
/github subscribe list features
```

依實際 repo 與目標分支替換占位內容。設定前確認應接收通知的頻道及所需權限。

- pulls：PR 活動
- reviews：PR review 通知
- workflows：GitHub Actions workflow run 通知；未加篩選時預設為針對預設分支的 PR，若要同時看 push，需明確設定事件篩選
- commits：commit 通知與 workflow 通知是不同項目；需要時另外設定 commits:main 或 commits:*

設定後分別核對符合條件的 PR 與 push 事件，以及 workflow 完成回覆。沒有事件或 workflow 可觀察時，應記錄為尚未驗證。首次訂閱 workflows 可能要求額外權限，需另依授權流程處理。

GitHub bot 發送通知，不等於 dot 已讀取或被自動喚醒，也不表示任意 @ChatGPT 提及一定有效。只有已核實的入口及實際回覆，才能算接收或執行成功。

功能與語法來源：[Customizing notifications for GitHub in Slack](https://docs.github.com/en/integrations/how-tos/slack/customize-notifications)

## Copilot AI 是另一項功能

一般 GitHub 通知訂閱與 Copilot AI 任務要分開判斷。GitHub 文件說明，Slack 的 Copilot cloud agent 需要付費 Copilot 方案及相應設定；其方案與用量應另行確認，不能視為 ChatGPT／dot 訂閱已涵蓋。此功能仍在公開預覽，可能變動。

向 @GitHub 發出 AI 任務可能啟動 Copilot，並把整個 Slack thread 當作上下文，內容也可能進入產生的 artifacts。需要先取得使用者對該 AI、工作與分享內容的明確授權，再啟動；不能用試發 AI 訊息來驗證一般通知功能。

來源：[Integrating Copilot cloud agent with Slack](https://docs.github.com/en/copilot/how-tos/copilot-integrations/integrate-cloud-agent-with-slack)

## 完成紀錄

回報應附上實際產物與驗證結果，例如 commit／PR 連結、通過與未執行的測試。文件存在、通知訂閱成功、AI 任務啟動與軟體完成，是各自需要證據的結果。
