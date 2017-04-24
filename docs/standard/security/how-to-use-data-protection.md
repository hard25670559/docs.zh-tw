---
title: "How to: Use Data Protection | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "DPAPI"
  - "encryption [.NET Framework], data protection API"
  - "data [.NET Framework], decryption"
  - "ProtectedMemory class, about ProtectedMemory class"
  - "ProtectedData class, about ProtectedData class"
  - "cryptography [.NET Framework], data protection API"
  - "data protection API [.NET Framework]"
  - "decryption"
  - "data [.NET Framework], encryption"
ms.assetid: 606698b0-cb1a-42ca-beeb-0bea34205d20
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Use Data Protection
.NET Framework 提供資料保護 API \(DPAPI\) 的存取，這可讓您使用目前使用者帳戶或電腦的資訊來加密資料。  當您使用 DPAPI 時，會減少明確產生並儲存密碼編譯金鑰的困難問題。  
  
 使用 <xref:System.Security.Cryptography.ProtectedMemory> 類別來加密記憶體中的位元組陣列。  這項功能提供於 Microsoft Windows XP 和更新版本的作業系統。  您可以指定由目前處理序加密的記憶體只能由目前的處理序解密、可由所有處理序解密，或是可從相同的使用者內容解密。  請參閱 <xref:System.Security.Cryptography.MemoryProtectionScope> 列舉，以取得 <xref:System.Security.Cryptography.ProtectedMemory> 選項的詳細說明。  
  
 使用 <xref:System.Security.Cryptography.ProtectedData> 類別來加密位元組陣列的複本。  這項功能提供於 Microsoft Windows 2000 和更新版本的作業系統。  您可以指定由目前使用者帳戶加密的資料只能由相同的使用者帳戶解密，或是您可以指定目前使用者帳戶加密的資料可以由電腦上的任何帳戶解密。  請參閱 <xref:System.Security.Cryptography.DataProtectionScope> 列舉，以取得 <xref:System.Security.Cryptography.ProtectedData> 選項的詳細說明。  
  
### 使用資料保護來加密記憶體中的資料  
  
1.  呼叫靜態 <xref:System.Security.Cryptography.ProtectedMemory.Protect%2A> 方法並傳遞要加密的位元組陣列、entropy 及記憶體保護範圍。  
  
### 使用資料保護來解密記憶體中的資料  
  
1.  呼叫靜態 <xref:System.Security.Cryptography.ProtectedMemory.Unprotect%2A> 方法並傳遞要解密的位元組陣列及記憶體保護範圍。  
  
### 使用資料保護將資料加密到檔案或資料流  
  
1.  建立隨機的 entropy。  
  
2.  呼叫靜態 <xref:System.Security.Cryptography.ProtectedData.Protect%2A> 方法並傳遞要加密的位元組陣列、entropy 及資料保護範圍。  
  
3.  將加密的資料寫入檔案或資料流。  
  
### 使用資料保護從檔案或資料流解密資料  
  
1.  從檔案或資料流讀取加密的資料。  
  
2.  呼叫靜態 <xref:System.Security.Cryptography.ProtectedData.Unprotect%2A> 方法並傳遞要解密的位元組陣列及資料保護範圍。  
  
## 範例  
 下列程式碼範例示範兩種形式的加密和解密。  首先，程式碼範例會加密，然後再解密記憶體中的位元組陣列。  接下來，程式碼範例會加密位元組陣列的複本、將它儲存至檔案、從檔案載入資料，然後再解密資料。  此範例會顯示原始資料、加密的資料和解密的資料。  
  
 [!code-csharp[DPAPI-HowTO#1](../../../samples/snippets/csharp/VS_Snippets_CLR/DPAPI-HowTO/cs/sample.cs#1)]
 [!code-vb[DPAPI-HowTO#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DPAPI-HowTO/vb/sample.vb#1)]  
  
## 編譯程式碼  
  
-   包含 `System.Security.dll` 的參考。  
  
-   包含 <xref:System>、<xref:System.IO>、<xref:System.Security.Cryptography> 和 <xref:System.Text> 命名空間。  
  
## 請參閱  
 <xref:System.Security.Cryptography.ProtectedMemory>   
 <xref:System.Security.Cryptography.ProtectedData>