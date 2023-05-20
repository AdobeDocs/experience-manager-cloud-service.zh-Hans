---
title: AEM 项目存储库结构包
description: Adobe Experience Manager as a Cloud Service Maven專案需要存放庫結構子套件定義，其唯一用途是定義專案的程式碼子套件部署到的JCR存放庫根目錄。
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 9%

---

# AEM 项目存储库结构包

Adobe Experience Manager as a Cloud Service的Maven專案需要存放庫結構子套件定義，其唯一目的是定義專案程式碼子套件部署到的JCR存放庫根目錄。 這可確保JCR資源相依性自動對Experience Manageras a Cloud Service的套件安裝排序。 缺少相依性可能會導致子結構安裝在其父結構之前，並因此意外被移除，中斷部署的情況。

如果您的代码包部署到代码包&#x200B;**未涵盖**&#x200B;的位置，则必须在存储库结构包中枚举任何上级资源（比较靠近 JCR 根的 JCR 资源），以建立这些依赖关系。

![存放庫結構套件](./assets/repository-structure-packages.png)

存放庫結構套件定義了的預期、常見狀態 `/apps` 套件驗證器使用哪個區域來判斷「不會發生潛在衝突」，因為這些區域是標準根。

要包含在存放庫結構封裝中的最典型路徑是：

+ `/apps` 是系統提供的節點
+ `/apps/cq/...`， `/apps/dam/...`， `/apps/wcm/...`、和 `/apps/sling/...` 提供下列專案的一般覆蓋圖： `/libs`.
+ `/apps/settings` 這是共用的內容感知設定根路徑

請注意，此子封裝 **沒有** 任何內容，且僅由 `pom.xml` 定義篩選根目錄。

## 建立存放庫結構套件

若要為您的Maven專案建立存放庫結構套件，請建立新的空Maven子專案，包含以下內容 `pom.xml`，更新專案中繼資料以符合您的父Maven專案。

更新 `<filters>` 以包含您部署程式碼套件的所有JCR存放庫路徑根。

確保將此新Maven子專案新增到父專案 `<modules>` 清單。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- ====================================================================== -->
    <!-- P A R E N T  P R O J E C T  D E S C R I P T I O N                      -->
    <!-- ====================================================================== -->
    <parent>
        <groupId>com.my-company</groupId>
        <artifactId>my-app</artifactId>
        <version>x.x.x</version>
        <relativePath>../pom.xml</relativePath>
    </parent>

    <!-- ====================================================================== -->
    <!-- P R O J E C T  D E S C R I P T I O N                                   -->
    <!-- ====================================================================== -->
    <artifactId>ui.apps.structure</artifactId>
    <packaging>content-package</packaging>
    <name>UI Apps Structure - Repository Structure Package for /apps</name>

    <description>
        Empty package that defines the structure of the Adobe Experience Manager repository the code packages in this project deploy into.
        Any roots in the code packages of this project should have their parent enumerated in the filters list below.
    </description>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.jackrabbit</groupId>
                <artifactId>filevault-package-maven-plugin</artifactId>
                <extensions>true</extensions>
                <properties>
                    <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package will be deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!--
                        Examples of complex roots


                        Overlays of /libs typically require defining the overlayed structure, at each level here.

                        For example, adding a new section to the main AEM Tools navigation, necessitates the following rules:

                        <filter><root>/apps/cq</root></filter>
                        <filter><root>/apps/cq/core</root></filter>
                        <filter><root>/apps/cq/core/content</root></filter>
                        <filter><root>/apps/cq/core/content/nav/</root></filter>
                        <filter><root>/apps/cq/core/content/nav/tools</root></filter>


                        Any /apps level Context-aware configurations need to enumerated here. 
                        
                        For example, providing email templates under `/apps/settings/notification-templates/com.day.cq.replication` necessitates the following rules:

                        <filter><root>/apps/settings</root></filter>
                        <filter><root>/apps/settings/notification-templates</root></filter>
                        <filter><root>/apps/settings/notification-templates/com.day.cq.replication</root></filter>
                        -->

                    </filters>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## 參考存放庫結構套件

若要使用存放庫結構套件，請透過所有程式碼套件（部署到的子套件）參照它 `/apps`) Maven專案（透過FileVault content package Maven外掛程式） `<repositoryStructurePackage>` 設定。

在 `ui.apps/pom.xml`，以及任何其他程式碼套件 `pom.xml`s，將專案的存放庫結構套件(#repository-structure-package)設定的參考新增到FileVault package Maven外掛程式。

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
</build>
<dependencies>
    <!-- Add the dependency for the repository structure package so it resolves -->
    <dependency>
        <groupId>${project.groupId}</groupId>
        <artifactId>ui.apps.structure</artifactId>
        <version>${project.version}</version>
        <type>zip</type>
    </dependency>
    ...
</dependencies>
```

## 多程式碼套件使用案例

較不常見且較複雜的使用案例是支援部署安裝在JCR存放庫相同區域中的多個程式碼套件。

例如：

+ 程式碼套件A部署至 `/apps/a`
+ 程式碼套件B部署至 `/apps/a/b`

如果程式碼套件A上的程式碼套件B未建立套件層級的相依性，程式碼套件B可能會先部署到 `/apps/a`，接著是程式碼套件B，部署至 `/apps/a`，因此會移除先前安裝的 `/apps/a/b`.

在此案例中：

+ 程式碼套件A應該定義 `<repositoryStructurePackage>` 在專案的存放庫結構套件(其中應具有篩選器 `/apps`)。
+ 程式碼套件B應該定義 `<repositoryStructurePackage>` 位於程式碼套件A上，因為程式碼套件B會部署至程式碼套件A共用的空間。

## 錯誤與偵錯

如果存放庫結構套件未正確設定，在Maven構建將報告錯誤：

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

這表示中斷程式碼套件沒有 `<repositoryStructurePackage>` 該清單 `/apps/some/path` 在其篩選清單中。

## 其他资源

+ [FileVault Content Package Maven外掛程式](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
