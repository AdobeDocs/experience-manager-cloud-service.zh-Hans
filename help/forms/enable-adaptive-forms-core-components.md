---
title: 在 AEM Forms as a Cloud Service 和开发环境上启用自适应表单核心组件
seo-title: Step-by-Step Guide for enabling Adaptive Forms Core Components on AEM Forms as a Cloud Service and local development environment
description: 通过我们的分步指南，了解如何在 AEM Forms as a Cloud Service 上启用自适应表单核心组件。我们的教程将引导您完成整个过程，使您可以轻松地为您的 AEM Forms 环境启用这一强大的功能。
seo-description: Learn how to enable Adaptive Forms Core Components on AEM Forms as a Cloud Service with our step-by-step guide. Our tutorial walks you through the process, making it easy to enable this powerful feature for your AEM Forms environment.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin
source-git-commit: f22554450d2eb1f4948f749ba00f78b568ee308f
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 100%

---


# 在 AEM Forms as a Cloud Service 和开发环境上启用自适应表单核心组件 {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

在 AEM Forms as a Cloud Service 上启用自适应表单核心组件后，您可以使用 AEM Forms Cloud Service 实例为多个渠道创建、发布和交付基于核心组件的自适应表单和 Headless Forms。您需要具备启用了自适应表单核心组件的环境才能使用 Headless 自适应表单。

## 注意事项

* 当您创建新的 AEM Forms as a Cloud Service 程序时，您的环境中便[已经启用了自适应表单核心组件和 Headless 自适应表单](#are-adaptive-forms-core-components-enabled-for-my-environment)。

* 如果您的 Forms as a Cloud Service 程序是旧版，并且其中[未启用](#enable-components)核心组件，您可以在 AEM as a Cloud Service 存储库中[添加自适应表单核心组件依赖项](#enable-headless-adaptive-forms-for-an-aem-forms-as-a-cloud-service-environment)，并将该存储库部署到 Cloud Service 环境，以启用 Headless 自适应表单。

* 如果您现有的 Cloud Service 环境提供[创建基于核心组件的自适应表单](creating-adaptive-form-core-components.md)的选项，则您的环境中已经启用了自适应表单核心组件和 Headless 自适应表单，您可以将基于核心组件的自适应表单作为 Headless Forms 提供给 Mobile、Web、本地应用程序以及需要 Headless 呈现自适应表单的服务等渠道。


## 启用自适应表单核心组件和 Headless 自适应表单 {#enable-headless-forms}

按列出的顺序执行以下步骤，为 AEM Forms as a Cloud Service 环境启用自适应表单核心组件和 Headless 自适应表单


![](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## 1. 克隆 AEM Forms as a Cloud Service Git 存储库 {#clone-git-repository}

1. 登录到 [Cloud Manager](https://my.cloudmanager.adobe.com/) 并选择您的组织和计划。

1. 从&#x200B;**程序概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;信息卡，点击&#x200B;**访问存储库信息**&#x200B;按钮，该按钮可用于访问和管理您的 Git 存储库。该页面包括以下信息：

   * Cloud Manager Git 存储库的 URL。
   * Git 存储库的凭据（用户名和密码）Git 用户名。

   点击&#x200B;**生成密码**&#x200B;查看或生成密码。

1. 在本地计算机上打开终端或命令提示符并运行以下命令：

   ```Shell
   git clone [Git Repository URL]
   ```

   出现提示时，提供凭据。存储库已克隆到您的本地计算机。


## 2. 将自适应表单核心组件依赖项添加到您的 Git 存储库 {#add-adaptive-forms-core-components-dependencies}

1. 在纯文本代码编辑器中打开 Git 存储库文件夹。例如，VS 代码。
1. 打开要编辑的`[AEM Repository Folder]\pom.xml`文件。
1. 将 `core.forms.components.version`、`core.forms.components.af.version` 和 `core.wcm.components.version` 组件的版本替换为[核心组件文档](https://github.com/adobe/aem-core-forms-components)中指定的版本。如果该组件不存在，请添加这些组件。

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.wcm.components.version>2.22.10</core.wcm.components.version>
       <core.forms.components.version>2.0.18</core.forms.components.version>
       <core.forms.components.af.version>2.0.18</core.forms.components.af.version>
   </properties>
   ```

   ![提及最新版本的 Forms 核心组件](/help/forms/assets/latest-forms-component-version.png)

1. 在`[AEM Repository Folder]\pom.xml`文件的依赖项部分，添加以下依赖项，并保存文件。

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

1. 打开要编辑的`[AEM Repository Folder]/all/pom.xml`文件。在`<embeddeds>`部分添加以下依赖项，并保存文件。

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
   >  要查找您的 `${appId}`，请在 `[AEM Repository Folder]/all/pom.xml` 文件中，搜索 `-packages/application/install`术语。`-packages/application/install` 术语之前的文本是您的 `${appId}`。例如，下列代码 `myheadlessform` 是 `${appId}`。
   >
   >   
   ```
   >             <embedded>
   >                     <groupId>com.myheadlessform</groupId>
   >                     <artifactId>myheadlessform.ui.apps<artifactId>
   >                     <type>zip</type>
   >                   <target>/apps/myheadlessform-packages/application install</target>
   >             </embedded>
   >   ```

1. 在 `[AEM Repository Folder]/all/pom.xml` 文件的 `<dependencies>` 部分，添加以下依赖项并保存文件：

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

1. 打开要编辑的 `[AEM Repository Folder]/ui.apps/pom.xml`。添加 `af-core bundle` 依赖项，并保存文件。

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


1. 保存并关闭文件。

## 3. 构建并部署更新后的代码

将更新后的代码部署到您的本地开发和 Cloud Service 环境，以在这两个环境中启用核心组件：

* [在本地开发环境中构建和部署更新的代码 (AEM as a Cloud Service SDK)](#core-components-on-aem-forms-local-sdk)

* [在 AEM Forms as a Cloud Service 环境中构建和部署更新的代码](#core-components-on-aem-forms-cs)

### 在本地开发环境中构建和部署更新的代码 {#core-components-on-aem-forms-local-sdk}

1. 打开命令提示符或终端。

1. 导航到 Git 存储库项目的根目录。

1. 通过运行以下命令为您的环境构建程序包：

   ```Shell
       mvn clean install
   ```



   程序包构建成功后，您可以在 [Git Repository Folder]\all\target\[appid].all-[version].zip 中找到它

1. 使用[程序包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en)在本地开发环境上部署 [AEM Archetype Project Folder]\all\target\[appid].all-[version].zip 程序包。


### 在 AEM Forms as a Cloud Service 环境中构建和部署更新的代码 {#core-components-on-aem-forms-cs}

1. 打开命令提示符或终端。
1. 导航到您的 `[AEM Repository Folder]`，并按列出的顺序运行以下命令

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. 文件提交到 Git 存储库后，[运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html)。

   管道运行成功后，对应的环境便会启用自适应表单核心组件。此外，自适应表单（核心组件）模板和 Canvas 3.0 主题会添加到您的 Forms as a Cloud Service 环境中，为您提供自定义和创建基于核心组件的自适应表单的选项。


## 常见问题解答 {#faq}

### 什么是核心组件？ {#core-components}

[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)是一组用于 AEM 的标准化网站内容管理 (WCM) 组件，可加快开发速度并降低网站的维护成本。

### 启用核心组件时会添加哪些功能？ {#core-components-capabilities}

当为您的环境启用自适应表单核心组件时，您的环境中会加入一个空白的基于核心组件的自适应表单模板和 Canvas 3.0 主题。为您的环境启用自适应表单核心组件后，您可以：

* [创建基于核心组件的自适应表单](/help/forms/creating-adaptive-form-core-components.md)。
* [创建基于核心组件的自适应表单模板](/help/forms/template-editor.md)。
* [为基于核心组件的自适应表单模板创建自定义主题。](/help/forms/using-themes-in-core-components.md)
* [为 Mobile、Web、本机应用程序和需要表单 Headless 呈现的服务等渠道提供基于核心组件的自适应表单的 JSON 呈现。](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)

### 我的环境是否启用了自适应表单核心组件？ {#enable-components}

若要查看您的环境是否启用了自适应表单核心组件：

1. [克隆 AEM Forms as a Cloud Service 存储库。](#1-clone-your-aem-forms-as-a-cloud-service-git-repository)

1. 打开您的 AEM Forms Cloud Service Git 存储库的 `[AEM Repository Folder]/all/pom.xml` 文件。

1. 搜索以下依赖项：

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![找到 core-forms-components-af-core artifact in all/pom.xml](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   如果存在依赖项，则您的环境启用了自适应表单核心组件。

