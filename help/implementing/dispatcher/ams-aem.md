---
title: 将 Dispatcher 配置从 AMS 迁移到 AEM as a Cloud Service
description: 将 Dispatcher 配置从 AMS 迁移到 AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 17%

---

# 将 Dispatcher 配置从 AMS 迁移到 AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## AMS Dispatcher與AEMas a Cloud Service之間的主要差異 {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

AEMas a Cloud Service中的Apache和Dispatcher設定相當類似於AMS設定。 主要差異如下：

* 在AEMas a Cloud Service中，可能不使用某些Apache指示詞(例如 `Listen` 或 `LogLevel`)
* 在AEMas a Cloud Service中，只能將Dispatcher設定的某些片段放入包含檔案中，其命名很重要。 例如，您要在不同主機上重複使用的篩選規則必須放在名為的檔案中 `filters/filters.any`. 如需詳細資訊，請參閱參考頁面。
* AEMas a Cloud Service中有額外的驗證，不允許使用撰寫篩選規則 `/glob` 以防止安全性問題。 從 `deny *` 將使用，而不是 `allow *` （無法使用），客戶將受益於在本機執行Dispatcher並進行試用和錯誤，檢視記錄以確切瞭解Dispatcher篩選器阻止了哪些路徑以便可以新增。

## 將Dispatcher設定從AMS移轉至AEMas a Cloud Service的准則

Dispatcher設定結構在Managed Services和AEMas a Cloud Service之間有所差異。 以下提供如何從AMS Dispatcher設定版本2移轉至AEMas a Cloud Service的逐步指南。

## 如何將AMS轉換為AEM as a Cloud Service Dispatcher設定

以下章節提供如何轉換AMS設定的逐步指示。 此工具假設您有一個封存，其結構與中所述的結構類似 [Cloud Manager Dispatcher設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### 提取存档并删除最后的前缀

將封存解壓縮至資料夾，並確認直接子資料夾的開頭為 `conf`， `conf.d`，
`conf.dispatcher.d` 和 `conf.modules.d`. 如果沒有，請在階層中向上移動它們。

### 移除未使用的子資料夾和檔案

移除子資料夾 `conf` 和 `conf.modules.d`，以及相符的檔案 `conf.d/*.conf`.

### 删除所有未发布的虚拟主机

移除中的任何虛擬主機檔案 `conf.d/enabled_vhosts` 具有 `author`， `unhealthy`， `health`，
`lc` 或 `flush` 在其名稱中。 中的所有虛擬主機檔案 `conf.d/available_vhosts` 您也可以移除未連結至的。

### 移除或注释未引用端口 80 的虚拟主机部分

如果您的虛擬主機檔案中仍有區段專門參照連線埠80以外的連線埠，例如：

```
<VirtualHost *:443>
...
</VirtualHost>
```

，
则请移除或注释该部分。这些部分中的语句将不会得到处理，但是如果保留它们，您可能最终仍会对其进行编辑，并且不会有任何效果，这可能会造成混淆。

### 检查 rewrites

輸入目錄 `conf.d/rewrites`.

移除任何名為的檔案 `base_rewrite.rules` 和 `xforwarded_forcessl_rewrite.rules` 並記得移除 `Include` 虛擬主機檔案中引用這些陳述式的陳述式。

若 `conf.d/rewrites` 現在包含單一檔案，應將其重新命名為 `rewrite.rules` 還有，別忘了改寫 `Include` 陳述式也在虛擬主機檔案中引用該檔案。

然而，如果資料夾包含多個虛擬主機專屬的檔案，則應將其內容複製到 `Include` 在虛擬主機檔案中引用它們的陳述式。

### 检查 variables

輸入目錄 `conf.d/variables`.

移除任何名為的檔案 `ams_default.vars` 並記得移除 `Include` 虛擬主機檔案中引用這些陳述式的陳述式。

若 `conf.d/variables` 現在包含單一檔案，應將其重新命名為 `custom.vars` 還有，別忘了改寫 `Include` 陳述式也在虛擬主機檔案中引用該檔案。

然而，如果資料夾包含多個虛擬主機專屬的檔案，則應將其內容複製到 `Include` 在虛擬主機檔案中引用它們的陳述式。

### 移除允許清單

移除資料夾 `conf.d/whitelists` 和移除 `Include` 陳述式，指涉該子資料夾中的某個檔案。

### 替换任何不再可用的变量

在所有虚拟主机文件中：

重新命名 `PUBLISH_DOCROOT` 至 `DOCROOT`
移除引用下列變數的章節： `DISP_ID`， `PUBLISH_FORCE_SSL` 或 `PUBLISH_WHITELIST_ENABLED`

### 通过运行验证器检查状态

在目錄中執行Dispatcher驗證器，使用 `httpd` 子命令：

```
$ validator httpd .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果您看到未列入允許清單的Apache指示詞，請將其移除。

### 删除所有未发布的场

移除中的任何伺服器陣列檔案 `conf.dispatcher.d/enabled_farms` 具有 `author`， `unhealthy`， `health`，
`lc` 或 `flush` 在其名稱中。 中的所有伺服器陣列檔案 `conf.dispatcher.d/available_farms` 您也可以移除未連結至的。

### 重命名场文件

中的所有陣列 `conf.d/enabled_farms` 必須重新命名以符合模式 `*.farm`，例如，名為的伺服器陣列檔案 `customerX_farm.any` 應重新命名 `customerX.farm`.

### 检查 cache

輸入目錄 `conf.dispatcher.d/cache`.

移除所有前缀为 `ams_` 的文件。

若 `conf.dispatcher.d/cache` 現在為空，請複製檔案 `conf.dispatcher.d/cache/rules.any`
從標準Dispatcher設定移至此資料夾。 您可以在資料夾中找到標準Dispatcher設定 `src` 此SDK的。 別忘了改寫
`$include` 陳述式中提及的 `ams_*_cache.any` 伺服器陣列檔案中的規則檔案。

若改為 `conf.dispatcher.d/cache` 現在包含單一檔案及其尾碼 `_cache.any`，應重新命名為 `rules.any` 還有，別忘了改寫 `$include` 在伺服器陣列檔案中引用該檔案的陳述式。

然而，如果資料夾包含多個採用該模式的伺服器陣列特定檔案，則應將其內容複製到 `$include` 在伺服器陣列檔案中引用它們的陳述式。

移除任何尾碼的檔案 `_invalidate_allowed.any`.

複製檔案 `conf.dispatcher.d/cache/default_invalidate_any` 從雲端Dispatcher設定中的預設AEM移至該位置。

在每個伺服器陣列檔案中，移除 `cache/allowedClients` 區段並取代為：

```
$include "../cache/default_invalidate.any"
```

### 检查 client headers

輸入目錄 `conf.dispatcher.d/clientheaders`.

移除所有前缀为 `ams_` 的文件。

若 `conf.dispatcher.d/clientheaders` 現在包含單一檔案及其尾碼 `_clientheaders.any`，應重新命名為 `clientheaders.any` 還有，別忘了改寫 `$include` 在伺服器陣列檔案中引用該檔案的陳述式。

然而，如果資料夾包含多個採用該模式的伺服器陣列特定檔案，則應將其內容複製到 `$include` 在伺服器陣列檔案中引用它們的陳述式。

複製檔案 `conf.dispatcher/clientheaders/default_clientheaders.any` 從預設的AEMas a Cloud ServiceDispatcher設定切換到該位置。

在每個伺服器陣列檔案中，取代任何如下所示的clientheader include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

替换为语句：

```
$include "../clientheaders/default_clientheaders.any"
```

### 检查 filter

輸入目錄 `conf.dispatcher.d/filters`.

移除所有前缀为 `ams_` 的文件。

若 `conf.dispatcher.d/filters` 現在包含單一檔案，應將其重新命名為
`filters.any` 還有，別忘了改寫 `$include` 在伺服器陣列檔案中引用該檔案的陳述式。

然而，如果資料夾包含多個採用該模式的伺服器陣列特定檔案，則應將其內容複製到 `$include` 在伺服器陣列檔案中引用它們的陳述式。

複製檔案 `conf.dispatcher/filters/default_filters.any` 從預設的AEMas a Cloud ServiceDispatcher設定切換到該位置。

在每個伺服器陣列檔案中，取代任何如下所示的filter include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

替换为语句：

```
$include "../filters/default_filters.any"
```

### 检查 renders

輸入目錄 `conf.dispatcher.d/renders`.

移除该文件夹中的所有文件。

複製檔案 `conf.dispatcher.d/renders/default_renders.any` 從預設的AEMas a Cloud ServiceDispatcher設定切換到該位置。

在每個伺服器陣列檔案中，移除 `renders` 區段並取代為：

```
$include "../renders/default_renders.any"
```

### 检查 virtualhosts

重新命名目錄 `conf.dispatcher.d/vhosts` 至 `conf.dispatcher.d/virtualhosts` 並輸入。

移除所有前缀为 `ams_` 的文件。

若 `conf.dispatcher.d/virtualhosts` 現在包含單一檔案，應將其重新命名為
`virtualhosts.any` 還有，別忘了改寫 `$include` 在伺服器陣列檔案中引用該檔案的陳述式。

然而，如果資料夾包含多個採用該模式的伺服器陣列特定檔案，則應將其內容複製到 `$include` 在伺服器陣列檔案中引用它們的陳述式。

複製檔案 `conf.dispatcher/virtualhosts/default_virtualhosts.any` 從預設的AEMas a Cloud ServiceDispatcher設定切換到該位置。

在每個伺服器陣列檔案中，取代任何如下所示的filter include陳述式：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

替换为语句：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 通过运行验证器检查状态

在目錄中執行AEMas a Cloud ServiceDispatcher驗證器，使用 `dispatcher` 子命令：

```
$ validator dispatcher .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果看到有关未定义变量 `PUBLISH_DOCROOT` 的错误，请将该变量重命名为 `DOCROOT`。

有关其他每个错误，请参阅验证器工具文档的“疑难解答”部分。

### 使用本機部署測試您的設定（需要安裝Docker）

使用指令碼 `docker_run.sh` 在AEMas a Cloud ServiceDispatcher工具中，您可以測試您的設定不包含只會顯示在部署中的任何其他錯誤：

### 步驟1：使用驗證器產生部署資訊

```
validator full -d out .
```


这将验证完整配置并在 中生成部署信息`out`

### 步驟2：使用該部署資訊在Docker映像中啟動Dispatcher

在您的macOS電腦上執行AEM發佈伺服器，並在連線埠4503上接聽後，您可以在該伺服器前面執行啟動Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

这将启动容器并在本地端口 8080 上公开 Apache。

### 使用您的新Dispatcher設定

恭喜！如果驗證器不再回報任何問題，且Docker容器啟動時未出現任何失敗情況或警告，即可將您的設定移至 `dispatcher/src` Git存放庫的子目錄。

**使用AMS Dispatcher設定版本1的客戶應聯絡客戶支援，協助他們從版本1移轉至版本2，以便遵循上述指示。**
