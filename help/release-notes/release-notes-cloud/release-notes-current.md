---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 9eeb47dbca36f1b9f23e3ac4e0bee6594ffb7fda
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 3%

---


# [!DNL Adobe Experience Manager]as a Cloud Service的最新发行说明 {#release-notes}

以下部分概述了[!DNL Experience Manager]as a Cloud Service的当前（最新）版本的常规发行说明。

>[!NOTE]
>
>从此处，您可以导航到以前版本的发行说明；例如，2020年、2021年，等等。

>[!NOTE]
>
>请参阅[近期文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) ，以了解有关与版本不直接相关的文档更新的详细信息。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]的当前版本(2021.9.0)的发布日期是2021年10月6日。
以下版本(2021.10.0)发布于2021年10月28日。

## 发行视频 {#release-video}

请查看[2021年9月版概述](https://video.tv.adobe.com/v/337381)视频，了解所添加功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites]预发行渠道中的新功能 {#sites-prerelease-features}

* 现在，内容片段模型在发布后会自动设置为只读状态，以避免在重新发布已编辑的模型后无意中中断实时API查询。 尝试编辑已发布的模型时，系统会提示用户显示警告。 接受警告后，即可进行编辑。

## [!DNL Experience Manager Assets] as a  [!DNL Cloud Service] {#assets}

### [!DNL Assets]的新增功能 {#assets-features}

* 用户现在可以对列视图和卡片视图中搜索结果中显示的资产进行排序。 排序适用于“名称”、“已创建”、“已修改”或“无”列。

   ![在列视图和卡片视 [!DNL Assets] 图中对搜索结果排序](/help/assets/assets/sort-searched-assets.png)
   *图：在列视图和卡片视 [!DNL Assets] 图中对搜索结果排序。*

<!-- TBD: 'Unpublishing' this feature as suggested by engineering.

* To programmatically invoke processing using asset microservices, a new API is introduced. Developers can now apply an existing folder-level processing profile on one or more specific assets in a folder. The processing profile gets applied based on custom metadata properties updates. See `AssetProcessor` in the [[!DNL Experience Manager] API reference](https://www.adobe.io/experience-manager/reference-materials/). As before, it is possible to [use asset microservices from the user interface](/help/assets/asset-microservices-configure-and-use.md).

-->
<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature via CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms-sep-2021}

* **在自适应表单中使用Adobe Sign角色**:Adobe Sign的业务和企业服务级别可以选择扩展协议收件人的角色，而不仅仅是签名者，以更好地满足其工作流要求。现在，您可以使[的每个协议收件人都能够在自适应表单](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/create-an-adaptive-form/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform)中配置其角色，而签名者是默认角色。

* **用于自适应Forms的Analytics**:您现在可以通过自适 [应Forms的Adobe分析来捕](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/integrate-aem-forms-with-adobe-analytics.html) 获和跟踪最终用户行为，以收集最终用户分析。它有助于根据数据做出明智的决策，以改善最终用户体验。

* **轻松将AEM Forms与Microsoft Dynamics和Salesforce连接**:该服务为Microsoft Dynamics和Salesforce提供了开箱即用的数据源配置和数据模型，使开发人 [员能够更快、更轻松地将Microsoft Dynamics和Salesforce配置为自适应表单的数据源](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/use-form-data-model/configure-msdynamics-salesforce.html?lang=en)。

* **使用DocuSign对自适应表单进行电子签名：** [您可以使用DocuSign对自适应表单进行电子签名](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/integrate-docusign-adaptive-forms.html)。该服务提供自定义提交操作，以便将DocuSign与自适应表单结合使用。

### [!DNL Forms]的测试版功能 {#sep-what-is-new-forms-prerelease}

* **统一存储连接器：** 使用统一存储连接器将客户管理的存储库中的进程中数据外部化。例如，您可以将包含敏感个人数据(SPD)的正在处理的AEM工作流数据(AEM工作流变量数据)存储在客户管理的存储库中。

   <!--* Enable Forms Portal’s save and resume functionality and store adaptive forms drafts in a customer-managed data repository.-->

* **[!DNL AEM Forms as a Cloud Service - Communications]**: [通信](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/aem-forms-cloud-service-communications.html?lang=en) API您可以将XDP模板和XML数据组合在一起，以生成各种格式的打印文档。该服务允许您以同步模式生成文档。 利用API，可创建应用程序，以便：
   * 使用XML数据填充模板文件，以生成文档。
   * 以各种格式生成输出表单，包括非交互式PDF打印流。
   * 从XFA表单PDF和Adobe Acrobat表单生成打印PDF文件。

您可以写信给[!DNL formscsbeta@adobe.com]注册测试版程序。

## CIF附加组件 {#cloud-services-cif}

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

## [!DNL Experience Manager Screens] as a  [!DNL Cloud Service] {#screens}

### 新增功能 {#what-is-new-screens}

* 屏幕as a Cloud Service现在支持基本的播放监控。 现在，播放器将报告各种播放量度，并且每次ping（默认为30秒）。 根据这些量度，它能够检测各种边缘情况（体验卡住、空白屏幕、计划问题等）。 此功能允许团队远程监控播放器是否正确播放了内容，提高对空白屏幕或现场中已损坏体验的反应性，并降低向最终用户显示已损坏体验的风险。
有关更多详细信息，请参阅[基本播放监控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring)。

* 现在，Screensas a Cloud Service支持中对视频的缩略图支持。 内容作者可以为视频定义缩略图，以便图像可用作占位符，并在相应团队最终确定实际视频时，正确测试内容播放和定位。 在视频播放失败时，也可以使用图像。
有关更多详细信息，请参阅[视频的缩略图支持](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html)。

### 错误修复 {#bug-fixes-screens}

* 播放器无法显示嵌入页面中的内容，此问题现已修复。

* 成功登录后，导航到默认页面（渠道）最终会出现“内部服务器错误”页面。

* 删除播放列表时，未删除关联的标记条目。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager as a Cloud Service]的新增功能 {#foundation-features}

**高级网络**

>[!INFO]
>
>2021.9.0版中提供了高级联网功能，该功能将于10月中旬为客户启用。

[!DNL Adobe Experience Manager] as a现 [!DNL Cloud Service] 在提供多种类型的高级联网功能，包括：

* 灵活的端口出口，可将流量从非标准端口输出。 现在，无需联系Adobe支持部门即可。
* 专用出口IP地址，用于从唯一IP中as a Cloud Service出口AEM流量，现在支持所有端口。
* VPN，用于保护基础架构和AEMas a Cloud Service之间的流量。

请阅读[文档](/help/security/configuring-advanced-networking.md)以了解更多信息，包括如何使用Cloud Manager API自助服务配置高级网络。

**索引优化**

为了提高搜索查询和索引的性能，此版本中的[!DNL Adobe Experience Manager]中不再作为[!DNL Cloud Service]的现成索引lucene-2。 为了根据AEM客户在AEM环境中删除此全文索引，Adobe工程部门会单独和主动地与客户合作，以缓慢、持续地删除Lucene全文索引。 有关更多信息，请访问[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [文档](/help/operations/indexing.md#index-optimizations)，如果您有任何问题，请直接联系我们的支持人员。

## Cloud Manager {#cloud-manager}

本部分概述了AEM 2021.9.0和2021.8.0版中Cloud Manager的发行说明。

## 发布日期 {#release-date-cm-sept}

AEM 2021.9.0版中Cloud Manager的发布日期是2021年9月9日。
下一版本计划于2021年10月7日发布。

### 新增功能 {#what-is-new-cm-sept}

* Cloud Manager使用的AEM项目原型版本已更新至版本30。

* Cloud Manager登录页面上的项目卡以及关联的体验已刷新。

* 代码质量步骤日志现在包含有关OakPal扫描过程的详细日志记录信息。

* 现在，“活动”页面菜单选项中将包含一个用于&#x200B;**下载日志**&#x200B;的选项，以执行已完成的代码生成器。 选择此选项将下载生成步骤的日志。

* 现在，直接单击项目卡片将导航到Cloud Manager概述页面。

### 错误修复 {#bug-fixes-sept}

* 现在，当用户尝试在程序中添加新的IP允许列表(该程序已达到允许的最大可配置IP允许列表数)时，将看到一条更易理解的消息。

* 从“存储库”屏幕中选择“复制URL”菜单选项时，复制了错误的URL。

## Cloud Acceleration Manager {#cam}

### 发布日期 {#release-date-october-cam}

Cloud Acceleration Manager的发布日期是2021年10月4日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager现在为用户提供了以可打印预览方式查看BPA报表的功能，从而允许简单的打印或打印以PDF以方便共享。 请参阅[使用最佳实践分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis)中的步骤6和7。

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具v1.6.0的发布日期是2021年10月4日。

### 新增功能 {#what-is-new-ctt}

* 通过简化的用户体验改进了用户映射，其中包括以下功能。 有关更多详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool)。
   * 在运行用户映射之前，测试与用户管理API的连接
   * 优雅地跳过错误并继续用户映射活动
   * 如果访问令牌过期（24小时后），用户映射不再失败。 可以从上次停止的位置重新运行用户映射。

* 为了提高CTT稳健性，一次可以将内容摄取到创作实例或发布实例。

* 包含版本后，将自动包含路径`/var/audit`以迁移审核事件。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.18的发布日期是2021年9月2日。

### 新增功能 {#what-is-new}

* 能够检测并报告节点总数。

* 能够检测并报告节点存储类型和大小。

### 错误修复 {#bug-fixes-bpa}

* BPA错误地检测了Commerce Integration Framework的存在。
