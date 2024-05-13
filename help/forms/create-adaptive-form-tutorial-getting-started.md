---
title: 自适应Forms快速入门。
description: 通过我们的分步教程了解如何创建移动响应式自适应表单。这些表单可以跨设备无缝适应，从而确保流畅体验。
keywords: 自适应Forms、响应式Forms、HTML5 Forms
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
hide: true
hidefromtoc: true
source-git-commit: e6c58c835798b16158ab4aca26e381ab8f36afd3
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 2%

---


# 创建自适应表单（核心组件） — 教程

在当今时代，用户希望在所有交互中都能获得移动友好的体验，表单也不例外。 自适应表单可以帮助您创建不仅便于移动使用的表单，还可以提高用户参与度并缩短完成表单所需的时间。

本教程提供了创建自适应表单的分步指南。 它分为一个用例和多个指南，每个指南都会教您如何向自适应表单添加新功能。

在本教程结束时，您将能够：

* 创建自适应表单及其数据模型
* 设置自适应表单的样式
* 使用自适应表单规则编辑器构建业务规则
* 预填自适应表单字段
* 将电子签名添加到表单
* 使用Google reCAPTCHA从机器人Protect您的表单
* 将您的自适应表单本地化为不同的语言
* 配置表单以生成结构化数据
* 设置表单以将数据提交到REST端点
* 发布您的自适应表单


## 为何要创建基于核心组件的表单？

AEM Forms提供基础组件和核心组件以创建表单体验。 核心组件是创建任何新表单体验的现代且推荐的方法。 为何使用核心组件？ 这些组件轻量级、开源（在github上提供）、提供出色的Google Lighthouse和Web重要分数、符合辅助功能要求，并提供AEM Sites的所有熟悉功能（如版本控制和本地化）。 此外，这些组件样式更易于设计，您可以根据组织的品牌指南轻松自定义其外观。 这些组件没有第三方依赖项，因此任何了解JavaScript和CSS的开发人员都可以轻松自定义这些组件。

![为何要创建基于核心组件的自适应Forms？ 这些组件轻便、易于打造、得分较高、支持辅助功能标准、易于自定义、开放源、可在github上使用、不依赖于第三方库，并且对于AEM开发人员和AEM作者几乎没有任何学习曲线。最重要的是，AEM Forms核心组件具有AEM WCM核心组件的所有功能。](/help/forms/assets/cc-core-components-benefits.png){width="50%"}

## 用例：通过自适应Forms简化家庭贷款资格预审

在本教程中，您将为大型银行构建一个自适应表单。 用例是：

潜在购房者访问银行的网站或分行以探索房屋贷款选项。 传统的应用程序流程冗长且难以承受，通常需要事先提供文档。 这让一些买家不愿开始这个过程，既妨碍了银行创造商机，也妨碍了买家自信地寻找自己梦想中的家园。

您需要开发交互式家庭贷款资格预审表。 该表格将收集基本信息，根据借款人的输入进行资格预审，提供预计贷款金额、潜在首期付款需求以及基于不同贷款类型的利率。 资格预审用户将能够直接从资格预审表中启动完全贷款申请。

将使用自适应表单构建表单。 这样可以提供个性化的体验，同时收集必要的财务数据，以准确进行家庭贷款资格预审。

完成本教程后，您的表单将类似于以下表单：

![在此处添加工作表单](/help/forms/assets/cc-tutorial-final-form.png)

## 设置开发环境

在将自适应表单部署到Cloud Service环境之前，您可以直接在本地计算机上构建和测试该表单。 Adobe为提供了用于本地开发的AEM SDK，允许您

* 在本地创建、自定义和测试表单。
* 在本地设计表单主题和构建配置，
* 轻松将完成的资产部署到云。

使用AEM SDK进行本地开发可节省您的时间并简化开发过程


**准备好开始了吗？**

1. [为AEM项目设置开发工具](/help/forms/setup-local-development-environment.md#set-up-development-tools-for-aem-projects)：下载并安装最新版本的 [Java 11™](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#local-development-environment-set-up)， [Git](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-git)， [Node.js (npm)](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#node-js)、和 [Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#install-maven). 另外，请安装纯文本编辑器，本教程中的示例基于Visual Studio Code。

1. [安装AEM SDK](/help/forms/setup-local-development-environment.md#set-up-local-experience-manager-environment-for-development)：下载并安装最新版本的AEM SDK。 这为AEM开发提供了重要的工具。 记下AEM SDK的版本。

   ![软件分发](/help/forms/assets/software-distribution.png)

   ![安装AEM SDK](/help/forms/assets/start-aem-sdk.png)

1. [添加AEM Forms加载项](/help/forms/setup-local-development-environment.md#add-forms-archive-to-local-author-and-publish-instances-and-configure-forms-specific-users)：从下载并安装与AEM SDK版本匹配的AEM Forms加载项 [Software Distribution](https://experience.adobe.com/#/downloads) 门户。
   ![install-aem-forms-add-on](/help/forms/assets/install-aem-forms-add-on.png)

   +++安装AEM Forms附加组件：

   要安装AEM Forms加载项，请执行以下操作：

   1. 停止AEM SDK。
   1. 将AEM Forms附加组件(.far)文件添加到 `AEM SDK/crx-quickstart/install` 文件夹，
   1. 重新启动AEM SDK。

+++

1. [配置用户权限](/help/forms/setup-local-development-environment.md#configure-users-and-permissions)：创建具有开发、创作和其他权限的用户，并将这些用户添加到预定义的表单组。


1. [添加自适应Forms模板](/help/forms/setup-local-development-environment.md#set-up-a-development-project-for-forms-based-on-experience-manager-archetype)：使用AEM Archetypes 48或更高版本创建一个新的AEM项目并将其部署到您的AEM SDK。 该项目会将自适应Forms模板添加到AEM SDK。

   ![自适应表单模板](/help/forms/assets/adaptive-forms-templates.png)

   +++将自适应Forms模板添加到AEM SDK：

   1. 运行以下命令以创建AEM项目。

      ```
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate -D archetypeGroupId=com.adobe.aem -D archetypeArtifactId=aem-project-archetype -D archetypeVersion="48" -D appTitle=securbank -D appId=securbank -D groupId=com.securbank -D includeFormsenrollment="y" -D aemVersion="cloud"
      ```

      ![AEM-Archetyoe-Project](/help/forms/assets/aem-archetype-project.png)

   1. 将项目部署到您的本地开发环境。 您可以使用以下命令部署到本地开发环境

      ```
      cd securbank
      
      mvn -PautoInstallPackage clean install
      ```

   部署AEM项目后，您可以在环境中查看自适应Forms模板。

+++


有关设置本地AEM Forms开发环境的详细说明和分步指南，请参阅 [为AEM Forms设置本地开发环境](/help/forms/setup-local-development-environment.md) 文章。



## 后续步骤

配置开发环境后，即可创建自适应表单。 在下一篇文章中，您将学习

* 从空白模板创建自适应表单
* 布局字段以显示和轻松接受信息。
* 预览表单。

<!-- 

### Step 2: Create Form Data Model

A form data model lets you connect an adaptive form to disparate data sources. For example, AEM user profile, RESTful web services, SOAP-based web services, OData services, and relational databases. You can use the form data model with an adaptive form to retrieve, update, delete, and add data to connected data sources.

Goals of article:

* Create the form data model using Rest endpoint.
* Add data model objects so you can form the data model.
* Configure read and write services for the form data model.
* Test form data model and configured services with test data.

### Step 4: Apply rules to adaptive form fields

AEM Forms provide an editor to write rules on adaptive form objects. These rules define actions to trigger on form objects based on preset conditions, user inputs, and user actions on the form. It helps ensure accuracy and speeds up the form-filling experience.

Goals:

* Create and apply rules to adaptive form fields.
* Use rules to trigger form data model services to update the data to database.

### Step 5: Style your adaptive form

Adaptive forms provide OOTB themes and allows you to customize an existing theme to make a brand specific theme. 


A theme contains styling details for components and panels, and you can reuse a theme in different forms. Styles include properties such as background colors, state colors, transparency, alignment, and size. When you apply the theme to your form, the specified style reflects on corresponding components of your form.

Goals:

* Apply an out of the box theme to an adaptive form.
* Create your brand specific theme.


### Step 6: Publish your adaptive form

You can publish adaptive forms as a stand-alone form (single page application), include in AEM Sites page, or include in a non-AEM Sites page.

Goals:

* Publish the adaptive form as an AEM Page.
* Embed the adaptive form in an AEM Sites Page.
* Embed the adaptive form in an external webpage (a non-AEM webpage hosted outside AEM).

-->