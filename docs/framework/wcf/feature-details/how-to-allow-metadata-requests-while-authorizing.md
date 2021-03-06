---
title: "HOW TO：授權時同時允許中繼資料要求 | Microsoft Docs"
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
  - "授權 [WCF] 時同時允許中繼資料要求"
ms.assetid: 90cec34f-b619-452b-a056-8b1c0de49d05
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# HOW TO：授權時同時允許中繼資料要求
自訂授權期間，可能需要允許處理中繼資料的要求。下列主題逐步解說要驗證如此要求的步驟。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 授權的詳細資訊，請參閱 [授權](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)。  
  
### 授權時同時允許中繼資料要求  
  
1.  建立 <xref:System.ServiceModel.ServiceAuthorizationManager> 類別的延伸。  
  
2.  覆寫 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> 方法。方法會依據是否允許授權而傳回 `true` 或 `false`。關於目前程式的資訊可在 <xref:System.ServiceModel.OperationContext> 傳給方法的參數找到。  
  
3.  在覆寫中，如以下範例所示，檢查合約名稱、命名空間以及動作。若條件有效，會傳回 `true.`  
  
4.  使用擴充點套用類別。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][HOW TO：為服務建立自訂授權管理員](../../../../docs/framework/wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md).  
  
## 範例  
 下例範例示範 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> 方法的覆寫。  
  
 [!code-csharp[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/cs/source.cs#1)]
 [!code-vb[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/vb/source.vb#1)]  
  
## 請參閱  
 <xref:System.ServiceModel.ServiceAuthorizationManager>   
 [授權](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)   
 [使用身分識別模型來管理宣告與授權](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)