---
title: 為Adobe Experience Manager as a Cloud Service設定OSGi
description: 具有機密值和環境特定值的OSGi設定
feature: Deploying
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
source-git-commit: 26ca2addb14f62588035323ce886ae890919b759
workflow-type: tm+mt
source-wordcount: '3312'
ht-degree: 1%

---

# 為Adobe Experience Manager as a Cloud Service設定OSGi {#configuring-osgi-for-aem-as-a-cloud-service}

>[!NOTE]
>
>AEM在2021.12.0版中引進了使用Cloud Manager使用者介面來設定標準環境變數的功能。 如需詳細資訊，請參閱檔案 [此處](/help/implementing/cloud-manager/environment-variables.md).

[osgi](https://www.osgi.org/) 是Adobe Experience Manager (AEM)技術棧疊中的基本元素。 它可用來控制AEM的複合套件組合及其設定。

OSGi提供標準化的原語，允許使用小型、可重複使用的合作元件來建構應用程式。 這些元件可組成應用程式並部署。 這可讓您輕鬆地管理OSGi套件組合，因為它們可以個別停止、安裝和啟動。 系統會自動處理相依性。 每個OSGi元件都包含在各種套件組合中。 如需詳細資訊，請參閱 [OSGi規格](https://help.eclipse.org/latest/index.jsp).

您可以透過AEM程式碼專案一部分的組態檔案來管理OSGi元件的組態設定。

## OSGi組態檔 {#osgi-configuration-files}

設定變更是在AEM Project的程式碼套件中定義(`ui.apps`)作為組態檔(`.cfg.json`)在runmode特定設定資料夾下：

`/apps/example/config.<runmode>`

OSGi設定檔案的格式是以JSON為基礎，使用 `.cfg.json` Apache Sling專案定義的格式。

OSGi設定會透過元件的持續身分識別(PID) (預設為OSGi元件的Java™類別名稱)來鎖定OSGi元件。 例如，若要為以下實施的OSGi服務提供OSGi設定：

`com.example.workflow.impl.ApprovalWorkflow.java`

OSGi設定檔案定義於：

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

遵循 `cfg.json` OSGi設定格式。

>[!NOTE]
>
>使用不同檔案格式（例如）的先前版本AEM支援的OSGi設定檔案 `.cfg`， `.config` 和as XML `sling:OsgiConfig` 資源定義。 這些格式會由 `.cfg.json` OSGi設定格式。

## 執行模式解析度 {#runmode-resolution}

>[!TIP]
>
>AEM 6.x支援自訂執行模式，但AEMas a Cloud Service不支援。 AEMas a Cloud Service支援 [執行模式的確切集合](./overview.md#runmodes). AEMas a Cloud Service環境之間的OSGi設定任何變化必須使用來處理 [OSGi設定環境變數](#environment-specific-configuration-values).

使用執行模式可將特定OSGi設定鎖定到特定AEM執行個體。 若要使用runmode，請在下建立設定資料夾 `/apps/example` （範例是您的專案名稱），格式為：

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

如果設定資料夾名稱中定義的執行模式符合AEM使用的執行模式，則會使用此類資料夾中的任何OSGi設定。

例如，如果AEM使用runmodes author和dev，設定節點在 `/apps/example/config.author/` 和 `/apps/example/config.author.dev/` 套用，而設定節點位於 `/apps/example/config.publish/` 和 `/apps/example/config.author.stage/` 不會套用。

如果適用於同一PID的多個設定，則會套用符合執行模式數量最多的設定。

此規則的詳細程度為PID層級。 這表示您無法在中為相同的PID定義某些屬性 `/apps/example/config.author/` 以及中更具體的專案 `/apps/example/config.author.dev/` 相同PID的。 符合執行模式數量最多的設定將在整個PID中生效。

>[!NOTE]
>
>A `config.preview` OSGi設定資料夾 **無法** 以相同方式宣告 `config.publish` 可以宣告資料夾。 預覽層級會從發佈層級的值繼承其OSGi設定。

在进行本地开发时，运行架构启动参数 `-r` 用于指定运行架构 OSGI 配置。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

### 驗證執行模式

AEMas a Cloud Service執行模式已根據環境型別和服務進行了妥善定義。 檢閱 [可用AEMas a Cloud Service執行模式的完整清單](./overview.md#runmodes).

由執行模式指定的OSGi設定值可由以下驗證：

1. 開啟AEM as a Cloud Services環境的 [開發人員主控台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html)
1. 選取要檢查的服務層，使用 __Pod__ 下拉式清單
1. 選取 __狀態__ 標籤
1. 選取 __設定__ 從 __狀態傾印__ 下拉式清單
1. 選取 __取得狀態__ 按鈕

產生的檢視會顯示所選層的所有OSGi元件設定及其適用的OSGi設定值。 這些值可與AEM專案之原始程式碼中的OSGi設定值交叉參照，位於 `/apps/example/osgiconfig/config.<runmode(s)>`.


若要確認已套用適當的OSGi設定值：

1. 在開發人員控制檯的設定輸出中
1. 找到 `pid` 代表要驗證的OSGi設定；這是AEM專案原始碼中的OSGi設定檔案名稱。
1. Inspect `properties` 的清單 `pid` 並驗證索引鍵和值是否與正在驗證之執行模式的AEM專案原始碼中的OSGi設定檔相符。


## OSGi設定值的型別 {#types-of-osgi-configuration-values}

有三種不同的OSGi設定值可以搭配Adobe Experience Manager as a Cloud Service使用。

1. **內嵌值**，這些值會硬式編碼至OSGi設定中並儲存在Git中。 例如：

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **密碼值**，基於安全考量，這些值不得儲存在Git中。 例如：

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **環境特定值**，這些值在開發環境之間會有所不同，因此無法以執行模式準確鎖定目標(因為有單一 `dev` Adobe Experience Manager as a Cloud Service中的runmode)。 例如：

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   單一OSGi設定檔案可結合使用這些設定值型別的任何組合。 例如：

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## 如何選擇適當的OSGi設定值型別 {#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGi的常見案例使用內嵌OSGi設定值。 環境特定設定僅用於不同開發環境的值不同的特定使用案例。

![](assets/choose-configuration-value-type_res1.png)

環境特定設定擴充了包含內嵌值的傳統、靜態定義的OSGi設定，提供透過Cloud Manager API從外部管理OSGi設定值的功能。 重要的是，要瞭解何時應該使用定義內嵌值並將其儲存在Git中的常見和傳統方法，而不是將值抽象為特定於環境的配置。

以下指南說明何時使用非機密和機密環境特定設定：

### 何時使用內嵌設定值 {#when-to-use-inline-configuration-values}

內嵌設定值被視為標準方法，應儘可能使用。 內嵌設定提供下列優點：

* 這些區段會進行維護，並在Git中納入控管和版本記錄
* 值與程式碼部署隱含地連結
* 它們不需要任何其他部署考量或協調

每當定義OSGi設定值時，請從內嵌值開始，然後視使用案例需要僅選取密碼或環境特定的設定。

### 何時使用非機密環境特定設定值 {#when-to-use-non-secret-environment-specific-configuration-values}

僅使用環境特定設定(`$[env:ENV_VAR_NAME]`)適用於非機密設定值，前提是預覽層級的值有所不同，或開發環境之間的值不同。 這包括本機開發執行個體和任何Adobe Experience Manager as a Cloud Service開發環境。 除了設定預覽層級的唯一值外，請避免針對Adobe Experience Manager as a Cloud Service Stage或生產環境使用非機密環境專屬設定。

* 請僅針對發佈和預覽層級之間不同的設定值，或開發環境（包括本機開發執行個體）之間不同的值，使用非機密環境專屬設定。
* 除了預覽層級需要與發佈層級不同的情況，請在OSGi設定中將標準內嵌值用於中繼和生產非機密值。 因此，不建議使用環境特定的設定，以便於在執行階段對中繼和生產環境進行設定變更；這些變更應透過原始程式碼管理引入。

### 何時使用機密環境特定設定值 {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as a Cloud Service需要使用環境專屬設定(`$[secret:SECRET_VAR_NAME]`)設定值（例如密碼、私人API金鑰）或其他任何基於安全性原因而無法儲存在Git中的值。

使用秘密環境特定的設定來儲存所有Adobe Experience Manager as a Cloud Service環境（包括中繼和生產環境）的秘密值。

## 建立OSGi設定 {#creating-osgi-configurations}

建立OSGi設定的方式有兩種，如下所述。 前者通常用於設定具有開發人員所知OSGi屬性和值的自訂OSGi元件，而後者則用於AEM提供的OSGi元件。

### 寫入OSGi設定 {#writing-osgi-configurations}

JSON格式的OSGi設定檔案可直接在AEM專案中手動撰寫。 這通常是建立已知OSGi元件的OSGi設定的最快方式，尤其是由定義設定的相同開發人員設計和開發的自訂OSGi元件。 此方法也可用於在不同執行模式資料夾中複製/貼上並更新相同OSGi元件的設定。

1. 在IDE中，開啟 `ui.apps` 專案，找到或建立設定資料夾(`/apps/.../config.<runmode>`)以新OSGi設定需要生效的執行模式為目標
1. 在此設定資料夾中，建立 `<PID>.cfg.json` 檔案。 PID是OSGi元件的持續身分識別。 它通常是OSGi元件實作的完整類別名稱。 例如：
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
請注意，OSGi組態工廠檔案名稱會使用 `<factoryPID>-<name>.cfg.json` 命名慣例
1. 開啟新的 `.cfg.json` 檔案中，並定義OSGi屬性和值組的索引鍵/值組合，請遵循以下步驟 [JSON OSGi設定格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).
1. 將您的變更儲存至新的 `.cfg.json` 檔案
1. 新增新的OSGi設定檔案並將其提交到Git

### 使用AEM SDK快速入門產生OSGi設定 {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

AEM SDK快速入門Jar的AEM Web主控台可用於設定OSGi元件，以及將OSGi設定匯出為JSON。 這對於設定AEM提供的OSGi元件非常有用，在AEM專案中定義OSGi設定的開發人員可能無法很好地瞭解這些元件的OSGi屬性及其值格式。

>[!NOTE]
>
>AEM Web主控台的設定UI不會寫入 `.cfg.json` 檔案放入存放庫。 因此，請注意這一點，以避免在本機開發期間潛在的意外行為，當AEM專案定義的OSGi設定可能與產生的設定不同時。

1. 登入AEM SDK快速入門Jar的AEM Web主控台，網址為 `https://<host>:<port>/system/console` 作為管理員使用者
1. 導覽至 **osgi** > **設定**
1. 若要設定，請找到OSGi元件並點選其標題以進行編輯
   ![OSGi 配置](./assets/configuring-osgi/configuration.png)
1. 視需要透過Web UI編輯OSGi設定屬性值
1. 將持續身分識別(PID)記錄到安全的地方。 這稍後用於產生OSGi設定JSON
1. 點選「儲存」
1. 導覽至「OSGi > OSGi安裝程式設定印表機」
1. 貼入步驟5中複製的PID，確認序列化格式已設為「OSGi設定器JSON」
1. 點選「列印」
1. JSON格式的OSGi設定將顯示在序列化設定屬性區段中
   ![OSGi安裝程式設定印表機](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. 在IDE中，開啟 `ui.apps` 專案，找到或建立設定資料夾(`/apps/.../config.<runmode>`)以新OSGi設定需要生效的執行模式為目標。
1. 在此設定資料夾中，建立 `<PID>.cfg.json` 檔案。 PID與步驟5中的值相同。
1. 將步驟10中的序列化組態屬性貼入 `.cfg.json` 檔案。
1. 將您的變更儲存至新的 `.cfg.json` 檔案。
1. 新增新的OSGi設定檔案並將其提交到Git。


## OSGi設定屬性格式 {#osgi-configuration-property-formats}

### 內嵌值 {#inline-values}

內嵌值會依照標準JSON語法，格式化為標準名稱 — 值組。 例如：

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### 環境特定的設定值 {#environment-specific-configuration-values}

OSGi設定應該為打算根據環境定義的變數指派預留位置：

```
use $[env:ENV_VAR_NAME]
```

客戶應僅將此技巧用於與其自訂程式碼相關的OSGi設定屬性；不得使用此技巧來覆寫Adobe定義的OSGi設定。

>[!NOTE]
>
>預留位置不能用於 [repoinit陳述式](/help/implementing/deploying/overview.md#repoinit).

### 密碼設定值 {#secret-configuration-values}

OSGi設定應該為打算根據環境定義的密碼指派預留位置：

```
use $[secret:SECRET_VAR_NAME]
```

### 變數命名 {#variable-naming}

以下適用於特定環境和密碼設定值。

變數名稱必須符合下列規則：

* 最小長度：2
* 最大長度： 100
* 必須符合規則運算式： `[a-zA-Z_][a-zA-Z_0-9]*`

變數的值不得超過2048個字元。

>[!CAUTION]
>
>有些規則與變數名稱的特定首碼使用方式相關：
>
>1. 前置詞為的變數名稱 `INTERNAL_`， `ADOBE_`，或 `CONST_` 由Adobe保留。 任何以這些首碼開頭的客戶設定變數將會被忽略。
>
>1. 客戶不得參考前置詞為的變數 `INTERNAL_` 或 `ADOBE_` 兩者皆有。
>
>1. 前置詞為的環境變數 `AEM_` 由產品定義為公開API，以供客戶使用和設定。
   >   雖然客戶可以使用和設定以首碼開頭的環境變數 `AEM_` 他們不應使用此首碼定義自己的變數。


### 默认值 {#default-values}

以下適用於特定環境和密碼設定值。

如果未設定per-environment值，則在執行階段不會取代預留位置，而且由於未發生內插，因此會保留位置。 為避免此問題，可以使用以下語法在預留位置中提供預設值：

```
$[env:ENV_VAR_NAME;default=<value>]
```

在提供預設值時，預留位置會取代為根據環境提供的值或提供的預設值。

### 本地开发 {#local-development}

以下適用於特定環境和密碼設定值。

變數可在本機環境中定義，以便由本機AEM在執行階段擷取。 例如，在Linux®上：

```bash
export ENV_VAR_NAME=my_value
```

建議撰寫簡單的bash指令碼，此指令碼會設定設定中使用的環境變數，並在啟動AEM之前執行。 工具如 [https://direnv.net/](https://direnv.net/) 協助簡化此方法。 根據值的型別，如果可以在所有人之間共用這些值，則它們可能會被簽入原始程式碼管理。

密碼的值是從檔案中讀取的。 因此，您必須為每個使用密碼的預留位置建立包含密碼值的文字檔案。

例如，如果 `$[secret:server_password]` 已使用，文字檔名為 **server_password** 必須建立。 所有這些機密檔案都必須儲存在相同的目錄和框架屬性中 `org.apache.felix.configadmin.plugin.interpolation.secretsdir` 必須使用該本機目錄進行設定。

>[!CAUTION]
>
>文字檔不允許副檔名。
>
>因此，在上述範例中，必須將文字檔命名為 **server_password**  — 沒有副檔名。

此 `org.apache.felix.configadmin.plugin.interpolation.secretsdir` 是Sling架構屬性，所以此屬性不是在felix主控台(/system/console)中設定，而是在系統啟動時使用的sling.properties檔案中設定。 此檔案位於解壓縮的Jar/install資料夾(crx-quickstart/conf)的/conf子目錄中。

範例：將此行新增到&#39;crx-quickstart/conf/sling.properties&#39;-file的結尾處，將&#39;crx-quickstart/secretsdir&#39;設定為秘密資料夾：

```
org.apache.felix.configadmin.plugin.interpolation.secretsdir=${sling.home}/secretsdir
```

### 作者與發佈設定 {#author-vs-publish-configuration}

如果OSGi屬性對author和publish需要不同的值：

* 分隔 `config.author` 和 `config.publish` 必須使用OSGi資料夾，如 [執行模式解析區段](#runmode-resolution).
* 建立獨立變數名稱有兩個選項可供使用：
   * 建議使用的第一個選項：在所有OSGi資料夾中(例如 `config.author` 和 `config.publish`)宣告以定義不同的值，請使用相同的變數名稱。 例如
      `$[env:ENV_VAR_NAME;default=<value>]`，其中預設值對應至該層的預設值（作者或發佈）。 透過設定環境變數時 [Cloud Manager API](#cloud-manager-api-format-for-setting-properties) 或透過使用者端，使用「服務」引數來區分各階層，如以下所述 [API參考檔案](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/). 「service」引數會將變數的值繫結至適當的OSGi層。 可以是「作者」、「發佈」或「預覽」。
   * 第二個選項，是使用首碼宣告不同的變數，例如 `author_<samevariablename>` 和 `publish_<samevariablename>`

### 設定範例 {#configuration-examples}

在以下範例中，假設除了舞台和生產環境外，還有三個開發環境。

**範例1**

目的是OSGi屬性的值 `my_var1` 對stage和prod而言相同，但三個開發環境各有不同。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的內容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1"： "val"， "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" ： "$[env：my_var1]" "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
</table>

**範例2**

目的是OSGi屬性的值 `my_var1` 會因階段、prod和三個開發環境的不同而有所差異。 因此，必須呼叫Cloud Manager API來設定值 `my_var1` 適用於每個開發環境。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的內容</b>
</td>
</tr>
<tr>
<td>
config.stage
</td>
<td>
<pre>
{ "my_var1"： "val1"， "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ "my_var1"： "val2"， "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" ： "$[env：my_var1]" "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
</table>

**範例3**

目的是OSGi屬性的值 `my_var1` 階段、生產環境及其中一個開發環境相同，但其他兩個開發環境不同。 在此情況下，必須呼叫Cloud Manager API來設定值 `my_var1` 適用於每個開發環境，包括應該與中繼和生產具有相同值的開發環境。 它不會繼承資料夾中設定的值 **設定**.

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的內容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1"： "val1"， "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" ： "$[env：my_var1]" "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
</table>

完成此目標的另一種方式是在config.dev資料夾中設定取代權杖的預設值，使其與中的值相同 **設定** 資料夾。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的內容</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1"： "val1"， "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1"： "$[env：my_var1；default=val1]" "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
</table>

## 用於設定屬性的Cloud Manager API格式 {#cloud-manager-api-format-for-setting-properties}

另請參閱 [此頁面](https://developer.adobe.com/experience-cloud/cloud-manager/docs/) API的設定方式。
>[!NOTE]
>
>確保使用的Cloud Manager API已指派角色「部署管理員 — Cloud Service」。 其他角色無法執行下列所有命令。

### 透過API設定值 {#setting-values-via-api}

呼叫API會將新變數和值部署至雲端環境，類似於典型的客戶程式碼部署管道。 作者和發佈服務將重新啟動並參考新值，通常需要幾分鐘的時間。

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```
]
        {
                "name" : "MY_VAR1",
                "value" : "plaintext value",
                "type" : "string"  <---default
        },
        {
                "name" : "MY_VAR2",
                "value" : "<secret value>",
                "type" : "secretString"
        }
]
```

>[!NOTE]
>預設變數不是透過API設定，而是在OSGi屬性本身中設定。
>
>另請參閱 [此頁面](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) 以取得詳細資訊。

### 透過API取得值 {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

另請參閱 [此頁面](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) 以取得詳細資訊。

### 透過API刪除值 {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

若要刪除變數，請將其包含於空值中。

另請參閱 [此頁面](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) 以取得詳細資訊。

### 透過命令列取得值 {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### 透過命令列設定值 {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### 透過命令列刪除值 {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>另請參閱 [此頁面](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 有關如何使用Adobe I/OCLI的Cloud Manager外掛程式設定值的詳細資訊。

### 變數數量 {#number-of-variables}

每個環境最多可宣告200個變數。

## 秘密和環境特定設定值的部署考量事項 {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

由於秘密和環境特定的設定值位於Git之外，因此不屬於正式的Adobe Experience Manager as a Cloud Service部署機制，因此客戶應該管理、控管並整合到Adobe Experience Manager as a Cloud Service部署流程中。

如上所述，呼叫API會將新變數和值部署到雲端環境，類似於典型客戶程式碼部署管道。 作者和發佈服務將重新啟動並參考新值，通常需要幾分鐘的時間。 請注意，Cloud Manager在常規計畫碼部署期間執行的品質閘道和測試不會在此過程中執行。

通常，客戶在部署在Cloud Manager中依賴環境變數的程式碼之前，會呼叫API來設定環境變數。 在某些情況下，您可能想要在部署程式碼後修改現有變數。

>[!NOTE]
>
>當管道正在使用中(AEM更新或客戶部署)時，API可能不會成功，具體取決於當時端對端管道執行的部分。 錯誤回應會指出請求未成功，但不會指出特定原因。

在某些情況下，已排程的客戶程式碼部署會依賴現有變數來擁有新值，而這對目前的程式碼而言是不合適的。 如果這令人擔憂，建議以累加方式進行變數修改。 若要這麼做，請建立新的變數名稱，而非只變更舊變數的值，讓舊程式碼絕不會參考新值。 然後，當新的客戶版本看起來穩定時，您可以選擇移除舊的值。

同樣地，由於變數的值未建立版本，程式碼復原可能會導致它參照較新的值，進而導致問題。 前述的加法變數策略在此也有幫助。

此附加變數策略也適合用於災難復原的情況，當需要重新部署幾天前的程式碼時，其引用的變數名稱和值將保持不變。 這有賴於客戶在移除這些舊變數前會等待數天的策略，否則舊程式碼將沒有合適的變數可參照。
