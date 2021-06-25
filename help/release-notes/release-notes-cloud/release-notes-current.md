---
title: ' [!DNL Adobe Experience Manager] 作为Cloud Service的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] 作为Cloud Service的最新发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: c7cba6217ec960219c607b76ab7f2f096af7459a
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager]作为Cloud Service的最新发行说明 {#release-notes}

以下部分概述了作为Cloud Service的[!DNL Experience Manager]当前（最新）版本的常规发行说明。

>[!NOTE]
>从此处，您可以导航到以前版本的发行说明；例如，2020年、2021年等年份的客户。

>[!NOTE]
>
>请参阅[近期文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) ，以了解有关与版本不直接相关的文档更新的详细信息。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为Cloud Service2021.5.0的发布日期是2021年5月27日。
以下版本(2021.6.0)将于2021年6月24日发布。

## 发行视频 {#release-video}

请观看2021年5月版概述](https://video.tv.adobe.com/v/333602)视频，了解添加的功能摘要。[

## AEM as a A A Foundation( as aCloud Service基础) {#foundation}

### AEM as a A A Cloud的新增功能基础 {#what-is-new-foundation}

* [预发行渠道](/help/release-notes/prerelease.md):在即将推出的功能投入生产之前，请预览该功能整整一个月！

* [API弃用](/help/release-notes/deprecated-apis.md):提供了AEM as a Cloud Service的最新已弃用API列表。

* [AEM as a Cloud ServiceSDK Build Analyzer Maven插件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html):将您的Maven项目更新到最新版本，该版本包括已弃用的Java API检查和其他改进。

## [!DNL Adobe Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites]的新增功能 {#what-is-new-sites}

* 您很快将能够在新的[预览层](/help/sites-cloud/authoring/fundamentals/previewing-content.md)上验证内容，以像在发布层一样模拟最终体验外观。 这由AEM Sites托管发布向导启用，该向导现在允许您在发布或预览之间选择发布目标。 然后，可以通过专用URL访问预览体验。 验证“预览”后，内容可以照常从“创作”发布到“发布”。 在AEM as a Cloud Service环境中启用“预览服务”功能将在未来几周逐步推出。

## [!DNL Adobe Experience Manager Assets] as a  [!DNL Cloud Service] {#assets}

### 预发行渠道中提供的新增功能 {#what-is-new-assets-prerelease}

* 元数据架构可以直接应用到文件夹属性。

   ![从文件夹属性添加元数据架构](/help/assets/assets/metadata-schema-folder-properties.png)

* 资产批量摄取工具允许您在批量摄取期间添加元数据。

* 用户体验增强功能可显示文件夹中存在的资产数量。 对于文件夹中超过1000个资产，[!DNL Assets]显示的资产数量超过1000个。

   ![文件夹中的资产数量显示在界面上](/help/assets/assets/browse-folder-number-of-assets.png)

### [!DNL Assets]中修复的错误 {#assets-bugs-fixed}

* 上载超大文件会使[!DNL Experience Manager desktop app]崩溃。 (CQ-4320942)
* 从文件夹中选择同一收藏集和从搜索结果中选择该收藏集时，工具栏选项会有所不同。 (CQ-4321406)

#### [!DNL Dynamic Media]的新增功能 {#what-is-new-dm}

* 智能成像设备像素比(DPR)和网络带宽优化让您能够在具有高分辨率显示器和有限网络带宽的设备上高效地交付最佳质量的图像。 请参阅[智能成像常见问题解答](/help/assets/dynamic-media/imaging-faq.md)。

* 在[!DNL Dynamic Media]投放中引入了对下一代图像格式AVIF的支持（`fmt` URL修饰符）。 有关更多详细信息和时间轴，请参阅[图像提供和渲染API fmt](https://experienceleague.corp.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html)。

## [!DNL Adobe Experience Manager Forms] as a  [!DNL Cloud Service] {#forms}

### [!DNL Forms]的新增功能 {#what-is-new-forms}

* **上下文帮助**:为自适应表单编辑器、模板编辑器和主题编辑器添加了上下文帮助，以帮助作者更好地了解编辑器的各种功能。
* **属性浏览器中的错误消息**:为自适应Forms属性浏览器中的每个属性添加了错误消息。这些消息有助于了解字段的允许值。

### 即将推出的[!DNL Forms]测试版功能 {#what-is-new-forms-prerelease}

Output as a Cloud Service:输出服务可帮助您将XDP模板和XML数据结合起来，以生成各种格式的打印文档。 该服务允许您以同步和异步批处理模式生成文档。 通过输出服务，您可以创建应用程序，以便：

* 使用XML数据填充模板文件，生成最终表单文档。
* 以各种格式生成输出表单，包括非交互式PDF打印流。
* 从XFA表单PDF生成打印PDF。

您可以写信至formscsbeta@adobe.com注册测试版计划。

### [!DNL Forms]中修复的错误 {#forms-bugs-fixed}

* 在AEM Forms工作流的“分配任务”步骤中，当您将操作按钮的默认图标替换为珊瑚图标时，工作流会停止工作并记录异常。 使用默认图标时，工作流会按预期执行。
* 在布局层中，当更改列数、打开编辑层并将某些组件拖动到面板中时，自适应表单编辑器的内容区域中会开始出现正方形蓝框，且编辑器变得无响应。
* 与提供自适应或外部资产的URL相关的规则编辑器选项的错误消息太长，且用户不友好。

## Cloud Manager {#cloud-manager}

本部分概述了AEM as a 2021.6.0和2021.5.0Cloud Service中Cloud Manager的发行说明。

## 发布日期 {#release-date-june-cm}

AEM as a Cloud Service2021.6.0中Cloud Manager的发布日期是2021年6月10日。
下一版本计划于2021年7月15日发布。

### 新增功能 {#what-is-new-junecm}

* 预览服务将以滚动方式部署到所有程序。 当客户的计划启用了预览服务后，系统会在产品中通知客户。 有关更多详细信息，请参阅[访问预览服务](/help/implementing/cloud-manager/manage-environments.md#access-preview-service) 。

* 现在，在生成步骤期间下载的Maven依赖项将在管道执行之间缓存。 未来几周，将为客户启用此功能。

* 现在可以通过编辑程序对话框编辑程序的名称。

* 在项目创建期间和通过管理git工作流在默认推送命令中使用的默认分支名称已更改为`main`。

* 在UI中编辑项目体验已刷新。

* 质量规则`ImmutableMutableMixCheck`已更新，可将`/oak:index`节点分类为不可变。

* 质量规则`CQBP-84`和`CQBP-84--dependencies`已合并到单个规则中。 作为此整合的一部分，对依赖项的扫描可更准确地识别部署到AEM运行时的第三方依赖项中的问题。

* 为避免混淆，“环境详细信息”页面上的“发布AEM”和“发布Dispatcher”区段行已进行合并。

   ![](/help/onboarding/release-notes-cloud-manager/assets/aem-dispatcher.png)

* 添加了新的代码质量规则来验证`damAssetLucene`索引的结构。 有关更多详细信息，请参阅[自定义DAM资产Lucene Oak索引](/help/implementing/cloud-manager/custom-code-quality-rules.md#oakpal-damAssetLucene-sanity-check)。

* “环境详细信息”页面现在将显示发布和预览服务的多个域名（如果适用）。 有关更多详细信息，请参阅[环境详细信息](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。

### 错误修复 {#bug-fixes-junecm}

* 未正确解析根元素名称后包含换行符的JCR节点定义。

* 列表存储库API不会过滤已删除的存储库。

* 为计划步骤提供无效值时，显示错误消息。

* 有时，即使未部署该配置，用户也可能在IP允许列表旁看到绿色的&#x200B;*活动*&#x200B;状态。

* 某些程序编辑序列可能会导致无法创建或编辑生产管道。

* 某些程序编辑序列可能会导致在&#x200B;**概述**&#x200B;页面中显示一条误导性消息，以便重新执行程序设置。


### 发布日期 {#release-date-cm-may}

AEM as a Cloud Service2021.5.0中的Cloud Manager的发布日期是2021年5月6日。

### 新增功能 {#what-is-new-may}

* PackageOverlaps质量规则现在会检测在同一部署的包集中多次部署同一包的情况，即在多个嵌入位置中部署同一包的情况。

* 现在，公共API中的存储库端点包含Git URL。

* Cloud Manager用户下载的部署日志将更有洞察力，现在将包含有关失败和成功方案的详细信息。

* 现在，已解决将代码推送到AdobeGit时遇到的间歇性故障。

* 现在，可以在编辑项目工作流期间将商务加载项应用于沙盒项目。

* 编辑程序体验已刷新。

* “环境详细信息”页面中的“域名”表将通过分页显示多达250个域名。

* 添加程序和编辑程序工作流中的解决方案选项卡将显示解决方案，即使该程序只有一个解决方案可用。

* 生成步骤日志中未生成任何已部署的内容包时的错误消息不明确。

### 错误修复 {#bug-fixes-cm-may}

* 有时，即使未部署该配置，用户也可能会在IP允许列表旁边看到绿色的“活动”状态。

* 管道变量API不会删除“已删除”变量，而是仅以状态&#x200B;**DELETED**&#x200B;标记它们。

* 某些代码气味类型的质量问题错误地影响了可靠性评级。

* 由于不支持通配符域，因此UI将禁止用户提交通配符域。

* 当从午夜UTC到凌晨1点之间开始管道执行时，Cloud Manager生成的对象版本不保证大于前一天创建的版本。

* 在沙盒项目设置过程中，成功创建包含示例代码的项目后，“概述”页面中的“管理Git”将显示为主页卡中的链接。

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-latest}

内容传输工具v1.4.6的发布日期是2021年5月27日。

### 新增功能 {#what-is-new-ctt-latest}

* 如果用户没有对Java可执行文件的执行权限，则新的日志记录语句会添加到快速启动的错误日志中。

* 当用户从执行提取的CTT UI中删除迁移集时，将删除与该迁移集关联的`tmp`文件夹以节省空间。

### 错误修复 {#bug-fixes-ctt-latest}

* 删除迁移集时，CTT UI中有时会显示一条无用的错误消息。 此问题已修复。

* 运行用户映射时，如果用户在目标和主机上具有相同的电子邮件地址，但用户名不同，则整个摄取会失败。 此问题已修复。 在这种冲突的情景中，用户/组被跳过并在日志文件中记录为冲突。

### 发布日期 {#release-date-ctt-may}

内容传输工具v1.4.0的发布日期是2021年5月11日。

### 新增功能 {#what-is-new-ctt-may}

* 此版本的内容传输工具会为要迁移到Cloud Service的资产创建文本演绎版。 需要文本演绎版才能支持对摄取的资产进行全文搜索。
* 用户可以创建的内容传输工具迁移集的最大数量已从4个增加到10个。

### 错误修复 {#bug-fixes-ctt-may}

* 修复了与内容传输工具UI中的自动刷新功能相关的多个错误。
* 包含`wipe=true`的内容传输工具导致目标上的计数器索引不正确。 此问题已修复。

## 商务附加组件 {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品控制台属性中对关联内容的分页支持

### 错误修复 {#bug-fixes-commerce}

* 产品属性的资产选项卡中未显示资产缩略图

* 痕迹导航会重置产品控制台中的预览数据
