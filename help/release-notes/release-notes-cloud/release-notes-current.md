---
title: Adobe Experience Manager 云服务 2020.6.0 发行说明
description: Experience Manager 2020.6.0 发行说明
translation-type: tm+mt
source-git-commit: a725e5729d1086aba64ec59ed909577f25219aa9
workflow-type: tm+mt
source-wordcount: '1700'
ht-degree: 7%

---


# AEM 云服务 2020.6.0 发行说明 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.6.0 的常规发行说明。

## 发布日期 {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.6.0 is June 04, 2020.

## AEM Sites 的新增功能 {#aem-sites}

阅读本节内容，了解 AEM 云服务版本 2020.6.0 中 AEM Sites 的新增功能和更新。

### 错误修复 {#sites-bug-fixes}

* 在页面上再次复制和粘贴布局容器时，布局容器内的组件不可见。

* 修复了调整布局组件大小的问题。

* 添加了仅管理路由角度页面和AEM/角度页面的功能。

### 辅助功能 {#accessibility}

* 现在，在浏览模式下使用向下箭头导航时，“创建页面” **对话框中的** “砌体”项目可以使用旁白角色和状态。

* 在导航中添加了链接，以允许用户跳到主内容。

* 屏幕阅读器改进。


## AEM作为云服务的基础的新增功能 {#foundations}

通过删除AEM项目的pom.xml中对远程存储库的所有引用，AEM项目构建时间将会缩短 `https://downloads.experiencecloud.adobe.com/content/maven/public`。

AEM作为云服务SDK API Jar（以前在该位置托管）现在位于Maven Central中，Maven是Maven的默认对象存储库。

## Cloud Manager 的新增功能 {#cloud-manager}

阅读本节内容，了解 AEM 云服务版本 2020.6.0 中 Cloud Manager 的新增功能和更新。

### 新增功能 {#what-is-new-cloud-manager}

* 在云管理器中 *具有* “业务所有者”角色的用户现在可以从登陆页(通过项目卡上的快速操作按钮)或项目中删除沙箱项目。

* 现在，在云管理器 *中，业务* 所 *有者或部署管理器角色中的沙箱项目* ，可以通过云管理器UI删除其生产环境集和阶段集。 现在，可从概述页面和环境页面上的环境卡中使用删除选项。 在生产或舞台上选择删除选项也会删除集合中的另一个。

* 指导登陆页上的标记，以告知和指导用户基本导航。

* 指导“概述 ** ”页面上的标记，以通知并指导用户在云管理器中进行基本导航，以开始这些导航。

* “ **学习** ”页面现在在云管理器中可用，可通过顶部导航访问。 本页包含可帮助用户了解与他们在云管理器中分配的角色相关、最常使用的工作流的资源。

* 沙箱项目现在通过沙箱 **徽章** 进行标识，该徽章将显示在登陆页卡上的项目卡上以及“概述”页中的项目名 *称旁* 。

* 具有SysAdmin角 *色的用户* ，现在只需单击一下即可访问Admin Console中的位置，从中可以管理用户角色或云管理器权限。 在 **“添加** 项目”按钮旁的登陆页上将显示“ **管理角色** ”按钮。

* 具有SysAdmin角色的用户现在可以通过CM单击一次访问创作实例。

* 生成日志现在包含已发现对象的列表，包括跳过的内容包。

* “构建”步骤现在验证所有生成的内容包是否包含所有必需属性——名称、组和版本。

* “构建”步骤现在验证构建是否生成了至少一个内容包。

### 错误修复 {#bug-fixes-cm}

* 在某些情况下，“创建项目”对 **话框中的图** 标未对齐。

* AEM版本标识符在概述页面上显示 *不一* 致。

* 配置生产管道时，某些 **客户看不到** “计划部署”选项。

### 已知问题 {#known-issues-cm}

* 当在某一持续时间内未检测到环境时，沙箱项目内的活动将被休眠。 在云管理器中不会观察此状态。 但是，状态可以通过开发人员控制台来观察。 此问题将在即将发布的版本中解决。

* 直接从云管理器指向开发人员控制台的链接将不显示用于将沙箱项目的环境解除休眠／休眠的选项。 要解决此问题，请在“Developer Console(开发人员 `#release-cm-p1234-e5678` 控制台)”中，将模式添加到url的末尾， *其中1234* 是项目ID, *5678* 是环境ID。 此问题将在即将发布的版本中解决。

##  的新增功能[!DNL Adobe Experience Manager Assets]{#aem-assets}

<!-- 
Assets RNs are being authored and are a work in progress.
PM/EM review required before publishing.
-->

**增强智能标记的引导用户体验，由Adobe Sensei提供支持**

增强的智能标记允许组织培训智能标记模型，以除通用智能标记外，还根据客户特定的业务标记识别图像。

在此版本中，提供了新的指导式用户体验，可帮助为客户特定标签集设置智能标签培训并使用资产进行培训，这些标签在将来应该能够识别并标记。 这是一种更直观的体验。
培训增强的智能标签，以更直观地培训智能标签。 了 [解如何智能标记](/help/assets/smart-tags.md)[和配置智能标记](/help/assets/smart-tags-configuration.md)。

**支持3D内容的摄取、预览和投放**

组织现在可以在AEM资产中存储和使用3D文件。 用户可以上传、预览和利用各种核心3D文件，包括。obj、.stl、.gltf和。glb文件。 此外，还可 [!DNL Dynamic Media]以通过不可知的URL或查看器配置和提供3D体验。 这包括3 [!DNL Dynamic Media] D Experience Viewer、Sites 3D Viewer组件，以及通过(AR/VR)交付3D [!DNL Dynamic Media] 文件的功能。

<!-- TBD: Add link to the DM help article, if any. -->

<!-- Hiding this as the GA is at a later date. 
TBD: Add link to the AAL help article. 

**Adobe Asset Link support for Adobe XD**

With the latest release, [!DNL Experience Manager Assets] provides support for a new [!DNL Adobe Asset Link] plug-in that is released with [!DNL Adobe XD] v29. The integration allows designers to access and use assets from [!DNL Experience Manager] in their designs, without the need to leave [!DNL Adobe XD] application.

-->

**辅助功能增强**

[!DNL Adobe Experience Manager Assets] 现在可按照Web内容辅助功能指导原则(WCAG)v2.1原则更方便地访问。 对以下用例或界面的辅助功能进行了改进：

* 用户界面元素、控件、页面和对话框对屏幕阅读器友好。
* 用户界面元素、控件和输入表单字段可使用键盘访问。
* 更改某些界面元素的颜色或对比度，使视觉受限且无颜色感知的用户能够更清楚地识别这些元素。 例如，资产现在在“属性”页面和卡视图的星 [!UICONTROL 级] 图标中具有适当的对比度。

<!-- TBD: Add link to the a11y help article if created. Else add it post-GA. -->

**其他增强功能**

该版本提供了以下附加增强功能：

* 资产用户界面的辅助功能改进。
* 能够使用资产处理用户档案重新处理资产，让用户完全控制该流程(运行完全资产处理，只需应用特定处理用户档案，并决定是否应运行后期处理工作流)。
* 当基础群集实例在后台重新启动时，搜索查询返回结果的速度会更快（在以前的情况下，初始搜索运行可能会持续更长时间）。
* 在资产界面的列表视图和搜索结果中查看资产时，按“名称”排序。
* 在“资产”界面的列表视图和搜索结果中查看资产时，按“创建日期”进行排序。
* 支持将EPS文件转换为图像。

### 错误修复 {#assets-bug-fixes}

<!-- TBD: Add enhancements above and bug fixes below.
Seek DM bug fixes if any.
Add Nui update as shared on Slack: https://git.corp.adobe.com/nui/app/releases/tag/22
-->

除了上述新增功能，当前版本还根据客户反馈提供以下增强和错误修复 [!DNL Assets]。

* 对于MP3音乐文件，在DAM预览的缩略图上显示的播放按钮不起作用。 (CQ-4294731)
* 将指针悬停在卡视图上时，屏幕会因（自动）聚焦卡中可用的快速操作而滚动。 (GRANITE-26895)
* 滚动大量搜索结果后显示过多图像会导致浏览器崩溃。 (GRANITE-26432)
* 管理 [!UICONTROL 出版物]页面上的 [!UICONTROL “选项”、“范围]”和“工作流 [!UICONTROL ”进度指示符，] 屏幕阅读器不会将其读出为进度指示符。 相反，屏幕阅读器用户将这些状态指示器视为选项卡列表。 (CQ-4273015)
* 下载资产时，如果选择了电子邮件选项，即使提供了有效的电子邮件ID，下载选项也不可用。 (CQ-4296535)

* 在资产的“属 [!UICONTROL 性] ”页面中添加标记时，用户导航标记树结构。 树结构无法访问，因为屏幕阅读器用户在导航时不会听到任何声音。 (CQ-4272964)
* 在链接共享对话框中，在浏览模式下导航时，屏幕阅读器，

   * 加载对话框后立即对表信息进行解说。
   * 无法导航到所有列出的自动建议。
   * 不会为“添加电子邮件地址／搜索”组合 [!UICONTROL 框显示自动建议] 。 (CQ-4294232)

* 在元数据模式编辑器的NVDA浏览模式下，拖动选项无法使用键盘。 (CQ-4296326)
* 在“资产”用户界面上，视图设置无法通过键盘访问。 (CQ-4289038)
* 另存为智能收藏集的自定义过滤器无法正确应用于资产。 (CQ-4294942)
* 多项搜索和索引增强功能和错误修复可提高性能。 (CQ-4286373)
* 对于黄色等级图标，发光度比小于3:1。 它对视力有限、对颜色没有感知的用户并不有用。 等级星体显示在资 [!UICONTROL 产属性][!UICONTROL “高级”选项卡] 的“等级 [!UICONTROL ”部分或] 卡视图中(CQ-4295106)
* 组合框的列表框下拉框（位于不同页面上的各个字段中）现在将条目显示为屏幕阅读器可以宣布的选项的列表。 (CQ-4294017)
* 无法使用键盘访 [!UICONTROL 问时间] 轴中的V形向上箭头，以将工作流应用于资产。 (CQ-4289268)
* 现在，屏幕 [!UICONTROL 阅读器可]以访问用于删除“属性”“基本”选项卡中“ [!UICONTROL 标记][!UICONTROL ”字段下] 每个选定标记的选  项（含x）。 (CQ-4273033)
* 只读表单字段(例如资产属性“基本”选 [!UICONTROL 项卡上禁] 用的 [!UICONTROL 字段])现在可使用键盘聚焦。 (CQ-4273031)
* 现在可以使用键盘访问打开过滤器提要栏的选项。 (CQ-4273018)
* 各种组合框元素（如路径字段和在资产属性的“基本”选项卡中打开“选择”对话框的选项）的用途现在由屏幕阅读器正确宣布。 (CQ-4273016)
* [!UICONTROL 元数据模式编辑] 器页面及其元素无法使用键盘访问，并且屏幕阅读器不友好。 (CQ-4272953)
* 无法使用键盘访问视频音量控件。 (CQ-4272696)
* 资产用户界面上的许多可操作选项在使用键盘时不表示焦点。 (CQ-4272694)
* 屏幕阅读器用户不知道在使用键盘时，列表视图中的行是可选的。 只有鼠标悬停在行上时，才会宣布该信息。 (CQ-4271824)
* 某些表单字段（如登录页上的用户名和口令字段）只依赖占位符值来提供辅助标签。 (CQ-4271716)
* 现在，可以使用键盘访问交互式用户界面元素，如链接和选项（在资产页面的标题和缩放选项、文件夹导航中）。 (CQ-4271412)
* 资产上所有已浏览页面的 [!DNL Adobe Experience Manager] 标题现在是唯一的。 (CQ-4271409)
