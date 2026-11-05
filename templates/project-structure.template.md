# Project Structure Template v0.2

> 狀態：Draft｜待使用者確認
>
> 用途：提供 Codex 初始化新專案時可參考的**共用協作文件結構**。並非完整的程式碼架構，不強制將所有路徑或空資料夾一次建立完畢。

## 1. 共用參考結構

```text
Project/
├── AGENTS.md                       # Project 專屬行為／技術限制
├── Architecture.md                 # 經批准的 Project 技術架構與目錄決策（依需要）
├── templates/                      # 專案可存放共用範本副本或特定版本
│   ├── workflow.template.md
│   ├── validation.template.md
│   └── project-structure.template.md   # 可改為指向共用位置，不必強制複製
└── Workflows/                      # 實際執行紀錄；依任務建立
    └── <task-slug>/                    # 英文小寫連字號，一個待辦事項一個資料夾
        ├── workflow.md                # 子任務 A/B/C 依序累積
        ├── Validation.md              # 子任務 A/B/C 驗證紀錄
        └── handoff.md                 # 最新交接摘要
```

## 2. 路徑與責任

| 位置 | 定位 | 建立時機 |
|---|---|---|
| `AGENTS.md` | Project 層級技術、權限與特定限制 | 專案有對應規格時 |
| `Architecture.md` | 實際技術選型、模組、資料流及目錄結構 | 在 ChatGPT 討論確認後；適用時交付 Codex |
| `templates/` | 文件範本的專案副本或專用版 | 需要本地範本時；也可使用明確可存取的共用路徑 |
| `Workflows/<task-slug>/` | 各項任務的 Workflow、Validation、Handoff | 該任務開始規劃／執行時 |
| 程式與測試目錄 | 實際產品程式碼、測試和資源 | 依 Project Architecture 與技術框架決定 |

## 3. 專案技術目錄（僅示意，不是固定標準）

- FastAPI 專案可能使用 `app/` 與 `tests/`。
- Flutter 專案通常使用 `lib/`、`test/`、`assets/`（視需求）。
- 前後端整合專案可能使用 `frontend/`、`backend/`、`database/`，也可能採用其他分工。
- 不應將所有專案強制整理為 `app/frontend/`、`app/backend/`、`app/database/`；實際結構由專案需求決定。

## 4. Codex 套用時的確認事項

1. 取得本範本、已批准的 Project `Architecture.md`（如適用），以及當前 Step 的允許修改範圍。
2. 檢查現有專案目錄；既有專案不為符合示意圖而強制搬遷。
3. 只建立當前任務需要的檔案／資料夾，不預建所有空目錄。已授權範圍內可新增一般子目錄。
4. 超出 Step 修改範圍的變更先取得授權；若涉及重大模組職責或核心架構調整，依 L3 先批准並更新 Project Architecture。
5. 每個 Step 依 Global／Project `AGENTS.md` 進行 Git Scope Check：包含 staged、unstaged、untracked，必要時確認 ignored；新檔案須檢查路徑、內容及是否應納入提交，不能直接 `git add .`。
6. Git 不追蹤空目錄。只有空目錄是明確交付需求時，才另外確認其存在及保留方式。
7. 以 Notion 待辦事項 URL 對應 Task Slug；首次命名由 Codex 建議並經使用者確認，使用小寫英文、數字及連字號。保留中文待辦標題，不因 Notion 更名自動改變既有路徑。
8. `workflow.md`／`Validation.md` 在下一子任務獲准規劃後追加新區塊，保留舊子任務結果；`handoff.md` 只保存最新交接。

## 5. 套用原則

**Project Architecture 定義該專案實際採用的技術結構；本範本提供協作文件的共同起點；Global／Project AGENTS.md 定義執行與授權規則。** 若互相矛盾，回報並確認，不直接猜測或自行放寬授權。
