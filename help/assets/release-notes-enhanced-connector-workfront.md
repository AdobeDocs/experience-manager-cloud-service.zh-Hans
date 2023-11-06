---
title: 的发行说明 [!DNL Workfront for Experience Manager enhanced connector]
description: 的发行说明 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: f5f2c460815d273fe445c6f415dee7776cc18fce
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 100%

---

#  的发行说明[!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

以下部分概述了 [!DNL Workfront for Experience Manager enhanced connector] 的常规发行说明。

## 发布日期 {#release-date}

[!DNL Workfront for Experience Manager enhanced connector] 的最新版本 1.9.14 版的发布日期是 2023 年 10 月 13 日。

## 版本亮点 {#release-highlights}

[!DNL Workfront for Experience Manager enhanced connector] 的最新版本包括以下错误修复：

* 在高级设置下禁用事件订阅后，您仍可以选择选项以&#x200B;**订阅文档更新事件以更新 AEM 资源元数据**、**在项目完成后将所有项目资源发布到 Brand Portal**&#x200B;和&#x200B;**启用评论同步。**

* 在 Workfront 中预览 Experience Manager 中存储的某些资源时，这些资源无法正确呈现。

* 重新配置 Experience Manager 与 Workfront 的连接时，未成功创建评论同步更新、删除、文档更新等事件订阅。

* 主要 API 性能改进，针对链接的文件夹创建、更新、启用链接的文件夹、评论同步启用和禁用、连接器上的高级设置保存。


>[!NOTE]
>
>AEM 6.4 的扩展支持已结束。有关详细信息，请参阅我们的[技术支持期](https://helpx.adobe.com/cn/support/programs/eol-matrix.html)。在[这里](https://experienceleague.adobe.com/docs/?lang=en)找到支持的版本。


>[!IMPORTANT]
>
>Adobe 推荐您[升级到 [!DNL Workfront for Experience Manager enhanced connector] 的最新版本 1.9.14 版。](/help/assets/workfront-connector-install.md)

## 已知问题 {#known-issues}

* 在使用 AEM 6.4 配置项目链接文件夹时，Experience Manager 不会保存&#x200B;**[!UICONTROL 子文件夹]**&#x200B;以及&#x200B;**[!UICONTROL 在具有项目组合的项目中创建链接文件夹]**&#x200B;字段的值。**[!UICONTROL 子文件夹]**&#x200B;字段的值更新为&#x200B;**[!UICONTROL 未定义]**，在&#x200B;**[!UICONTROL 具有项目组合的项目中创建链接文件夹]**&#x200B;字段的值在保存配置后自动更新为&#x200B;**[!UICONTROL 默认项目组合。]**

* 在使用经典 Workfront 体验时，**[!UICONTROL 更多]**&#x200B;下拉列表中的&#x200B;**[!UICONTROL 收件人]**&#x200B;选项不允许您在 Experience Manager 中选择目标目的地。可在&#x200B;**[!UICONTROL 文档操作]**&#x200B;下拉列表中正常使用&#x200B;**[!UICONTROL 收件人]**&#x200B;选项。**[!UICONTROL 收件人]**&#x200B;选项适用于&#x200B;**[!UICONTROL 更多]**&#x200B;下拉列表和新 Workfront 体验中可用的&#x200B;**[!UICONTROL 文档操作]**&#x200B;下拉列表。

## 之前的版本 {#previous-releases}

### 2023 年 9 月版 {#september-2023-release}

* Experience Manager 增强型连接器会从 Workfront 中获取所有事件订阅，同时删除项目的事件订阅，这将影响应用程序的性能。

* 在将资源从 Workfront 发送到 Experience Manager 时，未在 Experience Manager 中将资源 MIME 类型设置为 `dc:format` 属性。

* Experience Manager 增强型连接器上存储的 Workfront 项目 ID 包含重复项。

### 2023 年 8 月版本 {#august-2023-release}

* 无法在 Experience Manager 中创建链接文件夹，因为没有与链接文件夹关联的用户帐户。

* 更新 Experience Manager 中资源的元数据期间的竞争条件。

### 2023 年 6 月版本 {#june-2023-release}

* 配置高级网络后，将内容从 Adobe Workfront 发送到 AEM as a Cloud Service。


### 2023 年 5 月版本 {#may-2023-release}

* Workfront 根据从 Experience Manager 到 Workfront 的 REST 调用为重复事件订阅返回 409 HTTP 响应，这将导致空指针异常。

### 2023 年 4 月版本 {#april-2023-release}

[!DNL Workfront for Experience Manager enhanced connector]2023 年 4 月 10 日发布的 1.9.9 版本包含以下更新：

* Experience Manager 在创建链接文件夹期间从 Workfront 收到上次修改日期时显示 `DateTimeParseException` 异常。

* 在短时间内创建多个链接的项目文件夹时出现问题。

* 无法为新的项目链接文件夹集的数量配置阈值限制。

### 2023 年 3 月版本 {#march-2023-release}

[!DNL Workfront for Experience Manager enhanced connector]2023 年 3 月 3 日发布的 1.9.8 版本包括以下更新：

* 在 Workfront 中创建项目链接文件夹时，Experience Manager 的性能得到改进。

* Workfront 中的评论删除现已反映在 Experience Manager 中。

* 能够对阻止 Experience Manager as a Cloud Service 的全新客户配置连接器进行管理。


### 2023 年 1 月版本 {#january-2022-release}

[!DNL Workfront for Experience Manager enhanced connector]2023 年 2 月 2 日发布的 1.9.7 版本包括以下更新：

* 安装 1.9.6 版本后，元数据编辑器不会列出 Workfront 自定义表单属性。

* 安装 Workfront 增强型连接器并打开 Assets 主页后，开发控制台显示 `/content/dam/jcr:content/metadata/wfProjectURL not found` 错误消息。

### 2022 年 12 月版本 {#december-2022-release}

[!DNL Workfront for Experience Manager enhanced connector]12 月 9 日发布的 1.9.6 版本包括以下更新：

**增强功能**

<!--

* Workfront enhanced connector now lets you use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront 增强型连接器现在支持对资源和文件夹执行全文搜索。

**错误修复**

* 文档版本元数据未在 Workfront 和 Experience Manager 之间正确同步。
* 在文件夹使用的架构在全局配置中缺少定义的情况下，创建链接到 Workfront 中的 Experience Manager 的文件夹时出现问题。
* 由于加载时间长于预期时间，导致元数据架构编辑器表单在您单击任意字段时停止响应。为自定义表单添加了特定的 OSGi 配置来解决该问题。日志中包含了您添加到元数据架构编辑器的自定义表单的名称。

### 2022 年 11 月版本 {#november-2022-release}

[!DNL Workfront for Experience Manager enhanced connector]11 月 11 日发布的 1.9.5 版本包括以下更新：

* 当您在 Workfront 中为多值字段仅定义一个值时，该字段值无法正确映射到 Experience Manager。

* Experience Manager 在访问资源文件夹时，由于对 `/content/dam/collections` 的权限无效，会在&#x200B;**[!UICONTROL 链接外部文件和文件夹]**&#x200B;屏幕上显示 `SERVER_ERROR`。

* 启用 Workfront 增强型连接器配置页面上的&#x200B;**[!UICONTROL 将资源发布到 Brand Portal]** 选项会产生不正确的事件。即使禁用该选项后，该事件也不会被删除。

  如要解决该问题：

   1. 升级到 1.9.5 版本的增强型连接器。

   1. 在高级设置下禁用&#x200B;**[!UICONTROL 将资源发布到 Brand Portal]** 选项。

   1. 启用&#x200B;**[!UICONTROL 将资源发布到 Brand Portal]**&#x200B;选项。

   1. 删除错误的事件订阅。

      1. 对 `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>` 执行 GET 调用

         对每个页码执行一次 API 调用。

      1. 搜索以下文本以查找与以下 URL 匹配且没有 `objId` 的事件订阅：

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         确保 `"objId": "",` 和 `"url"` 之间的内容与 JSON 响应匹配。建议的方法是从任何具有 `objId` 的事件订阅中进行复制，然后删除该编号。

      1. 记下事件订阅 ID。

      1. 删除错误的事件订阅。对 `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>` 进行 Delete API 调用

         `200` 作为响应代码表示成功删除了错误的事件订阅。
  >[!NOTE]
  >
  >如果在执行本过程中提到的步骤之前已经删除了错误的事件订阅，则可以跳过本过程的最后一步。

### 2022 年 10 月版本 {#october-2022-release}

[!DNL Workfront for Experience Manager enhanced connector]10 月 7 日发布的 1.9.4 版本包括以下更新：

* 由于事件太多，无法查看增强型连接器配置页面上的“事件订阅”选项卡。

* Workfront 无法获取项目中现有文件夹的列表，这会导致创建重复文件夹。

### 2022 年 9 月版 {#september-2022-release}

9 月 16 日发布的 [!DNL Workfront for Experience Manager enhanced connector] 1.9.3 版本包括以下更新：

* 无法上传超过 8 GB 的文件。
* 自动发布从 Workfront 发送到 AEM 的资源时出现问题。
* 编辑默认元数据架构表单时，“根路径”字段不可用于“标记”字段。
* 使用 AEM 工作流在 Workfront 中添加新版本时出现问题。
* 当您对 Workfront 中的可用资源执行 AEM 搜索时，AEM 会显示一条错误消息。
* 当您从资源创建 AEM 工作流任务，并且没有定义父任务名称时，不会在 Workfront 中创建任务。

### 2022 年 8 月版本 {#august-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.2 版本于 8 月 3 日发布，其中包括以下更新：

* **[!UICONTROL 上传文件]**&#x200B;工作流步骤无法将文档附加到 Workfront。

* **[!UICONTROL 上传文件]**&#x200B;工作流步骤无法将文档附加到任务以及 Workfront 中的问题。工作流步骤成功地将文档附加到项目。

### 2022 年 7 月版本 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.1 版包括以下更新：

* 使用 Workfront API 密钥为迁移到 Adobe IMS 的实例添加了对 Experience Manager 和 Workfront 应用程序之间身份验证的支持。

* 当您链接外部文件或文件夹时，Workfront 应用程序会显示 `SERVER_ERROR` 错误信息。错误消息指的是由于 API 密钥不匹配而导致的未经授权的异常。

* 为资源执行“创建任务”工作流时，“空指针”异常会显示在日志消息中。

* 当您在 Experience Manager 的高级设置中启用 `Replace Spaces with DASH` 配置选项时，会导致在 Workfront 中创建重复的文件夹。

### 2022 年 6 月版本 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 现在包括以下更新：

* 当您通过链接文件夹上传或使用 Workfront中的 `Send To` 操作将资源上传到 Experience Manager as a Cloud Service 时，资源会被损坏，并且无法在 Adobe Photoshop 中打开。

### 2022 年 3 月版本 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 现在包括以下更新：

* 即使有多个项目链接文件夹配置，您现在也可以在 Adobe Workfront 和 AEM Assets as a Cloud Service 之间创建链接文件夹。

* 添加了对事件订阅分页的支持。

* 添加了对 AEM 6.4.x 的支持。

* 添加了对代理环境的支持。

* 根据合作伙伴和客户的反馈修复了几个错误。

>[!MORELIKETHIS]
>
>* [与  [!DNL Workfront for Experience Manager enhanced connector] Experience Manager 6.5 ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=zh-Hans)集成
