---
title: 如何在AEM Formsas a Cloud Service和本地开发环境中启用自适应Forms核心组件
description: 了解如何在AEM Formsas a Cloud Service上启用自适应Forms核心组件。
contentOwner: Khushwant Singh
docset: CloudService
role: Admin
exl-id: 32a574e2-faa9-4724-a833-1e4c584582cf
source-git-commit: defeee2fee42c6274c71438d6f9fde6e49a05081
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 86%

---

# 启用自适应Forms核心组件 {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html) |
| AEM as a Cloud Service | 本文 |

在AEM Formsas a Cloud Service上启用自适应Forms核心组件，允许您使用AEM FormsCloud Service实例在多个渠道中创建、发布和交付基于核心组件的自适应Forms和Headless Forms。 您需要具备启用了自适应表单核心组件的环境才能使用 Headless 自适应表单。

## 注意事项

* 创建全新的 AEM Forms as a Cloud Service 程序时，[即已为您的环境启用自适应表单核心组件和 Headless 自适应表单](#are-adaptive-forms-core-components-enabled-for-my-environment)。

* 如果您拥有的是其中[未启用](#enable-components)核心组件的旧版 Forms as a Cloud Service 程序，则您可[将自适应表单核心组件依赖项添加到](#enable-headless-adaptive-forms-for-an-aem-forms-as-a-cloud-service-environment)您的 AEM as a Cloud Service 存储库，并将该存储库部署到您的 Cloud Service 环境以启用 Headless 自适应表单。

* 如果您现有的Cloud Service环境提供了以下选项： [创建基于核心组件的自适应Forms](creating-adaptive-form-core-components.md)，已为您的环境启用了自适应Forms核心组件和Headless自适应Forms，您可以将基于核心组件的自适应Forms作为Headless表单提供给需要Headless表示自适应Forms的移动、Web、本机应用程序和服务等渠道。


## 启用自适应表单核心组件和 Headless 自适应表单 {#enable-headless-forms}

按列出的顺序执行以下步骤，以便为 AEM Forms as a Cloud Service 环境启用自适应表单核心组件和 Headless 自适应表单


![启用核心组件和Headless自适应表单](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## 1. 克隆您的 AEM Forms as a Cloud Service Git 存储库 {#clone-git-repository}

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


## 2. 将自适应表单核心组件依赖项添加到您的 Git 存储库 {#add-adaptive-forms-core-components-dependencies}

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

## 3. 构建并部署更新后的代码

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


## 常见问题解答 {#faq}

### 什么是核心组件？ {#core-components}

[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)是一组用于 AEM 的标准化 Web 内容管理 (WCM) 组件，以缩短您网站的开发时间并降低维护成本。

### 启用核心组件时将添加哪些功能？ {#core-components-capabilities}

为您的环境启用自适应表单核心组件时，将有一个空白的基于核心组件的自适应表单模板和 Canvas 3.0 主题添加到您的环境。为您的环境启用自适应表单核心组件后，您可以：

* [创建基于核心组件的自适应表单](/help/forms/creating-adaptive-form-core-components.md)。
* [创建基于核心组件的自适应表单模板](/help/forms/template-editor.md)。
* [为基于核心组件的自适应表单模板创建自定义主题](/help/forms/using-themes-in-core-components.md)。
* [可以将基于核心组件的自适应表单的 JSON 表示形式提供给需要表单的 Headless 表示形式的移动、Web、原生应用程序和服务等渠道](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html)。

### 我的环境是否启用了自适应表单核心组件？ {#enable-components}

要查看是否为您的环境启用了自适应表单核心组件，请执行以下操作：

1. [克隆您的 AEM Forms as a Cloud Service 存储库](#1-clone-your-aem-forms-as-a-cloud-service-git-repository)。

1. 打开您的 AEM Forms Cloud Service Git 存储库的 `[AEM Repository Folder]/all/pom.xml` 文件。

1. 搜索以下依赖项：

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![找到 all/pom.xml 中的 core-forms-components-af-core 工件](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   如果存在依赖项，则为您的环境启用了自适应表单核心组件。
