---
title: 版发行说明 [!DNL Workfront for Experience Manager enhanced connector]
description: 版发行说明 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 8ce5b0a163c8ddf7f9c9672eff6d752a58c464bb
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 1%

---

#  版发行说明[!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

以下部分概述了的常规发行说明 [!DNL Workfront for Experience Manager enhanced connector].

## 发布日期 {#release-date}

最新版本1.9.8的发布日期 [!DNL Workfront for Experience Manager enhanced connector] 是2023年3月3日。

## 发行亮点 {#release-highlights}

最新版本的 [!DNL Workfront for Experience Manager enhanced connector] 包括以下更新：

* 在Workfront中创建项目链接文件夹时Experience Manager的性能改进。

* Workfront中的评论删除现在反映在Experience Manager中。

* 在as a Cloud Service于配置连接器的Experience Manager上管理阻止新网络客户的功能。


>[!IMPORTANT]
>
>Adobe建议您 [升级到最新的1.9.8版本](../assets/update-workfront-enhanced-connector.md) 的 [!DNL Workfront for Experience Manager enhanced connector].

## 已知问题 {#known-issues}

* 使用AEM 6.4配置项目链接文件夹时，Experience Manager不保存值 **[!UICONTROL 子文件夹]** 和 **[!UICONTROL 在具有项目组合的项目中创建链接文件夹]** 字段。 的值 **[!UICONTROL 子文件夹]** 字段更新至 **[!UICONTROL 未定义]** 和的值 **[!UICONTROL 在具有项目组合的项目中创建链接文件夹]** 字段更新至 **[!UICONTROL 默认Portfolio]** 在保存配置后自动。

* 当您使用经典Workfront体验时， **[!UICONTROL 发送至]** 中提供的选项 **[!UICONTROL 更多]** 下拉列表不允许您在Experience Manager中选择目标目标。 此 **[!UICONTROL 发送至]** 选项通过使用 **[!UICONTROL 文档操作]** 下拉列表。 此 **[!UICONTROL 发送至]** 选项对以下各项正常工作 **[!UICONTROL 更多]** 下拉列表以及 **[!UICONTROL 文档操作]** 下拉列表(可从新的Workfront experience中获取)。

## 以前版本 {#previous-releases}

### 2022年1月版 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.7于2023年2月2日发布，其中包括以下更新：

* 安装1.9.6版本后，元数据编辑器未列出Workfront自定义表单属性。

* 此时将显示开发控制台 `/content/dam/jcr:content/metadata/wfProjectURL not found` 安装Workfront增强型连接器并打开Assets主页后的错误消息。

### 2022年12月版 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.6于2009年12月发布，包括以下更新：

**增强功能**

<!--

* Workfront enhanced connector now allows you to use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront增强型连接器现在支持对资源和文件夹执行全文搜索。

**错误修复**

* 文档版本元数据未在Workfront和Experience Manager之间正确同步。
* 当文件夹使用的架构在全局配置中缺少定义时，创建链接到Workfront中的Experience Manager的文件夹时出现问题。
* 由于加载时间长于预期时间，元数据架构编辑器表单在您单击任何字段时停止响应。 为自定义表单添加了特定的OSGi配置以解决此问题。 日志中提供了您添加到元数据架构编辑器的自定义表单的名称。

### 2022年11月版 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.5于11月11日发布，其中包括以下更新：

* 当您在Workfront中为多值字段仅定义一个值时，该字段值未正确映射到Experience Manager。

* Experience Manager显示 `SERVER_ERROR` 在 **[!UICONTROL 链接外部文件和文件夹]** 由于对的无效权限访问资产文件夹时显示的屏幕 `/content/dam/collections`.

* 启用 **[!UICONTROL 将资源发布到Brand Portal]** Workfront增强型连接器配置页面上的选项会创建不正确的事件。 即使禁用了该选项，该事件也不会被删除。

   要解决此问题：

   1. 升级到1.9.5版本的增强型连接器。

   1. 禁用 **[!UICONTROL 将资源发布到Brand Portal]** 选项。

   1. 启用 **[!UICONTROL 将资源发布到Brand Portal]** 选项。

   1. 删除错误的事件订阅。

      1. 执行GET调用 `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         为每个页码执行一个API调用。

      1. 搜索以下文本以查找与以下URL匹配且没有的事件订阅 `objId`：

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         确保内容介于 `"objId": "",` 和 `"url"` 匹配JSON响应。 为此，建议从任何具有 `objId` 然后删除该编号。

      1. 记下事件订阅ID。

      1. 删除错误的事件订阅。 对进行删除API调用 `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` 响应代码表示成功删除了错误的事件订阅。
   >[!NOTE]
   >
   >如果在执行此过程中提到的步骤之前删除了错误的事件预订，则可以跳过此过程的最后一个步骤。

### 2022年10月版 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.4于2007年10月发布，其中包括以下更新：

* 由于大量事件，无法在增强型连接器配置页面上查看“事件订阅”选项卡。

* Workfront无法获取项目中现有文件夹的列表，从而导致创建重复的文件夹。

### 2022年9月版 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.3于9月16日发布，包括以下更新：

* 无法上载大小超过8 GB的文件。
* 自动发布从Workfront发送到AEM的资产时出现问题。
* 编辑默认元数据架构表单时，根路径字段不可用于“标记”字段。
* 使用AEM工作流在Workfront中添加新版本时出现问题。
* 在执行AEM搜索可在Workfront中找到的资源时，AEM显示错误消息。
* 当您创建用于从资源创建任务的AEM工作流，并且未定义父任务名称时，任务未在Workfront中创建。

### 2022年8月版 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.2于2003年8月发布，其中包括以下更新：

* 此 **[!UICONTROL 上传文档]** 工作流步骤无法将文档附加到Workfront。

* 此 **[!UICONTROL 上传文档]** 工作流步骤无法将文档附加到Workfront中的任务和问题。 工作流步骤成功将文档附加到项目。

### 2022年7月版 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.1包含以下更新：

* 为迁移到Adobe IMS的实例添加了对使用Workfront API密钥的Experience Manager应用程序和Workfront应用程序之间的身份验证的支持。

* 当您链接外部文件或文件夹时，Workfront应用程序会显示 `SERVER_ERROR` 错误消息。 错误消息是指由于API密钥不匹配，出现未经授权的异常。

* 为资源执行“创建任务”工作流时，日志消息中会显示“空指针”异常。

* 当您启用 `Replace Spaces with DASH` Experience Manager中的高级设置下的配置选项，将导致在Workfront中创建重复的文件夹。

### 2022年6月版 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 现在包含以下更新：

* 当您通过链接的文件夹上传或使用 `Send To` Workfront中可用于将资源上传到Experience Manageras a Cloud Service的操作，这些资源已损坏，无法在Adobe Photoshop中打开。

### 2022年3月版 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 现在包含以下更新：

* 现在，即使存在多个项目链接文件夹配置，您也可以在Adobe Workfront和AEM Assetsas a Cloud Service之间创建链接文件夹。

* 添加了对事件订阅分页的支持。

* 添加了对AEM 6.4.x的支持。

* 添加了对代理环境的支持。

* 基于合作伙伴和客户反馈的多项错误修复。

>[!MORELIKETHIS]
>
>* [集成 [!DNL Workfront for Experience Manager enhanced connector] 使用Experience Manager6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [集成 [!DNL Workfront for Experience Manager enhanced connector] 使用Experience Manager6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)