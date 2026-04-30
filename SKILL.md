---
name: ai-data-recovery
title: AI Data Recovery Tool
category: software-development
version: 2.0
---

# AI Data Recovery Tool - 完整指南

## 功能概述

AI Data Recovery 是一款專業的硬碟救援軟體，類似 Final Data。核心功能包括：

- 跳過 MBR 直接讀取磁區 (Raw Sector Reading)
- 識別文件簽名 (Magic Numbers) 進行資料恢復
- 支援多種文件格式的掃描與還原
- AI 增強修復 recover 出來的文件

## 專案結構

```
ai-data-recovery/
├── main.py                    # 進入點
├── ai-data-recovery.spec      # PyInstaller 配置
├── core/                    # 核心硬碟救援邏輯
│   ├── disk_recovery.py
│   ├── disk_sector_scanner.py
│   ├── interfaces.py
│   └── ...
├── gui/                   # GUI 介面
│   ├── gui_main.py
│   └── ...
├── utils/               # 輔助工具
│   ├── ai_repair.py
│   └── ...
├── tests/               # 測試
├── windows/           # Windows 相關
└── references/        # 參考文件
```

## 核心功能

### 1. 跳過 MBR 直接讀取磁區

```
直接訪問: \\.\PhysicalDrive0
→ 讀取 raw sectors
→ 不經過文件系統
→ 不依賴 MBR/分區表
```

### 2. 文件識別

```
Magic Numbers:
• JPG: \xFF\xD8\xFF
• PNG: \x89PNG\r\n\x1a\n
• PDF: %!P(MISSING)DF
• ZIP: PK\x03\x04
• MP3: \xFF\xFB
• MP4: \x00\x00\x00\x1f\x66\x74\x79\x70
```

### 3. 數據恢復流程

```
掃描磁區 → 識別文件簽名 → 提取數據 → 恢復文件
```

## 與 FinalData 的相似之處

| 功能 | FinalData | AI Data Recovery |
|------|-----------|------------------|
| 跳過 MBR | ✅ | ✅ |
| Raw Sector Reading | ✅ | ✅ |
| File Signature Detection | ✅ | ✅ |
| Data Recovery | ✅ | ✅ |
| File Repair | ⭐ | ✅ (AI 增強) |

## 使用方式

```python
# Windows
python gui_main.py

# 或使用生成的 .exe
AI Data Recovery.exe
```

## 注意事項

1. **需要管理員權限** - 訪問物理磁碟需要 elevated permissions
2. **只讀模式** - 預設只讀，避免進一步損壞
3. **備份優先** - recover 後請立即備份
4. **不要寫入原磁碟** - 避免覆蓋 recover 的數據

## 🔨 打包為 Windows 執行檔

```bash
pyinstaller --onefile --windowed --name "AI Data Recovery" gui_main.py
```

## 🔄 GitHub Actions CI/CD

自動構建 Windows .exe 並上傳至 GitHub Releases。
