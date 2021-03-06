---
title: "HOW TO：讓 WCF 能夠存取 X.509 憑證 | Microsoft Docs"
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
  - "憑證 [WCF], 讓 WCF 能夠存取 X.509 憑證"
  - "X.509 憑證 [WCF]"
  - "X.509 憑證 [WCF], 讓 WCF 能夠存取"
ms.assetid: a54e407c-c2b5-4319-a648-60e43413664b
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# HOW TO：讓 WCF 能夠存取 X.509 憑證
若要讓 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 能夠存取 X.509 憑證，應用程式程式碼必須指定憑證存放區名稱及位置。在某些狀況下，處理序身分識別必須能夠存取包含與 X.509 憑證相關聯之私密金鑰的檔案。若要取得與憑證存放區中 X.509 憑證相關聯的私密金鑰，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 必須有進行這項作業的權限。根據預設，只有擁有人和系統帳戶能夠存取憑證的私密金鑰。  
  
### 讓 WCF 能夠存取 X.509 憑證  
  
1.  對於用以執行 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的帳戶，授與含有與 X.509 憑證相關聯之私密金鑰之檔案的讀取權限。  
  
    1.  判斷 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 是否需要 X.509 憑證之私密金鑰的讀取權限。  
  
         下表詳細列出在使用 X.509 憑證時是否必須要提供私密金鑰。  
  
        |X.509 憑證使用方式|私密金鑰|  
        |------------------|----------|  
        |數位簽署傳出的 SOAP 訊息。|是|  
        |確認傳入之 SOAP 訊息的簽章。|否|  
        |加密傳出的 SOAP 訊息。|否|  
        |解密傳入的 SOAP 訊息。|是|  
  
    2.  判斷憑證存放於其中的憑證存放區位置和名稱。  
  
         憑證存放於其中的憑證存放區會指定於應用程式程式碼或組態中。例如，下列範例會指定憑證是位於名為 `My` 的 `CurrentUser` 憑證存放區中。  
  
         [!code-csharp[x509Accessible#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/x509accessible/cs/source.cs#1)]
         [!code-vb[x509Accessible#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/x509accessible/vb/source.vb#1)]  
  
    3.  使用 [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md) 工具，即可判斷憑證的私密金鑰在電腦上的位置。  
  
         [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md) 工具需要憑證存放區名稱、憑證存放區位置，以及可以唯一識別該憑證的資料。此工具會接受憑證的主體名稱或是其指紋來做為唯一識別項。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何判斷憑證指紋的詳細資訊，請參閱 [HOW TO：擷取憑證的指紋](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)。  
  
         下列程式碼範例會使用 [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md) 工具，配合指紋 `46 dd 0e 7a ed 0b 7a 31 9b 02 a3 a0 43 7a d8 3f 60 40 92 9d` 來判斷 `CurrentUser` 之 `My` 存放區中憑證之私密金鑰的位置。  
  
        ```  
        findprivatekey.exe My CurrentUser -t "46 dd 0e 7a ed 0b 7a 31 9b 02 a3 a0 43 7a d8 3f 60 40 92 9d" -a  
        ```  
  
    4.  判斷 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在其下執行的帳戶。  
  
         下表詳細列出在特定案例中用以執行 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的帳戶。  
  
        |案例|處理序身分識別|  
        |--------|-------------|  
        |用戶端 \(主控台或 WinForms 應用程式\)。|目前登入的使用者。|  
        |自我裝載的服務。|目前登入的使用者。|  
        |裝載於 IIS 6.0 \([!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]\) 或 IIS 7.0 \([!INCLUDE[wv](../../../../includes/wv-md.md)]\) 中的服務。|網路服務|  
        |裝載於 IIS 5.X \([!INCLUDE[wxp](../../../../includes/wxp-md.md)]\) 中的服務。|由 Machine.config 檔中的 `<processModel>` 項目控制。預設帳戶是 ASPNET。|  
  
    5.  使用類似 cacls.exe 的工具，對用以執行 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的帳戶授與包含該私密金鑰之檔案的讀取權限。  
  
         下列程式碼範例會編輯 \(\/E\) 已指定檔案的存取控制清單 \(ACL\)，以便對網路服務帳戶授與 \(\/G\) 該檔案的讀取權限 \(:R\)。  
  
        ```  
        cacls.exe "C:\Documents and Settings\All Users\Application Data\Microsoft\Crypto\RSA\MachineKeys\8aeda5eb81555f14f8f9960745b5a40d_38f7de48-5ee9-452d-8a5a-92789d7110b1" /E /G "NETWORK SERVICE":R  
        ```  
  
## 請參閱  
 [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md)   
 [HOW TO：擷取憑證的指紋](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)   
 [使用憑證](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)