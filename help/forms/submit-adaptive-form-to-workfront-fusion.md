---
title: Adobe Workfront Fusion与AEM Forms提交的集成
description: Adobe Workfront Fusion允许您专注于新任务，而不是重复的任务。 您可以使用表单提交功能将Adobe Workfront Fusion连接到自适应表单。
keywords: 将自适应表单提交到Adobe Workfront Fusion、Adobe Workfront Fusion与AEM Forms提交的集成、Adobe Workfront Fusion与AEM Forms的集成、Workfront Fusion与AEM Forms的集成、将Workfront Fusion连接到AEM Forms、AEM Forms和Workfront Fusion、如何将Workfront Fusion与AEM Forms连接？以及将Workfront Fusion连接到表单
topic-tags: author, developer
feature: Adaptive Forms
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: 3e1e1eba822bf3156ef563b88269cdef2298e951
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 4%

---

# 向 Adobe Workfront Fusion 提交自适应表单

<span class="preview"> 该功能在早期采用者计划下提供。 您可以从官方电子邮件ID写信到aem-forms-early-adopter-program@adobe.com ，加入率先采用者计划并请求获取该功能的访问权限。 </span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) 自动执行重复相同任务的过程，例如文档审批工作流、电子邮件筛选和排序，使您能够专注在新任务上而不是重复任务。 Adobe Workfront Fusion包含多个场景。 场景由一系列模块组成，这些模块在应用程序和Web服务之间执行数据传输。 在场景中，添加各种步骤（模块）以自动执行任务。

例如，使用Workfront Fusion，您可以创建一个方案，以便使用自适应表单收集数据、处理数据并将数据发送到数据存储进行存档。 一旦设置了场景，Workfront Fusion就会在用户填写表单时自动执行任务，从而无缝更新数据存储。

AEM Formsas a Cloud Service提供了一个OOTB连接器，用于连接自适应表单并将其提交到Adobe Workfront Fusion。 将表单提交到Adobe Workfront Fusion可以具备以下优势：
* 它支持将表单提交数据无缝传输到Workfront Fusion工作流。
* 它有助于自动执行由表单提交触发的各种任务。 这可以包括启动项目、将任务分配给特定团队成员、发送通知以及更新项目状态 — 所有这些操作都不需要手动干预。
* 在Workfront Fusion中捕获的所有表单提交都为项目相关信息提供了单一的真实来源


<!--  AEM as a Cloud Service offers various out of the box submit actions for handling form submissions. You can learn more about these options in the [Adaptive Form Submit Action](/help/forms/configure-submit-actions-core-components.md)  article.-->

>[!VIDEO](https://video.tv.adobe.com/v/3427145/adaptive-forms-adobe-workfront-af-workfront-workfront-aem-forms/?quality=12&learn=on)

## 将AEM Forms与Adobe Workfront Fusion集成的先决条件 {#prerequisites}

要在Workfront Fusion与AEM Forms之间建立连接，需要满足以下条件：

* 有效的 [Workfront和Workfront Fusion许可证](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html).
* 有权访问的AEM用户 [开发控制台](https://my.cloudmanager.adobe.com/) 到 [检索服务凭据](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).

## 将AEM Forms与Adobe Workfront Fusion集成

连接 [Workfront融合](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) 对于表单，请执行以下步骤：

### 1.创建Workfront方案 {#workflow-scenario}

要创建Workfront方案，请执行以下操作：
1. 登录您的 [Workfront Fusion帐户](https://app-qa.workfrontfusion.com/).
1. 单击 **[!UICONTROL 方案]** ![“共享”图标](/help/forms/assets/Smock_ShareAndroid_18_N.svg) 在左侧面板中。
1. 单击 **[!UICONTROL 创建新方案]** 在页面的右上角。 屏幕上会显示创建新方案的页面。
1. 选择 **[!UICONTROL 新方案]** （位于页面的左上角），并为场景键入正确的名称。
1. 单击问号，并确保将第一个模块添加为 **[!UICONTROL AEM Forms]**.

   ![添加AEM Forms模块](/help/forms/assets/workfront-aemforms.png)

   此 **[!UICONTROL 关注表单事件]** 对话框。

   >[!NOTE]
   >
   > 必须将第一个模块添加为 **[!UICONTROL AEM Forms]**.

1. 选择 **[!UICONTROL 关注表单事件]** 对话框和添加webhook的窗口出现。

#### 1.1添加webhook {#add-webhook}

![添加webhook](/help/forms/assets/workfront-add-webhook.png)

要添加webhook，请执行以下操作：

1. 单击 **[!UICONTROL 添加]** 和 **[!UICONTROL 添加webhook]** 对话框。
1. 指定webhook名称。

   >[!NOTE]
   >
   > 建议您仔细选择您的webhook名称，因为指定的webhook名称会显示在AEM实例中。

1. 单击 **[!UICONTROL 添加]** 以添加新连接。 此 **[!UICONTROL 创建连接]** 对话框。

#### 1.2添加与webhook的连接 {#add-connection}

![添加连接](/help/forms/assets/workfront-add-connection.png)

要添加连接，请执行以下操作：

1. 指定 **[!UICONTROL 连接名称]** 在 **[!UICONTROL 创建连接]** 对话框。

1. 选择 **环境** 和 **类型** 下拉列表中。

1. 输入 **实例URL**.

   >[!NOTE]
   >
   > 实例URL是指向特定AEM Forms实例的唯一网址。

   您可以检索 [来自开发人员控制台的服务凭据](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html) 创建连接时需要。

1. 替换 `ims-na1.adobelogin.com` 在 **IMS端点** 值为 **imsEndpoint** 来自开发人员控制台中的服务凭据。

   >[!NOTE]
   >
   > 保留 `https://` 在 **IMS端点** 文本框 `imsEndpoint` URL。

1. 在中指定以下值 **[!UICONTROL 创建连接]** 对话框：
   * 指定 **客户端ID** 具有值 **clientId** 来自开发人员控制台中的服务凭据。
   * 指定 **客户端密码** 具有值 **客户端密钥** 来自开发人员控制台中的服务凭据。
   * 指定 **技术帐户ID**  具有值 **id** 来自开发人员控制台中的服务凭据。
   * 指定 **组织ID**  具有值 **org** 来自开发人员控制台中的服务凭据。
   * **元范围**  具有值 **metascope** 来自开发人员控制台中的服务凭据。
   * **私钥**  具有值 **私钥** 来自开发人员控制台中的服务凭据。

   >[!NOTE]
   >
   >* 对象 **私钥**，删除 `\r\n` 从它的值开始。
   >  例如，如果私钥值为：
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`，则在删除 `\r\n` 与私钥相比，该密钥将类似于以下内容，并且两个值都显示在单独的行中：
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >* 您还可以选择从文件检索私钥或证书，方法是选择 **Extract** 按钮。

1. 单击&#x200B;**“继续”**。

   创建的连接开始显示在 **[!UICONTROL 连接]** 在 **[!UICONTROL 添加webhook]** 对话框。

1. 选择已创建的连接 **[!UICONTROL 连接]** 下拉列表中。
1. 单击&#x200B;**[!UICONTROL 保存]**。
1. 单击 **[!UICONTROL 确定]** 并保存方案的更改。
1. 要激活方案，请单击方案编辑器中的打开/关闭切换按钮。

>[!NOTE]
>
> 如果未激活Workfront方案，它将检测不到表单提交，并且将提交操作设置为Workfront会导致提交失败。

### 2.配置Workfront Fusion自适应表单的提交操作

您可以为Workfont Fusion配置提交操作，用于：
* [新的自适应Forms](#new-af-submit-action)
* [现有自适应表单](#existing-af-submit-action)

#### 配置适用于Workfront Fusion的新自适应表单的提交操作 {#new-af-submit-action}

要配置适用于Workfront Fusion的新自适应表单的提交操作，请执行以下操作：

1. 登录到您的AEM实例。
1. 转到 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]** > **[!UICONTROL 创建]** > **[!UICONTROL 自适应表单]**. 此 **[!UICONTROL 创建表单]** 出现向导。
1. 从中选择自适应表单模板 **[!UICONTROL 来源]** 选项卡。
1. 从中选择主题 **[!UICONTROL 样式]** 选项卡。

   ![适用于Workfront Fusion的提交操作](/help/forms/assets/workfront-scenario-new-af.png)

1. 选择 **[!UICONTROL 调用Workfront Fusion场景]** 从 **[!UICONTROL 提交]** 选项卡。
1. 从中选择创建的webhook **[!UICONTROL 选项]** 选项卡 **[!UICONTROL 属性]** 窗口。

   >[!NOTE]
   >
   > Workfront方案的webhook名称显示在中 **选项** 下拉列表。

1. 单击&#x200B;**[!UICONTROL 创建]**。
1. 指定新自适应表单的名称，然后单击 **[!UICONTROL 创建]**.

#### 配置现有Workfront Fusion自适应表单的提交操作 {#existing-af-submit-action}

要配置现有Workfront Fusion自适应表单的提交操作，请执行以下操作：

1. 登录到您的AEM实例。
1. 转到 **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**.
1. 选择一个自适应表单，然后在编辑模式下打开该表单。
1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。

   ![适用于Workfront Fusion的提交操作](/help/forms/assets/workfront-scenario-existing-af.png)

1. 打开 **[!UICONTROL 提交]** 选项卡。
1. 选择 **[!UICONTROL 提交操作]** 作为 **[!UICONTROL 调用Workfront Fusion场景]**
1. 选择 **[!UICONTROL Workfront Fusion场景]** 下拉列表中。
1. 单击&#x200B;**[!UICONTROL 完成]**。

## 最佳实践 {#best-practices}

* 建议您仔细选择您的webhook名称，因为在AEM实例上无法获取场景名称。 如果将来更改webhook名称，该名称将不会反映在AEM Forms提交操作下拉列表中。
* 一个方案可以有多个webhook链接，但一次只能有一个webhook链接处于活动状态。 建议删除未链接的webhook，以便它不会出现在AEM Forms提交操作下拉列表中。

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->

## 相关文章

{{af-submit-action}}