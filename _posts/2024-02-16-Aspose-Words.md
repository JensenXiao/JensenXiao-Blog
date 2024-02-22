---
layout: post
title: EUDC Characters in Aspose.Words
date: 2024-02-16
description: How to use User-Defined Characters (EUDC) in Aspose.Words
tags: [Windows , Form , C Sharp]
cover: 'assets/images/AsposeWords.png'
last_modified_at: 2024-02-22
--- 
## Aspose.Words 自造字無法顯示問題  

- 套印 word 文件時，EUDC 自造字無法正確顯示  
  
  ![難字不正常](https://hackmd.io/_uploads/SJn6ENEn6.png)  

- 設定 EUDC 字型檔案與系統字型連結  
    - 當拿到字造字型檔 (TTE or TTF) 放到電腦後，要設定機碼讓它連結到系統字型  
    - 在開始中輸入「regedit」，機碼目錄為 電腦\HKEY_CURRENT_USER\EUDC\950  
    - 機碼 SystemDefaultEUDCFont，修改值為 EUDC 字型檔所在目錄  
  
- 重開機後，可直接開啟 Word 檔，另存成 PDF 檔案來驗證 一般字及自造字 是否完整呈現  


## Aspose.Words 轉 PDF 檔，只有顯示自造字  

- 使用 Aspose.Words 將 word 文件轉 PDF 檔時，只有 EUDC 自造字正確顯示，其他字型變成黑點  
  
  ![系統字型錯誤](https://hackmd.io/_uploads/SJBMHNN26.png)  
  
- 在 C# 程式 SetFontsSources 載入字型方法中  
    - 除了載入自造字型(FileFontSource)  
    - 也需載入系統自型(SystemFontSource)  

    ```csharp
    Aspose.Words.Document doc = new Aspose.Words.Document(@"C:\EUDC\Test.doc");

    FontSettings.DefaultInstance.SetFontsSources(
        new FontSourceBase[]
        { 
            new SystemFontSource(), 
            new FileFontSource(@"C:\EUDC\JH.TTE") 
        });
        
    doc.Save(@"C:\EUDC\Test.pdf");
    ```
- 補上之後查看 Test.pdf 一般字及自造字皆有正確呈現  
  
  ![字型正常顯示](https://hackmd.io/_uploads/r1drBVNhp.png)  
