# Project Architecture v0.2

> 狀態：Draft｜待確認  
> 專案：FastAPI / Docker / PostgreSQL 開發環境與 CI/CD 練習

## 1. 專案概述

本專案用於學習與實作 Python 後端開發環境，以及後續的 CI/CD 自動化流程。

主要技術包含：

- Python / FastAPI：建立後端 API
- PostgreSQL：關聯式資料庫
- Docker / Docker Compose：容器化及本機服務管理
- Git / GitHub：版本控制及程式碼協作
- Pytest：自動化測試
- GitHub Actions：後續 CI/CD 流程

專案採逐步建置方式，不預先實作尚未進入的開發階段。

## 2. 技術架構

### 系統資料流

```text
HTTP Client
     │
     ▼
  FastAPI
     │
     ▼
 PostgreSQL
     │
     ▼
Named Volume
```

### 架構說明

- FastAPI 提供 HTTP API 服務。
- PostgreSQL 負責儲存應用程式資料。
- Docker Compose 管理 API 與資料庫容器。
- PostgreSQL 使用 Docker Named Volume 保存資料。
- Pytest 負責自動化測試。
- GitHub Actions 用於後續 CI/CD 階段。

## 3. 專案目錄結構

以下為預期的專案結構，實際檔案與目錄依開發階段逐步建立。

```text
Project/
├── Architecture.md
│
├── templates/
│   ├── project-structure.template.md
│   ├── workflow.template.md
│   ├── validation.template.md
│   └── handoff.template.md
│
├── Workflows/
│   └── <task-slug>/
│       ├── workflow.md
│       ├── Validation.md
│       └── handoff.md
│
├── app/
│   └── main.py
│
├── tests/
│
├── Dockerfile
├── compose.yaml
├── .gitignore
└── README.md
```

### 目錄職責

| 路徑 | 職責 |
|---|---|
| `Architecture.md` | 專案技術架構與目錄設計 |
| `templates/` | 共用工作文件範本 |
| `Workflows/<task-slug>/` | 各待辦事項的執行、驗證及交接紀錄 |
| `app/` | FastAPI 應用程式 |
| `tests/` | 自動化測試 |
| `Dockerfile` | FastAPI 容器映像定義 |
| `compose.yaml` | API 與 PostgreSQL 服務配置 |
| `README.md` | 專案啟動及操作說明 |

## 4. 專案架構決策

1. **保持最小必要結構**  
   不為尚未實作的功能提前建立額外模組或資料夾。

2. **FastAPI 採用 `app/` 目錄**  
   初期使用簡單結構，未來依實際需求擴充。

3. **資料持久化使用 Named Volume**  
   PostgreSQL 容器重新建立後，資料仍應保留。

4. **健康檢查與資料庫檢查分離**  
   `/health` 只表示 API 服務本身可回應，不以資料庫連線成功作為必要條件。

5. **CI/CD 逐步導入**  
   GitHub Actions 屬於後續階段，不在初始開發環境建置時提前實作。

6. **協作文件依待辦事項管理**  
   每個 Notion 待辦事項使用獨立的英文 Task Slug 資料夾，Workflow／Validation 依子任務 A、B、C 追加紀錄，Handoff 保留最新交接狀態。

---

本文件只描述專案架構。Codex 的工作範圍、授權、驗證與執行規則遵循 Global AGENTS.md；待辦事項與子任務需求以 Notion 已確認內容為準。
