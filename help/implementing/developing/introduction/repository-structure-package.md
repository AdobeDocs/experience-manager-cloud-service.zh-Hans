---
title: AEM 项目存储库结构包
description: Adobe Experience Manager as a Cloud Service上的Maven项目需要存储库结构子包定义，其唯一用途是定义项目的代码子包部署到其中的JCR存储库根。
exl-id: dec08410-d109-493d-bf9d-90e5556d18f0
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 520ab0229b4f00a1de981209bf26059b0d00c3da
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 2%

---

# AEM 项目存储库结构包

Adobe Experience Manager as a Cloud Service的Maven项目需要存储库结构子包定义，其唯一用途是定义项目的代码子包部署到其中的JCR存储库根。 此方法确保按照JCR资源依赖关系对Experience Manageras a Cloud Service中包的安装自动排序。 缺少依赖项可能会导致出现以下情况：子结构将安装在父结构之前，因此被意外移除，从而破坏部署。

如果您的代码包部署到代码包未涵盖&#x200B;**的位置**，则必须在存储库结构包中枚举任何上级资源（靠近JCR根的JCR资源）。 建立这些依赖关系需要此过程。

![存储库结构包](./assets/repository-structure-packages.png)

存储库结构包定义了`/apps`的预期共同状态，包验证器将使用该状态来确定作为标准根的区域“免受潜在冲突的影响”。

要包含在存储库结构包中的最典型路径包括：

+ `/apps`是系统提供的节点
+ `/apps/cq/...`、`/apps/dam/...`、`/apps/wcm/...`和`/apps/sling/...`为`/libs`提供公共覆盖。
+ `/apps/settings`，共享上下文感知配置根路径

此子包&#x200B;**没有**&#x200B;任何内容，并且仅由定义过滤器根的`pom.xml`组成。

## 创建存储库结构包

要为Maven项目创建存储库结构包，请使用以下`pom.xml`创建一个空的Maven子项目，更新项目元数据以符合父Maven项目。

更新`<filters>`以包含您的代码包部署到的所有JCR存储库路径。

确保将此新的Maven子项目添加到父项目`<modules>`列表。

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
                    <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
                    <cloudManagerTarget>none</cloudManagerTarget>
                </properties>
                <configuration>
                    <properties>
                        <!-- Set Cloud Manager Target to none, else this package is deployed and remove all defined filter roots -->
                        <cloudManagerTarget>none</cloudManagerTarget>
                    </properties>
                    <filters>

                        <!-- /apps root -->
                        <filter><root>/apps</root></filter>

                        <!--
                        Examples of complex roots


                        Overlays of /libs typically require defining the overlay structure, at each level here.

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

要使用存储库结构包，请通过FileVault内容包Maven插件`<repositoryStructurePackage>`配置通过所有代码包（部署到`/apps`的子包）引用Maven项目。

在`ui.apps/pom.xml`和任何其他代码包`pom.xml`中，将对该项目的存储库结构包(#repository-structure-package)配置的引用添加到FileVault包Maven插件中。

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

不太常见、但更复杂的用例支持部署多个代码包，这些代码包安装在JCR存储库的相同区域中。

例如：

+ 代码包A部署到`/apps/a`中
+ 代码包B部署到`/apps/a/b`

如果未从代码包A上的代码包B建立包级别依赖关系，则代码包B可能首先部署到`/apps/a`中。 如果随后是部署到`/apps/a`中的代码包A ，则结果为删除以前安装的`/apps/a/b`。

在本例中：

+ 代码包A应在项目的存储库结构包中定义一个`<repositoryStructurePackage>`（它应具有`/apps`的筛选器）。
+ 代码包B应在代码包A上定义`<repositoryStructurePackage>`，因为代码包B部署到代码包A共享的空间中。

## 错误和调试

如果存储库结构包未正确设置，则会在Maven中报告错误：

```
1 error(s) detected during dependency analysis.
Filter root's ancestor '/apps/some/path' is not covered by any of the specified dependencies.
```

此错误表示中断代码包在其筛选器列表中没有列出`/apps/some/path`的`<repositoryStructurePackage>`。

## 其他资源

+ [FileVault Content Package Maven插件](https://jackrabbit.apache.org/filevault-package-maven-plugin/)
