---
title: "預先不可部分完成 XName 物件 (LINQ to XML) (C#)"
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
ms.assetid: e84fbbe7-f072-4771-bfbb-059d18e1ad15
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: bc71a1a5b6d8fe038a9eefaff1649df0ea81aa02
ms.contentlocale: zh-tw
ms.lasthandoff: 07/28/2017

---
# <a name="pre-atomization-of-xname-objects-linq-to-xml-c"></a>預先不可部分完成 XName 物件 (LINQ to XML) (C#)
在 LINQ to XML 中改善效能的一個方式是預先不可部分完成 <xref:System.Xml.Linq.XName> 物件。 預先不可部分完成表示您先將字串指派給 <xref:System.Xml.Linq.XName> 物件，再使用 <xref:System.Xml.Linq.XElement> 和 <xref:System.Xml.Linq.XAttribute> 類別的建構函式建立 XML 樹狀結構。 接著，不是將字串傳遞至建構函式，這會將字串以隱含方式轉換成 <xref:System.Xml.Linq.XName>，而是傳遞初始化的 <xref:System.Xml.Linq.XName> 物件。  
  
 當您建立重複特定名稱的大型 XML 樹狀結構時，這樣做可以改善效能。 若要這樣做，請在建構 XML 樹狀結構之前先宣告並初始化 <xref:System.Xml.Linq.XName> 物件，然後使用 <xref:System.Xml.Linq.XName> 物件，而非指定項目和屬性名稱的字串。 如果您使用相同的名稱來建立大量項目 (或屬性)，這項技巧可能會大幅提升效能。  
  
 您應該使用自己的案例來測試預先不可部分完成，以便決定是否應該使用此作業。  
  
## <a name="example"></a>範例  
 下列範例為其示範。  
  
```csharp  
XName Root = "Root";  
XName Data = "Data";  
XName ID = "ID";  
  
XElement root = new XElement(Root,  
    new XElement(Data,  
        new XAttribute(ID, "1"),  
        "4,100,000"),  
    new XElement(Data,  
        new XAttribute(ID, "2"),  
        "3,700,000"),  
    new XElement(Data,  
        new XAttribute(ID, "3"),  
        "1,150,000")  
);  
  
Console.WriteLine(root);  
```  
  
 這個範例會產生下列輸出：  
  
```xml  
<Root>  
  <Data ID="1">4,100,000</Data>  
  <Data ID="2">3,700,000</Data>  
  <Data ID="3">1,150,000</Data>  
</Root>  
```  
  
 下列範例顯示 XML 文件位於命名空間中的相同技巧：  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XName Root = aw + "Root";  
XName Data = aw + "Data";  
XName ID = "ID";  
  
XElement root = new XElement(Root,  
    new XAttribute(XNamespace.Xmlns + "aw", aw),  
    new XElement(Data,  
        new XAttribute(ID, "1"),  
        "4,100,000"),  
    new XElement(Data,  
        new XAttribute(ID, "2"),  
        "3,700,000"),  
    new XElement(Data,  
        new XAttribute(ID, "3"),  
        "1,150,000")  
);  
  
Console.WriteLine(root);  
```  
  
 這個範例會產生下列輸出：  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Data ID="1">4,100,000</aw:Data>  
  <aw:Data ID="2">3,700,000</aw:Data>  
  <aw:Data ID="3">1,150,000</aw:Data>  
</aw:Root>  
```  
  
 下列範例更類似於您可能會在真實世界中遇到的狀況。 在此範例中，項目的內容是由查詢提供：  
  
```csharp  
XName Root = "Root";  
XName Data = "Data";  
XName ID = "ID";  
  
DateTime t1 = DateTime.Now;  
XElement root = new XElement(Root,  
    from i in System.Linq.Enumerable.Range(1, 100000)  
    select new XElement(Data,  
        new XAttribute(ID, i),  
        i * 5)  
);  
DateTime t2 = DateTime.Now;  
  
Console.WriteLine("Time to construct:{0}", t2 - t1);  
```  
  
 上一則範例的執行效能比下列範例要好，因為其名稱並非預先不可部分完成：  
  
```csharp  
DateTime t1 = DateTime.Now;  
XElement root = new XElement("Root",  
    from i in System.Linq.Enumerable.Range(1, 100000)  
    select new XElement("Data",  
        new XAttribute("ID", i),  
        i * 5)  
);  
DateTime t2 = DateTime.Now;  
  
Console.WriteLine("Time to construct:{0}", t2 - t1);  
```  
  
## <a name="see-also"></a>另請參閱  
 [效能 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/performance-linq-to-xml.md)   
 [不可部分完成的 XName 和 XNamespace 物件 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/atomized-xname-and-xnamespace-objects-linq-to-xml.md)

