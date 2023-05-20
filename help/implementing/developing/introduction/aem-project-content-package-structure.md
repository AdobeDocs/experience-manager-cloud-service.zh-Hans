---
title: AEM 项目结构
description: 瞭解如何定義套件結構以部署至Adobe Experience ManagerCloud Service。
exl-id: 38f05723-5dad-417f-81ed-78a09880512a
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '2931'
ht-degree: 12%

---

# AEM 项目结构

>[!TIP]
>
>熟悉基本知識 [AEM專案原型使用](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，以及 [FileVault Content Maven外掛程式](/help/implementing/developing/tools/maven-plugin.md) 因為本文章是以這些學問和概念為基礎而建立。

本文概述Adobe Experience Manager Maven專案為與AEMas a Cloud Service相容所需的變更，確保專案遵守可變和不可變內容的分割，建立相依性以建立無衝突、確定性的部署，並封裝成可部署的結構。

AEM應用程式部署必須由單一AEM套件組成。 此套件繼而應包含子套件，子套件包含應用程式運作所需的一切，包括程式碼、設定及任何支援的基準線內容。

AEM需要分隔 **內容** 和 **程式碼**，這表示單一內容套件 **無法** 部署至 **兩者** `/apps` 和執行階段可寫入區域(例如， `/content`， `/conf`， `/home`，或不存在的任何專案 `/apps`)。 相反，应用程序必须将代码和内容分离到离散包中，以部署到 AEM 中。

本文档中概述的包结构与本地开发部署&#x200B;**和** AEM 云服务部署兼容。

>[!TIP]
>
>本檔案中概述的設定是由 [AEM專案Maven Archetype 24或更新版本](https://github.com/adobe/aem-project-archetype/releases).

## 可變與不可變存放庫區域 {#mutable-vs-immutable}

`/apps` 和 `/libs`**被视为 AEM 中的不可变区域，因为 AEM 启动后（例如，运行时），无法对其进行更改（创建、更新、删除）。**&#x200B;运行时对不可改变区域所做的任何更改尝试都将失败。

存放庫中的所有其他專案， `/content`， `/conf`， `/var`， `/etc`， `/oak:index`， `/system`， `/tmp`等。 全部 **可變** 區域，表示可在執行階段變更這些區域。

>[!WARNING]
>
>和舊版AEM一樣， `/libs` 不應修改。 只有AEM產品程式碼可以部署至 `/libs`.

### Oak索引 {#oak-indexes}

Oak索引(`/oak:index`)會由AEMas a Cloud Service部署程式專門管理。 這是因為Cloud Manager必須等到部署任何新索引並完全重新索引後，才能切換至新的程式碼影像。

因此，雖然Oak索引在執行階段是可變的，但它們必須部署為程式碼，以便在安裝任何可變套件之前可以安裝。 因此 `/oak:index` 設定是程式碼套件的一部分，而不是內容套件的一部分 [如下所述](#recommended-package-structure).

>[!TIP]
>
>如需AEMas a Cloud Service索引的詳細資訊，請參閱本檔案 [內容搜尋與索引](/help/operations/indexing.md).

## 建議的封裝結構 {#recommended-package-structure}

![Experience Manager專案封裝結構](assets/content-package-organization.png)

此圖表提供建議的專案結構和套件部署成品概觀。

建議的應用程式部署結構如下：

### 程式碼套件/ OSGi套裝

+ 會產生OSGi套件Jar檔案，並直接內嵌在所有專案中。

+ 此 `ui.apps` 套件包含要部署的所有程式碼，且僅部署至 `/apps`. 的常見元素 `ui.apps` 套件包含但不限於：
   + [元件定義和HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=zh-Hans) 指令碼
      + `/apps/my-app/components`
   + JavaScript和CSS (透過 [使用者端資料庫](/help/implementing/developing/introduction/clientlibs.md))
      + `/apps/my-app/clientlibs`
   + [覆蓋](/help/implementing/developing/introduction/overlays.md) 之 `/libs`
      + `/apps/cq`， `/apps/dam/`等。
   + 遞補內容感知設定
      + `/apps/settings`
   + ACL （許可權）
      + 任何 `rep:policy` 下的任何路徑 `/apps`
   + [預先編譯的套件指令碼](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/precompiled-bundled-scripts.html)

>[!NOTE]
>
>所有環境都必須部署相同的程式碼。 這是為了確保中繼環境上的信賴驗證層級也用於生產環境所需。 如需詳細資訊，請參閱以下章節： [執行模式](/help/implementing/deploying/overview.md#runmodes).


### 內容套件

+ 此 `ui.content` 套件包含所有內容和設定。 內容套件包含不在中的所有節點定義 `ui.apps` 或 `ui.config` 封裝，或換言之，任何不在中的內容 `/apps` 或 `/oak:index`. 的常見元素 `ui.content` 套件包含但不限於：
   + 內容感知設定
      + `/conf`
   + 必要的複雜內容結構(即 內容建置以存放庫初始化中定義的過去基準內容結構為基礎並加以擴充。)
      + `/content`， `/content/dam`等。
   + 控管的標籤分類
      + `/content/cq:tags`
   + 舊版ETC節點（最好將這些節點移轉至非/etc位置）
      + `/etc`

### 容器封裝

+ 此 `all` 套件是容器套件，僅包含可部署的成品、OSGI套件Jar檔案、 `ui.apps`， `ui.config` 和 `ui.content` 套件作為內嵌。 此 `all` 套件不得具有 **任何內容或程式碼** 將其本身部署，而是將所有部署委派給存放庫的子包或OSGi捆綁Jar檔案。

   套件現在包含使用Maven [FileVault Package Maven外掛程式的內嵌設定](#embeddeds)，而非 `<subPackages>` 設定。

   對於複雜的Experience Manager部署，最好建立多個 `ui.apps`， `ui.config` 和 `ui.content` 代表AEM中特定網站或租使用者的專案/套件。 如果這樣做，請確保遵循可變和不可變內容之間的拆分，並將所需的內容包和OSGi捆綁Jar檔案嵌入到中的子包中 `all` 容器內容封裝。

   例如，複雜的部署內容套件結構可能如下所示：

   + `all` 內容套件內嵌下列套件，以建立單一部署成品
      + `common.ui.apps` 部署所需的程式碼 **兩者** 網站A和網站B
      + `site-a.core` 網站A所需的OSGi套件Jar
      + `site-a.ui.apps` 部署網站A所需的程式碼
      + `site-a.ui.config` 部署網站A所需的OSGi設定
      + `site-a.ui.content` 部署網站A所需的內容和設定
      + `site-b.core` 網站B所需的OSGi套件Jar
      + `site-b.ui.apps` 部署網站B所需的程式碼
      + `site-b.ui.config` 部署網站B所需的OSGi設定
      + `site-b.ui.content` 部署網站B所需的內容和設定

+ 此 `ui.config` 套件包含全部 [OSGi設定](/help/implementing/deploying/configuring-osgi.md)：
   + 視為程式碼且屬於OSGi套件組合，但不包含一般內容節點。 因此會標示為容器封裝
   + 包含執行模式特定OSGi設定定義的組織資料夾
      + `/apps/my-app/osgiconfig`
   + 包含套用至所有目標AEMas a Cloud Service部署目標的預設OSGi設定的通用OSGi設定資料夾
      + `/apps/my-app/osgiconfig/config`
   + 執行包含套用至所有目標AEMas a Cloud Service部署目標的預設OSGi設定的特定模式OSGi設定資料夾
      + `/apps/my-app/osgiconfig/config.<author|publish>.<dev|stage|prod>`
   + Repo Init OSGi設定指令碼
      + [Repo Init](#repo-init) 建議使用此方式部署（可變）內容，這些內容在邏輯上屬於AEM應用程式的一部分。 Repo Init OSGi設定應放置在適當的位置 `config.<runmode>` 資料夾（如上所述），並用來定義：
         + 基準內容結構
         + 用户
         + 服務使用者
         + 组
         + ACL （許可權）

### 額外的應用程式套件{#extra-application-packages}

如果AEM部署使用其他AEM專案（專案本身由專案自己的程式碼和內容套件組成），則應將其容器套件內嵌在專案的 `all` 封裝。

例如，包含2個廠商AEM應用程式的AEM專案可能如下所示：

+ `all` 內容套件內嵌下列套件，以建立單一部署成品
   + `core` AEM應用程式所需的OSGi套件Jar
   + `ui.apps` 部署AEM應用程式所需的程式碼
   + `ui.config` 部署AEM應用程式所需的OSGi設定
   + `ui.content` 部署AEM應用程式所需的內容和設定
   + `vendor-x.all` 部署廠商X應用程式所需的一切（程式碼和內容）
   + `vendor-y.all` 部署廠商Y應用程式所需的一切（程式碼和內容）

## 封裝型別 {#package-types}

套件將標示其宣告的套件型別。 套件型別有助於釐清套件的用途和部署。

+ 容器套件必須設定其 `packageType` 至 `container`. 容器套件不得包含一般節點。 僅允許OSGi套件組合、設定和子套件。 AEMas a Cloud Service中的容器不允許使用 [安裝鉤點](https://jackrabbit.apache.org/filevault/installhooks.html).
+ 程式碼（不可變）套件必須設定其 `packageType` 至 `application`.
+ 內容（可變）套件必須設定其 `packageType` 至 `content`.


如需詳細資訊，請參閱 [Apache Jackrabbit FileVault — 套件Maven外掛程式檔案](https://jackrabbit.apache.org/filevault-package-maven-plugin/package-mojo.html#packageType)， [Apache Jackrabbit套件型別](https://jackrabbit.apache.org/filevault/packagetypes.html)，以及 [FileVault Maven設定片段](#marking-packages-for-deployment-by-adoube-cloud-manager) 下方的。

>[!TIP]
>
>請參閱 [POM XML代碼片段](#xml-package-types) 區段以取得完整的程式碼片段。

## 透過AdobeCloud Manager標籤要部署的套件 {#marking-packages-for-deployment-by-adoube-cloud-manager}

默认情况下，Adobe Cloud Manager 会收集由 Maven 内部版本生成的所有包，但是，由于容器 (`all`) 包是包含所有代码和内容包的单个部署对象，因此我们必须确保&#x200B;**仅**&#x200B;部署容器 (`all`) 包。要确保这一点，Maven 内部版本生成的其他包必须使用 `<properties><cloudManagerTarget>none</cloudManageTarget></properties>` 的 FileVault Content Package Maven Plug-In 配置进行标记。

>[!TIP]
>
>請參閱 [POM XML代碼片段](#pom-xml-snippets) 區段以取得完整的程式碼片段。

## Repo Init{#repo-init}

Repo Init提供定義JCR結構的指示或指令碼，範圍從資料夾樹狀結構等通用節點結構，到使用者、服務使用者、群組和ACL定義。

Repo Init的主要優點是，它們具有執行其指令碼定義之所有動作的隱含許可權，並在部署生命週期的早期叫用，以確保在執行程式碼時存在所有必要的JCR結構。

雖然Repo Init指令碼本身會在 `ui.config` 以指令碼方式專案時，可以也應該使用它們來定義下列可變結構：

+ 基準內容結構
+ 服務使用者
+ 用户
+ 组
+ ACL

存放庫初始指令碼儲存為 `scripts` 專案： `RepositoryInitializer` 因此，OSGi工廠設定可由執行模式隱含定位，以允許AEM Author和AEM Publish Services的Repo Init指令碼之間的差異，甚至環境（開發、階段和生產環境）之間的差異。

Repo Init OSGi設定最好寫入 [`.config` OSGi設定格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-config-1) 因為它們支援多行，這是使用的最佳實務的例外情況 [`.cfg.json` 定義OSGi設定的方式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).

請注意，定義使用者和群組時，只有群組會被視為應用程式的一部分，應在此處定義其功能的組成部分。 組織使用者和群組仍應在AEM中在執行階段定義；例如，如果自訂工作流程將工作指派給已命名的群組，則該群組應透過AEM應用程式中的Repo Init在中定義，但是，如果群組只是組織性的，例如「Wendy&#39;s Team」和「Sean&#39;s Team」，則這些會最佳定義，並在AEM中執行階段進行管理。

>[!TIP]
>
>存放庫初始指令碼 *必須* 在內嵌中定義 `scripts` 欄位，以及 `references` 設定無法運作。

Repo Init指令碼的完整辭彙表可在以下網址取得： [Apache Sling Repo初始檔案](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

>[!TIP]
>
>請參閱 [Repo初始程式碼片段](#snippet-repo-init) 區段以取得完整的程式碼片段。

## 存放庫結構套件 {#repository-structure-package}

程式碼套件需要將FileVault Maven外掛程式的設定設定為參照 `<repositoryStructurePackage>` 這會強制結構相依性的正確性（以確保一個程式碼套件不會安裝在另一個程式碼套件上）。 您可以 [為您的專案建立自己的存放庫結構套件](repository-structure-package.md).

此操作&#x200B;**仅适用于**&#x200B;代码包，即任何标有 `<packageType>application</packageType>` 的包。

若要瞭解如何為您的應用程式建立存放庫結構套件，請參閱 [開發存放庫結構套件](repository-structure-package.md).

請注意，內容套件(`<packageType>content</packageType>`) **不要** 需要此存放庫結構套件。

>[!TIP]
>
>請參閱 [POM XML代碼片段](#xml-repository-structure-package) 區段以取得完整的程式碼片段。

## 在容器软件包中嵌入子软件包{#embeddeds}

內容或程式碼套件會放置在特殊的「side-car」資料夾中，並可鎖定為安裝在AEM author、AEM publish上，或兩者上都使用FileVault Maven外掛程式的 `<embeddeds>` 設定。 請注意 `<subPackages>` 不應使用設定。

常見的使用案例包括：

+ AEM作者使用者和AEM發佈使用者之間不同的ACL/許可權
+ 僅用於支援AEM作者上活動的設定
+ 程式碼（例如與後台系統的整合）僅需在AEM作者上執行

![內巢狀件](assets/embeddeds.png)

若要鎖定AEM作者、AEM發佈或兩者，套件會內嵌於 `all` 容器封裝在特殊資料夾位置中，格式如下：

`/apps/<app-name>-packages/(content|application|container)/install(.author|.publish)?`

劃分此資料夾結構：

+ 第一層資料夾 **必須是** `/apps`.
+ 第二層資料夾代表應用程式，具有 `-packages` 在資料夾名稱中加上後置修正。 通常只有單一的第二層資料夾，所有子套件都內嵌於其下，但是可以建立任意數量的第二層資料夾以最好地代表應用程式的邏輯結構：
   + `/apps/my-app-packages`
   + `/apps/my-other-app-packages`
   + `/apps/vendor-packages`

   >[!WARNING]
   >
   >按照惯例，子包嵌入式文件夹的名称带有后缀 `-packages`。这样可确保部署代码和内容包&#x200B;**不会**&#x200B;部署到任何子包 `/apps/<app-name>/...` 的目标文件夹，否则将会导致破坏性的循环安装行为。

+ 第3層資料夾必須是
   `application`, `content` 或 `container`
   + 此 `application` 資料夾內含程式碼套件
   + 此 `content` 資料夾內含內容封裝
   + 此 `container` 資料夾保留任何 [額外的應用程式套件](#extra-application-packages) AEM應用程式可能包含的資訊。
此資料夾名稱對應至 [封裝型別](#package-types) 包含之套裝軟體的ID。
+ 第 4 级文件夹包含子包，且必须是以下包之一：
   + `install`，以在 AEM 作者&#x200B;**和** AEM 发布上安装
   + `install.author`，以&#x200B;**仅**&#x200B;在 AEM 作者上安装
   + `install.publish` 至 **僅限** 安裝在AEM發佈僅請注意 `install.author` 和 `install.publish` 支援的目標。 不支持其 **他运行模式** 。

例如，包含AEM作者和發佈特定套件的部署看起來可能像這樣：

+ `all` 容器套件內嵌下列套件，以建立單一部署成品
   + `ui.apps` 內嵌於 `/apps/my-app-packages/application/install` 將程式碼部署到AEM作者和AEM發佈
   + `ui.apps.author` 內嵌於 `/apps/my-app-packages/application/install.author` 將程式碼僅部署給AEM作者
   + `ui.content` 內嵌於 `/apps/my-app-packages/content/install` 將內容和設定部署到AEM作者和AEM發佈
   + `ui.content.publish` 內嵌於 `/apps/my-app-packages/content/install.publish` 僅將內容和設定部署到AEM publish

>[!TIP]
>
>請參閱 [POM XML代碼片段](#xml-embeddeds) 區段以取得完整的程式碼片段。

### 容器封裝的篩選器定義 {#container-package-filter-definition}

由於程式碼和內容子套件內嵌在容器套件中，因此內嵌的目標路徑必須新增到容器專案的 `filter.xml` 以確保在建置時內巢狀件包含在容器套件中。

只需新增 `<filter root="/apps/<my-app>-packages"/>` 包含要部署的子包的任何第二級資料夾的專案。

>[!TIP]
>
>請參閱 [POM XML代碼片段](#xml-container-package-filters) 區段以取得完整的程式碼片段。

## 內嵌第三方套件 {#embedding-3rd-party-packages}

所有套件都必須透過 [Adobe的公用Maven成品存放庫](https://repo1.maven.org/maven2/com/adobe/) 或可存取的公開、可參照的第三方Maven成品存放庫。

如果第三方包位于 **Adobe 的公共 Maven 对象存储库**，则 Adobe Cloud Manager 无需进一步配置即可解析对象。

如果第三方包位于&#x200B;**公共的第三方 Maven 对象存储库**，则必须在项目的 `pom.xml` 中注册此存储库，并将其嵌入到[以上所述](#embeddeds)的以下方法中。

第三方應用程式/聯結器應使用其 `all` 封裝為專案容器中的容器(`all`)封裝。

新增Maven相依性會遵循標準Maven實務，以及內嵌第三方成品（程式碼和內容套件）有 [上面概述](#embedding-3rd-party-packages).

>[!TIP]
>
>請參閱 [POM XML代碼片段](#xml-3rd-party-maven-repositories) 區段以取得完整的程式碼片段。

## 套件之間的相依性 `ui.apps` 從 `ui.content` 套件 {#package-dependencies}

為確保正確安裝套件，建議建立套件間相依性。

一般規則是包含可變內容的套件(`ui.content`)取決於不可變程式碼(`ui.apps`)可支援呈現和使用可變內容。

此一般規則有一個顯著的例外情況，就是如果不可變的程式碼套件(`ui.apps` 或任何其他)， __僅限__ 包含OSGi套件組合。 如果是，則任何AEM套件都不應宣告其上的相依性。 這是因為不可變的程式碼套件 __僅限__ 包含OSGi套件組合未向AEM註冊 [封裝管理員，](/help/implementing/developing/tools/package-manager.md) 因此，依賴它的任何AEM套件都會有不滿意的相依性，並且無法安裝。

>[!TIP]
>
>請參閱 [POM XML代碼片段](#xml-package-dependencies) 區段以取得完整的程式碼片段。

內容套件相依性的常見模式包括：

### 簡易部署套件相依性 {#simple-deployment-package-dependencies}

簡單案例會設定 `ui.content` 可變的內容套件依賴於 `ui.apps` 不可變的程式碼套件。

+ `all` 沒有相依性
   + `ui.apps` 沒有相依性
   + `ui.content` 依據 `ui.apps`

### 複雜的部署套件相依性 {#complex-deploxment-package-dependencies}

複雜的部署會以簡單案例展開，並設定對應可變內容與不可變程式碼套件之間的相依性。 如有需要，也可以在不可變的程式碼套件之間建立相依性。

+ `all` 沒有相依性
   + `common.ui.apps.common` 沒有相依性
   + `site-a.ui.apps` 依據 `common.ui.apps`
   + `site-a.ui.content` 依據 `site-a.ui.apps`
   + `site-b.ui.apps` 依據 `common.ui.apps`
   + `site-b.ui.content` 依據 `site-b.ui.apps`

## 本機開發和部署 {#local-development-and-deployment}

本文中概述的專案結構和組織為 **完全相容** 本機開發AEM執行個體。

## POM XML代碼片段 {#pom-xml-snippets}

以下是Maven `pom.xml` 可新增至Maven專案的設定片段以與上述建議一致。

### 封裝型別 {#xml-package-types}

作为子包部署的代码和内容包必须声明&#x200B;**应用程序**&#x200B;或&#x200B;**内容**&#x200B;包类型,具体取决于它们包含的内容。

#### 容器封裝型別 {#container-package-types}

容器 `all/pom.xml` 專案 **不會** 宣告 `<packageType>`.

#### 程式碼（不可變）封裝型別 {#immutable-package-types}

程式碼套件必須設定其 `packageType` 至 `application`.

在 `ui.apps/pom.xml`，則 `<packageType>application</packageType>` 建置以下專案的設定指令： `filevault-package-maven-plugin` 外掛程式宣告會宣告其封裝型別。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>my-app.ui.apps</name>
        <packageType>application</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

#### 內容（可變）封裝型別 {#mutable-package-types}

內容套件必須設定其 `packageType` 至 `content`.

在 `ui.content/pom.xml`，則 `<packageType>content</packageType>` 建置的組態指示詞 `filevault-package-maven-plugin` 外掛程式宣告會宣告其封裝型別。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        <group>${project.groupId}</group>
        <name>my-app.ui.content</name>
        <packageType>content</packageType>
        <accessControlHandling>merge</accessControlHandling>
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### 標籤套件以AdobeCloud Manager部署 {#cloud-manager-target}

在生成包的每个项目中，**除**&#x200B;容器 (`all`) 项目外，将 `<cloudManagerTarget>none</cloudManagerTarget>` 添加到 `filevault-package-maven-plugin` 插件声明的 `<properties>` 配置中，以确保 Adobe Cloud Manager **不**&#x200B;部署这些它们。容器(`all`)套件應該是透過Cloud Manager部署的單一套件，接著會嵌入所有必要的程式碼和內容套件。

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <properties>
          <cloudManagerTarget>none</cloudManagerTarget>
        </properties>
      </configuration>
    </plugin>
    ...
```

### Repo Init{#snippet-repo-init}

包含Repo Init指令碼的Repo Init指令碼定義於 `RepositoryInitializer` OSGi工廠設定，透過 `scripts` 屬性。 請注意，由於這些指令碼是在OSGi設定中定義，因此可使用一般方式以執行模式輕鬆設定其範圍 `../config.<runmode>` 資料夾語意。

請注意，由於指令碼通常是多行宣告，因此在 `.config` 檔案，而非JSON型 `.cfg.json` 格式。

`/apps/my-app/config.author/org.apache.sling.jcr.repoinit.RepositoryInitializer-author.config`

```plain
scripts=["
    create service user my-data-reader-service

    set ACL on /var/my-data
        allow jcr:read for my-data-reader-service
    end

    create path (sling:Folder) /conf/my-app/settings
"]
```

此 `scripts` OSGi屬性包含由定義的指令 [Apache Sling的Repo Init語言](https://sling.apache.org/documentation/bundles/repository-initialization.html#the-repoinit-repository-initialization-language).

### 存放庫結構套件 {#xml-repository-structure-package}

在 `ui.apps/pom.xml` 和任何其他 `pom.xml` 會宣告程式碼套件(`<packageType>application</packageType>`)，將下列存放庫結構封裝設定新增至FileVault Maven外掛程式。 您可以 [為您的專案建立自己的存放庫結構套件](repository-structure-package.md).

```xml
...
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.jackrabbit</groupId>
      <artifactId>filevault-package-maven-plugin</artifactId>
      <extensions>true</extensions>
      <configuration>
        ...
        <repositoryStructurePackages>
          <repositoryStructurePackage>
              <groupId>${project.groupId}</groupId>
              <artifactId>ui.apps.structure</artifactId>
              <version>${project.version}</version>
          </repositoryStructurePackage>
        </repositoryStructurePackages>
      </configuration>
    </plugin>
    ...
```

### 在容器软件包中嵌入子软件包 {#xml-embeddeds}

在 `all/pom.xml`，新增下列專案 `<embeddeds>` 指令到 `filevault-package-maven-plugin` 外掛程式宣告。 請記住， **不要** 使用 `<subPackages>` 設定，因為這會包含中的子封裝 `/etc/packages` 而非 `/apps/my-app-packages/<application|content|container>/install(.author|.publish)?`.

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <embeddeds>

          <!-- Include the application's ui.apps and ui.content packages -->
          <!-- Ensure the artifactIds are correct -->

          <!-- OSGi Bundle Jar file that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.core</artifactId>
              <type>jar</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

           <!-- OSGi configuration code package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.config</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install</target>
          </embedded>

          <!-- Code package that deploys ONLY to AEM Author -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.apps.author</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/application/install.author</target>
          </embedded>

          <!-- Content package that deploys to BOTH AEM Author and AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install</target>
          </embedded>

          <!-- Content package that deploys ONLY to AEM Publish -->
          <embedded>
              <groupId>${project.groupId}</groupId>
              <artifactId>my-app.ui.content.publish-only</artifactId>
              <type>zip</type>
              <target>/apps/my-app-packages/content/install.publish</target>
          </embedded>

          <!-- Include any other extra packages  -->
          <embedded>
              <groupId>com.vendor.x</groupId>
              <artifactId>vendor.plug-in.all</artifactId>
              <type>zip</type>
              <target>/apps/vendor-packages/container/install</target>
          </embedded>
      <embeddeds>
  </configuration>
</plugin>
...
```

### 容器封裝的篩選器定義 {#xml-container-package-filters}

在 `all` 项目的 `filter.xml` (`all/src/main/content/jcr_root/META-INF/vault/definition/filter.xml`) 中，**包括**&#x200B;要部署的任何包含子包的 `-packages` 文件夹：

```xml
<filter root="/apps/my-app-packages"/>
```

若為多個 `/apps/*-packages` 內嵌目標中使用，則所有專案都必須在這裡列舉。

### 第三方Maven存放庫 {#xml-3rd-party-maven-repositories}

>[!WARNING]
>
>由於會檢查其他Maven存放庫的相依性，因此新增更多Maven存放庫可能會延長Maven構建時間。

在Reactor專案的 `pom.xml`，新增任何必要的第三方公用Maven存放庫指示。 完整 `<repository>` 應該可以從第三方存放庫提供者取得設定。

```xml
<repositories>
  ...
  <repository>
      <id>3rd-party-repository</id>
      <name>Public 3rd Party Repository</name>
      <url>https://repo.3rdparty.example.com/...</url>
      <releases>
          <enabled>true</enabled>
          <updatePolicy>never</updatePolicy>
      </releases>
      <snapshots>
          <enabled>false</enabled>
      </snapshots>
  </repository>
  ...
</repositories>
```

### 套件之間的相依性 `ui.apps` 從 `ui.content` 套件 {#xml-package-dependencies}

在 `ui.content/pom.xml`，新增下列專案 `<dependencies>` 指令到 `filevault-package-maven-plugin` 外掛程式宣告。

```xml
...
<plugin>
  <groupId>org.apache.jackrabbit</groupId>
  <artifactId>filevault-package-maven-plugin</artifactId>
  <extensions>true</extensions>
  <configuration>
      ...
      <dependencies>
        <!-- Declare the content package dependency in the ui.content/pom.xml on the ui.apps project -->
        <dependency>
            <groupId${project.groupId}</groupId>
            <artifactId>my-app.ui.apps</artifactId>
            <version>${project.version}</version>
        </dependency>
      </dependencies>
    ...
  </configuration>
</plugin>
...
```

### 正在清除容器專案的目標資料夾 {#xml-clean-container-package}

在 `all/pom.xml` 新增 `maven-clean-plugin` 此外掛程式，會在Maven組建之前清除目標目錄。

```xml
<plugins>
  ...
  <plugin>
    <artifactId>maven-clean-plugin</artifactId>
    <executions>
      <execution>
        <id>auto-clean</id>
        <!-- Run at the beginning of the build rather than the default, which is after the build is done -->
        <phase>initialize</phase>
        <goals>
          <goal>clean</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
  ...
</plugins>
```

## 其他资源 {#additional-resources}

+ [使用Maven管理套件](/help/implementing/developing/tools/maven-plugin.md)
+ [FileVault Content Package Maven外掛程式](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
