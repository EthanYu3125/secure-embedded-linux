# Linux 架構與功能

## 類別
    1. 核心 : linux這個詞代表的本身，可以自己新增修改種多功能
    2. 開發商版本 : 融入眾多功能，讓用戶不用很熟悉指令也可以操作電腦，ex : ubnutu 
## 原版 linux 架構
linux 由C語言撰寫(大部分)，可自行修改/編譯核心功能
七大核心區塊:

    1. 啟動 : 驅動系統
    2. 通訊 : 網路管理
    3. 排程 : 行程管理
    4. MEM : 記憶體管理
    5. 文件 : 文件管理
    6. 中斷 : 中斷系統
    7. 錯誤 : 錯誤偵測

簡易資料夾結構:

    linux/
    ├── arch/                # [重要] 硬體架構相關代碼 (Architecture)
    │   ├── arm/             # ARM 架構相關 (QEMU 模擬通常看這)
    │   │   └── boot/dts/    # 設備樹 (Device Tree) - 定義硬體長什麼樣
    │   └── x86/             # PC 架構相關
    ├── drivers/             # [重要] 驅動程式 (佔核心 60% 以上的代碼)
    │   ├── char/            # 字元設備 (如 UART, 序列埠)
    │   ├── net/             # 網路卡驅動
    │   └── usb/             # USB 相關
    ├── kernel/              # [核心] 核心排程、行程管理 (Process Management)
    ├── mm/                  # 記憶體管理 (Memory Management)
    ├── fs/                  # 檔案系統 (Filesystems: Ext4, FAT, NFS...)
    ├── net/                 # 網路協議棧 (TCP/IP 邏輯)
    ├── include/             # 標頭檔 (.h)
    └── scripts/             # 編譯過程中會用到的輔助腳本

* AI提供(建議後續驗證)
## 嵌入式 linux 架構
在原版的架構上修改
`linux 的核心比較簡單，也有提供配置功能，可自主配置相關內容`

## linux build 工具介紹
除去特殊形況，通常會使用開源的 build linux 工具加快linux 建立。
（kernel + rootfs + user-space）

1. Buildroot : 小而精簡
2. Yocto : 較複雜的管理、彈性高、不好學習
3. Ubuntu Core / Debian : 完整性高、彈性低
4. OpenWrt : 為網路設備設計


## ~~原版 vs 嵌入式~~