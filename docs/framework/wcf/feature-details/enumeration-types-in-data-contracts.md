---
title: "資料合約中的列舉型別 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "資料合約 [WCF], 列舉型別"
ms.assetid: b5d694da-68cb-4b74-a5fb-75108a68ec3b
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# 資料合約中的列舉型別
列舉可以在資料合約模型中表示。  本主題將逐步介紹幾個範例，說明程式設計模型。  
  
## 列舉基本知識  
 使用資料合約模型中列舉型別的其中一種方法是，將 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性套用至型別。  然後您必須將 <xref:System.Runtime.Serialization.EnumMemberAttribute> 屬性套用至必須包含在資料合約中的各個成員。  
  
 以下範例顯示兩個類別。  第一個是使用列舉，而第二個是定義列舉。  
  
 [!code-csharp[c_DataContractEnumerations#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#1)]
 [!code-vb[c_DataContractEnumerations#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#1)]  
  
 只有 `condition` 欄位設定為值 `New`、`Used` 或 `Rental` 的其中之一時，才可以傳送或接收 `Car` 類別的執行個體。  如果 `condition` 是 `Broken` 或 `Stolen`，便會擲回 <xref:System.Runtime.Serialization.SerializationException>。  
  
 您可以和往常一樣，對列舉資料合約使用 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性 \(<xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> 和 <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>\)。  
  
### 列舉成員值  
 資料合約通常包括列舉成員名稱，而不是數值。  然而，當使用資料合約模型時，如果接收端是 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 用戶端，匯出的結構描述就會保存數值。  請注意，當使用 [使用 XmlSerializer 類別](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md)時則否。  
  
 在前例中，如果 `condition` 設定為 `Used` 且資料序列化為 XML，結果 XML 就是 `<condition>Used</condition>` 而不是 `<condition>1</condition>`。  因此，下列資料合約相等於 `CarConditionEnum` 的資料合約。  
  
 [!code-csharp[c_DataContractEnumerations#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#2)]
 [!code-vb[c_DataContractEnumerations#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#2)]  
  
 例如，您可以在傳送端上使用 `CarConditionEnum`，而在接收端上使用 `CarConditionWithNumbers`。  雖然傳送端對 `Used` 使用 "1" 值，而接收端使用 "20" 值，但是 XML 表示法對兩端都是 `<condition>Used</condition>`。  
  
 如果要包含在資料合約中，您必須套用 <xref:System.Runtime.Serialization.EnumMemberAttribute> 屬性。  在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 中，您永遠可以對列舉套用特殊值 0 \(零\)，這也是任何列舉的預設值。  然而，即使這個特殊的零值也無法序列化，除非它標上 <xref:System.Runtime.Serialization.EnumMemberAttribute> 屬性。  
  
 這種情形有兩個例外狀況：  
  
-   旗標列舉 \(本主題稍後說明\)。  
  
-   <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 屬性設定為 `false` 的列舉資料成員 \(在這種情況中，只會從序列化的資料中省略值為零的列舉\)。  
  
### 自訂列舉成員值  
 您可以使用 <xref:System.Runtime.Serialization.EnumMemberAttribute> 屬性 \(Attribute\) 的 <xref:System.Runtime.Serialization.EnumMemberAttribute.Value%2A> 屬性 \(Property\) 來自訂列舉成員值，該值會成為資料合約的一部分。  
  
 例如，下列資料合約也相等於 `CarConditionEnum` 的資料合約。  
  
 [!code-csharp[c_DataContractEnumerations#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#3)]
 [!code-vb[c_DataContractEnumerations#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#3)]  
  
 當序列化時，`PreviouslyOwned` 的值具有 XML 表示法 `<condition>Used</condition>`。  
  
## 簡單列舉  
 您也可以序列化列舉型別至尚未套用的 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性。  此類列舉型別的處理方式完全如先前所述，除了每個成員 \(未套用 <xref:System.NonSerializedAttribute> 屬性\) 會被視為已套用 <xref:System.Runtime.Serialization.EnumMemberAttribute> 屬性之外。  例如，以下列舉隱含具有相等於上一個 `CarConditionEnum` 範例的資料合約。  
  
 [!code-csharp[c_DataContractEnumerations#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#6)]
 [!code-vb[c_DataContractEnumerations#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#6)]  
  
 當您不需要自訂列舉的資料合約名稱和命名空間和列舉成員值時，可以使用簡單列舉。  
  
#### 簡單列舉的注意事項  
 將 <xref:System.Runtime.Serialization.EnumMemberAttribute> 屬性套用至簡單列舉沒有作用。  
  
 <xref:System.SerializableAttribute> 屬性是否套用至列舉並沒有差別。  
  
 事實上 <xref:System.Runtime.Serialization.DataContractSerializer> 類別允許套用至列舉成員的 <xref:System.NonSerializedAttribute> 屬性，與 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 和 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> 的行為是不同的。  這兩個序列化程式都會略過 <xref:System.NonSerializedAttribute> 屬性。  
  
## 旗標列舉  
 您可以將 <xref:System.FlagsAttribute> 屬性套用至列舉。  在這種情況下，可以同時傳送或接收零或更多列舉值的清單。  
  
 如果要執行這項操作，請將 <xref:System.Runtime.Serialization.DataContractAttribute> 屬性套用至旗標列舉，然後將所有為二之次方的成員以 <xref:System.Runtime.Serialization.EnumMemberAttribute> 屬性標示。  請注意，如果要使用旗標列舉，級數必須是 2 的次方的不中斷序列 \(例如，1、2、4、8、16、32、64\)。  
  
 下列步驟適用於傳送旗標的列舉值：  
  
1.  請嘗試尋找對應至數值的列舉成員 \(已套用 <xref:System.Runtime.Serialization.EnumMemberAttribute> 屬性\)。  如果找到，請傳送只包含該成員的清單。  
  
2.  請嘗試將數值中斷至某個總和，以具有對應至該總和之各部分的列舉成員 \(每個都套用 <xref:System.Runtime.Serialization.EnumMemberAttribute> 屬性\)。  傳送所有這些成員的清單。  請注意，「*窮盡演算法*」\(Greedy Algorithm\) 是用於尋找此類總和，因此即使此類總和存在，也不保證會找到。  如果要避免這個問題，請確保列舉成員的數值是二的次方。  
  
3.  如果上述兩個步驟失敗，且數值非零，請擲回 <xref:System.Runtime.Serialization.SerializationException>。  如果數值為零，則傳送空白清單。  
  
### 範例  
 下面的列舉範例可用於旗標作業中。  
  
 [!code-csharp[c_DataContractEnumerations#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#4)]
 [!code-vb[c_DataContractEnumerations#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#4)]  
  
 下列範例值會依指示進行序列化。  
  
 [!code-csharp[c_DataContractEnumerations#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractenumerations/cs/source.cs#5)]
 [!code-vb[c_DataContractEnumerations#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractenumerations/vb/source.vb#5)]  
  
## 請參閱  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 [使用資料合約](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [指定服務合約中的資料傳輸](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)