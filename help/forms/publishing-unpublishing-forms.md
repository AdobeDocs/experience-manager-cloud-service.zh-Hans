---
title: 如何在AEM表单中发布和取消发布表单和文档？
description: 安排自适应Forms的发布和取消发布。 发布的表单将在发布实例上复制。
content-type: reference
topic-tags: publish
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
feature: Adaptive Forms
role: User
hide: true
hidefromtoc: true
exl-id: 9496e4f5-ed74-4b40-b8f9-17153170af66
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 1%

---

# 发布和取消发布 Form 和文档{#publishing-and-unpublishing-forms-and-documents}

[!DNL AEM Forms]允许您轻松创建、发布和取消发布表单。 [!DNL AEM Forms]服务器提供两个实例： Author和Publish。 创作实例用于创建和管理表单资源和资源。 Publish实例用于保留可供最终用户使用的资源和相关资源。

## 支持的资源   {#supported-assets-nbsp}

[!DNL AEM Forms]支持以下类型的资产：

* 自适应表单
* 自适应文档
* 自适应表单片段
* 主题
* 表单模板<!-- (XFA forms) -->
* PDF forms
* 单据(平面PDF单据)
* 表单集
* 资源（图像、架构和样式表）

最初，所有资产仅在创作实例中可用。 管理员或表单作者可以发布除资源以外的所有资源。

选择并发布表单时，也会发布其相关资源和资源。 但是，依赖关系资产不会发布。 在此上下文中，相关资源和资源是已发布资源使用或引用的资源。 依赖资产是指引用已发布资产的资产。

您的自适应Forms可能会利用一些未自动发布的配置、设置和自定义设置。 建议您在发布自适应表单之前发布或激活这些资源。

* 可编辑的自适应表单模板
* Adobe Sign、Typekit、reCAPTCHA和表单数据模型(FDM)的Cloud Service配置
* 仅当用户具有管理员权限时，才会激活其他Cloud Service配置。
* 自定义。 这些包括但不限于：

   * 自定义布局
   * 自定义外观
   * CSS文件 — 在自适应表单容器属性对话框中用作输入
   * 客户端库类别 — 在自适应表单容器属性对话框中作为输入使用
   * 可能包含在自适应表单模板中的任何其他客户端库。
   * 设计路径

## 资产状态 {#asset-states}

资产可以具有以下状态：

* **未发布：**&#x200B;从未发布的资源(未发布状态仅适用于Forms资源。 通信管理资产没有“未发布”状态。)
* **已发布**：已发布并在Publish实例上可用的资源
* **已修改**：发布后修改的资产

## Publish资产 {#publish-an-asset}

1. 登录到[!DNL AEM Forms]服务器。
1. 使用下列选项之一选择和发布资产。

   1. 将指针移动到资源上并选择&#x200B;**[!UICONTROL Publish]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png)。
   1. 执行以下操作之一，然后选择Publish：

      * 如果您在卡片视图中，请选择&#x200B;**[!UICONTROL 输入选择]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)，然后选择资产。 已选择资源。
      * 如果您在列表视图中，请选中资源的复选框。 已选择资源。
      * 选择资产以显示其详细信息。
      * 通过点按视图属性![viewproperties](assets/viewproperties.png)显示资源的属性。

      >[!NOTE]
      >
      >请勿选择多个资源。 不支持一次发布多个资产。

1. Publish流程启动时，会显示一个确认对话框，其中列出了所有相关资源和资源。 在包含相关资源的对话框中，选择&#x200B;**[!UICONTROL Publish]**。 发布资源，并显示Publish Assets成功对话框。

   >[!NOTE]
   >
   >对于自适应Forms以及相关的资源，还会显示自适应表单页面名称。

   ![包含所有相关资源和资源的确认对话框](assets/p4.png)

   包含所有相关资源和资源的确认对话框。

   >[!NOTE]
   >
   >对于Forms Manager，如果用户没有发布所列资源的权限，则Publish操作将被禁用。 需要额外权限的资源以红色显示。

   发布资源后，该资源的元数据属性将会复制到Publish实例，并且资源的状态会更改为已发布。 已发布的依赖关系资产的状态也会更改为已发布。

   <!-- After publishing an asset, you can use the Forms Portal to display all the assets on a web page. For more information, see [Introduction to publishing forms on a portal](introduction-publishing-forms.md).-->

## Publish所有通信管理Assets {#publish-all-the-correspondence-management-assets}

[!DNL AEM Forms]允许您一次性发布服务器上的所有通信管理资产。 已发布的资产包括所有相应的管理资产和相关依赖项。

完成以下步骤以在服务器上发布所有相应的管理资产：

1. 登录到[!DNL AEM Forms]服务器。
1. 在全局导航栏中选择&#x200B;**Adobe Experience Manager**。
1. 选择![工具](assets/tools.png)，然后选择&#x200B;**Forms**。
1. 选择&#x200B;**Publish Correspondence Management Assets**。

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   此时将显示Publish All Correspondence Management Assets页面，其中显示有关上次尝试Publish Correspondence Management Assets进程的信息。

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. 选择&#x200B;**Publish**，然后在确认消息中选择&#x200B;**确定**。

   批处理完成后，您可以查看上次运行的详细信息。 这包括管理员登录信息以及批处理是否成功运行的信息。

   >[!NOTE]
   >
   >Publish进程一旦启动便无法取消。 此外，在Publish操作处理期间，请勿创建、删除、修改或发布任何资源，也不要启动“导出所有通信管理Assets”操作。

## 自动发布和取消发布Forms和文档 {#automate-publishing-and-unpublishing-for-forms-amp-documents}

[!DNL AEM Forms]允许您为Forms和文档计划资产发布和取消发布。 您可以在元数据编辑器中指定计划。 有关管理表单元数据的详细信息，请参阅[管理表单元数据](manage-form-metadata.md)。

请按照以下步骤计划发布和取消发布Forms &amp; Documents资产的日期和时间：

1. 选择资产，然后选择&#x200B;**[!UICONTROL 查看属性]**。 此时将打开“元数据属性”页面。
1. 在“元数据属性”页中，选择&#x200B;**[!UICONTROL 高级]**，然后选择&#x200B;**[!UICONTROL 编辑]** ![illustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png)。
1. 在&#x200B;**[!UICONTROL Publish开启时间]**&#x200B;和&#x200B;**[!UICONTROL Publish关闭时间]**&#x200B;字段中，选择日期和时间。\
   选择&#x200B;**[!UICONTROL 完成]** ![aem6forms_check](assets/aem6forms_check.png)。

## 取消发布资源 {#unpublish-an-asset}

1. 选择已发布的资产，然后选择&#x200B;**[!UICONTROL 取消发布]** ![取消发布](assets/unpublish.png)。
1. 使用下列选项之一选择并取消发布资产。

   1. 将指针移动到资产上并选择&#x200B;**[!UICONTROL 取消发布]** ![取消发布](assets/unpublish.png)。
   1. 执行以下操作之一，然后选择取消发布：

      * 如果您在卡片视图中，请选择&#x200B;**[!UICONTROL 输入选择]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)，然后选择资产。 已选择资源。

      * 如果您在列表视图中，请将鼠标悬停在资产上并选择![selectassetcheckmark](assets/selectassetcheckmark.png) 。 已选择资源。

      * 选择资产以显示其详细信息。
      * 通过点按视图属性![viewproperties](assets/viewproperties.png)显示资源的属性。

1. 当取消发布过程启动时，将显示确认对话框。 选择&#x200B;**[!UICONTROL 取消发布]**。

   >[!NOTE]
   >
   >仅取消发布选定的资产，不会取消发布其子资产和引用的资产（如果有）。

## 将资源或书信还原到先前发布的版本 {#revert-an-asset-or-letter-to-the-previously-published-version}

每次在编辑资源或信件后发布该资源或信件时，都会创建资源或信件的版本。 您可以将资源或信件还原到先前发布的版本。 如果资源或文档的当前版本出现问题，您可能需要执行此操作。

>[!NOTE]
>
>如果已从系统中删除发布书信中使用的任何依赖资产，请勿将书信恢复为上次发布状态。

1. 选择资源并选择&#x200B;**[!UICONTROL 还原到以前发布的版本]** ![reverttopreviouslypublishedversion](assets/reverttopreviouslypublishedversion.png)。
1. 在还原资源之前，会显示确认对话框。 选择&#x200B;**[!UICONTROL 恢复]**。

   资产或书信将回滚到其先前发布的版本。

## 删除资源 {#delete-an-asset}

>[!NOTE]
>
>删除资源会将其从发布实例中移除， 删除资产时，还会删除其版本历史记录（基础版本除外）。

1. 选择资产并选择&#x200B;**[!UICONTROL 删除]** ![删除](assets/delete.png)。

   >[!NOTE]
   >
   >通过点按资产显示资产详细信息或通过点按查看属性![viewproperties](assets/viewproperties.png)显示资产属性时，也可以使用“删除”选项。

1. 在删除资源之前，会显示确认对话框。 选择&#x200B;**[!UICONTROL 删除]**。

   >[!NOTE]
   >
   >仅删除选定的资源，并且不会删除依赖关系资源和资源。 要检查某个资源的引用，请选择![个引用](assets/references.png)，然后选择一个资源。
   >
   >
   >如果您尝试删除的资源是其他资源的子资源，则不会删除它。 要删除此类资产，请从其他资产中删除对此资产的引用，然后重试。

## 受保护的自适应Forms {#protected-adaptive-forms}

您可以为希望选定用户访问的表单启用身份验证。 为表单启用身份验证后，用户会在访问表单之前看到登录屏幕。 只有拥有授权凭据的用户才能访问表单。

要为表单启用身份验证，请执行以下操作：

1. 在浏览器中，打开发布实例中的configMgr 。\
   URL： `https://<hostname>:<PublishPort>/system/console/configMgr`

1. 在Adobe Experience Manager Web控制台配置中，单击&#x200B;**Apache Sling身份验证服务**&#x200B;以对其进行配置。
1. 在出现的Apache Sling身份验证服务对话框中，使用&#x200B;**+**&#x200B;按钮添加路径。\
   添加路径时，将为该路径中的表单启用身份验证服务。
