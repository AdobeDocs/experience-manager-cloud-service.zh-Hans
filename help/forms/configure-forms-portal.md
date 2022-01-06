---
title: 如何在Forms页面上创建Experience Manager Sites门户
description: 了解如何在Forms页面上创建AEM Sites门户并使用现成的核心组件。
source-git-commit: 50eeb2c1e6925b39b03bbbdd627169453ea1c1d8
workflow-type: tm+mt
source-wordcount: '1784'
ht-degree: 1%

---


# 在门户上列出自适应Forms {#publish-forms-on-portal}

在典型的以表单为中心的门户部署场景中，表单开发和门户开发是两个不相干的活动。 表单设计人员在存储库中设计和存储表单时， Web开发人员会创建一个Web应用程序来列出表单和处理表单提交。 Forms将复制到Web层，因为表单存储库与Web应用程序之间没有通信。

这种情况往往导致管理问题和生产延迟。 例如，如果存储库中有较新版本的表单可用，则需要替换Web层上的表单，修改Web应用程序，并在公共网站上重新部署该表单。 重新部署Web应用程序可能会导致服务器停机。 通常，服务器停机是计划的活动，因此更改不能即时推送到公共站点。

AEM Forms提供门户组件，可减少管理开销和生产延迟。 这些组件使Web开发人员能够在使用Adobe Experience Manager(AEM)创作的网站上创建和自定义Forms门户。

表单门户组件允许您添加以下功能：

* 以自定义布局列出表单。 现成提供了列表视图和卡片视图布局。 您可以创建自己的自定义布局。
* 允许您在列出自定义元数据和自定义操作时显示它们。
* 在使用AEM Forms Portal组件的发布实例上列出由Forms UI发布的表单。
* 允许最终用户以HTML和PDF格式呈现表单。
* 允许根据标题和描述搜索表单。
* 使用自定义CSS自定义门户的外观。
* 创建指向表单的链接。
* 列出与最终用户创建的自适应Forms相关的草稿和提交。

## Forms门户页面的组件 {#forms-portal-components}

AEM Forms开箱即用地提供以下门户组件：

* 搜索和制表人：此组件允许您将表单从表单存储库列到门户页面上，并提供配置选项以根据指定的条件列出表单。

* 草稿和提交：搜索和制表人组件显示由Forms作者公开的表单，而草稿和提交组件则显示另存为草稿的表单，以供日后完成和提交的表单。 此组件可为任何已登录的用户提供个性化体验。

* 链接：此组件允许您创建指向页面上任意位置的表单的链接。

您可以 [导入现成的Forms门户组件](#import-forms-portal-components-aem-archetype) 从AEM项目原型。 导入后，请执行以下配置：
* [配置外部存储](#configure-azure-storage-adaptive-forms)
* [启用Forms Portal组件](#enable-forms-portal-components)
* [配置Forms Portal组件](#configure-forms-portal-components)

## 导入Forms Portal组件 {#import-forms-portal-components-aem-archetype}

要在AEM Formsas a Cloud Service上导入现成的Forms门户组件，请执行以下步骤：

1. **在本地开发实例上克隆Cloud Manager Git存储库：**  您的Cloud Manager Git存储库包含一个默认的AEM项目。 基于 [AEM原型](https://github.com/adobe/aem-project-archetype/). 使用Cloud Manager UI中的自助服务Git帐户管理来克隆Cloud Manager Git存储库，以将项目引入本地开发环境。 有关访问存储库的详细信息，请参阅 [访问存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/accessing-repos.html).

1. **创建 [!DNL Experience Manager Forms] as a [Cloud Service] 项目：** 创建 [!DNL Experience Manager Forms] as a [Cloud Service] 项目基于 [AEM原型27](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) 或更晚。 原型可帮助开发人员轻松开始开发 [!DNL AEM Forms] as a Cloud Service。 它还包含一些帮助您快速入门的示例主题和模板。

   创建 [!DNL Experience Manager Forms] as a Cloud Service项目，打开命令提示符并运行以下命令。 包含 [!DNL Forms] 特定配置、主题和模板，设置 `includeForms=y`.

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=30 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   此外，更改 `appTitle`, `appId`和 `groupId`，以反映您的环境。

1. **在预发行版本中，执行以下步骤以使用Forms Portal组件：**
   * [启用预发行渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en).
   * 替换 `core-forms-components-*` 的预发行版本(例如，1.0.4-PRERELEASE-20211223) `Cloud Manager/AEM Archetype` 通过更新项目 `<core.forms.components.version>x.y.z</core.forms.components.version>` 顶级属性 `pom.xml` 原型项目。

1. **将项目部署到本地开发环境：** 您可以使用以下命令部署到本地开发环境

   `mvn -PautoInstallPackage clean install`

   有关命令的完整列表，请参阅 [构建和安装](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=en#building-and-installing)

1. [将代码部署到 [!DNL AEM Forms] as a Cloud Service环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html#embeddeds).


## 为自适应Forms配置Azure存储 {#configure-azure-storage-adaptive-forms}

[[!DNL Experience Manager Forms] 数据集成](data-integration.md) 提供 [!DNL Azure] 存储配置，将表单与 [!DNL Azure] 存储服务。 表单数据模型可用于创建与交互的自适应Forms [!DNL Azure] 服务器启用业务工作流。

### 创建 Azure 存储配置 {#create-azure-storage-configuration}

在执行这些步骤之前，请确保您拥有Azure存储帐户和访问密钥，以授权访问 [!DNL Azure] 存储帐户。

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Azure存储]**.
1. 选择要创建配置的文件夹，然后点按 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 标题]** 字段。
1. 指定 [!DNL Azure] 存储帐户 **[!UICONTROL Azure存储帐户]** 字段。

### 为Forms门户配置统一存储连接器 {#configure-usc-forms-portal}

执行以下步骤来为AEM工作流配置统一存储连接器：

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 统一存储连接器]**.
1. 在 **[!UICONTROL Forms门户]** 选择 **[!UICONTROL Azure]** 从 **[!UICONTROL 存储]** 下拉列表。
1. 指定 [Azure存储配置的配置路径](#create-azure-storage-configuration) 在 **[!UICONTROL 存储配置路径]** 字段。
1. 点按 **[!UICONTROL 发布]** 然后点按 **[!UICONTROL 保存]** 以保存配置。

## 启用Forms Portal组件 {#enable-forms-portal-components}

要在Adobe Experience Manager(AEM)网站中使用任何核心组件（包括现成的门户组件），您必须创建一个代理组件并为您的网站启用该组件。 有关创建代理组件和启用门户组件的信息，请参阅 [使用核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html?lang=en#create-proxy-components).

启用门户组件后，即可在网站页面的创作实例中使用该组件。

## 添加和配置Forms Portal组件 {#configure-forms-portal-components}

您可以通过添加和配置门户组件，在使用AEM创作的网站上创建和自定义Forms门户。 确保 [组件已启用](#enable-forms-portal-components) 在Forms门户中使用它们之前，请执行以下操作：

要添加组件，请将组件从组件窗格拖放到页面上的布局容器，或点按布局容器上的添加图标，然后从 [!UICONTROL 插入新组件] 对话框。

### 配置草稿和提交组件 {#configure-drafts-submissions-component}

草稿和提交组件显示另存为草稿的表单，以供日后完成和提交的表单。 要配置，请点按组件，然后点按 ![“配置”图标](assets/configure_icon.png). 在 [!UICONTROL 草稿和提交] 对话框中，指定标题以指示表单列表为草稿或提交的表单。 此外，还选择组件应将草稿表单或提交的表单以卡片或列表格式列出。

![草稿图标](assets/drafts-component.png)

![“提交”图标](assets/submission-listing.png)

### 配置搜索和制表器组件 {#configure-search-lister-component}

搜索和制表人组件用于在页面上列出自适应表单，并对列出的表单实施搜索。

![“搜索和制表人”图标](assets/search-and-lister-component.png)

要配置，请点按组件，然后点按 ![“配置”图标](assets/configure_icon.png). 的 [!UICONTROL 搜索和Lister] 对话框。

1. 在 [!UICONTROL 显示] 选项卡，请配置以下内容：
   * 在 **[!UICONTROL 标题]**，指定搜索和制表器组件的标题。 指示性标题使用户能够在表单列表中执行快速搜索。
   * 从 **[!UICONTROL 布局]** 列表，选择以卡片或列表格式表示表单的布局。
   * 选择 **[!UICONTROL 隐藏搜索]** 和 **[!UICONTROL 隐藏排序]** 以隐藏搜索并按功能排序。
   * 在 **[!UICONTROL 工具提示]**，提供将鼠标悬停在组件上时显示的工具提示。
1. 在 [!UICONTROL 资产文件夹] 选项卡上，指定从中提取并列出表单的位置。 您可以配置多个文件夹位置。
1. 在 [!UICONTROL 结果] 选项卡，配置每页要显示的最大表单数。 默认为每页8个表单。

### 配置链接组件 {#configure-link-component}

链接组件允许您提供指向页面上自适应表单的链接。 要配置，请点按组件，然后点按 ![“配置”图标](assets/configure_icon.png). 的 [!UICONTROL 编辑链接组件] 对话框。

1. 在 [!UICONTROL 显示] 选项卡上，提供链接标题和工具提示，以便识别链接所表示的表单。
1. 在 [!UICONTROL 资产信息] 选项卡，指定存储资产的存储库路径。
1. 在 [!UICONTROL 查询参数] 选项卡，以键值对格式指定其他参数。 单击链接后，这些附加参数将随表单一起传递。

## 使用Adobe Sign配置异步表单提交 {#configure-asynchronous-form-submission-using-adobe-sign}

只有在所有收件人都完成了签名仪式后，您才能配置为提交自适应表单。 请按照以下步骤使用Adobe Sign配置设置。

1. 在创作实例中，以编辑模式打开自适应表单。
1. 从左窗格中，点按属性图标，然后展开 **[!UICONTROL 电子签名]** 选项。
1. 选择 **[!UICONTROL 启用Adobe Sign]**. 将显示各种配置选项。
1. 在 [!UICONTROL 提交表单] 选择 **[!UICONTROL 每个收件人完成签约仪式]** 选项，以配置“提交表单”操作，在该操作中，表单首先会发送给所有收件人以供签名。 所有收件人在表单上签名后，才会提交表单。

## 将自适应Forms另存为草稿 {#save-adaptive-forms-as-drafts}

您可以将表单另存为草稿，以备日后完成。 表单保存为草稿的方式有两种：
* 在表单组件（例如按钮）上创建“保存表单”规则。 单击按钮时，规则触发器和表单将保存为草稿。
* 启用自动保存功能，该功能会根据指定事件或在配置的时间间隔后保存表单。

### 创建规则以将自适应表单另存为草稿 {#rule-to-save-adaptive-form-as-draft}

要在表单组件（例如按钮）上创建“保存表单”规则，请执行以下步骤：

1. 在创作实例中，以编辑模式打开自适应表单。
1. 从左窗格中，点按 ![“组件”图标](assets/components_icon.png) 然后拖动 [!UICONTROL 按钮] 组件。
1. 点按 [!UICONTROL 按钮] 组件，然后点按 ![“配置”图标](assets/configure_icon.png).
1. 点按 [!UICONTROL 编辑规则] 图标以打开规则编辑器。
1. 点按 **[!UICONTROL 创建]** 以配置和创建规则。
1. 在 [!UICONTROL When] 中，选择“已单击”，然后在 [!UICONTROL 然后] ，请选择“保存表单”选项。
1. 点按 **[!UICONTROL 完成]** 来保存规则。

### 启用自动保存 {#enable-auto-save}

您可以按照以下方式为自适应表单配置自动保存功能：

1. 在创作实例中，以编辑模式打开自适应表单。
1. 从左窗格中，点按 ![“属性”图标](assets/configure_icon.png) 并展开 [!UICONTROL 自动保存] 选项。
1. 选择 **[!UICONTROL 启用]** 复选框以启用表单的自动保存。 您可以配置以下各项：
* 默认情况下， [!UICONTROL 自适应表单事件] 设置为“true”，这意味着在每个事件后都会自动保存表单。
* 在 [!UICONTROL 触发器]，配置以根据事件的发生或特定时间间隔后触发自动保存。
