---
title: "dotnet test 命令 - .NET Core CLI"
description: "dotnet test 命令是用來在指定的專案中執行單元測試。"
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: 55329bed71be21a787d6e77d8c0ea67d607676b8
ms.contentlocale: zh-tw
ms.lasthandoff: 08/14/2017

---
# <a name="dotnet-test"></a>dotnet test

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet test` - 用來執行單元測試的 .NET 測試驅動程式。

## <a name="synopsis"></a>概要

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)


```
dotnet test [<PROJECT>] [-a|--test-adapter-path] [-c|--configuration] [--collect] [-d|--diag] [-f|--framework] [--filter] [-l|--logger] [--no-build] [--no-restore] [-o|--output] [-r|--results-directory] [-s|--settings] [-t|--list-tests] [-v|--verbosity]
dotnet test [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```
dotnet test [<PROJECT>] [-a|--test-adapter-path] [-c|--configuration] [-d|--diag] [-f|--framework] [--filter] [-l|--logger] [--no-build] [-o|--output] [-s|--settings] [-t|--list-tests]  [-v|--verbosity]
dotnet test [-h|--help]
```
---

## <a name="description"></a>說明

`dotnet test` 命令是用來在指定的專案中執行單元測試。 單元測試是與單元測試架構 (例如 MSTest、NUnit 或 xUnit) 具有相依性的主控台應用程式專案，以及該單元測試架構的 dotnet 測試執行器。 這些會封裝為 NuGet 套件，並還原為專案的一般相依性。

測試專案也必須指定測試執行器。 這是使用一般 `<PackageReference>` 元素所指定，如下列範例專案檔中所示：

[!code-xml[XUnit 基本範本](../../../samples/snippets/csharp/xunit-test/xunit-test.csproj)]

## <a name="arguments"></a>引數

`PROJECT`

指定測試專案的路徑。 如果省略，則會預設為目前目錄。

## <a name="options"></a>選項

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

在測試執行中，從指定的路徑使用自訂測試配接器。

`-c|--configuration {Debug|Release}`

定義組建組態。 預設值是 `Debug`，但您的專案組態無法覆寫這個預設的 SDK 設定。

`--collect <DATA_COLLECTOR_FRIENDLY_NAME>`

測試回合啟用資料收集器。 如需詳細資訊，請參閱[監視及分析測試回合](https://aka.ms/vstest-collect)。

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

針對測試平台啟用診斷模式，並將診斷訊息寫入至指定的檔案。

`-f|--framework <FRAMEWORK>`

尋找特定[架構](../../standard/frameworks.md)的測試二進位檔。

`--filter <EXPRESSION>`

使用指定的運算式篩選出目前專案中的測試。 如需詳細資訊，請參閱[篩選選項詳細資料](#filter-option-details)一節。 如需如何使用選擇性單元測試篩選的其他資訊及範例，請參閱[執行選擇性單元測試](../testing/selective-unit-tests.md)。

`-h|--help`

印出命令的簡短說明。

`-l|--logger <LoggerUri/FriendlyName>`

指定測試結果的記錄器。

`--no-build`

請不要在執行之前建置測試專案。

`--no-restore`

執行命令時，不執行隱含的還原。

`-o|--output <OUTPUT_DIRECTORY>`

在其中尋找要執行的二進位檔的目錄。

`-r|--results-directory <PATH>`

要放置測試結果的目錄。 指定的目錄如不存在即建立。

`-s|--settings <SETTINGS_FILE>`

執行測試時要使用的設定。

`-t|--list-tests`

列出在目前專案中探索到的所有測試。

`-v|--verbosity <LEVEL>`

設定命令的詳細資訊層級。 允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-a|--test-adapter-path <PATH_TO_ADAPTER>`

在測試執行中，從指定的路徑使用自訂測試配接器。

`-c|--configuration {Debug|Release}`

定義組建組態。 預設值是 `Debug`，但您的專案組態無法覆寫這個預設的 SDK 設定。

`-d|--diag <PATH_TO_DIAGNOSTICS_FILE>`

針對測試平台啟用診斷模式，並將診斷訊息寫入至指定的檔案。

`-f|--framework <FRAMEWORK>`

尋找特定[架構](../../standard/frameworks.md)的測試二進位檔。

`--filter <EXPRESSION>`

使用指定的運算式篩選出目前專案中的測試。 如需詳細資訊，請參閱[篩選選項詳細資料](#filter-option-details)一節。 如需如何使用選擇性單元測試篩選的其他資訊及範例，請參閱[執行選擇性單元測試](../testing/selective-unit-tests.md)。

`-h|--help`

印出命令的簡短說明。

`-l|--logger <LoggerUri/FriendlyName>`

指定測試結果的記錄器。

`--no-build`

請不要在執行之前建置測試專案。

`-o|--output <OUTPUT_DIRECTORY>`

在其中尋找要執行的二進位檔的目錄。

`-s|--settings <SETTINGS_FILE>`

執行測試時要使用的設定。

`-t|--list-tests`

列出在目前專案中探索到的所有測試。

`-v|--verbosity <LEVEL>`

設定命令的詳細資訊層級。 允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

---

## <a name="examples"></a>範例

執行目前目錄之專案中的測試：

`dotnet test`

執行 `test1` 專案中的測試︰

`dotnet test ~/projects/test1/test1.csproj`

## <a name="filter-option-details"></a>篩選選項詳細資料

`--filter <EXPRESSION>`

`<Expression>` 的格式為 `<property><operator><value>[|&<Expression>]`。

`<property>` 為 `Test Case` 的屬性。 以下為熱門單元測試架構所支援的屬性：

| 測試架構 | 支援的屬性                                                                                      |
| :------------: | --------------------------------------------------------------------------------------------------------- |
| MSTest         | <ul><li>FullyQualifiedName</li><li>名稱</li><li>ClassName</li><li>優先權</li><li>TestCategory</li></ul> |
| xUnit          | <ul><li>FullyQualifiedName</li><li>DisplayName</li><li>特性</li></ul>                                   |

`<operator>` 描述屬性和值之間的關聯性：

| 運算子 | 函式        |
| :------: | --------------- |
| `=`      | 完全相符     |
| `!=`     | 不完全相符 |
| `~`      | 包含        |

`<value>` 為字串。 所有的查閱皆不區分大小寫。

沒有 `<operator>` 的運算式會自動被視為 `FullyQualifiedName` 屬性上的 `contains` (例如，`dotnet test --filter xyz` 等同於 `dotnet test --filter FullyQualifiedName~xyz`)。

運算式可以使用條件運算子聯結：

| 運算子 | 函式 |
| :------: | :------: |
| `|`      | 或       |
| `&`      | AND      |

使用條件運算子時，您可以用括弧括住運算式 (例如，`(Name~TestMethod1) | (Name~TestMethod2)`)。

如需如何使用選擇性單元測試篩選的其他資訊及範例，請參閱[執行選擇性單元測試](../testing/selective-unit-tests.md)。

## <a name="see-also"></a>請參閱

 [架構與目標](../../standard/frameworks.md)   
 [.NET Core 執行階段識別項 (RID) 目錄](../rid-catalog.md)

