---
title: 在AEM Forms as a Cloud Service上检查并启用自适应Forms核心组件
description: 了解如何检查是否已启用自适应Forms核心组件，以及如何根据需要在AEM Forms as a Cloud Service上启用它们。
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
exl-id: 32a574e2-faa9-4724-a833-1e4c584582cf
hide: true
hidefromtoc: true
source-git-commit: 3c1931d67e69d155e777c8761fe2bbbd21461ddf
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 54%

---

# 检查和启用自适应Forms核心组件 {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html) |
| AEM as a Cloud Service | 本文 |

已针对大多数Forms as a Cloud Service客户启用了自适应AEM Forms核心组件和Headless自适应Forms 。 这使您能够使用AEM Forms Cloud Service实例创建、发布基于核心组件的自适应Forms和Headless Forms，并将其交付到多个渠道。

## 检查是否已启用自适应Forms核心组件 {#check-if-enabled}

在执行以下任何启用步骤之前，请检查是否已为您的环境启用了自适应Forms核心组件：

### 对于新的AEM Forms as a Cloud Service程序

当您创建新的AEM Forms as a Cloud Service项目时，已针对您的环境启用了自适应Forms核心组件和Headless自适应Forms。

### 对于现有Cloud Service环境

如果您现有的Cloud Service环境提供了[创建基于核心组件的自适应Forms](creating-adaptive-form-core-components.md)的选项，则您的环境已启用了自适应Forms核心组件和Headless自适应Forms。

### 通过检查存储库进行验证

要确认已为您的环境启用自适应Forms核心组件，请执行以下操作：

1. 克隆AEM Forms as a Cloud Service存储库。

1. 打开您的 AEM Forms Cloud Service Git 存储库的 `[AEM Repository Folder]/all/pom.xml` 文件。

1. 搜索以下依赖项：

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![找到 all/pom.xml 中的 core-forms-components-af-core 工件](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   如果存在这些依赖项，则为您的环境启用自适应Forms核心组件。

## 需要手动启用时 {#when-manual-enablement-needed}

仅当您的旧版Forms as a Cloud Service程序未启用核心组件（由上面的检查确认）时，您才需要手动将Adaptive Forms核心组件依赖项添加到AEM as a Cloud Service存储库，并将存储库部署到Cloud Service环境。

+++ 手动启用步骤 

>[!WARNING]
>
>如果上述验证检查确认没有为您的环境启用自适应Forms核心组件，请仅执行以下步骤。

按照列出的顺序，执行以下步骤，为AEM Forms as a Cloud Service环境启用自适应Forms核心组件和Headless自适应Forms：

![启用核心组件和Headless自适应表单](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## &#x200B;1. 克隆您的 AEM Forms as a Cloud Service Git 存储库 {#clone-git-repository}

1. 登录到 [Cloud Manager](https://my.cloudmanager.adobe.com/) 并选择您的组织和计划。

1. 从您的&#x200B;**程序概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;卡片，单击&#x200B;**访问存储库信息**&#x200B;按钮以访问和管理您的 Git 存储库。该页面包括以下信息：

   * Cloud Manager Git 存储库的 URL。
   * Git 存储库的凭据（用户名和密码）Git 用户名。

   单击&#x200B;**生成密码**&#x200B;以查看或生成密码。

1. 在本地计算机上打开终端或命令提示符并运行以下命令：

   ```Shell
   git clone [Git Repository URL]
   ```

   出现提示时，提供凭据。随后将该存储库克隆到您的本地计算机。


## &#x200B;2. 将自适应表单核心组件依赖项添加到您的 Git 存储库 {#add-adaptive-forms-core-components-dependencies}

1. 在纯文本代码编辑器中打开您的 Git 存储库文件夹。例如 VS Code。
1. 打开 `[AEM Repository Folder]\pom.xml` 文件以供编辑。
1. 将 `core.forms.components.version`、`core.forms.components.af.version` 和 `core.wcm.components.version` 组件的版本替换为[核心组件文档](https://github.com/adobe/aem-core-forms-components)中指定的版本。如果不存在，请添加这些组件。

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.wcm.components.version>2.22.10</core.wcm.components.version>
       <core.forms.components.version>2.0.18</core.forms.components.version>
       <core.forms.components.af.version>2.0.18</core.forms.components.af.version>
   </properties>
   ```

   ![提及最新版本的 Forms 核心组件](/help/forms/assets/latest-forms-component-version.png)

1. 在 `[AEM Repository Folder]\pom.xml` 文件的依赖项部分中添加以下依赖项，然后保存该文件。

   ```XML
       <!-- WCM Core Component Examples Dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
               <version>${core.wcm.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <version>${core.wcm.components.version}</version>
               <type>zip</type>
           </dependency>    
           <!-- End of WCM Core Component Examples Dependencies -->
           <!-- Forms Core Component Dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-core</artifactId>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <version>${core.forms.components.version}</version>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
               <version>${core.forms.components.version}</version>
           </dependency>
   <!-- End of AEM Forms Core Component Dependencies -->
   ```

1. 打开 `[AEM Repository Folder]/all/pom.xml` 文件以供编辑。在 `<embeddeds>` 部分中添加以下依赖项，然后保存该文件。

   ```XML
   <!-- WCM Core Component Examples Dependencies -->
   
   <!-- inside plugin config of filevault-package-maven-plugin -->  
   <!-- embed wcm core components examples artifacts -->
   
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.cq</groupId>
       <artifactId>core.wcm.components.examples.ui.config</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <!-- embed forms core components artifacts -->
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       <target>/apps/${appId}-vendor-packages/application/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-apps</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   <embedded>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-examples-content</artifactId>
       <type>zip</type>
       <target>/apps/${appId}-vendor-packages/content/install</target>
   </embedded>
   ```

   >[!NOTE]
   >
   >
   >  将 `${appId}` 替换为您的 appId。
   >
   >  要查找您的 `${appId}`，请在 `[AEM Repository Folder]/all/pom.xml` 文件中搜索 `-packages/application/install` 一词。在 `-packages/application/install` 一词之前的文本就是您的 `${appId}`。例如，下列代码 `myheadlessform` 是 `${appId}`。
   >
   >   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. 在 `[AEM Repository Folder]/all/pom.xml` 文件的 `<dependencies>` 部分中添加以下依赖项，然后保存该文件：

   ```XML
           <!-- Other existing dependencies -->
           <!-- wcm core components examples dependencies -->
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.config</artifactId>
               <type>zip</type>
               </dependency>
           <dependency>
               <groupId>com.adobe.cq</groupId>
               <artifactId>core.wcm.components.examples.ui.content</artifactId>
               <type>zip</type>
           </dependency>
               <!-- forms core components dependencies -->
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-af-apps</artifactId>
               <type>zip</type>
           </dependency>
           <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-apps</artifactId>
               <type>zip</type>
           </dependency>
               <dependency>
               <groupId>com.adobe.aem</groupId>
               <artifactId>core-forms-components-examples-content</artifactId>
               <type>zip</type>
           </dependency>
   ```

1. 打开 `[AEM Repository Folder]/ui.apps/pom.xml` 以供编辑。添加 `af-core bundle` 依赖项，然后保存该文件。

   ```XML
       <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   >
   >确保您的项目中不包含以下自适应表单核心组件工件。
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-apps</artifactId>`
   >
   > `</dependency>`
   >
   > 和
   >
   > `<dependency>`
   >
   >   `<groupId>com.adobe.aem</groupId>`
   >   `<artifactId>core-forms-components-core</artifactId>`
   >
   > `</dependency>`


1. 保存并关闭该文件。

## &#x200B;3. 构建并部署更新后的代码

将更新后的代码部署到您的本地开发环境和 Cloud Service 环境，以便在这两个环境上启用核心组件：

* [构建更新后的代码并将其部署在本地开发环境 (AEM as a Cloud Service SDK) 上](#core-components-on-aem-forms-local-sdk)

* [构建更新后的代码并将其部署在 AEM Forms as a Cloud Service 环境上](#core-components-on-aem-forms-cs)

### 构建更新后的代码并将其部署在本地开发环境上 {#core-components-on-aem-forms-local-sdk}

1. 打开命令提示符或终端。

1. 导航到您的 Git 存储库项目的根目录。

1. 运行以下命令以构建适合您环境的包：

   ```Shell
       mvn clean install
   ```



   成功构建该包后，可在 [Git Repository Folder]\all\target\[appid].all-[version].zip 中找到它

1. 使用[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en)将 [AEM Archetype Project Folder]\all\target\[appid].all-[version].zip 包部署在本地开发环境上。


### 构建更新后的代码并将其部署在 AEM Forms as a Cloud Service 环境上 {#core-components-on-aem-forms-cs}

1. 打开终端或命令提示符。
1. 导航到您的 `[AEM Repository Folder]`，并按列出的顺序运行以下命令

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. 将文件提交到 Git 存储库后，[运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)。

   成功运行管道后，即为相应的环境启用自适应表单核心组件。此外，还将自适应表单（核心组件）模板和 Canvas 3.0 主题添加到您的 Forms as a Cloud Service 环境，并为您提供自定义和创建基于核心组件的自适应表单的选项。

+++

## 常见问题解答 {#faq}

### 什么是核心组件？ {#core-components}

[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)是一组用于 AEM 的标准化 Web 内容管理 (WCM) 组件，以缩短您网站的开发时间并降低维护成本。

### 启用核心组件时将添加哪些功能？ {#core-components-capabilities}

为您的环境启用自适应表单核心组件时，将有一个空白的基于核心组件的自适应表单模板和 Canvas 3.0 主题添加到您的环境。为您的环境启用自适应表单核心组件后，您可以：

* [创建基于核心组件的自适应表单](/help/forms/creating-adaptive-form-core-components.md)。
* [创建基于核心组件的自适应表单模板](/help/forms/template-editor.md)。
* [为基于核心组件的自适应表单模板创建自定义主题](/help/forms/using-themes-in-core-components.md)。
* [可以将基于核心组件的自适应表单的 JSON 表示形式提供给需要表单的 Headless 表示形式的移动、Web、原生应用程序和服务等渠道](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)。

### 如何知道是否需要手动启用自适应Forms核心组件？ {#manual-enablement-needed-faq}

大多数客户已经启用了自适应Forms核心组件。 在以下情况下，您只需手动启用它们：

1. 在自动包含核心组件之前，您已创建了一个较早的Forms as a Cloud Service程序
1. [检查自适应Forms核心组件是否已启用](#check-if-enabled)部分中的验证检查，确认存储库中缺少所需的依赖项

如果不确定，请按照上面[检查自适应Forms核心组件是否已启用](#check-if-enabled)部分中的验证步骤操作。

### 为什么基于核心组件的表单无法在项目中呈现？

由于Forms核心组件包与项目原型中包含的版本不匹配，基于核心组件的表单可能无法呈现。 当项目原型中指定的版本等于或高于与Forms核心组件包捆绑的版本时，通常会发生此问题。 要解决此问题，请执行以下操作之一：

* 在项目原型中使用较低版本的Forms核心组件包。
* 从项目原型中删除Forms核心组件依赖项，因为AEM as a Cloud Service中已包含所需版本。 Forms核心组件包与从版本20133开始的AEM as a Cloud SDK捆绑在一起，例如`AEM SDK v2025.3.20133.20250325T063357Z-250300`。

>[!MORELIKETHIS]
>
>* [创建自适应表单](/help/forms/creating-adaptive-form-core-components.md)
