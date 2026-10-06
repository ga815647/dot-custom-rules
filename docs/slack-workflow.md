# Slack 開發協作流程

更新日期：2026-10-06

這份文件記錄協作方式與產品功能。它不是生效規則，也不會建立訂閱、啟動 AI 或改變權限；自訂規則仍以帳號目前設定為準。

## 主頻道紀錄與工作討論串

1. 工作已有使用者指定用途及接收對象的 Slack 頻道時，在該處討論、回報與交接；沒有明確對應頻道時，先在目前對話處理
2. 主頻道保留可回溯的實質工作紀錄，例如新任務、重要階段結果、重大決策、新阻塞與需要處理的下一步；這些事項可以建立新的主訊息與討論串
3. 同一事項的細節、測試證據、問題釐清與後續進度延續原討論串。同一事項只維護一個主要討論串，避免紀錄分散
4. 不為例行的「收到」、「已接手」或重複狀態另外發布主訊息。回報區分已驗證事實、待確認事項與未執行檢查，讓使用者能直接判斷影響和下一步
5. 可以整理該工作相關的帳戶設定、費用、備份容量、驗證與排除項目摘要；只分享已指定用途與接收對象所需、且已獲授權的內容

GitHub bot 等機器通知與 dot 的實質工作回報分開處理；通知到達本身不算已讀、已接手或完成驗證。

## 決策與交接

1. 把目標、已確認決策、目前進度、測試結果、阻塞及下一步整理在主要工作串；交接附上可核對的來源，例如相關訊息、issue、PR、commit 或測試結果
2. 先確認來源仍適用，避免沿用過期決策。交接至少包含目標、repo／工作目錄、允許修改範圍、完成條件與下一步；在缺少授權或資訊時先確認
3. 原串太長或難以回溯時，可另開交接串。新串連回舊串與已授權來源，舊串也連到新串，並明確指出後續以哪個串為主；保留歷史，不刪除舊訊息
4. 發布前移除金鑰、密碼、權杖、驗證碼、登入或含憑證連結及付款卡資料；醫療、金融資產、未成年人或他人的私人資訊，須另獲明確授權
5. 這些工作紀錄不授權刪除訊息、更改頻道或成員、擴大權限、聯絡其他 AI、付費或部署。公開 Git 文件只放通用流程，不收錄私人工作串、帳戶資訊、備份細節或專案執行證據

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
