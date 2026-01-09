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