---
title: "載入或剖析 XML 時保留空白字元1 | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: f3ff58c4-55aa-4fcd-b933-e3a2ee6e706c
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1b2ec9b5b1bbc343fde5c9527c1e4f4ad7f14796
ms.lasthandoff: 03/13/2017

---
# <a name="preserving-white-space-while-loading-or-parsing-xml"></a>載入或剖析 XML 時保留空白字元
這個主題描述如何控制 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 的空白字元行為。  
  
 常見的案例為讀取縮排的 XML、建立沒有任何空白字元文字節點 (也就是不保留空白字元) 的記憶體中 XML 樹狀結構、在 XML 上執行某些作業，然後儲存包含縮排的 XML。 當您序列化具有格式的 XML 時，只會保留 XML 樹狀結構中的有效空白字元。 這是 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 的預設行為。  
  
 其他常見案例為讀取與修改已經過刻意縮排的 XML。 您可能不想用任何方式變更這個縮排。 在 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 中，如果您在載入或剖析 XML 時保留空白字元，並在序列化 XML 時停用格式化，就可以達到這個效果。  
  
 這個主題描述填入 XML 樹狀之方法的空白字元行為。 如需序列化 XML 樹狀結構時控制空白字元的資訊，請參閱[序列化時保留空白字元](../../../../csharp/programming-guide/concepts/linq/preserving-white-space-while-serializing.md)。  
  
## <a name="behavior-of-methods-that-populate-xml-trees"></a>填入 XML 樹狀之方法的行為  
 下列 <xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq.XDocument> 類別中的方法會填入 XML 樹狀結構。 您可以從檔案、<xref:System.IO.TextReader>、<xref:System.Xml.XmlReader> 或字串填入 XML 樹狀結構：  
  
-   <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=fullName>  
  
 如果此方法不採用 <xref:System.Xml.Linq.LoadOptions> 當做引數，該方法將不會保留有效的空白字元。  
  
 在大部分的情況下，如果此方法採用 <xref:System.Xml.Linq.LoadOptions> 當做引數，您可以選擇性地保留有效空白字元當做 XML 樹狀結構中的文字節點。 不過，如果此方法是從 <xref:System.Xml.XmlReader> 載入 XML，則 <xref:System.Xml.XmlReader> 會決定是否要保留空白字元。 設定 <xref:System.Xml.Linq.LoadOptions> 不會有任何作用。  
  
 利用這些方法，如果保留空白字元，會將有效的空白字元插入到 XML 樹狀結構中，當做 <xref:System.Xml.Linq.XText> 節點。 如果不保留空白字元，則不會插入文字節點。  
  
 您可以使用 <xref:System.Xml.XmlWriter> 來建立 XML 樹狀結構。 寫入到 <xref:System.Xml.XmlWriter> 中的節點會填入樹狀結構中。 不過，當您使用這個方法建置 XML 樹狀時，不管節點是否為空白字元，也不管空白字元是否有效，都會保留所有節點。  
  
## <a name="see-also"></a>另請參閱  
 [剖析 XML (C#)](../../../../csharp/programming-guide/concepts/linq/parsing-xml.md)