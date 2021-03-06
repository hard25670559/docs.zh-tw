---
title: "SQL 產生 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e16aa02-d458-4418-a765-58b42aad9315
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# SQL 產生
當您為 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 撰寫提供者時，您必須將 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 命令樹轉譯成特定資料庫可以了解的 SQL，例如 SQL Server 的 Transact\-SQL 或 Oracle 的 PL\/SQL。  在本章節中，您將會學習如何為 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 提供者開發 SQL 產生元件 \(適用於 SELECT 查詢\)。  如需插入、更新及刪除查詢的詳細資訊，請參閱[修改 SQL 產生](../../../../../docs/framework/data/adonet/ef/modification-sql-generation.md)。  
  
 若要了解本章節，您應該要熟悉 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 及 ADO.NET 提供者模型。  您也應該了解命令樹和 <xref:System.Data.Common.CommandTrees.DbExpression>。  
  
## SQL 產生模組的角色  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 提供者的 SQL 產生模組會將給定的查詢命令樹轉譯成單一 SQL SELECT 陳述式，此陳述式是以 SQL:1999 相容的資料庫為目標。  產生的 SQL 應該盡量擁有少一點的巢狀查詢。  SQL 產生模組不應該簡化查詢命令樹的輸出。  [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 將會進行這項處理，例如藉由除去聯結及摺疊連續的篩選節點。  
  
 <xref:System.Data.Common.DBProviderServices> 類別是存取 SQL 產生層的起點，可將命令樹轉換成 <xref:System.Data.Common.DbCommands>。  
  
## 本章節內容  
 [命令樹的形狀](../../../../../docs/framework/data/adonet/ef/the-shape-of-the-command-trees.md)  
  
 [從命令樹產生 SQL \- 最佳作法](../../../../../docs/framework/data/adonet/ef/generating-sql-from-command-trees-best-practices.md)  
  
 [範例提供者中的 SQL 產生](../../../../../docs/framework/data/adonet/ef/sql-generation-in-the-sample-provider.md)  
  
## 請參閱  
 [撰寫 Entity Framework 資料提供者](../../../../../docs/framework/data/adonet/ef/writing-an-ef-data-provider.md)