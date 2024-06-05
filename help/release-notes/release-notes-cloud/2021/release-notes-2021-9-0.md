---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.9.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.9.0 版的发行说明。'
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 20%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>从此处，您可以导航到以前版本的发行说明；例如，2020版和2021版的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的发布日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前版本(2021.9.0)为2021年10月6日。
以下版本(2021.10.0)的发布日期为2021年11月4日。

## 发布视频 {#release-video}

请查看 [2021年9月发行版概述](https://video.tv.adobe.com/v/337381) 视频以了解新增功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 的新增功能 [!DNL Sites] 预发行渠道 {#sites-prerelease-features}

* 内容片段模型现在在发布后自动设置为只读状态，以避免在重新发布已编辑的模型后无意中中断实时API查询。 在尝试编辑已发布的模型时，系统会提示用户并显示警告。 接受警告时可以进行编辑。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 用户现在可以对列视图和卡片视图的搜索结果中显示的资源进行排序。 排序仅对名称、创建、修改或无列起作用。

  ![将搜索结果排序于 [!DNL Assets] 在列视图和卡片视图中](/help/assets/assets/sort-searched-assets.png)
  *图：对搜索结果排序 [!DNL Assets] 在“列”和“卡片”视图中。*

* 为了以编程方式使用资产微服务调用处理，引入了一个新的API。 开发人员现在可以对文件夹中的一个或多个特定资产应用现有的文件夹级别处理配置文件。 处理配置文件将根据自定义元数据属性更新进行应用。 请参阅 `AssetProcessor` 在 [[!DNL Experience Manager] API参考](https://developer.adobe.com/experience-manager/reference-materials/). 和以前一样，可以 [从用户界面使用资源微服务](/help/assets/asset-microservices-configure-and-use.md).

<!-- Leave this commented.

### New feature in the [!DNL Assets] prerelease channel {#assets-prerelease-features}

Apparently, no new Assets features in Sep beta channel.
A/V transcription feature by way of CQ-4303854 has moved to Oct beta now.

### Bugs fixed in [!DNL Assets] {#assets-bugs-fixed}

No customer-reported bugs fixed in Sep release.
CQ-4328183 was not reported on CS so not documented here.
-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms-sep-2021}

* **在自适应表单中使用Adobe Sign角色**  — 用于商业和企业服务级别的Adobe Sign允许您选择扩展协议接受者的角色，而不只是签名者角色，以便更好地匹配他们的工作流要求。 您现在可以 [使每个协议接收者在自适应表单中配置自己的角色](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html#addsignerstoanadaptiveform)，签名者是默认角色。

* **Analytics for Adaptive Forms**  — 您现在可以通过Adobe Analytics for Adaptive Forms捕获和跟踪最终用户行为，从而收集最终用户洞察。 这有助于根据数据做出明智的决策，从而改善最终用户体验。

* **轻松地将Adobe Experience Manager (AEM) Forms与Microsoft® Dynamics和Salesforce连接**  — 该服务为Microsoft®Dynamics和Salesforce提供现成的数据源配置和数据模型。 这就使它 [开发人员可以更快、更轻松地将Microsoft®Dynamics和Salesforce配置为自适应表单的数据源](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html).

* **使用DocuSign对自适应表单进行电子签名**  — 您可以使用DocuSign对自适应表单进行电子签名。 该服务提供了自定义提交操作，可将DocuSign与自适应表单结合使用。 您可以安装Software Distribution上提供的软件包以导入提交操作。

### [!DNL Forms] 的 Beta 版功能 {#sep-what-is-new-forms-prerelease}

* **统一存储连接器**  — 使用统一存储连接器将客户管理的存储库中的进程内数据外部化。 例如，您可以
   * 启用 Forms Portal 的保存和恢复功能，将自适应表单草稿存储到客户管理的数据存储库中。
   * 将包含敏感个人数据 (SPD) 的进程内 AEM Workflow 数据（AEM Workflow 变量数据）存储在客户管理的存储库中。

* **[!DNL AEM Forms as a Cloud Service - Communications]** - [通信API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) 帮助您组合XDP模板和XML数据以生成各种格式的打印文档。 该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：
   * 使用 XML 数据填充模板文件来生成文档。
   * 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   * 利用 XFA 表单 PDF 和 Adobe Acrobat 表单生成打印版 PDF 文件。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* AEM Sites编辑器中新的“关联的商业内容”选项卡通过快速访问当前上下文的相关AEM产品内容来提高创作效率

  ![关联的商务内容](/help/assets/CIF/associated-commerce-content.png)

* 改进了产品选取器UI，以提供更好的用户体验、更高的效率并支持复杂的产品目录

  ![新产品选取器](/help/assets/CIF/product-picker.png)

* 在导航组件中遵循“include_in_menu”属性

### 错误修复 {#bug-fixes-cif}

* 菜单缓存刷新未按预期工作

* AEM CS部署步骤期间以及不使用客户端组件时出现JS错误

* 无法在具有sling：configs节点的文件夹中创建CIF云配置

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 新增功能 {#what-is-new-screens}

* Screensas a Cloud Service现在支持基本回放监控。 播放器现在报告每次ping（默认为30秒）的各种回放指标。 它可以基于指标检测各种边缘情况（卡住体验、空白屏幕、调度问题等）。 团队可以使用此功能远程监控播放器是否正确播放内容。 它提高了对空白屏幕或现场中断体验的反应性，并降低了向用户显示中断体验的风险。
请参阅 [基本回放监控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html#playback-monitoring) 以了解更多详细信息。

* Screensas a Cloud Service中现在支持视频缩略图。 内容作者可以定义视频的缩略图，以便在相应团队最终确定实际视频时，将图像用作占位符并正确测试内容播放和定位。 在视频播放失败时，也可以使用该图像。
请参阅 [视频的缩略图支持](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) 以了解更多详细信息。

### 错误修复 {#bug-fixes-screens}

* 播放器无法显示嵌入页面中的内容，此问题现已修复。

* 成功登录后，导航到默认页面（渠道）最后会进入内部服务器错误页面。

* 删除播放列表时未删除关联的标记条目。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager as a Cloud Service] 中的新增功能 {#foundation-features}

**高级网络**

>[!INFO]
>
>高级联网功能是2021.9.0版本的一部分，于2021年10月中旬为客户启用。

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 现在提供了多种高级联网功能，包括：

* 灵活端口出口，将流量输出到非标准端口。 现在无需联系Adobe支持即可实现。
* 专用出口IP地址用于输出as a Cloud Service于唯一IP的AEM流量，现在支持所有端口。
* VPN用于保护您的基础设施与AEMas a Cloud Service之间的流量。

阅读 [文档](/help/security/configuring-advanced-networking.md) 有关更多信息（包括如何使用Cloud Manager API自助配置高级网络）。

**索引优化**

为了提高搜索查询和索引的性能，不再在中现成使用全文索引lucene-2 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 此版本中的。 为了根据AEM客户在AEM环境中删除此全文索引，Adobe工程部单独并主动与客户合作，以温和且可持续的方式删除Lucene全文索引。 访问 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [文档](/help/operations/indexing.md#index-optimizations) 有关更多信息，如有疑问，请直接联系Adobe的支持部门。

## Cloud Manager {#cloud-manager}

本节概述了AEMas a Cloud Service2021.9.0和2021.8.0中的Cloud Manager发行说明。

## 发布日期 {#release-date-cm-sept}

AEMas a Cloud Service2021.9.0中的Cloud Manager的发布日期是2021年9月9日。
下一个版本计划于2021年10月7日发布。

### 新增功能 {#what-is-new-cm-sept}

* Cloud Manager 使用的 AEM 项目原型的版本已更新到版本 30。

* Cloud Manager 登陆页面上的程序信息卡和相关体验都已更新。

* 代码质量步骤日志现在包括有关 OakPal 扫描过程的详细日志信息。

* 活动页面菜单选项现在包括一个选项，用于&#x200B;**下载已完成的代码生成器执行的日志。** 选择此选项可下载构建步骤的日志。

* 直接点击程序卡，现在可导航至Cloud Manager概述页面。

### 错误修复 {#bug-fixes-sept}

* 列入允许列表 列入允许列表现在，当用户尝试在已达到可配置的最大允许IP数量的程序中添加IP时，会看到一条更易于理解的消息。

* 从存储库屏幕选择复制URL菜单选项时复制了错误的URL。

## Cloud Acceleration Manager {#cam}

### 发布日期 {#release-date-october-cam}

Cloud Acceleration Manager的发布日期是2021年10月4日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager现在使用户能够在可打印预览中查看BPA报告，从而允许简单打印或打印以PDF以便于共享。 请参阅中的步骤6和7 [使用“最佳实践分析”卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-readiness-phase.html#best-practices-analysis).

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具版本1.6.0的发布日期为2021年10月4日。

### 新增功能 {#what-is-new-ctt}

* 通过简化的用户体验改进了用户映射，包括以下列出的功能。 有关更多详细信息，请参阅 [使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/legacy-user-mapping-tool/using-user-mapping-tool-legacy.html#using-user-mapping-tool).
   * 在运行用户映射之前测试与用户管理API的连接
   * 正常跳过错误并继续用户映射活动
   * 如果访问令牌过期（24小时后），用户映射不再失败。 可以从上次停止的位置重新运行用户映射。

* 为了提高CTT的稳健性，可将内容一次摄取到“创作”实例或“发布”实例。

* 当包含版本时，路径 `/var/audit` 将自动包含以迁移审核事件。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.18的发布日期是2021年9月2日。

### 新增功能 {#what-is-new}

* 能够检测和报告节点总数。

* 能够检测和报告节点存储类型和大小。

### 错误修复 {#bug-fixes-bpa}

* BPA错误地检测到Commerce integration framework的存在。
