---
title: ' [!DNL Workfront for Experience Manager enhanced connector] 的发行说明'
description: ' [!DNL Workfront for Experience Manager enhanced connector] 的发行说明'
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: b1c5df329e45128704ae82f49673c6a755a61a73
workflow-type: ht
source-wordcount: '1573'
ht-degree: 100%

---

# [!DNL Workfront for Experience Manager enhanced connector] 的发行说明 {#release-notes-enhanced-connector-workfront}

以下部分概述了 [!DNL Workfront for Experience Manager enhanced connector] 的常规发行说明。

## 发布日期 {#release-date}

[!DNL Workfront for Experience Manager enhanced connector] 的最新版本 1.9.16 版的发布日期是 2024 年 1 月 19 日。

## 版本亮点 {#release-highlights}

[!DNL Workfront for Experience Manager enhanced connector] 的最新版本包括以下错误修复：

* [!DNL CRX DE] 中的 [!DNL Workfront] 配置当前未存储 `project ID`，导致应用只读权限时出错。详细了解如何[配置权限](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html#linked-folders)。

* 没有公开的文档涉及如何将自定义属性添加到现成的索引定义。详细了解[添加自定义属性](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/integrations/workfront-connector-configure.html#metadata-schema-mapping)。

* 删除增强型连接器上的连接配置显著影响事件订阅和其他保存的配置，导致其指向旧 URL。

* 安装表单附加组件包却不安装&#x200B;**[!UICONTROL 切换路由器]**，导致 [!DNL WFEC AMS environment Toggle] 功能故障。

* 在 EWC 设置上启用事件订阅导致在首次设置 [!DNL Workfront] 增强型连接器时调用 API 反复失败，发生 `HTTP 400` 错误。

* 在 Workfront 上删除关于链接文件夹资源的评论无法在 AEM 上找到链接文件夹路径。

* AEM 中对大文件资源的支持不足导致 4 字节大小问题。

* 对于链接文件夹、文档更新和注释更新中的关键流程无请求时处理。

>[!NOTE]
>
>AEM 6.4 已结束延期支持。请参阅我们的[技术支持期](https://helpx.adobe.com/cn/support/programs/eol-matrix.html)。请在[此处](https://experienceleague.adobe.com/docs/?lang=en)查找支持的版本。


>[!IMPORTANT]
>
>Adobe 推荐您[升级到 [!DNL Workfront for Experience Manager enhanced connector] 的最新版本 1.9.16 版](/help/assets/workfront-connector-install.md)。

## 已知问题 {#known-issues}

* 在使用 AEM 6.4 配置项目链接文件夹时，Experience Manager 不保存&#x200B;**[!UICONTROL 子文件夹]**&#x200B;和&#x200B;**[!UICONTROL 在具有作品集的项目中创建链接文件夹]**&#x200B;字段的值。在保存配置后，**[!UICONTROL 子文件夹]**&#x200B;字段的值自动更新为&#x200B;**[!UICONTROL 未定义]**，**[!UICONTROL 在具有作品集的项目中创建链接文件夹]**&#x200B;字段的值自动更新为&#x200B;**[!UICONTROL 默认作品集]**。

* 在使用经典 Workfront 体验时，**[!UICONTROL 更多]**&#x200B;下拉列表中的&#x200B;**[!UICONTROL 收件人]**&#x200B;选项不允许您在 Experience Manager 中选择目标目的地。当使用&#x200B;**[!UICONTROL 文档操作]**&#x200B;下拉列表时，**[!UICONTROL 收件人]**&#x200B;选项正常地发挥作用。**[!UICONTROL 更多]**&#x200B;下拉列表和可在新 Workfront 体验中找到的&#x200B;**[!UICONTROL 文档操作]**&#x200B;下拉列表的&#x200B;**[!UICONTROL 收件人]**&#x200B;选项正常地发挥作用。

## 以前的版本 {#previous-releases}

### 2023 年 11 月版本 {#november-2023-release}

* 查看 AEM 文件夹列表时，该对话框需要一分多钟的时间才能加载。
* 授权 [!DNL Workfront] 用户持续收到身份验证失败错误日志。

### 2023 年 10 月版本 {#october-2023-release}

* 在“高级设置”下禁用事件订阅后，仍可选择&#x200B;**订阅文档更新事件以更新 AEM 资源元数据**、**在项目完成后将所有项目资源发布到 Brand Portal** 和&#x200B;**启用评论同步**&#x200B;选项。

* 在 Workfront 中预览 Experience Manager 中存储的某些资源时，这些资源无法正确呈现。

* 重新配置 Experience Manager 与 Workfront 的连接时，未成功创建评论同步更新、删除、文档更新等事件订阅。

* 对于创建、更新链接的文件夹、启用链接的文件夹、启用和禁用评论同步、在连接器上保存高级设置大幅提高了 API 性能。

### 2023 年 9 月版 {#september-2023-release}

* Experience Manager 增强型连接器在删除项目的事件订阅时从 Workfront 获取所有事件订阅，而这影响应用程序的性能。

* 将资源从 Workfront 发送到 Experience Manager 后，在 Experience Manager 中没有将该资源的 MIME 类型设置为 `dc:format` 属性。

* Experience Manager 增强型连接器上存储的 Workfront 项目 ID 包含重复项。

### 2023 年 8 月版本 {#august-2023-release}

* 无法在 Experience Manager 中创建链接文件夹，因为没有与链接文件夹关联的用户帐户。

* 在 Experience Manager 中更新资源的元数据期间发生竞争状况。

### 2023 年 6 月版本 {#june-2023-release}

* 配置高级网络后，将内容从 Adobe Workfront 发送到 AEM as a Cloud Service 时出现问题。


### 2023 年 5 月版本 {#may-2023-release}

* Workfront 根据从 Experience Manager 到 Workfront 的 REST 调用为重复事件订阅返回 409 HTTP 响应，而这导致 null 指针异常。

### 2023 年 4 月版本 {#april-2023-release}

2023 年 4 月 10 日发布的 [!DNL Workfront for Experience Manager enhanced connector] 1.9.9 版本包括以下更新：

* Experience Manager 在创建链接文件夹期间从 Workfront 收到上次修改日期时显示 `DateTimeParseException` 异常。

* 在短时间内创建多个链接的项目文件夹时出现问题。

* 无法针对新的一组项目链接文件夹的数量配置阈值限制。

### 2023 年 3 月版本 {#march-2023-release}

2023 年 3 月 3 日发布的 [!DNL Workfront for Experience Manager enhanced connector] 1.9.8 版本包括以下更新：

* 提高了在 Workfront 中创建项目链接文件夹时 Experience Manager 中的性能。

* 在 Workfront 中删除评论现在可反映在 Experience Manager 中。

* 可管理是否阻止 Experience Manager as a Cloud Service 上的全新客户配置连接器。


### 2023 年 1 月版本 {#january-2022-release}

2023 年 2 月 2 日发布的 [!DNL Workfront for Experience Manager enhanced connector] 1.9.7 版本包括以下更新：

* 安装 1.9.6 版本后，元数据编辑器不列出 Workfront 自定义表单属性。

* 安装 Workfront 增强型连接器并打开 Assets 主页后，开发控制台显示 `/content/dam/jcr:content/metadata/wfProjectURL not found` 错误消息。

### 2022 年 12 月版本 {#december-2022-release}

12 月 9 日发布的 [!DNL Workfront for Experience Manager enhanced connector] 1.9.6 版本包括以下更新：

**增强**

<!--

* Workfront enhanced connector now lets you use new search parameters to be more specific while defining folder names on large repositories.

-->

* Workfront 增强型连接器现在支持对资源和文件夹执行全文搜索。

**错误修复**

* 在 Workfront 与 Experience Manager 之间未正确同步“文档版本”元数据。
* 在 Workfront 中创建链接到 Experience Manager 的文件夹且该文件夹使用在全局配置中缺少定义的架构时出现问题。
* 单击任意字段后，因加载时间比预期的长，元数据架构编辑器表单停止响应。为自定义表单添加了特定的 OSGi 配置以解决该问题。可在日志中找到添加到元数据架构编辑器的自定义表单的名称。

### 2022 年 11 月版本 {#november-2022-release}

11 月 11 日发布的 [!DNL Workfront for Experience Manager enhanced connector] 1.9.5 版本包括以下更新：

* 在 Workfront 中为多值字段仅定义一个值时，未正确地将该字段值映射到 Experience Manager。

* 在访问资源文件夹时，因对 `/content/dam/collections` 的权限无效，Experience Manager 在&#x200B;**[!UICONTROL 链接外部文件和文件夹]**&#x200B;屏幕上显示 `SERVER_ERROR`。

* 启用 Workfront 增强型连接器配置页面上的&#x200B;**[!UICONTROL 将资源发布到 Brand Portal]** 选项产生不正确的事件。即使在禁用该选项后也未删除该事件。

  要解决该问题，请执行以下操作：

   1. 升级到增强型连接器的 1.9.5 版本。

   1. 在高级设置下禁用&#x200B;**[!UICONTROL 将资源发布到 Brand Portal]** 选项。

   1. 启用&#x200B;**[!UICONTROL 将资源发布到 Brand Portal]** 选项。

   1. 删除错误的事件订阅。

      1. 对 `/attask/eventsubscription/api/v1/subscriptions?page=<page-number>` 调用 GET

         为每个页码执行一个 API 调用。

      1. 搜索以下文本以查找与以下 URL 匹配且没有 `objId` 的事件订阅：

         ```
              "objId": "",
             "url": "<your-aem-domain>/bin/workfront-tools/events/linkedfolderprojectupdate<your-aem-domain>/
         ```

         确保 `"objId": "",` 和 `"url"` 之间的内容与 JSON 响应匹配。为此建议的方法是从任何具有 `objId` 的事件订阅复制，然后删除该编号。

      1. 记下事件订阅 ID。

      1. 删除错误的事件订阅。对 `<your-aem-domain>/attask/eventsubscription/api/v1/subscriptions/<event-subscription-ID-from-previous-step>` 调用删除 API

         `200` 作为响应代码表示成功删除了错误的事件订阅。
  >[!NOTE]
  >
  >如果在执行本过程中提到的步骤之前已经删除了错误的事件订阅，则可以跳过本过程的最后一步。

### 2022 年 10 月版本 {#october-2022-release}

10 月 7 日发布的 [!DNL Workfront for Experience Manager enhanced connector] 1.9.4 版本包括以下更新：

* 由于事件太多，无法查看增强型连接器配置页面上的“事件订阅”选项卡。

* Workfront 无法获取项目中现有文件夹的列表，而这导致创建重复的文件夹。

### 2022 年 9 月版 {#september-2022-release}

9 月 16 日发布的 [!DNL Workfront for Experience Manager enhanced connector] 1.9.3 版本包括以下更新：

* 无法上传超过 8 GB 的文件。
* 自动发布从 Workfront 发送到 AEM 的资源时出现问题。
* 编辑默认元数据架构表单时，“标记”字段无“根路径”字段可用。
* 使用 AEM 工作流在 Workfront 中添加新版本时出现问题。
* 对可在 Workfront 中找到的资源执行 AEM 搜索时，AEM 显示一条错误消息。
* 当创建一个从资源创建任务的 AEM 工作流且未定义父任务名称时，在 Workfront 中不创建任务。

### 2022 年 8 月版本 {#august-2022-release}

8 月 3 日发布的 [!DNL Workfront for Experience Manager enhanced connector] 1.9.2 版本包括以下更新：

* **[!UICONTROL 上传文档]**&#x200B;工作流步骤未能将文档附加到 Workfront。

* **[!UICONTROL 上传文档]**&#x200B;工作流步骤未能将文档附加到 Workfront 中的“任务和问题”。工作流步骤成功地将文档附加到“项目”。

### 2022 年 7 月版本 {#july-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 1.9.1 版包括以下更新：

* 为迁移到 Adobe IMS 的实例添加了对于使用 Workfront API 密钥在 Experience Manager 与 Workfront 应用程序之间进行身份验证的支持。

* 当链接外部文件或文件夹时，Workfront 应用程序显示 `SERVER_ERROR` 错误信息。该错误消息表示因 API 密钥中存在不匹配，产生未经授权的异常。

* 为资源执行“创建任务”工作流时，在日志消息中显示“Null 指针”异常。

* 在 Experience Manager 中的“高级设置”下启用 `Replace Spaces with DASH` 配置选项时，导致在 Workfront 中创建重复的文件夹。

### 2022 年 6 月版本 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 现在包括以下更新：

* 当通过链接文件夹上传或使用可在 Workfront 中找到的 `Send To` 操作将资源上传到 Experience Manager as a Cloud Service 时，该资源损坏，无法在 Adobe Photoshop 中打开该资源。

### 2022 年 3 月版本 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] 现在包括以下更新：

* 即使有多个项目链接文件夹配置，您现在也可以在 Adobe Workfront 和 AEM Assets as a Cloud Service 之间创建链接文件夹。

* 添加了对事件订阅分页的支持。

* 添加了对 AEM 6.4.x 的支持。

* 添加了对代理环境的支持。

* 根据合作伙伴和客户反馈修复了若干错误。

>[!MORELIKETHIS]
>
>* [将 [!DNL Workfront for Experience Manager enhanced connector] 与 Experience Manager 6.5 集成](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=zh-Hans)
