---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.5.0 版的发行说明。'
exl-id: 3f9d7339-7e37-4702-821e-f2b03cd7e224
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 46%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>从此处，您可以导航到早期版本的发行说明；例如，2020版、2021版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的发布日期 [!DNL Adobe Experience Manager] as a Cloud Service2021.5.0是2021年5月27日。
下一个版本(2021.6.0)将于2021年6月28日发布。

## AEMas a Cloud Service基础 {#foundation}

### AEMas a Cloud Service基础的新增功能 {#what-is-new-foundation}

* [预发行渠道](/help/release-notes/prerelease.md)：在即将推出的功能正式发布前的一个月内进行预览！

* [API弃用](/help/release-notes/deprecated-apis.md)：提供了适用于AEMas a Cloud Service的最新弃用API的列表。

* [AEMas a Cloud ServiceSDK构建分析器Maven插件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html)：将您的maven项目更新到最新版本，其中包括弃用的Java API检查和其他改进。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 的新增功能 {#what-is-new-sites}

* 您很快便能够验证新版本上的内容 [预览层](/help/sites-cloud/authoring/fundamentals/previewing-content.md) 模拟最终体验外观，就像在发布层上一样。 这是通过AEM Sites托管发布向导启用的，现在允许您在发布或预览之间选择发布目标。 随后，可以通过专用URL访问预览体验。 在“预览”上进行验证后，内容可以像往常一样从“创作”发布到“发布”。 在接下来的几周内将逐步在AEMas a Cloud Service环境中启用“预览”服务。

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 您可以使用链接共享功能下载共享的资产。 现在，此下载使用异步服务，即使对于非常大的下载，该服务也能提供更快且无中断的下载。 参见 [下载资产](/help/assets/download-assets-from-aem.md#link-share-download).

  ![下载收件箱](/help/assets/assets/download-inbox.png)

### 预发行渠道中可用的新功能 {#what-is-new-assets-prerelease}

* 可以将元数据架构直接应用于文件夹属性。

  ![从文件夹属性添加元数据架构](/help/assets/assets/metadata-schema-folder-properties.png)

* 在批量提取期间，可使用资源批量提取器工具添加元数据。

* 用户体验增强功能会显示文件夹中存在的资源数量。 对于文件夹中的1000多项资源， [!DNL Assets] 显示1000+。

  ![文件夹中的资源数显示在界面上](/help/assets/assets/browse-folder-number-of-assets.png)

### [!DNL Assets] 中修复的错误 {#assets-bugs-fixed}

* 上传超大文件会导致 [!DNL Experience Manager desktop app]. (CQ-4320942)
* 在从文件夹中选择同一收藏集或从搜索结果中选择收藏集时，工具栏选项会有所不同。 (CQ-4321406)

#### Dynamic Media的新增功能 {#what-is-new-dm}

* 智能成像DPR（设备像素比）和网络带宽优化使您能够在具有高分辨率显示器和受限网络带宽的设备上高效地提供最佳质量的图像。 有关更多信息，请参阅 [智能成像常见问题解答](/help/assets/dynamic-media/imaging-faq.md) 和 [使用下一代图像格式WebP和AVIF优化图像。](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)
* 在Dynamic Media交付中引入了对下一代图像格式AVIF的支持（fmt URL修饰符）。

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **上下文帮助**：添加了自适应表单编辑器、模板编辑器和主题编辑器的上下文帮助，以帮助作者更好地了解各编辑器的各种功能。
* **属性浏览器中的错误消息**：在自适应表单属性浏览器中为每个属性添加了错误消息。这些消息有助于了解字段的允许值。

### 即将推出的 [!DNL Forms] Beta 版功能 {#what-is-new-forms-prerelease}

Output as a Cloud Service：Output 服务可帮助您组合 XDP 模板和 XML 数据以生成各种格式的打印文档。该服务允许您以同步和异步批处理模式生成文档。Output 服务使您能够创建应用程序，这些应用程序允许您：

* 使用 XML 数据填充模板文件来生成最终表单文档。
* 生成各种格式的输出表单，包括非交互式 PDF 打印流。
* 从 XFA 表单 PDF 生成打印 PDF。

您可以将电子邮件发送到 formscsbeta@adobe.com 以注册 Beta 项目。

### [!DNL Forms] 中修复的错误 {#forms-bugs-fixed}

* 在 AEM Forms Workflows 的“分配任务”步骤中，当您将操作按钮的默认图标替换为珊瑚色图标时，工作流将停止工作并记录异常。使用默认图标时，工作流按预期执行。
* 在版面层中，当您更改列数、打开编辑层并在面板中拖动某些组件时，自适应表单编辑器的内容区域中会开始显示蓝色方形框，并且编辑器将变得无响应。
* 与提供自适应或外部资产的 URL 相关的规则编辑器选项的错误消息太长，并且对用户不友好。


## Cloud Manager {#cloud-manager}

此部分概述了 AEM as a Cloud Service 2021.5.0 中的 Cloud Manager 的发行说明。

### 发布日期 {#release-date-cm-may}

AEM as a Cloud Service 2021.5.0 中的 Cloud Manager 的发布日期是 2021 年 5 月 6 日。下一个版本计划于 2021 年 6 月 03 日发布。

### 新增功能 {#what-is-new-may}

* PackageOverlaps质量规则现在可检测多次部署同一个包的情况，即在同一个部署的包集中部署在多个嵌入位置。

* 公共 API 中的存储库端点现在包括 Git URL。

* Cloud Manager用户下载的部署日志具有更丰富的见解，其中包括有关失败和成功情况的详细信息。

* 现已解决将代码推送到 Adobe git 时遇到的间歇性故障。

* 现在可在“编辑程序”工作流程中将商业加载项应用于沙盒程序。

* 已更新编辑程序体验。

* “环境详情”页面中的“域名”表将通过分页的方式显示最多 250 个域名。

* 即使程序只有一个解决方案可用，“添加程序”和“编辑程序”工作流中的“解决方案”选项卡将显示解决方案。

* 当构建未生成任何部署的内容包时构建步骤日志中的错误消息不明确。

### 错误修复 {#bug-fixes-cm-may}

* 有时，即使未部署配置，用户也会在 IP 允许列表旁边看到绿色的“活动”状态。

* 管道变量 API 不会移除“已删除”变量，而只会将其标记为&#x200B;**已删除**&#x200B;状态。

* 一些代码气味类型的质量问题错误地影响了可靠性评级。

* 由于不支持通配符域，UI 将禁止用户提交通配符域名。

* 当管道执行在 UTC 午夜至凌晨 1 点之间启动时，Cloud Manager 生成的工件版本不能保证大于前一天创建的版本。

* 在沙盒程序设置过程中，一旦成功创建了带有示例代码的项目，“管理 Git”将作为主信息卡中的链接出现在”概述“页面中。

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具版本1.4.6的发布日期为2021年5月27日。

### 新增功能 {#what-is-new-ctt-latest}

* 如果用户没有Java可执行文件的运行权限，则会在快速入门的错误日志中添加新的日志记录语句。

* 当用户从执行提取的CTT用户界面删除迁移集时， `tmp` 已删除与该迁移集关联的文件夹以节省空间。

### 错误修复 {#bug-fixes-ctt-latest}

* 删除迁移集时，CTT UI中偶尔会显示一条无用的错误消息。 此问题已得到修复。

* 在运行用户映射时，如果用户在目标和主机上拥有相同的电子邮件地址，但用户名不同，则整个摄取操作将失败。 此问题已得到修复。在这种冲突场景中，用户/组被跳过，并在日志文件中记录为冲突。

### 发布日期 {#release-date-ctt}

内容传输工具版本1.4.0的发布日期为2021年5月11日。

### 新增功能 {#what-is-new-ctt-may}

* 此版本的内容传输工具为迁移到Cloud Service的资源创建文本演绎版。 需要文本演绎版才能支持对所摄取的资产进行全文搜索。
* 用户可以创建的内容传输工具迁移集的最大数量已从4个增加到10个。

### 错误修复 {#bug-fixes-ctt-may}

* 与内容传输工具UI中的自动刷新功能相关的多个错误修复。
* 内容传输工具 `wipe=true` 导致目标上的计数器索引不正确。 此问题已得到修复。

## Commerce加载项 {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品控制台属性中的关联内容支持分页

### 错误修复 {#bug-fixes-commerce}

* 资产缩略图未显示在产品属性的“资产”选项卡中

* 痕迹导航在产品控制台中重置预览数据
