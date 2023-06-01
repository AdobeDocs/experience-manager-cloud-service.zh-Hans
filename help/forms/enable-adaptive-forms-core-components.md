---
title: 在AEM Formsas a Cloud Service和本地开发环境中启用自适应Forms核心组件
seo-title: Step-by-Step Guide for enabling Adaptive Forms Core Components on AEM Forms as a Cloud Service and local development environment
description: 了解如何使用我们的分步指南在AEM Formsas a Cloud Service上启用自适应Forms核心组件。 我们的教程将指导您完成该过程，以便您轻松为AEM Forms环境启用此强大功能。
seo-description: Learn how to enable Adaptive Forms Core Components on AEM Forms as a Cloud Service with our step-by-step guide. Our tutorial walks you through the process, making it easy to enable this powerful feature for your AEM Forms environment.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin
hide: true
hidefromtoc: true
source-git-commit: 7dc36220c1f12177037aaa79d864c1ec2209a301
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 3%

---


# 在AEM Formsas a Cloud Service和本地开发环境中启用自适应Forms核心组件 {#enable-headless-adaptive-forms-on-aem-forms-cloud-service}

在AEM Formsas a Cloud Service上启用自适应Forms核心组件，允许您使用AEM FormsCloud Service实例向多个渠道开始创建、发布和交付基于核心组件的自适应Forms和Headless Forms。 您需要启用自适应Forms核心组件的环境才能使用Headless自适应Forms。

## 注意事项

* 当您创建全新AEM Formsas a Cloud Service程序时， [已为您的环境启用了自适应Forms核心组件和Headless自适应Forms](#are-adaptive-forms-core-components-enabled-for-my-environment).

* 如果您有一个旧版的Formsas a Cloud Service程序，其核心组件是 [未启用](#enable-components)，您可以 [添加Adaptive Forms核心组件依赖项](#enable-headless-adaptive-forms-for-an-aem-forms-as-a-cloud-service-environment) 到AEMas a Cloud Service存储库，并将存储库部署到Cloud Service环境，以启用Headless自适应Forms。

* 如果您现有的Cloud Service环境提供了 [创建基于核心组件的自适应Forms](creating-adaptive-form-core-components.md)，您的环境已启用了自适应Forms核心组件和Headless自适应Forms，您可以将基于核心组件的自适应Forms作为Headless表单提供给需要自适应Forms的Headless呈现的移动设备、Web、本机应用程序和服务等渠道。


## 启用自适应Forms核心组件和Headless自适应Forms {#enable-headless-forms}

按照列出的顺序，执行以下步骤，为AEM Formsas a Cloud Service环境启用自适应Forms核心组件和Headless自适应Forms


![](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service.png)


## 1.克隆AEM Formsas a Cloud Service的Git存储库 {#clone-git-repository}

1. 登录 [Cloud Manager](https://my.cloudmanager.adobe.com/) 并选择您的组织和项目。

1. 导航到 **管道** 来自您的的 **计划概述** 页面上，单击 **访问存储库信息** 按钮来访问和管理Git存储库。 该页面包含以下信息：

   * Cloud Manager Git存储库的URL。
   * Git存储库的凭据（用户名和密码） Git用户名。

   单击 **生成密码** 查看或生成密码。

1. 在本地计算机上打开终端或命令提示符并运行以下命令：

   ```Shell
   git clone [Git Repository URL]
   ```

   出现提示时，提供凭据。 存储库已克隆到您的本地计算机。


## 2.将自适应Forms核心组件依赖项添加到您的Git存储库 {#add-adaptive-forms-core-components-dependencies}

1. 在纯文本代码编辑器中打开Git存储库文件夹。 例如，VS代码。
1. 打开 `[AEM Repository Folder]\pom.xml` 要编辑的文件。
1. 替换的版本 `core.forms.components.version`， `core.forms.components.af.version` 和 `core.wcm.components.version` 版本中指定的组件 [核心组件文档](https://github.com/adobe/aem-core-forms-components). 如果组件不存在，请添加这些组件。

   ```XML
   <!-- Replace the version with the latest released version at https://github.com/adobe/aem-core-forms-components/tags -->
   
   <properties>
       <core.forms.components.version>2.0.14</core.formscomponents.version>
       <core.forms.components.af.version>2.0.14</core.forms.components.af.version>  
       <core.wcm.components.version>2.21.2</core.wcmcomponents.version>
   </properties>
   ```

   ![提及最新版本的Forms核心组件](/help/forms/assets/latest-forms-component-version.png)

1. 在的依赖关系部分 `[AEM Repository Folder]\pom.xml` 文件，添加以下依赖关系并保存文件。

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

1. 打开 `[AEM Repository Folder]/all/pom.xml` 要编辑的文件。 将以下依赖关系添加到 `<embeddeds>` 并保存文件。

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
   >  Replace `${appId}` 使用您的appId。
   >
   >  查找您的 `${appId}`，在 `[AEM Repository Folder]/all/pom.xml` 文件，搜索 `-packages/application/install` 术语。 之前的文本 `-packages/application/install` 术语是您的 `${appId}`. 例如，以下代码， `myheadlessform` 是 `${appId}`.
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

1. 在 `<dependencies>` 部分 `[AEM Repository Folder]/all/pom.xml` 文件，添加以下依赖关系并保存文件：

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

1. 打开 `[AEM Repository Folder]/ui.apps/pom.xml` 进行编辑。 添加 `af-core bundle` 依赖关系，并保存文件。

   ```XML
       <dependency>
       <groupId>com.adobe.aem</groupId>
       <artifactId>core-forms-components-af-core</artifactId>
       </dependency>
   ```

   >[!NOTE]
   >
   >确保您的项目中不包含以下自适应Forms核心组件工件。
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

## 3.生成并部署更新的代码

将更新后的代码部署到本地开发和Cloud Service环境，以在这两个环境中启用核心组件：

* [在本地开发环境中生成和部署更新的代码(AEMas a Cloud ServiceSDK)](#core-components-on-aem-forms-local-sdk)

* [在AEM Formsas a Cloud Service环境中生成和部署更新的代码](#core-components-on-aem-forms-cs)

### 在本地开发环境中生成和部署更新的代码 {#core-components-on-aem-forms-local-sdk}

1. 打开命令提示符或终端。

1. 导航到Git存储库项目的根目录。

1. 运行以下命令为您的环境构建包：

   ```Shell
       mvn clean install
   ```



   成功构建包后，您可以在以下位置找到它： [Git存储库文件夹]\all\target\[appid].all-[version].zip

1. 使用 [包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hans) 以部署 [AEM原型项目文件夹]\all\target\[appid].all-[version].zip包。


### 在AEM Formsas a Cloud Service环境中生成和部署更新的代码 {#core-components-on-aem-forms-cs}

1. 打开终端或命令提示符。
1. 导航到 `[AEM Repository Folder]` 并按列出的顺序运行以下命令

   ```Shell
    git add pom.xml
    git add all/pom.xml
    git add ui.apps/pom.xml
    git commit -m "Added dependencies for Adaptive Forms Core Components"
    git push origin
   ```

1. 将文件提交到Git存储库后， [运行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

   管道运行成功后，将为相应的环境启用自适应Forms核心组件。 此外，还向Formsas a Cloud Service环境添加了自适应Forms（核心组件）模板和Canvas 3.0主题，为您提供了基于核心组件的自适应Forms的自定义和创建选项。


## 常见问题解答 {#faq}

### 核心组件是什么？ {#core-components}

此 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 是一组适用于AEM的标准化Web内容管理(WCM)组件，可加快开发速度并降低网站的维护成本。

### 在启用核心组件上添加了哪些功能？ {#core-components-capabilities}

在您的环境中启用自适应Forms核心组件后，会向环境中添加一个基于空白核心组件的自适应表单模板和画布3.0主题。 为您的环境启用自适应Forms核心组件后，您可以：

* [创建基于核心组件的自适应Forms](/help/forms/creating-adaptive-form-core-components.md).
* [创建基于核心组件的自适应表单模板](/help/forms/template-editor.md).
* [为基于核心组件的自适应表单模板创建自定义主题](/help/forms/using-themes-in-core-components.md).
* [为移动设备、Web、本机应用程序等需要表单Headless表示的渠道和服务提供基于核心组件的自适应表单的JSON表示](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html).

### 是否为我的环境启用了自适应Forms核心组件？ {#enable-components}

要检查是否为您的环境启用了自适应Forms核心组件，请执行以下操作：

1. [克隆AEM Formsas a Cloud Service存储库](#1-clone-your-aem-forms-as-a-cloud-service-git-repository).

1. 打开 `[AEM Repository Folder]/all/pom.xml` AEM FormsCloud ServiceGit存储库的文件。

1. 搜索以下依赖项：

   * core-forms-components-af-core
   * core-forms-components-core
   * core-forms-components-apps
   * core-forms-components-af-apps
   * core-forms-components-examples-apps
   * core-forms-components-examples-content

   ![在all/pom.xml中找到core-forms-components-af-core构件](/help/forms/assets/enable-headless-adaptive-forms-on-aem-forms-cloud-service-locate-core-af-artifact.png)

   如果存在依赖关系，则为您的环境启用自适应Forms核心组件。

