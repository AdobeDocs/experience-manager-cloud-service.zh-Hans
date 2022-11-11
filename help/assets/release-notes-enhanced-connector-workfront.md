---
title: 版发行说明 [!DNL Workfront for Experience Manager enhanced connector]
description: 版发行说明 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: 8bcfcae211b2203915e7facc361188a0f5739547
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 1%

---

#  版发行说明[!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

以下部分概述了 [!DNL Workfront for Experience Manager enhanced connector].

## 发布日期 {#release-date}

最新版本1.9.5( [!DNL Workfront for Experience Manager enhanced connector] 是2022年11月11日。

## 发行亮点 {#release-highlights}

的最新版本 [!DNL Workfront for Experience Manager enhanced connector] 包括以下增强功能和错误修复：

* 如果在Workfront中只为多值字段定义一个值，则该字段值未正确映射到Experience Manager。

* Experience Manager显示 `SERVER_ERROR` 在 **[!UICONTROL 链接外部文件和文件夹]** 屏幕时， `/content/dam/collections`.

* 启用 **[!UICONTROL 将资产发布到Brand Portal]** Workfront增强连接器配置页面上的选项会创建错误事件。 即使在禁用选项后，该事件也不会被删除。

   要解决此问题，请执行以下操作：

   1. 升级到增强型连接器的1.9.5版。

   1. 禁用 **[!UICONTROL 将资产发布到Brand Portal]** 选项。

   1. 启用 **[!UICONTROL 将资产发布到Brand Portal]** 选项。

   1. 删除错误的事件订阅。

      1. 执行GET调用 `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>`

         为每个页码执行一个API调用。

      1. 搜索以下文本，以查找与以下URL匹配且没有 `objId`:

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         确保 `"objId": "",` 和 `"url"` 与JSON响应匹配。 为此，建议从具有 `objId` 然后删除数字。

      1. 记下事件订阅ID。

      1. 删除错误的事件订阅。 调用删除API `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>`

         `200` 因为响应代码表示成功删除了错误的事件订阅。
   >[!NOTE]
   >
   >如果在执行此过程中所述的步骤之前已删除错误的事件订阅，则可以跳过步骤4。


>[!IMPORTANT]
>
>Adobe建议您 [升级到最新的1.9.5版本](../assets/update-workfront-enhanced-connector.md) 的 [!DNL Workfront for Experience Manager enhanced connector].

## 已知问题 {#known-issues}

* 使用AEM 6.4配置项目链接文件夹时，Experience Manager不会保存 **[!UICONTROL 子文件夹]** 和 **[!UICONTROL 在具有项目组合的项目中创建链接文件夹]** 字段。 的值 **[!UICONTROL 子文件夹]** 字段更新至 **[!UICONTROL 未定义]** 和 **[!UICONTROL 在具有项目组合的项目中创建链接文件夹]** 字段更新至 **[!UICONTROL 默认Portfolio]** 自动。

* 当您使用经典Workfront体验时， **[!UICONTROL 发送到]** 选项 **[!UICONTROL 更多]** 下拉列表不允许您在Experience Manager中选择目标目标。 的 **[!UICONTROL 发送到]** 选项可使用 **[!UICONTROL 文档操作]** 下拉列表。 的 **[!UICONTROL 发送到]** 选项可正确用于 **[!UICONTROL 更多]** 下拉列表以及 **[!UICONTROL 文档操作]** 新Workfront体验中提供的下拉列表。

## 以前版本 {#previous-releases}

### 2022年10月版 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.4（于2007年10月发布）包含以下更新：

* 由于事件数量很大，无法在增强型连接器配置页面上查看事件订阅选项卡。

* Workfront无法获取项目中现有文件夹的列表，这会导致创建重复的文件夹。

### 2022年9月版 {#september-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.3（于9月16日发布）包含以下更新：

* 无法上载大小超过8 GB的文件。
* 自动发布从Workfront发送到AEM的资产时出现问题。
* 编辑默认元数据架构表单时，根路径字段不可用于标记字段。
* 使用AEM工作流在Workfront中添加新版本时出现问题。
* 在您搜索Workfront中可用的资产时，AEM会显示一条错误消息。
* 当您为从资产创建任务创建AEM工作流，但未定义父任务名称时，不会在Workfront中创建任务。

### 2022年8月版 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.2（于2003年8月发布）包含以下更新：

* 的 **[!UICONTROL 上载文档]** 工作流步骤无法将文档附加到Workfront。

* 的 **[!UICONTROL 上载文档]** 工作流步骤无法将文档附加到Workfront中的任务和问题。 工作流步骤可成功将文档附加到项目。

### 2022年7月版 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 版本1.9.1包含以下更新：

* 为迁移到Adobe IMS的实例添加了对使用Workfront API密钥的Experience Manager和Workfront应用程序之间身份验证的支持。

* 链接外部文件或文件夹时，Workfront应用程序会显示 `SERVER_ERROR` 错误消息。 错误消息是指由于API密钥不匹配而导致的未授权异常。

* 为资产执行创建任务工作流时，日志消息中会显示空指针异常。

* 当您启用 `Replace Spaces with DASH` 配置选项中“Experience Manager中的高级设置”下，会导致在Workfront中创建重复的文件夹。

### 2022年6月版 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 现在包括以下更新：

* 当您通过链接的文件夹上传或使用 `Send To` Workfront中可用于将资产上传到Experience Manageras a Cloud Service的操作，导致资产损坏，无法在Adobe Photoshop中打开。

### 2022年3月版 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 现在包括以下更新：

* 现在，即使存在多个项目链接文件夹配置，您也可以在Adobe Workfront和AEM Assetsas a Cloud Service之间创建链接文件夹。

* 添加了对事件订阅分页的支持。

* 添加了对AEM 6.4.x的支持。

* 添加了对代理环境的支持。

* 根据合作伙伴和客户反馈进行了若干错误修复。

>[!MORELIKETHIS]
>
>* [集成 [!DNL Workfront for Experience Manager enhanced connector] 与Experience Manager6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [集成 [!DNL Workfront for Experience Manager enhanced connector] 与Experience Manager6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)

