---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.9.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2021.9.0 版的发行说明。'
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 29%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hans)。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新版本(2021.9.0)是2021年10月6日发行的。
以下版本(2021.10.0)发布于2021年11月4日。

## 发布视频 {#release-video}

请查看 [2021年9月版概述](https://video.tv.adobe.com/v/337381) 视频，了解添加的功能摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 的新增功能 [!DNL Sites] 预发行渠道 {#sites-prerelease-features}

* 现在，内容片段模型在发布后会自动设置为只读状态，以避免在重新发布已编辑的模型后无意中中断实时API查询。 尝试编辑已发布的模型时，系统会提示用户显示警告。 接受警告后，即可进行编辑。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 用户现在可以对列视图和卡片视图中搜索结果中显示的资产进行排序。 排序适用于“名称”、“已创建”、“已修改”或“无”列。

   ![在中对搜索结果排序 [!DNL Assets] 在列视图和卡片视图中](/help/assets/assets/sort-searched-assets.png)
   *图：在中对搜索结果排序 [!DNL Assets] 列视图和卡片视图中。*

* 为了以编程方式使用资产微服务调用处理，引入了一个新的API。 开发人员现在可以对文件夹中一个或多个特定资产应用现有文件夹级别的处理配置文件。 将根据自定义元数据属性更新应用处理配置文件。 请参阅 `AssetProcessor` 在 [[!DNL Experience Manager] API参考](https://www.adobe.io/experience-manager/reference-materials/). 与以前一样， [从用户界面使用资产微服务](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-sep-2021}

* **在自适应表单中使用 Adobe Sign 角色**：用于商业和企业服务级别的 Adobe Sign 可让您选择扩展协议接收者的角色（不仅限于签名者），以便更好地匹配他们的工作流要求。您现在可以[允许每个协议接收者在自适应表单中配置自己的角色](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform)，签名者是默认角色。

* **Analytics for Adaptive Forms**：您现在可以通过 Adobe Analytics for Adaptive Forms 捕获和跟踪最终用户行为，从而收集最终用户洞察。这有助于根据数据做出明智的决策，从而改善最终用户体验。

* **轻松地将 AEM Forms 与 Microsoft Dynamics 和 Salesforce 连接**：此服务为 Microsoft Dynamics 和 Salesforce 提供现成的数据源配置和数据模型，使得[开发人员可以更快、更轻松地配置 Microsoft Dynamics 和 Salesforce 作为自适应表单的数据源](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en)。

* **使用 DocuSign 对自适应表单进行电子签名：**&#x200B;您可以使用 DocuSign 对自适应表单进行电子签名。此服务提供了自定义提交操作，可将 DocuSign 与自适应表单结合使用。您可以安装Software Distribution上提供的包以导入提交操作。

### [!DNL Forms] 的 Beta 版功能 {#sep-what-is-new-forms-prerelease}

* **统一存储连接器：**&#x200B;使用统一存储连接器将客户管理的存储库中的进程内数据外部化。例如，您可以
   * 启用 Forms Portal 的保存和恢复功能，将自适应表单草稿存储到客户管理的数据存储库中。
   * 将包含敏感个人数据 (SPD) 的进程内 AEM Workflow 数据（AEM Workflow 变量数据）存储在客户管理的存储库中。

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=en) 帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：
   * 使用 XML 数据填充模板文件来生成文档。
   * 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   * 利用 XFA 表单 PDF 和 Adobe Acrobat 表单生成打印版 PDF 文件。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 站点编辑器中新增的“关联的商务内容”选项卡可快速访问当前上下文的相关AEM产品内容，从而提高创作效率

   ![关联的商务内容](/help/assets/CIF/associated-commerce-content.png)

* 改进了产品选取器UI，以改善用户体验、提高效率并支持复杂的产品目录

   ![新产品选取器](/help/assets/CIF/product-picker.png)

* 在导航组件中遵循“include_in_menu”属性

### 错误修复 {#bug-fixes-cif}

* 菜单缓存刷新无法按预期工作

* 在AEM CS部署步骤和不使用客户端组件时出现JS错误

* 无法在具有sling:configs节点的文件夹中创建CIF云配置

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 新增功能 {#what-is-new-screens}

* 屏幕as a Cloud Service现在支持基本的播放监控。 现在，播放器将报告各种播放量度，并且每次ping（默认为30秒）。 根据这些量度，它能够检测各种边缘情况（体验卡住、空白屏幕、计划问题等）。 此功能允许团队远程监控播放器是否正确播放了内容，提高对空白屏幕或现场中已损坏体验的反应性，并降低向最终用户显示已损坏体验的风险。
请参阅 [基本播放监控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) 以了解更多详细信息。

* 现在，Screensas a Cloud Service支持中对视频的缩略图支持。 内容作者可以为视频定义缩略图，以便图像可用作占位符，并在相应团队最终确定实际视频时，正确测试内容播放和定位。 在视频播放失败时，也可以使用图像。
请参阅 [视频的缩略图支持](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) 以了解更多详细信息。

### 错误修复 {#bug-fixes-screens}

* 播放器无法显示嵌入页面中的内容，此问题现已修复。

* 成功登录后，导航到默认页面（渠道）最终会出现“内部服务器错误”页面。

* 删除播放列表时，未删除关联的标记条目。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager as a Cloud Service] 中的新增功能 {#foundation-features}

**高级网络**

>[!INFO]
>
>2021.9.0版中提供了高级联网功能，该功能将于10月中旬为客户启用。

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 现在提供多种类型的高级联网功能，包括：

* 灵活的端口出口，可将流量从非标准端口输出。 现在，无需联系Adobe支持部门即可。
* 专用出口IP地址，用于从唯一IP中as a Cloud Service出口AEM流量，现在支持所有端口。
* VPN，用于保护基础架构和AEMas a Cloud Service之间的流量。

阅读 [文档](/help/security/configuring-advanced-networking.md) 有关更多信息，包括如何使用Cloud Manager API自助服务配置高级网络。

**索引优化**

为了提高搜索查询和索引的性能，全文索引lucene-2不再在 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 从此版本开始。 为了根据AEM客户在AEM环境中删除此全文索引，Adobe工程部门会单独和主动地与客户合作，以缓慢、持续地删除Lucene全文索引。 请访问 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [文档](/help/operations/indexing.md#index-optimizations) 如有任何问题，请直接联系我们的支持人员，以了解更多信息。

## Cloud Manager {#cloud-manager}

本部分概述了AEM 2021.9.0和2021.8.0版中Cloud Manager的发行说明。

## 发布日期 {#release-date-cm-sept}

AEM 2021.9.0版中Cloud Manager的发布日期是2021年9月9日。
下一版本计划于2021年10月7日发布。

### 新增功能 {#what-is-new-cm-sept}

* Cloud Manager使用的AEM项目原型版本已更新至版本30。

* Cloud Manager登录页面上的项目卡以及关联的体验已刷新。

* 代码质量步骤日志现在包含有关OakPal扫描过程的详细日志记录信息。

* “活动”页面菜单选项现在将包含 **下载日志** 代码生成器执行完成。 选择此选项将下载生成步骤的日志。

* 现在，直接单击项目卡片将导航到Cloud Manager概述页面。

### 错误修复 {#bug-fixes-sept}

* 现在，当用户尝试在程序中添加新的IP允许列表(该程序已达到允许的最大可配置IP允许列表数)时，将看到一条更易理解的消息。

* 从“存储库”屏幕中选择“复制URL”菜单选项时，复制了错误的URL。

## Cloud Acceleration Manager {#cam}

### 发布日期 {#release-date-october-cam}

Cloud Acceleration Manager的发布日期是2021年10月4日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager现在为用户提供了以可打印预览方式查看BPA报表的功能，从而允许简单的打印或打印以PDF以方便共享。 请参阅 [使用最佳实践分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具v1.6.0的发布日期是2021年10月4日。

### 新增功能 {#what-is-new-ctt}

* 通过简化的用户体验改进了用户映射，其中包括以下功能。 有关更多详细信息，请参阅 [使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool).
   * 在运行用户映射之前，测试与用户管理API的连接
   * 优雅地跳过错误并继续“用户映射”活动
   * 如果访问令牌过期（24小时后），用户映射不再失败。 可以从上次停止的位置重新运行用户映射。

* 为了提高CTT稳健性，一次可以将内容摄取到创作实例或发布实例。

* 包含版本时，路径 `/var/audit` 会自动包含在内以迁移审核事件。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.18的发布日期是2021年9月2日。

### 新增功能 {#what-is-new}

* 能够检测并报告节点总数。

* 能够检测并报告节点存储类型和大小。

### 错误修复 {#bug-fixes-bpa}

* BPA错误地检测了Commerce Integration Framework的存在。
