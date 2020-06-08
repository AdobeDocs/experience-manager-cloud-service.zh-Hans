---
title: 'AEM 项目存储库结构包  '
description: Adobe Experience Manager作为云服务Maven项目需要存储库结构子包定义，其唯一用途是定义JCR存储库根，项目的代码子包从中部署。
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 9%

---


# AEM 项目存储库结构包

将Adobe Experience Manager作为云服务的现有项目需要一个存储库结构子包定义，其唯一目的是定义JCR存储库根，项目的代码子包将部署到该JCR存储库根。 这可确保在Experience Manager中以云服务的形式安装包时，JCR资源依赖项会自动进行排序。 缺少依赖关系可能会导致子结构安装在其父结构之前，因此意外删除，从而中断部署。

如果您的代码包部署到代码包&#x200B;**未涵盖**&#x200B;的位置，则必须在存储库结构包中枚举任何上级资源（比较靠近 JCR 根的 JCR 资源），以建立这些依赖关系。

![存储库结构包](./assets/repository-structure-packages.png)

存储库结构包定义预期的公共状态，包验证 `/apps` 程序使用该状态确定区域“不受潜在冲突的影响”，因为它们是标准根。

存储库结构包中包含的最典型路径为：

+ `/apps` 是系统提供的节点
+ `/apps/cq/...`、 `/apps/dam/...`、 `/apps/wcm/...`和， `/apps/sling/...` 它们为提供通用叠加 `/libs`。
+ `/apps/settings` 共享的上下文感知配置根路径

请注意，此子包 **没有任何内** 容，仅由定义过滤 `pom.xml` 器根的一个组成。

## 创建存储库结构包

要为Maven项目创建存储库结构包，请新建一个空的Maven子项目，并使用以下项 `pom.xml`目更新项目元数据以符合您的父Maven项目。

更新该 `<filters>` 更新，以包含您的代码包部署到的所有JCR存储库路径根。

确保将此新的Maven子项目添加到父项目 `<modules>` 列表。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
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

## 引用存储库结构包

要使用存储库结构包，请通过FileVault内容包Maven插件配置通过所有代码包（部署到的子包） `/apps`引用它来管理项 `<repositoryStructurePackage>` 目。

在和 `ui.apps/pom.xml`任何其他代码包 `pom.xml`中，将对项目的存储库结构包(#repository-structure-package)配置的引用添加到FileVault包Maven插件。

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

## 多代码包用例

一个不太常见、更复杂的用例支持部署安装在JCR存储库相同区域的多个代码包。

例如：

+ 代码包A部署到 `/apps/a`
+ 代码包B部署到 `/apps/a/b`

如果未从代码包A上的代码包B建立包级依赖关系，则代码包B可先部署到 `/apps/a`，然后部署到代码包B中， `/apps/a`从而删除先前安装的 `/apps/a/b`。

在本例中：

+ 代码包A应在项 `<repositoryStructurePackage>` 目的存储库结构包上定义一个(它应具有筛选器 `/apps`)。
+ 代码包B应在代码 `<repositoryStructurePackage>` 包A上定义一个，因为代码包B部署到由代码包A共享的空间中。

## 错误和调试

如果存储库结构包设置不正确，在Maven内部版本时将报告错误：

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

这表示中断代码包的筛选器 `<repositoryStructurePackage>` 列表中没 `/apps/some/path` 有列表。

## 其他资源

+ [FileVault内容包Maven插件](http://jackrabbit.apache.org/filevault-package-maven-plugin/)
