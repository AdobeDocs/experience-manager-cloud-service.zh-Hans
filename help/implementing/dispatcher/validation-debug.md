---
title: 使用 Dispatcher 工具进行验证和调试
description: 使用 Dispatcher 工具进行验证和调试
feature: Dispatcher
exl-id: 9e8cff20-f897-4901-8638-b1dbd85f44bf
source-git-commit: a56b0ed1efff7b8d04e65921ee9dd25ae7030dbd
workflow-type: tm+mt
source-wordcount: '2865'
ht-degree: 1%

---

# 使用 Dispatcher 工具进行验证和调试 {#Dispatcher-in-the-cloud}

## 简介 {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>如需雲端中的Dispatcher以及如何下載Dispatcher工具的詳細資訊，請參閱 [雲端中的Dispatcher](/help/implementing/dispatcher/disp-overview.md) 頁面。 如果您的Dispatcher設定處於舊版模式，請參閱 [舊版模式檔案](/help/implementing/dispatcher/validation-debug-legacy.md).

以下各節將說明彈性模式的檔案結構、本機驗證、偵錯以及從舊版模式移轉至彈性模式。

本文假設您的專案的Dispatcher設定包含檔案 `opt-in/USE_SOURCES_DIRECTLY`，可讓SDK和執行階段以比舊版模式更好的方式驗證和部署設定，移除檔案數量和大小的相關限制。

因此，如果您的Dispatcher設定不包括上述檔案，它會 **強烈建議** 從舊版模式移轉至彈性模式，如 [從舊版模式移轉至彈性模式](#migrating) 區段。

## 檔案結構 {#flexible-mode-file-structure}

專案的Dispatcher子資料夾的結構如下：

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   ├── my_site.vhost # Created by customer
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── my_site.vhost -> ../available_vhosts/my_site.vhost  # Created by customer
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
│── opt-in
│   └── USE_SOURCES_DIRECTLY
└── conf.dispatcher.d
    ├── available_farms
    │   ├── my_farm.farm # Created by customer
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   ├── marketing_query_parameters.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── my_farm.farm -> ../available_farms/my_farm.farm  # Created by customer
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

以下是可修改的重大檔案說明：

**可自訂的檔案**

以下檔案可自訂，將在部署時傳輸到您的雲端執行個體：

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

您可以有一或多個這些檔案。 它們包含 `<VirtualHost>` 與主機名稱相符的專案，並允許Apache使用不同規則處理每個網域流量。 檔案建立於 `available_vhosts` 目錄，並透過中的符號連結啟用 `enabled_vhosts` 目錄。 從 `.vhost` 檔案、其他檔案（例如重寫程式和變數）都會包含在內。

>[!NOTE]
>
>在彈性模式中，您應該使用相對路徑，而不是絕對路徑。

請確定至少有一個符合ServerAlias的虛擬主機始終可用 `\*.local`， `localhost` 和 `127.0.0.1` dispatcher失效所需的引數。 伺服器別名 `*.adobeaemcloud.net` 和 `*.adobeaemcloud.com` 在至少一個vhost設定中也需要，並且是內部Adobe程式所需。

如果您因為有多個vhost檔案而想要比對正確的主機，您可以依照以下範例操作：

```
<VirtualHost *:80>
	ServerName	"example.com"
	# Put names of which domains are used for your published site/content here
	ServerAlias	 "*example.com" "\*.local" "localhost" "127.0.0.1" "*.adobeaemcloud.net" "*.adobeaemcloud.com"
	# Use a document root that matches the one in conf.dispatcher.d/default.farm
	DocumentRoot "${DOCROOT}"
	# URI dereferencing algorithm is applied at Sling's level, do not decode parameters here
	AllowEncodedSlashes NoDecode
	# Add header breadcrumbs for help in troubleshooting which vhost file is chosen
	<IfModule mod_headers.c>
		Header add X-Vhost "publish-example-com"
	</IfModule>
  ...
</VirtualHost>
```

* `conf.d/rewrites/rewrite.rules`

此檔案包含在您的 `.vhost` 檔案。 它有一組重寫規則 `mod_rewrite`.

* `conf.d/variables/custom.vars`

此檔案包含在您的 `.vhost` 檔案。 您可以在此位置新增Apache變數的定義。

* `conf.d/variables/global.vars`

此檔案包含在 `dispatcher_vhost.conf` 檔案。 您可以變更您的Dispatcher並重新寫入此檔案中的記錄層級。

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

您可以有一或多個這些檔案，而且它們包含陣列以符合主機名稱，並允許Dispatcher模組使用不同規則處理每個陣列。 檔案建立於 `available_farms` 目錄，並透過中的符號連結啟用 `enabled_farms` 目錄。 從 `.farm` 檔案、其他檔案（例如篩選器、快取規則等）都會包含在內。

* `conf.dispatcher.d/cache/rules.any`

此檔案包含在您的 `.farm` 檔案。 它會指定快取偏好設定。

* `conf.dispatcher.d/clientheaders/clientheaders.any`

此檔案包含在您的 `.farm` 檔案。 它會指定要將哪些請求標頭轉送至後端。

* `conf.dispatcher.d/filters/filters.any`

此檔案包含在您的 `.farm` 檔案。 它有一組規則，可變更應該篩選掉的流量，而不是使其進入後端。

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

此檔案包含在您的 `.farm` 檔案。 它有一個主機名稱或URI路徑的清單，將通過glob匹配進行匹配。 這會決定使用哪個後端來處理請求。

* `opt-in/USE_SOURCES_DIRECTLY`

此檔案可讓排程程式設定更靈活，並移除先前對檔案數量和大小的限制。 它也會讓SDK和執行階段以改良的方式驗證和部署設定。

上述檔案會參考下列不可變的組態檔。 雲端環境中的Dispatcher不會處理不可變檔案的變更。

**不可變組態檔**

這些檔案是基本框架的一部分，可強制實施標準和最佳實務。 這些檔案被視為不可變，因為在本機修改或刪除它們將不會對您的部署造成影響，因為它們將不會傳輸到您的雲端執行個體。

建議上述檔案參考下列不可變檔案，然後加上任何其他陳述式或覆寫。 將Dispatcher設定部署到雲端環境時，將會使用不可變檔案的最新版本，無論本機開發中使用的版本為何。

* `conf.d/available_vhosts/default.vhost`

包含範例虛擬主機。 針對您自己的虛擬主機，建立此檔案的復本、自訂，然後前往 `conf.d/enabled_vhosts` 並建立自訂復本的符號連結。
請勿將default.vhost檔案直接複製到 `conf.d/enabled_vhosts`.

確保虛擬主機一律可用，且符合ServerAlias `\*.local`， `localhost` 和 `127.0.0.1` dispatcher失效所需的引數。 伺服器別名 `*.adobeaemcloud.net` 和 `*.adobeaemcloud.com` 內部Adobe程式所需。

* `conf.d/dispatcher_vhost.conf`

基本框架的一部分，用來說明如何包含虛擬主機和全域變數。

* `conf.d/rewrites/default_rewrite.rules`

適用於標準專案的預設重寫規則。 如果您需要自訂，請修改 `rewrite.rules`. 在您的自訂中，如果預設規則符合您的需求，您仍然可以先包含這些規則。

* `conf.dispatcher.d/available_farms/default.farm`

包含範例Dispatcher陣列。 針對您自己的陣列，建立此檔案的復本、自訂，然後前往 `conf.d/enabled_farms` 並建立自訂復本的符號連結。

* `conf.dispatcher.d/cache/default_invalidate.any`

基礎框架的一部分，在啟動時產生。 您是 **必填** 若要將此檔案納入您定義的每個陣列中，請在 `cache/allowedClients` 區段。

* `conf.dispatcher.d/cache/default_rules.any`

適用於標準專案的預設快取規則。 如果您需要自訂，請修改 `conf.dispatcher.d/cache/rules.any`. 在您的自訂中，如果預設規則符合您的需求，您仍然可以先包含這些規則。

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

轉送至後端的預設請求標頭，適用於標準專案。 如果您需要自訂，請修改 `clientheaders.any`. 在您的自訂中，您仍然可以先包含預設請求標頭（如果它們符合您的需求）。

* `conf.dispatcher.d/dispatcher.any`

基本框架的一部分，用於說明如何包含您的Dispatcher陣列。

* `conf.dispatcher.d/filters/default_filters.any`

適用於標準專案的預設篩選器。 如果您需要自訂，請修改 `filters.any`. 在您的自訂中，如果預設篩選器符合您的需求，您仍然可以先包含這些篩選器。

* `conf.dispatcher.d/renders/default_renders.any`

此檔案屬於基礎架構的一部分，會在啟動時產生。 您是 **必填** 若要將此檔案納入您定義的每個陣列中，請在 `renders` 區段。

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

適用於標準專案的預設主機萬用字元。 如果您需要自訂，請修改 `virtualhosts.any`. 在您的自訂中，不應包含預設主機萬用字元，因為它相符 **每** 傳入要求。

## 支持的 Apache 模块 {#apache-modules}

另請參閱 [支援的Apache模組](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## 本機驗證 {#local-validation-flexible-mode}

>[!NOTE]
>
>以下各節包含使用Mac或Linux版SDK的命令，但Windows SDK也可以透過類似方式使用。

使用 `validate.sh` 指令碼，如下所示：

```
$ validate.sh src/dispatcher
opt-in USE_SOURCES_DIRECTLY marker file detected
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv not found in deployment folder: /Users/foo/src - using files in 'conf.d' and 'conf.dispatcher.d' subfolders directly
processing configuration subfolder: conf.d
processing configuration subfolder: conf.dispatcher.d
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until localhost is available
localhost resolves to ::1
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {

... 

}
Syntax OK
Phase 2 finished
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt

...

no immutable file has been changed - check is SUCCESSFUL
Phase 3 finished
```

指令碼包含以下三個階段：

1. 它會執行驗證器。 如果設定無效，指令碼會失敗。
2. 它會執行 `httpd -t` 用來測試語法是否正確以讓apache httpd可以啟動的命令。 如果成功，設定應準備好進行部署。
3. 檢查Dispatcher SDK設定檔案的子集，這些檔案旨在不可變動，如 [檔案結構區段](##flexible-mode-file-structure)，尚未修改且符合目前的SDK版本。

在Cloud Manager部署期間， `httpd -t` 語法檢查也會執行，所有錯誤都會包含在Cloud Manager中 `Build Images step failure` 記錄。

>[!NOTE]
>
>請參閱 [自動重新載入和驗證](#automatic-loading) 區段以有效率地取代執行 `validate.sh` 在每次設定修改後。

### 階段1 {#first-phase}

如果指示詞未列入允許清單，工具會記錄錯誤並傳回非零的退出代碼。 此外，它會進一步掃描所有具有模式的檔案 `conf.dispatcher.d/enabled_farms/*.farm` 並檢查：

* 不存在允許使用的篩選規則 `/glob` (請參閱 [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) 以取得更多詳細資料。
* 未公開任何管理功能。 例如，存取路徑，例如 `/crx/de or /system/console`.

請注意，驗證工具只會報告未列入允許清單的Apache指示詞被禁止使用的情況。 不會報告您的Apache設定的語法或語義問題，因為此資訊僅適用於執行環境中的Apache模組。

以下是針對工具輸出的常見驗證錯誤進行除錯的疑難排解技巧：

**找不到 `conf.dispatcher.d` 封存中的子資料夾**

您的存档应包含文件夹 `conf.d` 和 `conf.dispatcher.d`。 请注意，您不应 **在**&#x200B;存档 `etc/httpd` 中使用前缀。

**在中找不到任何陣列`conf.dispatcher.d/enabled_farms`**

您啟用的陣列應位於提及的子資料夾中。

**包含的檔案(...)必須命名為： ...**

您的陣列設定中有兩個區段， **必須** 包含特定檔案： `/renders` 和 `/allowedClients` 在 `/cache` 區段。 這些區段必須如下所示：

```
/renders {
    $include "../renders/default_renders.any"
}
```

和:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**檔案包含在未知位置： ...**

您的伺服器陣列設定中有四個區段可讓您包含自己的檔案： `/clientheaders`， `filters`， `/rules` 在 `/cache` 區段和 `/virtualhosts`. 包含的檔案需要命名如下：

| 分区 | 包含檔案名稱 |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

或者，您也可以包含 **預設** 這些檔案的版本，其名稱會以字詞為前置詞 `default_`例如， `../filters/default_filters.any`.

**include陳述式位於(...)，在任何已知位置以外： ...**

除上述六節外，嚴禁您使用 `$include` 陳述式，例如，下列專案會產生此錯誤：

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**允許的使用者端/轉譯器不包括： ...**

若您未指定包含，則會產生此錯誤 `/renders` 和 `/allowedClients` 在 `/cache` 區段。 請參閱
**包含的檔案(...)必須命名為： ...** 區段以取得詳細資訊。

**篩選器不得使用glob模式來允許請求**

允許具有的請求是不安全的 `/glob` 樣式規則，會比對完整的請求行，例如

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

此陳述式的目的是允許以下專案的請求： `css` 檔案，但也允許請求 **任何** 後跟查詢字串的資源 `?a=.css`. 因此，禁止使用這類篩選器（另請參閱CVE-2016-0957）。

**包含的檔案(...)不符合任何已知檔案**

根據預設，Apache虛擬主機設定中的兩種檔案型別可指定為包含：重寫和變數。

| 类型 | 包含檔案名稱 |
|-----------|---------------------------------|
| 重寫 | `conf.d/rewrites/rewrite.rules` |
| 变量 | `conf.d/variables/custom.vars` |

在彈性模式中，也可以包含其他檔案，只要它們位於的子目錄中（在任何層級）。 `conf.d` 前置詞為以下的目錄。

| 包含檔案上層目錄前置詞 |
|-------------------------------------|
| `conf.d/includes` |
| `conf.d/modsec` |
| `conf.d/rewrites` |

例如，您可以將檔案包含在 `conf.d/includes` 目錄，如下所示：

```
Include conf.d/includes/mynewdirectory/myincludefile.conf
```

或者，您也可以包含 **預設** 重寫規則的版本，其名稱為 `conf.d/rewrites/default_rewrite.rules`.
請注意，變數檔案沒有預設版本。

**偵測到過時的配置配置，啟用相容性模式**

此訊息指出您的設定具有已棄用的版本1版面，其中包含完整的Apache設定和檔案，其中 `ams_` 字首。 雖然此版本仍支援回溯相容性，但您應切換至新版面。

請注意，第一階段也可以是 **單獨執行**，而不是從包裝函式 `validate.sh` 指令碼。

針對您的Maven成品或 `dispatcher/src` 子目錄，它會報告驗證失敗：

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

在Windows上，Dispatcher驗證器會區分大小寫。 因此，如果您未遵循設定所在路徑的大小寫，例如：

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
```

從Windows檔案總管複製並貼上路徑，然後在命令提示字元上使用 `cd` 命令匯入該路徑。

### 階段2 {#second-phase}

此階段會透過在Docker容器中啟動Apache HTTPD來檢查Apache語法。 Docker必須安裝在本機，但請注意AEM不需要運行。

>[!NOTE]
>
>Windows使用者需要使用支援Docker的Windows 10 Professional或其他發行版本。 這是在本機電腦上執行及偵錯Dispatcher的先決條件。
>對於Windows和macOS，我們建議使用Docker Desktop。

此階段也可以獨立執行 `bin/docker_run.sh src/dispatcher host.docker.internal:4503 8080`.

在Cloud Manager部署期間， `httpd -t` 語法檢查也會執行，所有錯誤都將包含在Cloud Manager建置影像步驟失敗記錄中。

### 階段3 {#third-phase}

如果此階段失敗，則表示Adobe已變更一個或多個不可變檔案，您必須將對應的不可變檔案替換為 `src` SDK的目錄。 以下記錄範例說明此問題：

```
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt
(...)
checking existing 'conf.dispatcher.d/clientheaders/default_clientheaders.any' for changes
immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed:
--- /etc/httpd/conf.dispatcher.d/clientheaders/default_clientheaders.any
+++ /etc/httpd-actual/conf.dispatcher.d/clientheaders/default_clientheaders.any
@@ -40,4 +40,3 @@
"Sling-uploadmode"
"x-requested-with"
"If-Modified-Since"
-"Authorization"
** error: immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed!
  
```

此階段也可以獨立執行 `bin/docker_immutability_check.sh src/dispatcher`.

您可以透過執行 `bin/update_maven.sh src/dispatcher` 您的dispatcher資料夾上的指令碼，其中 `src/dispatcher` 是您的Dispatcher設定目錄。 這也會更新父目錄中的任何pom.xml檔案，以便maven不可變性檢查也會更新。

## 偵錯您的Apache和Dispatcher設定 {#debugging-apache-and-dispatcher-configuration}

請注意，您可以使用在本機執行Apache Dispatcher `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`.

如前所述，Docker必須安裝在本機，AEM不需要運行。 Windows使用者需要使用支援Docker的Windows 10 Professional或其他發行版本。 這是在本機電腦上執行及偵錯Dispatcher的先決條件。

以下策略可用於增加Dispatcher模組的記錄輸出並檢視結果 `RewriteRule` 在本機和雲端環境中進行評估。

這些模組的記錄層級由變數定義 `DISP_LOG_LEVEL` 和 `REWRITE_LOG_LEVEL`. 可在檔案中設定 `conf.d/variables/global.vars`. 其相關部分如下：

```
# Log level for the dispatcher
#
# Possible values are: error, warn, info, debug and trace1
# Default value: warn
#
# Define DISP_LOG_LEVEL warn
 
# Log level for mod_rewrite
#
# Possible values are: error, warn, info, debug and trace1 - trace8
# Default value: warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL warn
```

在本機執行Dispatcher時，記錄會直接列印到終端機輸出。 大多數情況下，您都希望這些記錄位於DEBUG中，這可以通過在執行Docker時傳遞偵錯級別作為引數來完成。 例如：`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh src docker.for.mac.localhost:4503 8080`。

雲端環境的記錄會透過Cloud Manager中提供的記錄服務公開。

>[!NOTE]
>
>對於AEMas a Cloud Service環境，偵錯是最高詳細程度層級。 不支援追蹤記錄層級，因此您在雲端環境中工作時應該避免進行設定。

### 自動重新載入和驗證 {#automatic-reloading}

>[!NOTE]
>
>由於Windows作業系統的限制，此功能僅適用於macOS和Linux使用者。

不要執行本機驗證(`validate.sh`)並啟動Docker容器(`docker_run.sh`)每次修改設定時，您也可以執行 `docker_run_hot_reload.sh` 指令碼。  指令碼會監視設定的任何變更，並自動重新載入並重新執行驗證。 使用此選項可節省大量除錯時間。

您可以使用以下命令執行指令碼： `./bin/docker_run_hot_reload.sh src/dispatcher host.docker.internal:4503 8080`

請注意，輸出的第一行看起來會類似於執行的專案 `docker_run.sh`例如：

```
~ bin/docker_run_hot_reload.sh src host.docker.internal:8081 8082
opt-in USE_SOURCES_DIRECTLY marker file detected
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/15-check-pod-name.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until host.docker.internal is available
host.docker.internal resolves to 192.168.65.2
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
Running script /docker_entrypoint.d/80-frontend-domain.sh
Running script /docker_entrypoint.d/zzz-import-sdk-config.sh
WARN Mon Jul  4 09:53:54 UTC 2022: Pseudo symlink conf.d seems to point to a non-existing file!
INFO Mon Jul  4 09:53:55 UTC 2022: Copied customer configuration to /etc/httpd.
INFO Mon Jul  4 09:53:55 UTC 2022: Start testing
Cloud manager validator 2.0.43
2022/07/04 09:53:55 No issues found
INFO Mon Jul  4 09:53:55 UTC 2022: Testing with fresh base configuration files.
INFO Mon Jul  4 09:53:55 UTC 2022: Apache httpd informationServer version: Apache/2.4.54 (Unix)
```

## 每個環境的不同Dispatcher設定 {#different-dispatcher-configurations-per-environment}

目前，相同的Dispatcher設定會套用至所有AEMas a Cloud Service環境。 執行階段會有環境變數 `ENVIRONMENT_TYPE` 包含目前執行模式（dev、stage或prod）以及定義。 定義可以是 `ENVIRONMENT_DEV`， `ENVIRONMENT_STAGE` 或 `ENVIRONMENT_PROD`. 在Apache設定中，變數可直接在運算式中使用。 或者，可使用定義來建置邏輯：

```
# Simple usage of the environment variable
ServerName ${ENVIRONMENT_TYPE}.company.com
 
# When more logic is required
<IfDefine ENVIRONMENT_STAGE>
  # These statements are for stage
  Define VIRTUALHOST stage.example.com
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  # These statements are for production
  Define VIRTUALHOST prod.example.com
</IfDefine>
```

在Dispatcher設定中，相同的環境變數可供使用。 如果需要更多邏輯，請定義上述範例中顯示的變數，然後在Dispatcher設定區段中使用它們：

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

或者，您可以在httpd/dispatcher設定中使用Cloud Manager環境變數，但不是環境秘密。 如果程式有多個開發環境，而且其中一些開發環境的httpd/dispatcher設定值不同，此方法就特別重要。 系統會使用與上述範例相同的${VIRTUALHOST}語法，但不會使用上述變數檔案中的Define宣告。 閱讀 [Cloud Manager檔案](/help/implementing/cloud-manager/environment-variables.md) 以取得設定Cloud Manager環境變數的指示。

在本機測試您的設定時，您可以傳遞變數來模擬不同的環境型別 `DISP_RUN_MODE` 至 `docker_run.sh` 直接編寫指令碼：

```
$ DISP_RUN_MODE=stage docker_run.sh src docker.for.mac.localhost:4503 8080
```

未傳入DISP_RUN_MODE的值時的預設執行模式為「dev」。
如需可用選項和變數的完整清單，請執行指令碼 `docker_run.sh` 沒有引數。

## 檢視Docker容器正在使用的Dispatcher配置 {#viewing-dispatcher-configuration-in-use-by-docker-container}

使用環境特定設定時，可能很難判斷實際Dispatcher設定是什麼樣子。 使用啟動您的Docker容器後 `docker_run.sh` 其傾印方式如下：

* 確定正在使用的Docker容器ID：

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* 使用該容器ID執行以下命令列：

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## 從舊版模式移轉至彈性模式 {#migrating}

在Cloud Manager 2021.7.0版本中，新的Cloud Manager程式會產生maven專案結構 [AEM原型28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hans) 或更高版本，其中包括檔案 **opt-in/USE_SOURCES_DIRECTLY**. 如此一來，即會移除 [舊版模式](/help/implementing/dispatcher/validation-debug-legacy.md) 檔案的數量和大小，也會讓SDK和執行階段以改良的方式驗證和部署設定。 如果您的Dispatcher設定沒有此檔案，強烈建議您進行移轉。 請使用下列步驟來確保安全轉換：

1. **本機測試。** 使用最新的Dispatcher工具SDK，新增資料夾和檔案 `opt-in/USE_SOURCES_DIRECTLY`. 依照本文中的「本機驗證」指示，測試Dispatcher是否在本機運作。
1. **雲端開發測試：**
   * 提交檔案 `opt-in/USE_SOURCES_DIRECTLY` 非生產管道部署到雲端開發環境的Git分支。
   * 使用Cloud Manager來部署至雲端開發環境。
   * 徹底測試。 在將變更部署到更高層環境之前，請務必驗證Apache和Dispatcher設定的行為是否符合您的預期。 檢查與您的自訂設定相關的所有行為！ 如果您認為部署的Dispatcher設定未反映您的自訂設定，請提交客戶支援票證。

   >[!NOTE]
   >
   >在彈性模式中，您應該使用相對路徑，而不是絕對路徑。
1. **部署至生產環境：**
   * 提交檔案 `opt-in/USE_SOURCES_DIRECTLY` 至生產管道部署至雲端中繼和生產環境的Git分支。
   * 使用Cloud Manager來部署至中繼環境。
   * 徹底測試。 在將變更部署到更高層環境之前，請務必驗證Apache和Dispatcher設定的行為是否符合您的預期。 檢查與您的自訂設定相關的所有行為！ 如果您認為部署的Dispatcher設定未反映您的自訂設定，請提交客戶支援票證。
   * 使用Cloud Manager繼續部署到生產環境。
