# 完成 CI/CD 實作練習

本專案用於逐步練習 FastAPI、PostgreSQL、Docker 與 GitHub Actions。技術架構與目錄職責見 [Architecture.md](Architecture.md)；執行與授權規則依使用者提供的 Global AGENTS.md v0.2.4。

## 目前階段

目前進行「建立 FastAPI、Git 與 Docker 開發環境」的子任務 A：Git Repository 與開發流程。本機 Git 與 origin 已設定，main 已建立協作文件基底 Commit，目前於 `feat/git-dev-workflow` 更新初始化文件。

FastAPI、測試、Docker、PostgreSQL 與 CI 尚未實作；安裝及啟動方式會在對應子任務獲授權並完成後補充。目前尚未 Push、建立 PR 或 Merge。

## Git 開發流程

- Repository：[LMC1127/CI_Project](https://github.com/LMC1127/CI_Project)，origin 使用 `https://github.com/LMC1127/CI_Project.git`。
- main 保存整合結果；本次已批准一次性基底 Commit，後續功能於 Feature Branch 實作。
- 每個 Step 前後核對 staged、unstaged、untracked 與必要 ignored 檔案，檢查實際 Diff 及驗證結果。
- 驗證與範圍檢查通過後，選擇性 `git add <路徑>` 並 Commit；不使用 `git add .`，不提交本機機密或快取。
- Push、建立 PR、Merge 分別取得明確批准。PR 使用 Feature Branch 指向 main，合併後核對遠端 main 內容。

可用以下唯讀指令檢查目前狀態：

```bash
git status --short --untracked-files=all
git diff
git diff --cached
git ls-files --others --exclude-standard
```

`.gitignore` 排除本機環境檔、Python／測試快取與 Log；`.env.example` 保留為可追蹤的設定範本，內容只能使用示意值。

## 文件位置

| 路徑 | 用途 |
|---|---|
| `Architecture.md` | 專案技術架構與目錄設計 |
| `templates/project-structure.template.md` | 專案結構參考範本 |
| `templates/workflow.template.md` | 待辦事項累積執行紀錄範本 |
| `templates/validation.template.md` | 待辦事項累積驗證紀錄範本 |
| `templates/handoff.template.md` | 最新交接摘要範本 |
| `Workflows/fastapi-dev-setup/workflow.md` | 此待辦各子任務的累積計畫與執行進度 |
| `Workflows/fastapi-dev-setup/Validation.md` | 此待辦各 Step 驗證規格、證據與修復紀錄 |
| `Workflows/fastapi-dev-setup/handoff.md` | 此待辦最新交接摘要 |

標準檔名的結構、Workflow、Validation 範本為現有 `.v0.2.md` 範本的相同內容副本；原始版本檔保留。

## 後續建立時機

- 對應待辦事項開始規劃時，先確認是否已有紀錄目錄，並確認 Task Slug，再建立 `Workflows/<task-slug>/`。
- 每個待辦事項共用一份 `workflow.md`、`Validation.md` 與 `handoff.md`；後續子任務獲授權後依序追加，保留歷史紀錄。
- `app/`、`tests/`、`Dockerfile`、`compose.yaml` 及 CI 設定依已批准的開發 Step 建立。
- 本待辦完成子任務 A 後停止，下一子任務另行授權；Notion 完成進度同步須先經使用者審核批准。
