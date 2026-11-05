# Validation｜建立 FastAPI、Git 與 Docker 開發環境

- **Notion 待辦事項：** https://app.notion.com/p/40b3dcad730781819563cbd0dfb58591
- **Task Slug：** fastapi-dev-setup
- **Repository：** https://github.com/LMC1127/CI_Project.git

> 每個待辦事項一份累積文件；後續子任務另行授權後追加，不覆蓋原始 PASS／FAIL、證據或修復次數。本文件只定義子任務 A。

---

## 子任務 A｜Git Repository 與開發流程

### 1. 驗證總覽

| Step | 驗證項目 | 狀態 |
|---|---|---|
| A01 | origin、基底 Commit、Feature Branch 與共同祖先 | PASS |
| A02 | README 內容、忽略規則與交付檔可追蹤性 | PASS |
| A03 | 暫存範圍、Feature Commit SHA 與 Diff | NOT_RUN |
| A04 | main 與 Feature 遠端 SHA | NOT_RUN |
| A05 | PR URL、base/head 與實際 Diff | NOT_RUN |
| A06 | Merge 狀態、main 內容與完整交付 | NOT_RUN |

所有 Step 在執行前後使用 `git status --short --untracked-files=all`、`git diff`、`git diff --cached`、`git ls-files --others --exclude-standard` 檢查；必要時檢查 `git status --short --ignored`。新檔案要讀取必要內容，排除機密。A01 初始化前 Git 不適用，改記錄實際檔案清單與既有檔案雜湊；初始化後立即執行 Git Scope Check。

### 2. Step 驗證紀錄

#### A01｜Git 初始化、origin、共同基底與 Feature Branch

**驗證規格｜規劃時定義**

- **方法：** 執行前以 `git ls-remote --symref https://github.com/LMC1127/CI_Project.git HEAD 'refs/heads/*'` 重查；確認無既有歷史後才依批准方案初始化。用 `git rev-parse --show-toplevel`、`git remote get-url origin`、`git branch --show-current`、`git rev-parse main`、`git merge-base main feat/git-dev-workflow` 核對；`git show --stat main` 與 `git ls-tree -r --name-only main` 檢查基底選檔；對 Architecture.md、templates/ 比對既有雜湊。
- **預期：** 根目錄為目前 CI_Project；origin 為使用者指定 URL；目前分支 feat/git-dev-workflow；main 為明確批准的單一基底 Commit，與 Feature 有共同祖先；沒有 .DS_Store／機密被追蹤；架構與範本內容未變。若遠端非空或權限不足，停止並記錄，不猜測 PASS。

**執行結果｜執行後填寫**

- **實際：** 2026-11-05 21:23:26 CST (UTC+08:00) 完成 A01，所有預期條件通過。保留 Commit 前診斷紀錄：Commit 前額外檢查 `git diff --cached --check` 回傳 exit 2（FAIL），僅指出 Architecture.md 七處既有 Markdown 雙空格換行。雜湊確認架構原檔未變，非本次新增瑕疵；保留原檔，分別驗證架構原檔一致性及其餘檔案 whitespace，不修改或放寬功能驗收。此為檢查診斷，無程式修復，修復次數仍 0/3。
- **證據：** `git rev-parse --show-toplevel` = `/Users/liuzuoqi/Desktop/CI_Project`；origin = 指定 HTTPS URL；目前分支 `feat/git-dev-workflow`；`git rev-parse main`、HEAD、merge-base 均為 `7e0b0f7045c9a891e13bf502d09c7453272b1cfb`；`git rev-list --count main` = 1；`git ls-tree` 精確為 12 份批准的 Markdown；既有 Architecture.md、README.md、templates/ 雜湊一致；其餘檔案 whitespace 檢查 PASS。Commit 後 tracked diff 原為空；僅完成紀錄三檔保留 unstaged，.DS_Store untracked。
- **狀態：** PASS
- **修復次數：** 0/3
- **修復摘要：** 無

#### A02｜README 與 .gitignore

**驗證規格｜規劃時定義**

- **方法：** 讀取 README 與 .gitignore；用 `git diff --check` 檢查空白問題。以 `git check-ignore --no-index --stdin` 輸入虛擬路徑檢查 .DS_Store、.env、.env.local、.venv/probe、app/__pycache__/probe.pyc、.pytest_cache/probe、.ruff_cache/probe、.coverage、htmlcov/index.html、probe.log；不需建立測試機密檔。對 README.md、.env.example、app/main.py、tests/test_health.py、templates/workflow.template.md、Workflows/fastapi-dev-setup/workflow.md 確認未被忽略（未匹配時 exit 1 是預期）。
- **預期：** 所有應排除路徑被忽略，交付檔未被忽略；README 描述實際已完成階段、Repository 與分支／審查流程，無尚未存在的啟動成果；修改僅在 A02 scope。

**執行結果｜執行後填寫**

- **實際：** 2026-11-05 21:29:28 CST (UTC+08:00) PASS；README 已依現況更新，未宣稱 API／Docker 可執行；.gitignore 行為符合規格。
- **證據：** `git check-ignore --no-index --stdin` 對 12 個路徑回傳 exit 0 且逐項匹配（含規格 10 項及 Workflows/.DS_Store、templates/.DS_Store）；對 6 個交付路徑回傳 exit 1、無輸出，皆可追蹤。未建立測試探針或機密檔。`git diff --check` exit 0；README Diff 與 .gitignore 全文已檢查，檔案雜湊／路徑比對確認變更符合 A02 scope。
- **狀態：** PASS
- **修復次數：** 0/3
- **修復摘要：** 無

#### A03｜檔案範圍審查與 Feature Commit

**驗證規格｜規劃時定義**

- **方法：** Commit 前檢查 `git diff --cached --check`、`git diff --cached --name-status`、完整 staged diff 與所有 untracked；掃查預定提交內容是否含機密（發現疑似機密時不輸出原值）。Commit 後執行 `git rev-parse HEAD`、`git log --oneline main..HEAD`、`git diff --name-status main...HEAD`、`git diff main...HEAD`，對照已批准範圍。
- **預期：** Feature SHA 有效，Commit 位於 Feature Branch；差異僅為 README.md、.gitignore 與本待辦紀錄。記錄原有檔案僅被基底納入追蹤，不宣稱本次建立；無機密與無關檔案；Commit 後若有紀錄更新須明確列出，不要求為記錄自身 SHA 無限追加 Commit。

**執行結果｜執行後填寫**

- **實際：** 尚未執行
- **證據：** 無
- **狀態：** NOT_RUN
- **修復次數：** 0/3
- **修復摘要：** 無

#### A04｜Push 與遠端 SHA 核對

**驗證規格｜規劃時定義**

- **方法：** 先展示 origin URL、main／Feature 分支、各 SHA 與 Diff 摘要，取得 Push 明確批准；Push 前重跑 ls-remote。非強制 Push 後以 `git ls-remote origin refs/heads/main refs/heads/feat/git-dev-workflow` 比對本機 `git rev-parse main`、`git rev-parse feat/git-dev-workflow`，用 `git branch -vv` 核對 Feature upstream。
- **預期：** origin/main 等於批准的基底 SHA，origin/feat/git-dev-workflow 等於批准的 Feature SHA；Feature upstream 正確。Push 失敗不表示整體成功；一條成功另一條失敗時分別記錄並先讀取遠端再判斷，不盲目重試。

**執行結果｜執行後填寫**

- **實際：** 尚未執行
- **證據：** 無
- **狀態：** NOT_RUN
- **修復次數：** 0/3
- **修復摘要：** 無

#### A05｜建立 PR 與 Diff 核對

**驗證規格｜規劃時定義**

- **方法：** 先查同 head/base 是否已有 PR，展示完整標題／說明／Diff 供批准；經可用 GitHub 工具或已登入瀏覽器建立 PR 後，讀取 PR URL、base、head、head SHA、檔案清單與逐檔差異；與 A03／A04 記錄及 `git diff main...feat/git-dev-workflow` 比對。
- **預期：** 只有一個目標 PR，base main、head feat/git-dev-workflow；所有差異符合 scope，無缺漏交付或多餘內容；URL 可開啟且 head SHA 一致。無可用登入／工具時如實記錄未完成，不把 PR 草稿當已建立。

**執行結果｜執行後填寫**

- **實際：** 尚未執行
- **證據：** 無
- **狀態：** NOT_RUN
- **修復次數：** 0/3
- **修復摘要：** 無

#### A06｜Merge、main 核對與整體驗收

**驗證規格｜規劃時定義**

- **方法：** Merge 前重讀 PR head SHA、Diff、可合併狀態與必要 checks，展示具體合併方案供批准；合併後重讀 merged 狀態與合併 SHA。執行 `git fetch origin`、`git ls-remote origin refs/heads/main`、`git rev-parse origin/main`，以 `git show origin/main:README.md`、`git show origin/main:.gitignore` 核對內容；若採 merge commit，以 `git merge-base --is-ancestor <批准的Feature-SHA> origin/main` 驗證歷史。安全時才 fast-forward 本機 main；紀錄文件變更不得覆蓋或自動刪除。
- **預期：** 指定 PR 已 merged，遠端 main SHA 與 fetch 結果一致，包含批准的 Feature 修改；本機文件保留且分支狀態說明準確；無繞過 checks、Force Push 或破壞性操作；本機紀錄完整但不自動同步 Notion。

**執行結果｜執行後填寫**

- **實際：** 尚未執行
- **證據：** 無
- **狀態：** NOT_RUN
- **修復次數：** 0/3
- **修復摘要：** 無

### 3. 子任務整體驗收

**驗收規格｜規劃時定義**

- **方法：** 核對 A01–A06 實際 PASS、Git Scope PASS 與必要授權；確認 origin、Feature 流程、README／.gitignore、base／Feature／Merge SHA、Repository URL 與 PR URL。重新確認 PR merged 與遠端 main 的預期檔案內容。核對 workflow.md／Validation.md 的 Step ID、勾選與狀態一致，handoff.md 僅保存最新摘要；未提交紀錄明確列出。
- **預期：** Notion 子任務 A 六條驗收條件全部符合，6/6 Step 完成；Repository URL、PR URL、Commit SHA 與 README.md、.gitignore 可交付。沒有開發子任務 B–E 的變更，既有架構／範本未修改。報告包含 PASS／FAIL／NOT_RUN 數量、未解決事項與必要待批准操作，完成後停止。

**執行結果｜執行後填寫**

- **實際：** 尚未執行
- **證據：** 無
- **狀態：** NOT_RUN
- **未解決問題：** A01、A02 已通過，A03–A06 未執行。遠端寫入與 PR 登入尚未驗證，整體子任務仍 NOT_RUN。

### 4. 規劃查詢備註（不是 Step 執行證據）

- 本機 Git 探測回報 not a git repository，屬於初始化前現況，不是功能測試失敗。
- 初次受限環境 ls-remote 遇到 DNS 無法解析；改以獲准的網路執行環境重查後 exit 0、無任何 HEAD／分支輸出。這是唯讀查詢重試，不是程式修復，不計入 Step 0/3 次數；不代表已確認寫入權限。
- 規劃文件初次範圍檢查 FAIL：全檔案雜湊比對發現根目錄既有 .DS_Store 改變。唯讀分析確認只有該本機中繼資料改變，其來源無法確認，Codex 未操作、不覆寫或刪除；不屬於交付內容，不影響子任務文件。後續檢查對此項單獨揭露，仍要求其餘既有檔案雜湊完全一致，不將此規劃檢查當作 Step 執行或重設任何驗證歷史。
- 第二次規劃範圍檢查 FAIL：另出現 Workflows/.DS_Store，同樣未由 Codex 建立，來源未確認。最終檢查將所有名為 .DS_Store 的項目單獨列出，其他新增檔仍須精確等於三份協作文件；保留兩次原始失敗紀錄。
