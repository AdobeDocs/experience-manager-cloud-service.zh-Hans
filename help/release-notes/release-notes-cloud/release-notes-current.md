---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 0ef1e1915f2fdbe44cff209851eb43cc9d69958e
workflow-type: tm+mt
source-wordcount: '2261'
ht-degree: 31%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版或 2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates)。

## 发布日期 {#release-date}

的发布日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前功能版本(2024.3.0)为2024年4月11日。 下一个功能版本(2024.4.0)计划于2024年4月25日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- ## Release Video {#release-video}

Have a look at the March 2024 Release Overview video for a summary of the features added in the 2024.3.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新增功能 {#sites-features}

**Edge Delivery Services的AEM创作**

AEM Sites现在可以用作Edge Delivery Services的内容源。 作者在AEM中使用新的通用编辑器通过上下文wysiwyg创作管理其网站。 这使企业能够利用Edge Delivery Services构建快速的高性能网页，同时利用AEM的强大功能进行内容管理。

![AEM 创作](/help/edge/assets/universal_editor_edge_delivery_services.png)

欲了解更多信息，请参见 [文档](/help/edge/overview.md) 并观看 [AEM Gems - AEM创作和Edge Delivery Services快速入门](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/aem-gems-getting-started-with-aem-authoring-and-edge-delivery/m-p/652694#M43905)

**用于Headless实施的通用编辑器**

通用编辑器还使分离的Web应用程序能够利用以前专用于传统站点的直观的上下文内WYSIWYG创作。 内容创建者现在可以使用内容片段，与页面中的组件一样轻松地编辑布局。

Universal Editor与众不同之处在于它适应不同的Web体系结构，能够同时容纳服务器端和客户端渲染，保持与框架无关并消除了AEM托管的必要性。 将现有Web应用程序与通用编辑器集成以进行内容编辑非常简单，主要要求开发人员将特定数据属性合并到其标记中。

这样，无论内容结构或底层技术栈栈如何，通用编辑器都可以确保一致的编辑体验。 欲了解更多信息，请参见 [通用编辑器简介](/help/implementing/universal-editor/introduction.md).

**内容片段和模型的内容管理OpenAPI**

开发人员现在能够以编程方式与内容片段和内容片段模型交互，并使用内容管理OpenAPI对它们执行CruD操作。 有关更多信息，请参阅 [API文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/)

**体验片段的多站点管理支持**

为存储体验片段的文件夹结构扩展了多站点管理支持，允许用户转出包含体验片段的完整内容结构。

**比较内容片段版本**

新的内容片段编辑器现在允许内容作者比较和查看内容片段的当前版本与先前版本之间的差异。

### 早期采用者计划 {#sites-early-adopter}

**生成变体**

通过AEM新功能利用GenAI， [生成变体](/help/generative-ai/generate-variations.md)，现在可在Cloud Service中访问。 生成变体可帮助您通过使用创作AI生成和扩展内容创建。 请联系您的Adobe客户团队以考虑加入计划。

**在内容片段控制台中浏览资产**

内容作者现在可以浏览、查看图像和其他资产并对其执行操作，而无需离开内容片段控制台。

![资产浏览](/help/sites-cloud/administering/content-fragments/assets/cf-console-assets-browse.png)

是否有兴趣试用该功能并分享反馈？使用您的官方电子邮件ID向aemcs-headless-adopter@adobe.com发送电子邮件，了解有关率先采用者计划的更多信息。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理视图中的新增功能 {#admin-view}

**与 Adobe Express 的原生集成**

AEM Assets与Adobe Express进行原生集成，这使您能够从Adobe Express用户界面中直接访问存储在AEM Assets中的资源。 您可以将AEM Assets中管理的内容放在快速画布中，然后将新内容或编辑的内容保存到AEM Assets存储库中。

![从 Assets 加载项纳入资源](/help/assets/assets/adobe-express-native-integration.png)

**所有支持的视频类型都有预览演绎版**

Experience Manager Assets现在默认生成所有受支持视频类型的预览演绎版，而无需处理配置文件配置。

### 资源视图中的新增功能 {#assets-view}

**管理收藏集的权限**

Assets Essentials允许管理员管理存储库中可用专用收藏集的访问级别。 作为管理员，您可以创建用户组并向这些组分配权限以管理访问级别。您还可以将权限管理权限委派给用户组。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### AEM Forms的新增功能 {#forms-new-features}

* **[Adobe Experience Manager FormsEdge Delivery Services](/help/edge/docs/forms/overview.md)**：AEM FormsEdge Delivery Services是一组可组合的服务，可帮助实现快速开发环境，以便作者能够快速更新、发布和启动新表单。 这些服务提供卓越且具有高影响力的表单体验，从而推动参与度和转化率。这些表单体验很容易创作和开发。

  ![EDS Forms功能](/help/edge/assets/eds-forms-features.png)

这些服务使您能够：

* 在相同的表单网站上使用多个内容源并使用首选创作工具，例如Microsoft Excel、Google Sheets或自适应Forms编辑器。
* 提供数字注册体验，通过真实用户监控(RUM)快速加载和呈现并持续监控表单性能。
* 使用纯HTML、新式CSS和vanilla JavaScript创建卓越的体验，避免特定框架的陡峭学习曲线。


### AEM Forms预发行版中的新增功能 {#forms-pre-release}

* **基于核心组件的自适应Forms的增强可视化规则编辑器**：此版本显着升级了基于核心组件的自适应表单的可视化规则编辑器。 此版本显着升级了基于核心组件的自适应表单的可视规则编辑器。 此更新侧重于简化与自定义函数的交互，使您可构建更可靠和更高效的表单。

  您现在可以通过以下方式简化自定义函数交互：

   * 利用新批注提供更清晰的函数定义。
   * 将缓存机制用于自定义函数，可加快表单性能。
   * 在自定义函数中无缝使用全局对象。
   * 在自定义函数中定义并利用可选参数。

  此更新还为规则编辑器功能提供了以下增强功能。 您可以：

   * 为条件执行实施强大的“when-then-else”逻辑。
   * 利用现代JavaScript功能，如let和arrow函数（ES10支持）。
   * 不仅验证或重置字段，而且验证或重置整个面板和表单，从而扩展对用户交互的控制。

  这些改进为在可视规则编辑器中构建规则和自定义函数提供了更直观、更强大的体验。

* **创建自适应表单的多个版本**：您现在可以轻松管理现有表单的变体。 这简化了版本控制并有助于表单优化的比较，所有这些都在单个简化的工作流中。

* **比较自适应表单**：您现在可以轻松比较两个表单以识别两个表单之间的差异。 它通过使团队成员能够比较修订并高效讨论更改而促进顺利的协作。

* **涂鸦签名组件的辅助功能增强**：此更新显着改进了涂鸦签名组件的辅助功能：

  **改进了键盘导航：**
   * 按Tab键可让用户在签名对话框中的所有交互元素中进行导航。
   * 使用画笔或键盘签名并按Enter可关闭对话框。
   * 签名并单击“确定”后，焦点仍然在签名控件上。

  **清除签名功能：**

   * 可通过Tab键访问用于擦除签名的清除交叉图标。
   * 也可以通过选项卡导航访问“清除签名确认”对话框。

  **增强的标签和控件：**
   * 键盘签名按钮的标签现在更清晰了，使用“aria-label”来公告功能（例如“aria-label=&#39;Sign using Keyboard&#39;”）。
   * 改进的对比度确保涂鸦签名中的所有控件很容易区分。
   * 现在，“确定/复选标记”按钮会以可视方式指示其处于非活动状态。

  **屏幕Reader的签名反馈：**
   * 键入签名时，屏幕阅读器用户可以听到用于创建签名的文本。

此更新通过改进涂鸦签名组件的导航、清晰度和反馈，确保残障用户获得更包容的体验。

### 早期采用者计划 {#forms-early-adopter}

* **[将自适应表单提交到Adobe Workfront Fusion场景](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**：Formsas a Cloud Service提供了一个现成的选项，可轻松地将自适应表单与Adobe Workfront连接。 这简化了将自适应表单提交到 Adobe Workfront 场景的过程，使您可在提交自适应表单时触发 Workfront Fusion 场景。

  <br/> ![Adobe Workfront](/help/forms/assets/adobe-workfront.png) <br/> 使用Adobe Workfront Fusion连接器，您可以设计在提交自适应表单时自动触发的工作流。 例如，设想一个方案，其中启动一个工作流，向特定个人分配审核已提交数据的任务，允许根据通过自适应表单捕获的信息批准或拒绝应用程序。 这一简化的集成提高了效率，并将工作流流程的自动化水平提高到了一个新的水平。|

* **Reader扩展服务**： AEM Forms Communication API提供了Reader扩展服务，可让您为常规PDF添加表单填写和注释等功能，从而通过免费的Adobe Reader向用户提供交互式功能。

* [支持从右向左书写的语言](/help/forms/supporting-new-language-localization-core-components.md)：现在可用从右向左书写 (RTL) 的语言（如阿拉伯语、波斯语和乌尔都语）展示基于核心组件构建的自适应表单。全球有超过 20 亿人使用 RTL 语言。使用 RTL 语言的表单可扩大您自适应表单的覆盖范围，以满足这些不同受众的需求并选择进入 RTL 市场。在某些地区，提供当地语言的表单还是一项法律规定。通过使用当地语言，您不仅可以满足更广泛的受众的需求，还可以确保遵守相关法律法规。

* **[用 DocAssurance API（Communication API 的一部分）保护文档](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 使您能够通过为文档签名和加密来保护敏感信息。通过加密，可将文档内容转换为无法读取的格式，从而确保只有获得授权的用户可访问。这一层加强的保护不仅防止未经授权地查看宝贵的数据，还能让人安心。利用 Signature API，您的组织可以保护其分发和接收的 Adobe PDF 文档的安全和隐私。此服务使用数字签名和认证确保只有预期的接收者可更改文档。

  您可以通过您的官方电子邮件 ID 向 `aem-forms-ea@adobe.com` 发送电子邮件，以加入早期采用者计划并请求对该功能的访问权限。

* **[您可以利用真实用户监控 (RUM) 数据服务](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**为 AEM as a Cloud Service 启用客户端收集。
真实用户监控 (RUM) 数据服务能够更准确地反映用户交互，确保可靠地衡量网站参与度。这是一个深入了解页面性能的绝佳机会。而这对于使用 Adobe 管理的 CDN 或非 Adobe 管理的 CDN 的客户都很有用。此外，对于使用非 Adobe 管理的 CDN 的客户，现在可为其启用自动流量报告，这样即无需与 Adobe 共享任何流量报告。

  如果您有兴趣测试这项新功能并分享您的反馈，请从您与您的 Adobe ID 关联的电子邮件地址将一封电子邮件发送到 `aemcs-rum-adopter@adobe.com`，其中包含您要为其启用 RUM 的每个环境的域名。Adobe 的产品团队随后将为您启用真实用户监控 (RUM) 数据服务。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 早期采用者计划 {#foundation-early-adopter}

#### 流量过滤器规则警报（早期采用者计划） {#traffic-filter-rules-alerts-early-adopter}

最近发布的 [流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)包括可选许可的Web应用程序防火墙(WAF)规则，允许您配置应该允许或拒绝哪些流量。

现在您可以发送电子邮件至 **<aemcs-cdn-config-adopter@adobe.com>** 以加入率先采用者计划，这样您就可以在触发流量过滤器规则时收到警报。 操作中心电子邮件通知会在发生某些流量情况时通知您，以便您采取适当的措施。

#### CDN配置（早期采用者计划） {#cdn-config-early-adopter}

除了最近发布的 [流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)，包括可选许可的Web应用程序防火墙(WAF)规则，提供了使用配置管道声明和部署其他类型的CDN配置的机会。 [了解详情](/help/implementing/dispatcher/cdn-configuring-traffic.md) 并通过发送电子邮件加入率先采用者计划 **<aemcs-cdn-config-adopter@adobe.com>** 要获得对以下内容的访问权限：

* 301/302 客户端重定向
* 在边缘将请求代理到任意源(例如非AEM应用程序)
* URL 转换
* 设置或修改请求或响应标头
* CDN 无法访问 AEM 时显示的自定义错误页面

#### Apache/Dispatcher运行时摄取重写映射（早期采用者程序） {#apache-rewritemaps-early-adopter}

与AEM 6.5类似，Apache/Dispatcher将摄取并加载放置在发布存储库中特定位置的重写映射，而无需执行Web层管道。 这为企业用户提供了使用UI（如ACS Commons重定向映射管理器提供的用户界面）声明重定向的机会。 请联系 **<aemcs-cdn-config-adopter@adobe.com>** 以了解更多信息。

#### Edge Side Include (ESI)用于加载动态内容（早期采用者计划） {#esi-early-adopter}

Adobe托管的CDN现在支持Edge Side Include (ESI)，这是一种用于边缘级动态Web内容汇编的标记语言。 通过包含ESI片段，您可以在CDN上缓存具有较高TTL的整个HTML页面，同时更频繁地从源位置提取需要更高节奏更新（较低TTL）的较小部分。 请联系 **<aemcs-cdn-config-adopter@adobe.com>** 以了解更多信息。

#### RDE支持使用站点主题和站点模板的前端代码（早期采用者计划） {#rde-frontend-early-adopter}

对于早期采用者，[快速开发环境 (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 现在支持基于[站点主题](/help/sites-cloud/administering/site-creation/site-themes.md)和[站点模板](/help/sites-cloud/administering/site-creation/site-templates.md)的前端代码。在 RDE 的情况下，使用命令行指令而非[前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)实现这一点。请联系 **<aemcs-rde-support@adobe.com>** 以试用并提供反馈。

#### 增强了RDE的日志记录功能（率先采用者计划） {#rde-logging-early-adopter}

在中调试代码时 [快速开发环境(RDE)](/help/implementing/developing/introduction/rapid-development-environments.md)，开发人员现在可以使用命令行更高效地配置和流式传输日志，而无需修改版本控制中的OSGI属性。 功能包括：

* 在每个包或类级别上声明日志级别
* 自定义日志输出格式
* 并行流式传输多个日志

请联系 **<aemcs-rde-support@adobe.com>** 以试用并提供反馈。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
