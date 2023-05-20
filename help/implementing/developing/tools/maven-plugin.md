---
title: Adobe內容套件Maven外掛程式
description: 使用Content Package Maven外掛程式來部署AEM應用程式
exl-id: d631d6df-7507-4752-862b-9094af9759a0
source-git-commit: ba4e2427873fc9f5d91ee4f520df01018000a4c7
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 6%

---

# Adobe內容套件Maven外掛程式 {#adobe-content-package-maven-plugin}

使用Adobe內容套件Maven外掛程式，將套件部署和管理任務整合到您的Maven專案中。

將建構的套件部署到AEM是由Adobe內容套件Maven外掛程式執行，並允許自動化通常使用AEM執行的任務 [封裝管理員：](/help/implementing/developing/tools/package-manager.md)

* 從檔案系統中的檔案建立新封裝。
* 在AEM上安裝及解除安裝套件。
* 建置已在AEM上定義的套件。
* 取得AEM上安裝的套件清單。
* 從AEM移除套件。

本檔案詳細說明如何使用Maven管理這些任務。 不過，瞭解也很重要 [AEM專案及其套件的結構方式。](#aem-project-structure)

>[!NOTE]
>
>封裝 **建立** 現在是屬於 [Apache Jackrabbit FileVault Package Maven外掛程式。](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
>* 此 `content-package-maven-plugin` 不再支援1.0.2版的封裝。
>* 本文會說明 **部署** AEM的建構套件由Adobe內容套件Maven外掛程式執行。


## 套件和AEM專案結構 {#aem-project-structure}

AEMas a Cloud Service會遵循由最新AEM專案原型實作的套件管理和專案結構的最新最佳實務。

>[!TIP]
>
>如需詳細資訊，請參閱 [AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) AEMas a Cloud Service檔案中的文章以及 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 說明檔案。 AEM 6.5完全支援這兩項功能。

## 取得內容套件Maven外掛程式 {#obtaining-the-content-package-maven-plugin}

外掛程式可從 [Maven中央存放庫。](https://mvnrepository.com/artifact/com.day.jcr.vault/content-package-maven-plugin?repo=adobe-public)

## 內容套件Maven外掛程式目標和引數

若要使用Content Package Maven外掛程式，請在POM檔案的組建元素中新增下列外掛程式元素：

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>1.0.4</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

若要讓Maven下載外掛程式，請使用 [取得內容套件Maven外掛程式](#obtaining-the-content-package-maven-plugin) 區段。

## 內容套件Maven外掛程式的目標 {#goals-of-the-content-package-maven-plugin}

後續章節將說明「內容套件」外掛程式提供的目標與目標引數。 「一般引數」一節中說明的引數可用於大多數目標。 適用於一個目標的引數會在該目標的區段中說明。

### 外掛程式前置詞 {#plugin-prefix}

外掛程式首碼為 `content-package`. 使用此首碼從命令列執行目標，如下列範例所示：

```shell
mvn content-package:build
```

### 引數首碼 {#parameter-prefix}

除非另有說明，否則外掛程式目標和引數會使用 `vault` 前置詞，如下列範例所示：

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

### 代理 {#proxies}

使用AEM代理的目標會使用Maven設定中找到的第一個有效Proxy設定。 如果找不到Proxy設定，則不會使用Proxy。 請參閱 `useProxy` 中的引數 [常見引數](#common-parameters) 區段。

### 常見引數 {#common-parameters}

下表中的引數對所有目標都是通用的，除非在 **目標** 欄。

| 名称 | 类型 | 必填 | 默认值 | 描述 | 目標 |
|---|---|---|---|---|---|
| `failOnError` | `boolean` | 否 | `false` | 值 `true` 發生錯誤時導致建置失敗。 值 `false` 導致組建忽略錯誤。 | 所有目標，但 `package` |
| `name` | `String` | `build`：是， `install`：否， `rm`：是 | `build`：無預設值， `install`：的值 `artifactId` Maven專案的屬性 | 要對其採取動作的套件的名稱 | 所有目標，但 `ls` |
| `password` | `String` | 是 | `admin` | 用於使用AEM進行驗證的密碼 | 所有目標，但 `package` |
| `serverId` | `String` | 否 | 要從中擷取使用者名稱和密碼以進行驗證的伺服器ID | 所有目標，但 `package` |
| `targetURL` | `String` | 是 | `http://localhost:4502/crx/packmgr/service.jsp` | AEM套件管理員的HTTP服務API的URL | 所有目標，但 `package` |
| `timeout` | `int` | 否 | `5` | 與封裝管理程式服務通訊的連線逾時（以秒為單位） | 所有目標，但 `package` |
| `useProxy` | `boolean` | 否 | `true` | 值 `true` 會讓Maven使用找到的第一個作用中Proxy設定，以將請求代理至封裝管理員。 | 所有目標，但 `package` |
| `userId` | `String` | 是 | `admin` | 要向AEM驗證的使用者名稱 | 所有目標，但 `package` |
| `verbose` | `boolean` | 否 | `false` | 啟用或停用詳細記錄 | 所有目標，但 `package` |

### 建置 {#build}

建置已在AEM執行個體上定義的內容套件。

>[!NOTE]
>
>此目標不需要在Maven專案中執行。

#### 参数 {#parameters}

有關建置目標的所有引數的說明，請參見 [常見引數](#common-parameters) 區段。

### 安裝 {#install}

在存放庫中安裝套件。 執行此目標不需要Maven專案。 目標已繫結至 `install` Maven建置生命週期的階段。

#### 参数 {#parameters-1}

除了下列引數外，請參閱 [常見引數](#common-parameters) 區段。

| 名称 | 类型 | 必填 | 默认值 | 描述 |
|---|---|---|---|---|
| `artifact` | `String` | 否 | 的值 `artifactId` Maven專案的屬性 | 表單的字串 `groupId:artifactId:version[:packaging]` |
| `artifactId` | `String` | 否 | 无 | 要安裝的成品的ID |
| `groupId` | `String` | 否 | 无 | 此 `groupId` 要安裝的成品 |
| `install` | `boolean` | 否 | `true` | 決定是否在上傳封裝時自動將其解壓縮 |
| `localRepository` | `org.apache.maven.artifact.repository.ArtifactRepository` | 否 | 的值 `localRepository` 系統變數 | 無法透過外掛程式設定來設定的本機Maven存放庫，因為系統屬性一律使用 |
| `packageFile` | `java.io.File` | 否 | 為Maven專案定義的主要成品 | 要安裝的套件檔案名稱 |
| `packaging` | `String` | 否 | `zip` | 要安裝的成品封裝型別 |
| `pomRemoteRepositories` | `java.util.List` | 是 | 的值 `remoteArtifactRepositories` 為Maven專案定義的屬性 | 此值無法使用外掛程式設定進行設定，必須在專案中指定。 |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 為其設定外掛程式的專案 | 隱含的Maven專案，因為專案包含外掛程式設定 |
| `repositoryId` (POM)， `repoID` （命令列） | `String` | 否 | `temp` | 從中擷取成品的存放庫識別碼 |
| `repositoryUrl` (POM)， `repoURL` （命令列） | `String` | 否 | 无 | 從中擷取成品的存放庫URL |
| 版本 | 字符串 | 否 | 无 | 要安裝的成品版本 |

### ls {#ls}

列出部署至的套件 [封裝管理員。](/help/implementing/developing/tools/package-manager.md)

#### 参数 {#parameters-2}

ls目標的所有引數都說明於 [常見引數](#common-parameters) 區段。

### rm {#rm}

從以下位置移除套件 [封裝管理員。](/help/implementing/developing/tools/package-manager.md)

#### 参数 {#parameters-3}

RM目標的所有引數都說明於 [常見引數](#common-parameters) 區段。

### 解除安裝 {#uninstall}

解除安裝套件。 套件會維持在伺服器上未安裝狀態。

#### 参数 {#parameters-4}

有關解除安裝目標的所有引數的說明，請參見 [常見引數](#common-parameters) 區段。

### 封裝 {#package}

建立內容封裝。 套件目標的預設設定包含儲存已編譯檔案的目錄內容。 套件目標的執行需要編譯建置階段完成。 套件目標繫結至Maven建置生命週期的套件階段。

#### 参数 {#parameters-5}

除了下列引數外，請參閱 `name` 中的引數 [常見引數](#common-parameters) 區段。

| 名称 | 类型 | 必填 | 默认值 | 描述 |
|---|---|---|---|---|
| `archive` | `org.apache.maven.archiver.MavenArchiveConfiguration` | 否 | 无 | 要使用的封存設定 |
| `builtContentDirectory` | `java.io.File` | 是 | Maven組建的輸出目錄值 | 包含要包含在封裝中的內容的目錄 |
| `dependencies` | `java.util.List` | 否 | 无 |  |
| `embeddedTarget` | `java.lang.String` | 否 | 无 |  |
| `embeddeds` | `java.util.List` | 否 | 无 |  |
| `failOnMissingEmbed` | `boolean` | 是 | `false` | 值 `true` 在專案相依性中找不到內嵌成品時，會導致建置失敗。 值 `false` 導致組建忽略此類錯誤。 |
| `filterSource` | `java.io.File` | 否 | 无 | 此引數會定義一個檔案，用來指定工作區篩選器的來源。 在設定中指定並透過嵌入或子套件插入的篩選器會與檔案內容合併。 |
| `filters` | `com.day.jcr.vault.maven.pack.impl.DefaultWorkspaceFilter` | 否 | 无 | 此引數包含定義封裝內容的篩選元素。 執行時，篩選器包含在 `filter.xml` 檔案。 請參閱 [使用篩選器](#using-filters) 區段底下。 |
| `finalName` | `java.lang.String` | 是 | 此 `finalName` 在Maven專案中定義（建置階段） | 所產生套件ZIP檔案的名稱，不含 `.zip` 副檔名 |
| `group` | `java.lang.String` | 是 | 此 `groupID` 在Maven專案中定義 | 此 `groupId` 屬於內容套件的目標安裝路徑一部分的已產生內容套件的 |
| `outputDirectory` | `java.io.File` | 是 | 在Maven專案中定義的組建目錄 | 儲存內容套件的本機目錄 |
| `prefix` | `java.lang.String` | 否 | 无 |  |
| `project` | `org.apache.maven.project.MavenProject` | 是 | 无 | Maven專案 |
| `properties` | `java.util.Map` | 否 | 无 | 這些引數定義您可在下列位置設定的其他屬性： `properties.xml` 檔案。 這些屬性無法覆寫下列預先定義的屬性： `group` (使用 `group` 要設定的引數)， `name` (使用 `name` 要設定的引數)， `version` (使用 `version` 要設定的引數)， `description` （從專案說明設定）， `groupId` (`groupId` Maven專案描述項的)， `artifactId` (`artifactId` Maven專案描述項的)， `dependencies` (使用 `dependencies` 要設定的引數)， `createdBy` (的值 `user.name` 系統屬性)， `created` （目前系統時間）、 `requiresRoot` (使用 `requiresRoot` 要設定的引數)， `packagePath` （從群組和封裝名稱自動產生） |
| `requiresRoot` | `boolean` | 是 | false | 定義套件是否需要root。 這將會成為 `requiresRoot` 的屬性 `properties.xml` 檔案。 |
| `subPackages` | `java.util.List` | 否 | 无 |  |
| `version` | `java.lang.String` | 是 | Maven專案中定義的版本 | 內容套件的版本 |
| `workDirectory` | `java.io.File` | 是 | Maven專案（建置階段）中定義的目錄 | 包含要包含在封裝中的內容的目錄 |

#### 使用篩選器 {#using-filters}

使用篩選器元素來定義封裝內容。 篩選器會新增至 `workspaceFilter` 中的元素 `META-INF/vault/filter.xml` 封裝的檔案。

下列篩選範例顯示要使用的XML結構：

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

##### 导入模式 {#import-mode}

此 `mode` 元素會定義內容在匯入套件時如何影響存放庫。 可以使用以下值：

* **合併：** 已新增封裝中尚未在存放庫中的內容。 套件和存放庫中的內容皆未變更。 不會從存放庫移除任何內容。
* **取代：** 套件中不在存放庫中的內容會新增到存放庫。 存放庫中的內容會由套件中的相符內容取代。 當套件中不存在內容時，該內容會從存放庫移除。
* **更新：** 套件中不在存放庫中的內容會新增到存放庫。 存放庫中的內容會由套件中的相符內容取代。 現有內容會從存放庫中移除。

當篩選器包含否時 `mode` 元素，的預設值 `replace` 已使用。

### 帮助 {#help}

#### 参数 {#parameters-6}

| 名称 | 类型 | 必填 | 默认值 | 描述 |
|---|---|---|---|---|
| `detail` | `boolean` | 否 | `false` | 決定是否顯示每個目標的所有可設定屬性 |
| `goal` | `String` | 否 | 无 | 此引數會定義要顯示其說明的目標名稱。 如果未指定任何值，則會顯示所有目標的說明。 |
| `indentSize` | `int` | 否 | `2` | 用於每個層級縮排的空格數（如果已定義，則必須為正數） |
| `lineLength` | `int` | 否 | `80` | 顯示線的最大長度（如果已定義，則必須為正數） |

## 在套件中包含縮圖影像或屬性檔案 {#including-a-thumbnail-image-or-properties-file-in-the-package}

取代預設封裝組態檔以自訂封裝屬性。 例如，加入縮圖影像來區分中的套件 [封裝管理員。](/help/implementing/developing/tools/package-manager.md)

來源檔案可以位於檔案系統中的任何位置。 在POM檔案中，定義建置資源以將來源檔案複製到 `target/vault-work/META-INF` 以包含在套件中。

下列POM程式碼會將檔案新增至 `META-INF` 封裝的專案來源資料夾：

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

下列POM程式碼僅會將縮圖影像新增至套件。 縮圖影像必須命名為 `thumbnail.png`，且必須位於 `META-INF/vault/definition` 封裝的資料夾。 在此範例中，來源檔案位於 `/src/main/content/META-INF/vault/definition` 專案的資料夾：

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## 使用AEM專案原型來產生AEM專案 {#using-archetypes}

最新的AEM專案原型會針對內部部署和AMS實作實施最佳實務套件結構，並建議用於所有AEM專案。

>[!TIP]
>
>如需詳細資訊，請參閱 [AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) AEMas a Cloud Service檔案中的文章以及 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 說明檔案。 AEM 6.5完全支援這兩項功能。
