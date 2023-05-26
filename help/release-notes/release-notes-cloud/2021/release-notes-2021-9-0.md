---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.9.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.9.0 版的发行说明。'
exl-id: 8c12ff09-fbc8-42dd-87c0-46e509604f36
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 38%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的发布日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前版本(2021.9.0)为2021年10月6日。
以下版本(2021.10.0)的发布日期为2021年11月4日。

## 发布视频 {#release-video}

请查看 [2021年9月发行版概述](https://video.tv.adobe.com/v/337381) 视频，以了解新增功能的摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 的新增功能 [!DNL Sites] 预发行渠道 {#sites-prerelease-features}

* 现在，内容片段模型发布后会自动设置为只读状态，以避免重新发布已编辑的模型后无意间中断实时API查询。 在尝试编辑已发布的模型时，系统会提示用户并发出警告。 接受警告后可进行编辑。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 用户现在可以对列视图和卡片视图的搜索结果中显示的资源进行排序。 排序仅对名称、创建、修改或无列起作用。

   ![将搜索结果排序于 [!DNL Assets] 在“列”和“卡片”视图中](/help/assets/assets/sort-searched-assets.png)
   *图：将搜索结果排序于 [!DNL Assets] 在“列”和“卡片”视图中。*

* 为了以编程方式使用资源微服务调用处理，引入了一个新的API。 开发人员现在可以对文件夹中的一个或多个特定资产应用现有的文件夹级别处理配置文件。 处理配置文件将根据自定义元数据属性更新进行应用。 参见 `AssetProcessor` 在 [[!DNL Experience Manager] API参考](https://www.adobe.io/experience-manager/reference-materials/). 和以前一样，可以 [从用户界面使用资源微服务](/help/assets/asset-microservices-configure-and-use.md).

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

* **使用 DocuSign 对自适应表单进行电子签名：**&#x200B;您可以使用 DocuSign 对自适应表单进行电子签名。此服务提供了自定义提交操作，可将 DocuSign 与自适应表单结合使用。您可以安装Software Distribution上可用的软件包以导入提交操作。

### [!DNL Forms] 的 Beta 版功能 {#sep-what-is-new-forms-prerelease}

* **统一存储连接器：**&#x200B;使用统一存储连接器将客户管理的存储库中的进程内数据外部化。例如，您可以
   * 启用 Forms Portal 的保存和恢复功能，将自适应表单草稿存储到客户管理的数据存储库中。
   * 将包含敏感个人数据 (SPD) 的进程内 AEM Workflow 数据（AEM Workflow 变量数据）存储在客户管理的存储库中。

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[通信 API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications.html) 帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：
   * 使用 XML 数据填充模板文件来生成文档。
   * 生成各种格式的输出表单，包括非交互式 PDF 打印流。
   * 利用 XFA 表单 PDF 和 Adobe Acrobat 表单生成打印版 PDF 文件。

您可以将电子邮件发送到 [!DNL formscsbeta@adobe.com] 以注册 Beta 项目。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 站点编辑器中新的“关联的商业内容”选项卡通过快速访问当前上下文的相关AEM产品内容来提高创作效率

   ![关联的商务内容](/help/assets/CIF/associated-commerce-content.png)

* 改进了产品选取器UI，提供了更好的用户体验、更高的效率和对复杂产品目录的支持

   ![新产品选取器](/help/assets/CIF/product-picker.png)

* 在导航组件中遵守“include_in_menu”属性

### 错误修复 {#bug-fixes-cif}

* 菜单缓存刷新未按预期工作

* AEM CS部署步骤期间以及不使用客户端组件时出现JS错误

* 无法在具有sling：configs节点的文件夹中创建CIF云配置

## [!DNL Experience Manager Screens] as a [!DNL Cloud Service] {#screens}

### 新增功能 {#what-is-new-screens}

* Screens as a Cloud Service现在支持基本回放监控。 播放器现在将报告每次ping（默认为30秒）的各种播放量度。 基于量度，它提供检测各种边缘情况（卡住体验、空白屏幕、计划问题等）的能力。 此功能允许团队远程监控播放器是否正确播放内容，改善对空白屏幕或现场中断体验的反应性，并降低向最终用户显示中断体验的风险。
参见 [基本回放监控](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/manage-player-registration/installing-screens-cloud-player.html?lang=en#playback-monitoring) 了解更多详细信息。

* 现在，Screensas a Cloud Service支持视频的缩略图。 内容作者可以定义视频的缩略图，以便在适当的团队最终确定实际视频的同时，将图像用作占位符并正确测试内容播放和定位。 在视频播放失败时，也可以使用该图像。
参见 [视频的缩略图支持](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/core-product-features/thumbnail-support-videos.html) 了解更多详细信息。

### 错误修复 {#bug-fixes-screens}

* 播放器无法显示嵌入页面中的内容，此问题现已修复。

* 成功登录后，导航到默认页面（渠道）最后会进入内部服务器错误页面。

* 删除播放列表时未删除关联的标记条目。

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### [!DNL Experience Manager as a Cloud Service] 中的新增功能 {#foundation-features}

**高级联网**

>[!INFO]
>
>高级联网功能是2021.9.0版本的一部分，将于10月中旬为客户启用。

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 现在提供了多种高级联网功能，包括：

* 灵活端口出口，将流量从非标准端口输出。 现在无需联系Adobe支持即可实现。
* 专用出口IP地址，用于从as a Cloud Service于唯一IP的AEM输出流量，现在支持所有端口。
* VPN用于保护您的基础设施与AEMas a Cloud Service之间的流量。

阅读 [文档](/help/security/configuring-advanced-networking.md) 有关更多信息（包括如何使用Cloud Manager API自助配置高级网络）。

**索引优化**

为了提高搜索查询和索引的性能，不再在中现成使用全文索引lucene-2 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 此版本中的。 为了根据AEM客户的要求删除AEM环境中的此全文索引，Adobe工程部单独并主动与客户合作，以温和、可持续的方式删除Lucene全文索引。 请访问 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [文档](/help/operations/indexing.md#index-optimizations) 如果您有任何问题，请直接联系我们的支持人员，以获取更多信息。

## Cloud Manager {#cloud-manager}

本部分概述了AEMas a Cloud Service2021.9.0和2021.8.0中的Cloud Manager发行说明。

## 发布日期 {#release-date-cm-sept}

AEM as a Cloud Service 2021.9.0 中的 Cloud Manager 的发布日期是 2020 年 9 月 9 日。下一个版本计划于2021年10月7日发布。

### 新增功能 {#what-is-new-cm-sept}

* Cloud Manager 使用的 AEM 项目原型的版本已更新到版本 30。

* Cloud Manager 登陆页面上的程序信息卡和相关体验都已更新。

* 代码质量步骤日志现在包括有关 OakPal 扫描过程的详细日志信息。

* 活动页面菜单选项现在包括一个选项，用于&#x200B;**下载已完成的代码生成器执行的日志**。 选择此选项，将下载构建步骤的日志。

* 直接点击程序卡，现在可导航至Cloud Manager概述页面。

### 错误修复 {#bug-fixes-sept}

* 现在，当用户尝试在已达到可配置的最大允许 IP 允许列表数的程序中添加新的 IP 允许列表时，将看到更容易理解的消息。

* 从存储库屏幕选择复制 URL 菜单选项时复制了错误的 URL。

## Cloud Acceleration Manager {#cam}

### 发布日期 {#release-date-october-cam}

Cloud Acceleration Manager的发布日期是2021年10月4日。

### 新增功能 {#what-is-new-cam}

* Cloud Acceleration Manager现在使用户能够在可打印的预览中查看BPA报告，从而允许简单打印或打印以PDF以便于共享。 请参阅中的步骤6和7 [使用最佳实践分析卡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-readiness-phase.html?lang=en#best-practices-analysis).

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具版本1.6.0的发布日期为2021年10月4日。

### 新增功能 {#what-is-new-ctt}

* 通过简化的用户体验改进了用户映射，包括以下列出的功能。 有关更多详细信息，请参阅 [使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool).
   * 在运行用户映射之前测试与用户管理API的连接
   * 正常跳过错误并继续用户映射活动
   * 如果访问令牌过期（24小时后），用户映射不再失败。 可以从上次停止的位置重新运行用户映射。

* 为了提高CTT的稳健性，可以将内容一次摄取到“创作”实例或“发布”实例。

* 当包含版本时，路径 `/var/audit` 将自动包含以迁移审核事件。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa-latest}

Best Practices Analyzer v2.1.18的发布日期是2021年9月2日。

### 新增功能 {#what-is-new}

* 能够检测和报告节点总数。

* 能够检测和报告节点存储类型和大小。

### 错误修复 {#bug-fixes-bpa}

* BPA错误地检测到Commerce Integration Framework的存在。
