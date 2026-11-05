# Workflow｜建立 FastAPI、Git 與 Docker 開發環境

- **Notion 待辦事項：** https://app.notion.com/p/40b3dcad730781819563cbd0dfb58591
- **Task Slug：** fastapi-dev-setup（使用者已確認）
- **Repository：** https://github.com/LMC1127/CI_Project.git（使用者已指定）

> 每個待辦事項一份累積文件。本次只規劃子任務 A；後續子任務需另行授權並在文件尾端追加，不覆蓋歷史。

---

## 子任務 A｜Git Repository 與開發流程

### 1. 子任務資訊

- **目標：** 完成 Git 本機與 GitHub Remote 設定，透過 Feature Branch、Commit、Push、PR、Merge 練習開發流程並交付可核對的 URL 與 SHA。
- **計畫審核：** A01 與基底例外已批准；使用者先前授權 A02，本次「繼續」授權接續 A03；A04–A06 另行批准。
- **執行狀態：** A01、A02 完成；A03 執行中。
- **來源：** 上述 Notion 待辦的子任務 A；Global AGENTS.md v0.2.4；根目錄 Architecture.md v0.2；本機 templates/ 標準檔名範本。
- **執行方式：** 本 Session 依序執行，一次一個 Step。
- **查詢現況：** 本機尚無 Git Repository、Project AGENTS.md 或先前任務紀錄；現有 Architecture.md、README.md、templates/ 均為既有內容，不得當作本次新增成果。Git 已安裝且提交身分已設定；未安裝 gh，不擅自安裝。遠端 `git ls-remote --symref https://github.com/LMC1127/CI_Project.git HEAD 'refs/heads/*'` 成功且無輸出，查詢時未發現 HEAD 或分支；A01 前重查。
- **初始化方案／待批准例外：** 空遠端尚無 PR 共同基底。建議 A01 以 `git init -b main` 初始化，僅對既有 Architecture.md、README.md、templates/ 與本次已審核協作紀錄建立一次 main 基底 Commit，再建立 `feat/git-dev-workflow`；README 實際調整與 .gitignore 在 Feature Branch 完成。這是一次性基底 Commit 的明示例外，不授權日後直接在 main 開發。替代方案為先由使用者在 GitHub 建立基底 Commit，再依該遠端歷史接續；本計畫採建議方案；使用者於本次對話批准 A01 與所述基底例外。
- **共同邊界：** 可建立／更新 README.md、.gitignore、Workflows/fastapi-dev-setup/ 三份協作文件；Git 設定僅限本 Repository 的分支、origin 與追蹤關係。Architecture.md 與 templates/ 可納入初始版本控制，但內容不修改。排除 .DS_Store、憑證、真實 .env、快取與 Log；不建立 app/、tests/、Docker 或 CI 內容，不修改 Notion，不建立新遠端 Repository，不修改全域 Git 設定或安裝工具。
- **每 Step 規則：** 執行前後檢查 Git status、unstaged／staged diff、untracked 檔案與必要 ignored 項目；A01 初始化前以檔案清單與雜湊記錄代替不存在的 Git baseline。實際檢查結果填於當前 Step，不預填 PASS；修復每 Step 跨 Session 累計最多 3 次。

### 2. Step 總覽

| Step | 工作項目 | 等級 | 完成 |
|---|---|---|---|
| A01 | Git 初始化、origin、共同基底與 Feature Branch | L2（基底例外已批准） | [x] |
| A02 | README 與 .gitignore | L1 | [x] |
| A03 | 檔案範圍審查與 Feature Commit | L1 | [ ] |
| A04 | Push 與遠端 SHA 核對 | L2（另行批准） | [ ] |
| A05 | 建立 PR 與 Diff 核對 | L2（另行批准） | [ ] |
| A06 | Merge、main 核對與整體驗收 | L2（另行批准） | [ ] |

### 3. Step 詳細紀錄

#### A01｜Git 初始化、origin、共同基底與 Feature Branch

- **目標：** origin 精確指向指定 URL；建立一次性 main 基底 Commit，隨後切換至 feat/git-dev-workflow，共同祖先可核對。
- **允許修改：** 本機 .git/；選擇性暫存既有 Architecture.md、README.md、templates/ 的 Markdown 檔及已審核的本待辦協作紀錄以建立基底 Commit；更新本待辦紀錄。不得修改既有架構與範本內容，不納入 .DS_Store。若遠端已有分支／Commit，停止重新比對，不覆蓋遠端、不建立獨立且無關的歷史。
- **完成條件：** Validation A01 PASS、Git Scope PASS，且基底例外獲批准。
- **Git Baseline：** 初始化前無 .git；既有 12 份 Markdown 檔與 .DS_Store 清單／雜湊已記錄於本機暫存 baseline；未有 staged／unstaged／untracked 分類。遠端重查 exit 0 且無 HEAD／分支。
- **修改摘要：** 初始化本機 Git、設定指定 origin；只選擇性提交 12 份 Markdown 作為 main 基底，SHA `7e0b0f7045c9a891e13bf502d09c7453272b1cfb`；建立並切換 feat/git-dev-workflow。既有架構、README 與範本內容未變；未 Push。
- **Git Scope：** PASS；基底追蹤檔精確符合 12 檔清單；完成紀錄保留為本待辦三檔 unstaged 更新；.DS_Store 保留 untracked，不納入交付。
- **Validation：** PASS（詳細證據見 Validation A01；修復 0/3）
- **異常／待批准：** A01 批准與驗證已完成；依本次授權邊界停止，不進入 A02。

#### A02｜README 與 .gitignore

- **目標：** README 說明本階段 Git 工作流程、文件位置與尚未實作範圍；.gitignore 排除本機敏感檔及常見 Python／測試快取，不忽略應交付原始碼或 .env.example。
- **允許修改：** README.md、.gitignore、上述本待辦協作紀錄；不得宣稱 FastAPI／Docker 已可執行。規則涵蓋 .DS_Store、.env／本機環境檔（保留 .env.example）、.venv/、__pycache__/、*.pyc、.pytest_cache/、.ruff_cache/、.coverage、htmlcov/ 與 *.log。
- **完成條件：** Validation A02 PASS、Git Scope PASS。
- **Git Baseline：** feat/git-dev-workflow，HEAD 7e0b0f7；既有 unstaged 為 A01 的 workflow.md、Validation.md、handoff.md，無 staged；三個 .DS_Store 原為 untracked。README 與 .gitignore 尚無本次修改。
- **修改摘要：** README 更新實際階段、Repository、Git 開發與審查流程、累積文件位置；新增 .gitignore 排除本機環境檔及快取，保留 .env.example 可追蹤。
- **Git Scope：** PASS；本次僅 README.md、.gitignore 與本待辦三份紀錄；既有架構／範本未變，無暫存或 Commit。
- **Validation：** PASS；12 個排除路徑、6 個保留路徑與 whitespace 檢查通過；修復 0/3。
- **異常／待批准：** 本步已獲授權並完成；下一步 A03 尚未執行。

#### A03｜檔案範圍審查與 Feature Commit

- **目標：** 僅提交 A02 與本待辦紀錄，確認 Feature Commit SHA 與相對 main 的實際差異。
- **允許修改：** 選擇性 git add README.md、.gitignore 及本待辦紀錄；git commit；更新本待辦紀錄。不得 git add .，不得混入既有無關內容、機密或 ignored 檔。紀錄不強求包含其自身最終 SHA：Commit 後的 SHA／驗證與 handoff 更新可保留本機，下一次有意義 Commit 再納入，須明確列出未提交紀錄，避免反覆補 Commit。
- **完成條件：** Validation A03 PASS、Git Scope PASS，記錄 base SHA、Feature SHA 與 Diff 摘要。
- **Git Baseline：** feat/git-dev-workflow，HEAD／main 7e0b0f7；既有 README 與三份累積紀錄 unstaged、.gitignore untracked，無 staged；本次不將 A01／A02 既有修改視為 A03 新實作。
- **修改摘要：** 尚未執行
- **Git Scope：** NOT_RUN
- **Validation：** NOT_RUN
- **異常／待批准：** 使用者已授權 A03；Commit 完成後停在 A04 Push 前。

#### A04｜Push 與遠端 SHA 核對

- **目標：** 將已審核的 main 基底及 Feature Commit 發佈到指定 origin，確認兩條遠端分支 SHA。
- **允許修改：** 經明確批准後以一般非強制 Push 建立 origin/main 與 origin/feat/git-dev-workflow，設定該 Feature Branch upstream；更新本待辦紀錄。Push 前重查遠端；若出現新歷史，先分析並停止受影響操作，不 Force Push。
- **完成條件：** Push 範圍及兩分支 SHA 已展示並獲批准；Validation A04 PASS、Git Scope PASS。
- **Git Baseline：** 尚未記錄
- **修改摘要：** 尚未執行
- **Git Scope：** NOT_RUN
- **Validation：** NOT_RUN
- **異常／待批准：** 等待批准（具體 Push；整體計畫批准不代替此批准）。

#### A05｜建立 PR 與 Diff 核對

- **目標：** 建立 head feat/git-dev-workflow → base main 的 PR，確認實際 PR Diff 與已審核 Feature Commit 一致。
- **允許修改：** 經批准建立單一 PR，保存 URL；更新本待辦紀錄。先查重並展示具體標題、說明、base/head、Commit 與 Diff；不自行新增 CI 或分支保護。優先使用屆時可用的 GitHub 工具；無適用工具時用既有已登入瀏覽器，無權限則停止請求必要登入，不安裝 gh。
- **完成條件：** 具體 PR 草稿已獲批准；Validation A05 PASS、Git Scope PASS。
- **Git Baseline：** 尚未記錄
- **修改摘要：** 尚未執行
- **Git Scope：** NOT_RUN
- **Validation：** NOT_RUN
- **異常／待批准：** 等待批准（建立具體 PR）。

#### A06｜Merge、main 核對與整體驗收

- **目標：** PR 經批准合併，驗證遠端 main 包含預期 Feature 修改，完成本機累積驗證與交接。
- **允許修改：** 經批准合併指定 PR；正常 fetch 並 fast-forward 本機 main（僅當工作目錄安全可切換時）；更新本待辦紀錄。預設建議 merge commit 以保留練習歷史，具體方式於 Merge 審核時確認。不得繞過 GitHub 必要檢查、刪除分支、破壞性清理或覆寫未提交文件；若紀錄變更妨礙切換，保留 Feature Branch，以 origin/main 查核並明確記錄。
- **完成條件：** Merge 批准與 Validation A06 PASS、Git Scope PASS，整體驗收 PASS；所有必要 URL 與 SHA 已核對。
- **Git Baseline：** 尚未記錄
- **修改摘要：** 尚未執行
- **Git Scope：** NOT_RUN
- **Validation：** NOT_RUN
- **異常／待批准：** 等待批准（指定 PR 的 Merge）；Notion 同步另待子任務交付審核，不在本計畫自動執行。

### 4. 子任務完成摘要

- **完成 Step：** 2/6
- **整體驗收：** NOT_RUN
- **主要成果：** A01 Git 基底完成；A02 README 與 .gitignore 驗證通過，尚未 Commit；其餘 4 Step 未執行。
- **未解決問題：** 遠端寫入權限與 PR 操作登入尚未驗證；Architecture.md 檔頭仍為 Draft，內容不自行修改。
- **下一步：** A03 檔案範圍審查與 Feature Commit；本次停在 A02。
