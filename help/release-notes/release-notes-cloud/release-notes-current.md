---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 372e40eb90d87d9ed366e08a3c0117068542680b
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 35%

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

的发行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新版本(2022.3.0)是2022年3月31日。
以下版本(2022.4.0)发布于2022年4月28日。

## 发布视频 {#release-video}

请查看 [2022年3月版概述](https://video.tv.adobe.com/v/341465) 视频，了解2022.3.0版本中添加的功能摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* [!DNL AEM Dynamic Media] 现在提供了灵活性，让您可以在用户界面中[配置一个别名账户](/help/assets/dynamic-media/dm-alias-account.md)，从而确保开箱即用的 Dynamic Media URL 和查看器嵌入代码获得更新。这会对 SEO 产生积极影响，以反映对您的业务环境（如品牌再造）所做的更新。

* 您现在可以使用 [!DNL Experience Manager Assets] 用户界面执行以下操作：

   * 配置 [检测重复资产](/help/assets/manage-digital-assets.md#detect-duplicate-assets) 中。

   * 配置 [添加数字水印](/help/assets/watermark-assets.md) 到图像。

* 管理员现在可以为大型下载配置电子邮件服务。它让用户可以从 [!DNL Experience Manager Assets] 界面[为大型下载启用电子邮件通知](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads)。下载过程完成后，用户会收到电子邮件通知，其中包含已存档 zip 文件夹的下载链接。

* [管理发布](/help/assets/manage-publication.md)功能通过改进的用户界面得到增强。用户可以向所选目标发布内容或从中取消发布内容，可以从 DAM 存储库[添加内容](/help/assets/manage-publication.md#add-content)至发布列表，可以[包含文件夹设置](/help/assets/manage-publication.md#include-folder-settings)以发布选定文件夹的内容和应用筛选器，还可以[安排发布](/help/assets/manage-publication.md#publish-assets-later)到晚一点的日期或时间。

### [!DNL Assets] 预发行渠道中提供的新功能 {#prerelease-features-assets}

* 您可以 [排序标记](/help/assets/organize-assets.md#use-tags-to-organize-assets) 创建智能标记时，以及使用“标记”谓词应用搜索过滤器时，覆盖分类。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**: [文档生成API](/help/forms/aem-forms-cloud-service-communications.md) 帮助合并、重新排列和验证PDF文档。 该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：

   * 组合PDF文档。
   * 反汇编PDF文档。
   * 转换为并验证符合PDF/A的文档。

* **自动将大于15页的PDF forms转换为自适应表单**:现在，您可以使用automated forms conversion服务将最多40页的PDF forms转换为自适应表单。 该服务现在提供了将大于15页的表单部分转换为自适应表单片段的选项。 它有助于提高已转换表单的渲染速度，并且更便于在自适应表单编辑器中加载大型表单。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* **使用自定义XCI生成记录文档**:您现在可以使用自定义XCI文件来设置记录文档的各种属性。 它会通过自定义更改覆盖主控XCI。

* **在自适应表单中使用不可见的CAPTCHA**:只有在可疑活动时，才可使用不可见的验证码显示验证码挑战。 如果未发现可疑活动，则不显示验证码质询。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 测试版：AEM CIF搜索核心组件支持商务LiveSearch
* 改进了多存储方案的SEO:现在，可以通过CIF云配置属性在存储级别配置PDP/PLP的URL格式
* 产品选取器通过UI中的新筛选器选项支持暂存产品。  这样，内容从业者就可以为即将推出的产品准备产品内容管理
* 使用CIF云配置名称（而不是配置代理URL）简化CIF配置管理和错误处理
* 产品列表和轮播组件的手动类别选择。 这允许内容从业者在目录体验之外的内容页面上使用这些组件

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基础 {#foundation}

### 新增功能 {#what-is-new-foundation}

* 为了更高效、更高效地对云环境中的自定义功能进行故障诊断，我们发布了一款新的开发人员工具 —  [存储库浏览器](/help/implementing/developing/tools/repository-browser.md). 它是一个轻量级、只读的HTML浏览器，您可以从开发人员控制台中启动。 在发布者、作者和预览层以及所有环境（包括生产、暂存和开发环境）中，查看内容存储库。 浏览内容结构、查看属性以及预览和下载二进制文件。

   ![reprobrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* 现在，可以从开发人员控制台以自助方式在过期之前刷新用于验证服务器到服务器API调用的凭据（例如，用于GraphQL API请求）。 请参阅 [文档](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) 以了解更多信息。

* 将为新环境启用版本清除和审核日志清除维护任务（以前未启用）。 请参阅 [维护任务](/help/operations/maintenance.md) 文章。

* AEMas a Cloud ServiceSDK Dispatcher工具现在支持带有M1芯片的Mac计算机

## Cloud Manager {#cloud-manager}

### 2月发行日期 {#release-date-cm-feb}

AEM Manager在as a Cloud Service中的发布日期为2022.02.0 2022年2月10日。 下一版本计划于2022年3月10日发布。

### 新增功能 {#what-is-new-cm-feb}

* 新加速 [网层配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 已引入以专门部署HTTPD/调度程序配置。
   * 您必须使用AEM版本 `2021.12.6151.20211217T120950Z` 或较新和 [选择启用调度程序工具的灵活模式](/help/implementing/dispatcher/disp-overview.md#validation-debug) 以使用此功能。
   * 此功能将在2022.02.0版后的两周内分阶段推出。
* Cloud Manager登陆页面体验已刷新，以提供改进的导航、在网格/图块视图之间轻松切换，以及用于快速获取项目摘要的弹出窗口。
* 新的失败阈值(`< D`) [可靠性评级量度。](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)
   * 存在严重质量问题且影响系统稳定性的客户（主要与无效索引和工作流程相关）在这些问题得到解决之前将无法部署。
* 的严重性 `BannedPath` [质量规则](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules) 已从阻止程序更改为关键。
* 在配置 [网层配置管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) 关联。

### 错误修复 {#bug-fixes-cm-feb}

* 现在，在生成新密码时，旧的Git存储库密码始终无效。
* 在极少数情况下，通过API更新环境变量不再会妨碍管道执行。

### 3月发行日期 {#release-date-cm-march}

AEM 2022年3月10日as a Cloud Service的Cloud Manager 2022.3.0版的发布日期。 下一版本计划于2022年4月7日发布。

### 新增功能 {#what-is-new-cm-march}

* 使用开发人员角色可以访问AEM环境日志。

### 错误修复 {#bug-fixes-cm-march}

* 手动创建的git存储库的子集具有不正确的名称值，这会阻止生成对象重用功能生效。 这些存储库的名称已更改，用户将在Cloud Manager API/UI中看到更正的名称。
* 非生产管道的人造物在生产全堆流水线上被不当地重复使用。
* 添加或编辑代码质量管道时，不再显示用于处理量度失败的选项。
* 在生成步骤中，可能会导致一些意外的管道变量配置。

## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具v1.9.0的发布日期是2022年2月28日。

### 新增功能 {#what-is-new-ctt}

* 检查大小护栏 — 内容传输工具检查大小功能有助于减少失败的内容传输。  使用“检查大小”功能，用户可以1)确定他们在 `crx-quickstart` 提取前的子目录，以及2)估计迁移集大小并验证它是否受支持。 如果违反了这两项检查之一或两项，用户将在CTT UI中看到警告。 利用此护栏，您可以避免内容传输失败，并主动与Adobe客户关怀团队讨论迁移选项。 请参阅 [确定迁移集大小和磁盘空间](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#migration-set-size) 以了解更多详细信息。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.26 的发布日期是 2022 年 3 月 16 日。

### 新增功能 {#what-is-new-bpa}

* 能够监测未处理资源。如果检测到未处理资源，则需要将这些资源设置为已处理，或者在内容转移期间从迁移设置中删除这些资源，以避免在内容摄取期间遇到问题。
* 能够监测内容是否超过 1000 个虚名 URL。使用大量虚名 URL 不是最佳做法，因为它会给 Dispatcher 和 Publish 服务器带来负载。
* 能够识别 Oak 索引定义相关问题并检测与 AEM as a Cloud Service 兼容性。
* 能够检测和报告所使用的外部化程序配置。在 AEM as a Cloud Service 中，外部化程序配置由 Cloud Manager 设置，因此，需要重构现有的外部化程序配置以保持兼容性。

### 错误修复 {#bug-fixes-bpa}

* 在某些情况下，BPA 无法运行，因为 FormsSelectiveFeaturesAnalysis 抛出断言错误。此问题已得到修复。
* BPA 将与 WRK 模式相关的发现报告为 MAJOR 而非 CRITICAL。此问题已得到修复。
* BPA 错误地将 ui.apps 中与 OAK 索引定义有关的发现报告为 CRITICAL。此问题已得到修复
