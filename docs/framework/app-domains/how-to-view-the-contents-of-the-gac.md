---
title: "如何：檢視全域組件快取的內容"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- global assembly cache, viewing contents
- viewing assemblies in global assembly cache
- Gacutil.exe
- strong-named assemblies, global assembly cache
- GAC (global assembly cache), viewing contents
- list of assemblies in global assembly cache
- Global Assembly Cache tool
ms.assetid: c5f786a0-969b-4f14-9f02-e77c3384d9af
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 55ed52873b6fa944c3dd5d95066432f593719c2e
ms.contentlocale: zh-tw
ms.lasthandoff: 07/28/2017

---
# 如何：檢視全域組件快取的內容
您可以使用[全域組件快取工具 \(Gacutil.exe\)](../../../docs/framework/tools/gacutil-exe-gac-tool.md) 來檢視全域組件快取的內容。  
  
### 若要檢視全域組件快取中的組件清單  
  
1.  在 [Visual Studio 命令提示字元](../../../docs/framework/tools/developer-command-prompt-for-vs.md)輸入下列命令：  
  
     **gacutil \-l**   
     \-或\-               
     **gacutil \/l**  
  
 在舊版 .NET Framework 中，[Shfusion.dll](http://msdn.microsoft.com/zh-tw/0d9464cf-ddba-4ca9-bbec-f678fb58f380) Windows Shell Extension 可讓您在 \[檔案總管\] 中檢視全域組件快取。  從 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]開始，Shfusion.dll 已過時。  
  
## 請參閱  
 [使用組件和全域組件快取](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [Gacutil.exe (全域組件快取工具)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)

