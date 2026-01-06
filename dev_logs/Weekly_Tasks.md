## 🛡️ Secure Embedded Linux Device 專案進度表

> **專案週期**：12 週 (每週預計投入 20 小時)  
> **核心技術**：Buildroot, QEMU, C Language, Shell Scripting, OpenSSL, OTA Architecture


---

### ⬜ Phase 0: 建立專案結構與先備知識
> **目標：打好基礎，配置開發環境，完成專案資料夾結構。**

### 環境配置與工具準備
- [ ] **Linux 環境準備**
- [ ] **開發工具安裝**： `git`, `build-essential`, `gcc`, `g++`, `make`, `vim/vscode`。
- [ ] **編輯器設定**：`VS Code` 的 `Remote-SSH`,`WSL` 插件
- [ ] **版本控制初始化**：`.gitignore` (排除 `build/` 或 `output/` 大檔案)。

### 專案目錄結構設計 (Scaffolding)
- [ ] **建立資料夾階層**：
    - `docs/`: 存放技術筆記、架構圖、參考文件。
    - `src/`: 存放自定義 App 的 C 原始碼。
    - `scripts/`: 存放 OTA 腳本、簽章工具、QEMU 啟動腳本。
    - `buildroot/`: 用於存放 Buildroot 原始碼或作為 Submodule。
    - `configs/`: 存放 Buildroot 的 `.config` 備份。
- [x] **建立 README 骨架**：寫下專案名稱、目標以及這個進度追蹤表。

### 先備知識快速複習
- [ ] **Linux CLI 熟練度**：複習檔案操作 (`cd`, `ls`, `mkdir`, `cp`, `mv`) 與權限管理 (`chmod`)。
- [ ] **C 語言強化**：複習指標 (Pointers) 與基本檔案 I/O (`fopen`, `fread`, `fwrite`)。
- [ ] **編譯概念釐清**：理解何謂「交叉編譯 (Cross-Compilation)」以及「靜態連結 vs. 動態連結」。
- [ ] **閱讀初步文件**：快速瀏覽 Buildroot 官方文件的 [The basics](https://buildroot.org/downloads/manual/manual.html#_getting_started) 章節。

### 軟性技能與工作流
- [x] **制定筆記策略**：選定筆記工具 (Notion, Obsidian 或直接寫 Markdown)，確保每週五能產出進度回顧。
- [ ] **Know / Note 嵌入式**
- [ ] **Know / Note 嵌入式 linux 架構**
- [ ] **Know / Note linux 開機流程**
- [ ] **Know / Note 嵌入式設計思維**
- [ ] **Know / Note 嵌入式安全**
- [ ] **Know / Note 嵌入式安全**
- [ ] **Know / Note QEMU**
- [ ] **Know / Note Buildroot**

---

### 🟩 Phase 1: 基礎系統建置 (Week 1–2)
> **目標：從原始碼編譯出一個能在 QEMU 跑起來的最小化 Linux。**

#### Week 1: 環境與首次編譯
- [ ] 準備 Linux 開發環境 (建議 Ubuntu 22.04 LTS 或 WSL2)
- [ ] 安裝必要套件 (`build-essential`, `libncurses-dev`, `git`, `python3`, 等)
- [ ] 下載並配置 Buildroot 原始碼 (LTS 版本)
- [ ] 選定目標架構 (建議使用 `qemu_arm_vexpress_defconfig`)
- [ ] 執行首次完整編譯 (`make`) 並理解輸出產物：
    - `zImage` (Kernel)
    - `rootfs.ext2` (File System)
    - `u-boot.bin` (Bootloader)
- [ ] 使用 QEMU 成功開機並進入系統登入畫面
- [ ] 下週進度規劃及需求修正

#### Week 2: 系統自定義與核心理解
- [ ] 使用 `make menuconfig` 調整系統工具 (加入 BusyBox 常用工具)
- [ ] 修改 `board/qemu/arm-vexpress/post-build.sh` 或使用 `rootfs_overlay` 手動新增檔案
- [ ] 理解嵌入式 Linux 四大組件的交互關係
- [ ] **筆記紀錄**：記錄 Buildroot 基本指令與 QEMU 啟動參數意義
- [ ] 下週進度規劃及需求修正
---

### 🟩 Phase 2: 系統應用與架構 (Week 3–4)
> **目標：建立主應用程式並理解 Linux 如何管理行程。**

#### Week 3: 撰寫 Secure App 骨架
- [ ] 撰寫 C 語言主程式 `secure_app.c` (讀取系統資訊、模擬監控邏輯)
- [ ] 建立交叉編譯 (Cross-compilation) 環境使用的 Makefile
- [ ] 將 App 整合進 Buildroot 自動編譯流程 (撰寫 `.mk` 檔案與 `Config.in`)
- [ ] 實作基本的日誌功能，將資訊寫入 `/var/log/secure_app.log`
- [ ] 下週進度規劃及需求修正

#### Week 4: 初始化指令腳本 (Init Scripts)
- [ ] 撰寫符合 BusyBox `init` 規範的啟動腳本 `/etc/init.d/S99secureapp`
- [ ] 測試開機後自動啟動 App 且無須手動登入
- [ ] 理解並實驗 Linux Runlevels 與系統關機流程
- [ ] **交付物**：一個開機即運作且會持續記錄狀態的系統映像檔
- [ ] 下週進度規劃及需求修正

---

### 🟨 Phase 3: OTA 更新機制實作 (Week 5–6)
> **目標：實現「不重刷映像檔」即可更新軟體組件的功能。**

#### Week 5: 設計更新邏輯 (Update Logic)
- [ ] 定義更新包格式 (例如：包含 `payload.bin`, `version.txt`, `metadata`)
- [ ] 撰寫更新腳本 `ota_update.sh`：
    - 模擬從 `/tmp` 讀取更新包
    - 檢查版本號 (Version Comparison)
    - 替換舊版執行檔
- [ ] 實作簡單的 HTTP/Local 下載模擬
- [ ] 下週進度規劃及需求修正

#### Week 6: 原子更新與失敗處理 (Robustness)
- [ ] 實作「備份/回滾 (Rollback)」機制：更新前備份舊版，失敗則還原
- [ ] 使用 `sync` 指令確保資料確實寫入磁碟，防止斷電損壞
- [ ] 測試情境：更新檔案損壞、空間不足、版本過舊等例外處理
- [ ] **筆記紀錄**：畫出 OTA 更新狀態機 (State Machine) 圖解
- [ ] 下週進度規劃及需求修正

---

### 🟥 Phase 4: 安全機制強化 (Week 7–8)
> **目標：防止未授權的韌體更新。**

#### Week 7: 非對稱加密基礎設施
- [ ] 學習使用 OpenSSL 指令產生成對金鑰 (Private/Public Key)
- [ ] 實作開發端簽章腳本：`openssl dgst -sha256 -sign`
- [ ] 將公鑰 (Public Key) 整合進 Buildroot 映像檔的唯讀目錄中
- [ ] 下週進度規劃及需求修正

#### Week 8: 簽章驗證實作 (Verification)
- [ ] 在 `ota_update.sh` 中加入 `openssl dgst -verify` 邏輯
- [ ] 確保只有通過私鑰簽署的更新包才能被系統安裝
- [ ] 撰寫威脅模型分析 (Threat Model)：
    - 攻擊者篡改更新包 (Integrity)
    - 攻擊者冒充伺服器 (Authenticity)
- [ ] **測試**：嘗試用修改過的包進行更新，確認系統會攔截
- [ ] 下週進度規劃及需求修正

---

### 🟦 Phase 5: 穩定化與 Demo 準備 (Week 9–10)
> **目標：修復 Bug 並優化系統展示流程。**

#### Week 9: 系統重構與強化
- [ ] 縮減 Rootfs 體積 (清理編譯期的不必要 symbols 與 docs)
- [ ] 加入系統看門狗 (Watchdog) 概念邏輯：若 App 當掉則自動重啟
- [ ] 優化 Log 資訊顯示，確保面試展示時一眼就能看到重點
- [ ] 下週進度規劃及需求修正

#### Week 10: Demo 腳本化與壓力測試
- [ ] 撰寫一鍵啟動 Demo 環境的 Makefile/Bash 腳本
- [ ] 準備三個展示案例：
    1. 正常版本升級展示
    2. 簽章不符更新失敗展示
    3. 更新中斷回滾展示
- [ ] 錄製操作影片作為備份
- [ ] 下週進度規劃及需求修正

---

### 🟪 Phase 6: 整理、筆記與輸出 (Week 11–12)
> **目標：將工程成果轉化為技術資產。**

#### Week 11: 文件撰寫 (Documentation)
- [ ] 整理技術筆記：從零開始的 Embedded Linux 建置教學
- [ ] 繪製正式的系統架構圖 (可以使用 Draw.io 或 Excalidraw)
- [ ] 撰寫高品質的 `README.md` (包含系統特色、如何執行、安全設計說明)
- [ ] 下週進度規劃及需求修正

#### Week 12: 履歷化與 Final Review
- [ ] 將程式碼整理並 Push 到 GitHub (確保 commit 訊息乾淨)
- [ ] 在履歷中加入 3-5 點關於此專案的成就描述 (量化指標，如：縮減體積 30%, 實現簽章驗證)
- [ ] 模擬面試問答：準備 5 個關於專案安全性的回答練習