# 專案企畫書 proposal

## Overview
    1. 規劃總覽
    2. 專案需求
    3. 各週規劃

## 規劃總覽
規劃於 14 週，每週 20 小時。完成此專案 ( 2026 年寒假 )，大致分為以下7個階段性目標

    Week 01 ~ 02 : 建立專案結構 & 掌握先備知識
    Week 03 ~ 04 : Embedded Linux 環境建置
    Week 05 ~ 06 : 系統理解 & 簡易應用
    Week 07 ~ 08 : OTA 更新機制
    Week 09 ~ 10 : 安全機制
    Week 11 ~ 12 : 穩定 & Demo
    Week 13 ~ 14 : 筆記整理 & 專案總結

-----
## 專案需求
##### Functional 
    1. 系統 : 能在 QEMU 上成功載入 Bootloader、Kernel 並掛載 Rootfs (（kernel + rootfs + user-space）)
    2. 安全 : 系統更新前必須使用內建的公鑰驗證更新包的數位簽章進行認證
    3. OTA  : 系統能檢查目前軟體包是否為最新版本，拒絕格式錯誤或簽章失敗的更新
    4. 日誌 : 系統需記錄更新歷史、成功與失敗的原因，以便開發者除錯

##### Non-functional
    1. 安全性核心 : 完整/真實性確認、最小權限執行(可捨)
    2. 可靠性 : 即使 OTA 更新失敗，裝置也開機
    3. 資源效率 : Rootfs 的體積應盡量精簡（例如小於 50MB）、從開機到應用程式執行的時間控制在10秒內(可改)
    4. 可維護性 : 模組化 & 完整README

-----
## 各週規劃
計畫於前一週預留２小時進行下週進度規劃，不要求於第一週完成全局規劃。

#### Week 1 規劃加基礎了解
    1. ---
    2. 規劃 Week 1 / Week 2
    3. Know/note : 嵌入式系統 (GPT)
    4. Know/note : Embedded Linux 架構全景 (GPT)
    5. Know/note : 開機流程（Boot Flow）(GPT)
    5. week. 整理本週進度 -> week1.md

#### Week 2 學習/複習
    1. Know/note : 嵌入式系統限制與設計思維 (GPT)
    2. Know/note : 嵌入式系統安全 (GPT)
    3. Know/note : QEMU + Buildroot (GPT)
    4. 配置專案環境 linux / make file / 專案資料夾結構  
    5. Linux 指令複習 / 整理本週進度 -> week2.md
