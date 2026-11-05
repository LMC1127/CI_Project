# Session Handoff Template v0.1

> 狀態：Draft｜待使用者確認
>
> 用途：供 Codex 在 Session 結束、子任務完成或中止交接時，更新**同一待辦事項唯一一份** `Workflows/<待辦事項>/handoff.md`。只保留最新摘要；實際 Step／驗證歷史由 `workflow.md` 與 `Validation.md` 保存。
>
> 本範本是欄位格式，不取代 Global／Project `AGENTS.md` 的授權、驗證與恢復規範。以下方括號是填寫提示，生成正式 handoff.md 時請以真實資料替換，不得猜測。

# Session Handoff

## 1. 目前進度

- **更新時間：** [含時區的日期時間]
- **目前子任務：** [子任務 ID／名稱]
- **目前 Step：** [Step ID／狀態]
- **最後完成 Step：** [Step ID／無]

## 2. Git 狀態

- **Branch：** [分支名稱／無法確認]
- **未提交變更：** [主要檔案及 staged／unstaged／untracked 摘要／無]
- **注意事項：** [既有變更、部分完成的操作、重要 ignored／空目錄風險／無]

## 3. 驗證與待處理

- **最近驗證：** [Step ID／NOT_RUN、PASS、FAIL／必要簡述]
- **修復次數：** [目前 Step 累計已使用次數／3；依 Validation 核對]
- **待批准事項：** [具體操作及原因／無；不得僅憑此欄推定授權有效]
- **未解決問題：** [簡短摘要／無]

## 4. 下一步

- **預計執行：** [下一個 Step／待完成操作／等待授權]
- **恢復前核對：** [核對 Workflow、Validation、Git／實際檔案、有效授權；若有特殊風險可補充]
