---
title: Adobe Experience Manager as a Cloud Service 2020.6.0 发行说明
description: Experience Manager 2020.6.0 发行说明
exl-id: fd6ebe2b-6d98-498c-a45d-b9a9c34e6be7
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 97%

---

# AEM as a Cloud Service 2020.6.0 发行说明 {#release-notes}

本页面概述了 Experience Manager as a Cloud Service 2020.6.0 版的常规发行说明。

## 发布日期 {#release-date}

[!DNL Experience Manager] as a Cloud Service 2020.6.0 的发布日期是 2020 年 6 月 4 日。

## AEM Sites 的新增功能 {#aem-sites}

阅读本节内容，了解 AEM as a Cloud Service 版本 2020.6.0 中 AEM Sites 的新增功能和更新。

### 新增功能 {#whats-new-2020.6.0}

[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)版本 2.9.0 现已作为 AEM Sites 的一部分提供，包括：

* [Adobe 客户端数据层](https://github.com/adobe/adobe-client-data-layer)与核心组件的集成
* 适用于所有组件的可配置 HTML ID 属性
* 新的进度条组件
* 许多错误修复

### 错误修复 {#sites-bug-fixes}

* 在页面上再次复制并粘贴布局容器时，布局容器内的组件不可见。

* 修复了调整布局组件大小时出现的问题。

* 添加了管理仅路由 Angular 页面和 AEM/Angular 页面的功能。

### 辅助功能 {#accessibility}

* 现在，在&#x200B;**创建页面**&#x200B;对话框中以浏览模式使用向下箭头导航时，可以讲述 Masonry 项目的角色和状态。

* 在导航中添加了链接，以允许用户跳转到主内容。

* 屏幕阅读器改进。

## AEM as a Cloud Service 的新增基础功能 {#foundations}

通过删除 AEM 项目的 pom.xml 中对远程存储库 `https://downloads.experiencecloud.adobe.com/content/maven/public` 的所有引用，AEM 项目构建时间将会缩短。

AEM as a Cloud Service SDK API Jar（以前在该位置托管）现在位于 Maven Central（即 Maven 的默认项目存储库）中。

## Cloud Manager 的新增功能 {#cloud-manager}

阅读本节内容，了解 AEM as a Cloud Service 版本 2020.6.0 中 Cloud Manager 的新增功能和更新。

### 新增功能 {#what-is-new-cloud-manager}

* 在 Cloud Manager 中，具有“业务所有者”**&#x200B;角色的用户现在可以从登陆页面（通过项目卡上的快速操作按钮）或项目中删除沙盒项目。

   有关更多详细信息，请参阅[删除沙盒项目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html)。

* 在 Cloud Manager 中，具有“业务所有者”**&#x200B;或“部署管理者”**&#x200B;角色的沙盒项目用户现在可以通过 Cloud Manager UI 删除其生产和暂存环境集。删除选项现在可从&#x200B;**项目概述**&#x200B;页面和&#x200B;**环境**&#x200B;页面上的环境卡中使用。在生产或暂存环境中选择删除选项也会删除环境集中的另一个环境。

   有关更多详细信息，请参阅[删除沙盒项目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html)。

* 在登陆页面上显示引导标记，以告知和指示用户如何进行基本导航。

* 在&#x200B;**项目概述**&#x200B;页面上显示引导标记，以告知和指示用户如何在 Cloud Manager 中进行基本导航，以便开始操作。

* 现在 Cloud Manager 中提供了&#x200B;**学习**&#x200B;页面，可通过顶部导航访问该页面。该页面包含可帮助用户了解与他们在 Cloud Manager 中分配的角色相关的最常用工作流的资源。

* 沙盒项目现在通过&#x200B;**沙盒**&#x200B;徽章进行标识，该徽章将显示在登陆页面的项目卡上，以及&#x200B;**项目概述**&#x200B;页面中项目名称的旁边。

* 具有 SysAdmin 角色的用户现在通过一次单击即可访问 Admin Console 中的相应位置，以管理用户角色或 Cloud Manager 权限。现在，登陆页面上的&#x200B;**添加项目**&#x200B;按钮旁边提供了&#x200B;**管理访问权限**&#x200B;按钮。

   有关更多详细信息，请参阅 [SysAdmin 任务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks)。

* 具有 SysAdmin 角色的用户现在通过一次单击即可直接从 Cloud Manager 中访问创作实例。

   有关更多详细信息，请参阅[管理对创作实例的访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem)。

* “生成”日志现在包含已发现项目的列表，包括跳过的内容包。

* “生成”步骤现在会验证所有生成的内容包是否包含所有必需属性 - 名称、组和版本。

* “生成”步骤现在会验证是否生成了至少一个内容包。

### 错误修复 {#bug-fixes-cm}

* 在某些情况下，**创建项目**&#x200B;对话框中的图标未对齐。

* AEM 版本标识符在&#x200B;**项目概述**&#x200B;页面上显示不一致。

* 配置生产管道时，某些客户看不到&#x200B;**计划部署**&#x200B;选项。

### 已知问题 {#known-issues-cm}

* 在某一特定时间段内未检测到活动时，沙盒项目内的环境将会休眠。在 Cloud Manager 中不会观察到此状态。但是，可通过开发人员控制台观察到此状态。即将发布的版本中将解决此问题。

* 直接从 Cloud Manager 链接到开发人员控制台不会显示用于将沙盒项目的环境解除休眠/休眠的选项。要解决此问题，请在开发人员控制台中，将模式 `#release-cm-p1234-e5678` 添加到 URL 的末尾，其中 *1234* 是项目 ID，*5678* 是环境 ID。即将发布的版本中将解决此问题。

## [!DNL Adobe Experience Manager Assets] 的新增功能  {#aem-assets}

**增强型智能标记的引导式用户体验，由 Adobe Sensei 提供支持**

除通用智能标记以外，增强型智能标记还允许组织培训智能标记模型，以根据客户特定的业务标记识别图像。

在此版本中，提供了新的引导式用户体验，可帮助为客户特定标记集设置智能标记培训，并使用资产进行培训，这些资产应会在将来进行识别和标记。现在提供了更直观的体验。使用增强型智能标记，可更直观地培训智能标记。请参阅 [如何向资产添加智能标记](/help/assets/smart-tags.md).

**支持 3D 内容的摄取、预览和交付**

现在，组织可以在 AEM Assets 中存储和使用 3D 文件。用户可以上传、预览和使用各种核心 3D 文件，包括 OBJ、STL、GLTF 和 GLB 文件。除 [!DNL Dynamic Media] 以外，您还可以使用不可知的 URL 或查看器配置和提供 3D 体验。这包括 [!DNL Dynamic Media] 3D 体验查看器、Sites 3D 查看器组件，以及通过 [!DNL Dynamic Media] (AR/VR) 交付 3D 文件的功能。请参阅[在 Dynamic Media 中使用 3D 资产](/help/assets/dynamic-media/assets-3d.md)。

**对 Adobe XD 的 Adobe Asset Link 支持**

在最新版本中，[!DNL Experience Manager Assets] 支持随 [!DNL Adobe XD] v29.3 一起发布的新 [!DNL Adobe Asset Link] 插件。该集成使设计人员能够在其设计中访问和使用 [!DNL Experience Manager] 中的资产，而无需离开 [!DNL Adobe XD] 应用程序。请参阅[适用于 Adobe XD 的 Adobe Asset Link 文档](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link-for-xd.html)。

在此版本中，创意用户和设计人员现在可以在一系列 Creative Cloud 桌面应用程序（包括 [!DNL Adobe XD]、[!DNL Photoshop]、[!DNL Illustrator] 和 [!DNL InDesign]）中使用 [!DNL Adobe Asset Link] 处理 [!DNL AEM Assets] 中管理的资产。

**辅助功能增强功能**

现在，[!DNL Adobe Experience Manager Assets] 提供了更多辅助功能，以便遵循《Web 内容无障碍指南》(WCAG) v2.1。对以下用例或界面的辅助功能进行了改进：

用户界面元素让屏幕阅读器易于识别，可使用键盘访问，并且对比度更高。以下是增强功能的详细列表：

* [!UICONTROL 管理发布]页面上的[!UICONTROL 选项]、[!UICONTROL 范围]和[!UICONTROL 工作流]进度条无法让屏幕阅读器作为进度条读出。相反，屏幕阅读器用户将这些状态指示器视为选项卡列表。(CQ-4273015)

* 在资产的[!UICONTROL 属性]页面中添加标记时，用户会导航标记树结构。但是，树结构无法访问，因为屏幕阅读器用户在导航时听不到任何内容。(CQ-4272964)

* 在链接共享对话框中，在浏览模式下导航时，屏幕阅读器将：

   * 在加载对话框后立即讲述表信息。
   * 无法导航到所有列出的自动建议。
   * 对于[!UICONTROL 添加电子邮件地址/搜索]组合框，不会讲述所显示的自动建议。(CQ-4294232)

* [!UICONTROL 元数据架构编辑器]页面及其元素现在可使用键盘访问，并且让屏幕阅读器易于识别。(CQ-4272953) 用户可以在 NVDA 浏览模式下使用键盘拖动组件。(CQ-4296326)

* 在 Assets 用户界面上，无法通过键盘访问视图设置。(CQ-4289038)

* 黄色评级图标的光度比小于 3:1。它对视力有限和不能感知颜色的用户没有用处。星级评级显示在资产的选项卡或卡片视图中

* 某些用户界面元素的颜色和对比度已更新，以便视力有限和不能感知颜色的用户能够区分这些用户界面元素。例如，资产[!UICONTROL 属性]的[!UICONTROL 高级]选项卡[!UICONTROL 评级]部分和卡片视图中的星级图标颜色会根据相应的对比度进行更改。(CQ-4295106)

* 屏幕阅读器现在可以将组合框（在不同页面的各个字段中）的列表框弹出菜单条目读作选项列表。(CQ-4294017)

* 要将工作流应用于资产，可使用键盘访问[!UICONTROL 时间轴]中的 V 形箭头。(CQ-4289268)

* 用户可以使用 `x` 符号删除资产[!UICONTROL 属性]页面[!UICONTROL 基本]选项卡的[!UICONTROL 标记]字段中选定的标记。屏幕阅读器现在会朗读所选标记的用途和数量 (CQ-4273033)。

* 可以使用键盘将焦点置于只读表单字段。例如，资产[!UICONTROL 属性]页面的[!UICONTROL 基本]选项卡上禁用的字段。(CQ-4273031)

* 现在，可使用键盘访问左边栏中用于筛选资产的选项。(CQ-4273018)

* 屏幕阅读器会朗读各种组合框元素（如“路径”字段）的用途，以及资产[!UICONTROL 属性]页面的[!UICONTROL 基本]选项卡中用于打开“选择”对话框的选项。(CQ-4273016)

* 可使用键盘访问视频的音量控件。(CQ-4272696)

* 使用键盘时，Assets 用户界面上的许多可操作选项不会指示焦点。(CQ-4272694)

* 屏幕阅读器用户现在知道何时可以使用键盘选择列表视图中的行。当指针悬停在行上时，将朗读该信息。(CQ-4271824)

* 某些表单字段（如登录页上的用户名和密码字段）依赖占位符值来提供可访问的标签。(CQ-4271716)

* 现在，可以使用键盘访问交互式用户界面元素，例如链接和选项（如资产页面的标题和缩放选项或文件夹导航）。(CQ-4271412)

* 现在，[!DNL Adobe Experience Manager] Assets 上所有已浏览页面的标题是唯一的。(CQ-4271409)

**其他增强功能**

此版本提供了以下其他增强功能：

* 能够使用资产处理配置文件重新处理资产，让用户完全控制该流程（运行完全资产处理，仅应用特定处理配置文件，并确定是否应运行处理后工作流）。
* 现在，当基础群集实例在后台重新启动时，搜索查询返回结果的速度更快（之前在此类情况下，初始搜索运行可能会持续较长时间）。
* 在 Assets 界面的列表视图和搜索结果中查看资产时，可按“名称”排序。请参阅[搜索资产](/help/assets/search-assets.md#sort)。
* 在 Assets 界面的列表视图和搜索结果中查看资产时，可按“创建时间”（日期）排序。请参阅[搜索资产](/help/assets/search-assets.md#sort)。
* 支持使用资产微服务将 EPS 文件转换为图像。

### 错误修复 {#assets-bug-fixes}

除上述新增功能以外，当前版本还根据客户对 [!DNL Assets] 的反馈提供了以下错误修复。

* 对于 MP3 音乐文件，在 DAM 预览的缩略图上显示的播放按钮不起作用。(CQ-4294731)
* 将指针悬停在卡片视图上时，屏幕会因（自动）聚焦卡片中可用的快速操作而滚动。(GRANITE-26895)
* 滚动许多搜索结果后显示过多图像会导致浏览器崩溃。(GRANITE-26432)
* 下载资产时，如果选择了电子邮件选项，即使提供了有效的电子邮件 ID，下载选项也不可用。(CQ-4296535)
* 另存为智能收藏集的自定义筛选器无法正确应用于资产。(CQ-4294942)
* 多项搜索和索引增强功能与错误修复使性能得以提高。(CQ-4286373)
* 无法在Assets中访问文件夹属性选项卡，并返回500错误。 (CQ-4295701)
