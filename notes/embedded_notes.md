# What is 嵌入式
### 嵌入式特性
1. 有限資源
2. 有限功能
3. 有限操作 (固定功能)
4. 即時系統 (RTOS)
5. 需要特別注意 : 中斷 / us級計時 / IO 
<span style="color:red;"> * 反因為果 </span>
6. 定義已模糊 -> 內嵌邏輯核心 -> 資源受限

### 嵌入式硬體
    基礎層級 : 
        1. 微控制器 (MCU) : CPU / 記憶單元 / 控制單元 / IO ，無 MMU 不使用 linux ，如 Aduino
        2. 微處理器 (MPU) : CPU / 記憶單元 / 控制單元 ( 含 MMU ) / linux 作業系統 ， 已具有系統概念 ， 如 Raspberry Pi
        3. 應用Soc : 更複雜的 MPU，與 MPU 分界模糊，如手機晶片(Mobile Soc)

    特殊定義 : 
        1. FGPA : 可程式化邏輯閘陣列，可調整硬體邏輯，適用於開發階段
        2. Soc : 單晶片(多功能單元整合於單一晶片)，只要符合定義都可以是Soc
        3. SBC : 單板電腦 Soc + 電腦架構
        4. DSP : 數位訊號處理器，專為高效處理數字信號（音訊、影像）設計，常見於通信和音訊設備。

### 嵌入式系統 Bootloader (開機程序)
    1. CPU -> 讀取唯讀程式 -> 初始化記憶體 -> 二階段啟動裝置(SD/Flash/USB)(Bootloader)
    2. Bootloader 初始化記憶體 -> Linux Kernel 並把它搬進記憶體(kernel 安全認證) 
    3. kernel : 掛載Rootfs
    4. 第一個程式(init process)

### 嵌入式思維

    keyword:
        Embedded Linux 限制 
        Read-only root filesystem 唯獨式根目錄系統
        Embedded Linux update risk 更新陷阱
        Firmware update embedded device 韌體更新

### 嵌入式安全
    1. 設備辨識
    2. 安全性更新
    3. know (此專案無使用)
        (1) Secure Boot
        (2) Hardware Root of Trust 硬體信任根

一、設備辨識

    方式 :
    1. MAC
    2. 公私鑰數位證書
    3. 物理不可複製功能 -> 製程時的小誤差
二、 安全性更新

    why :
    1. 真實性(認證)
    2. 完整性
    3. 機密性

    流程 :
    1. 簽署 : 安全性證書 
        (1) 編譯固件：生成新的二進位檔案 (Binary)。 
        (2) 生成摘要：使用雜湊函數 (如 SHA-256) 計算固件摘要。
        (3) 數位簽署：使用私鑰 (Private Key) 對摘要進行加密，生成 數位簽章 (Digital Signature)。
        (4) 加密 (可選)：使用對稱密鑰 (如 AES) 對固件進行加密。
    
    2. 傳輸 : 傳到設備
    
    3. 驗證 : 證書確認 & 執行更新
        (1) 接收與暫存：將固件存放在副分區 (Secondary Slot)。
        (2) 驗證簽章：設備使用內置的 公鑰 (Public Key) 驗證簽章。若驗證失敗，立即捨棄更新。
        (3) 解密 (若有加密)：使用儲存在安全硬體中的密鑰解密。
        (4)防回滾檢查 (Anti-Rollback)：檢查版本號。確保新版本不低於當前版本，防止攻擊者強制設備降級到已知有漏洞的舊版本。
        (5) 寫入與重啟：更新引導程序 (Bootloader) 的指向，切換到新固件。


三、 更深入內容

1. Secure Boot 安全啟動    
    > 在系統軟體執行時的階段性檢查，類似安檢
2. Hardware Root of Trust 硬體信任根
    > 純硬體唯讀安全資料
3. 信任鍊 = 1. + 2. 



