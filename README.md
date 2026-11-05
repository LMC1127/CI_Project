# 完成 CI/CD 實作練習

本專案用於逐步練習 FastAPI、PostgreSQL、Docker 與 GitHub Actions。技術架構與目錄職責見 [Architecture.md](Architecture.md)；執行與授權規則依使用者提供的 Global AGENTS.md v0.2.4。

## 目前階段

目前僅完成專案基礎協作文件初始化，尚未執行任何 Notion 開發子任務，也未初始化 Git Repository。應用程式、測試、容器設定及 CI 的建立與啟動方式，於對應子任務獲授權並完成後補充。

## 文件位置

| 路徑 | 用途 |
|---|---|
| `Architecture.md` | 專案技術架構與目錄設計 |
| `templates/project-structure.template.md` | 專案結構參考範本 |
| `templates/workflow.template.md` | 待辦事項累積執行紀錄範本 |
| `templates/validation.template.md` | 待辦事項累積驗證紀錄範本 |
| `templates/handoff.template.md` | 最新交接摘要範本 |

標準檔名的結構、Workflow、Validation 範本為現有 `.v0.2.md` 範本的相同內容副本；原始版本檔保留。

## 後續建立時機

- 對應待辦事項開始規劃時，先確認是否已有紀錄目錄，並確認 Task Slug，再建立 `Workflows/<task-slug>/`。
- 每個待辦事項共用一份 `workflow.md`、`Validation.md` 與 `handoff.md`；後續子任務獲授權後依序追加，保留歷史紀錄。
- `app/`、`tests/`、`Dockerfile`、`compose.yaml`、`.gitignore` 及 CI 設定依已批准的開發 Step 建立。
- Git 初始化、Remote 設定、Push、建立 PR 及 Merge 依各操作的明確授權執行。
