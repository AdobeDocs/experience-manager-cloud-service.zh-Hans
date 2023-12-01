---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: a801e6c605fff46ca07699727f3078c9a285a943
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 24%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版或 2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的发布日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前功能版本(2023.11.0)为2023年11月30日。 下一个功能版本(2023.12.0)计划于2023年12月14日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

请查看2023年11月发布概述视频，了解2023.11.0版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 早期采用者计划 {#sites-early-adopter}

**[查找和替换内容片段中的字符串](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**：内容片段控制台为用户提供了一种简单直观的方式，用于替换同时出现在多个内容片段中的字符串，以加快内容速度。

![查找和替换](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

想试用该功能并分享反馈吗？发送电子邮件至 **aemcs-headless-adopter@adobe.com** 从您的官方电子邮件ID了解有关率先采用者计划的更多信息。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 资源视图中的新增功能 {#assets-view-features}

* **AEM Assets中的嵌入式Adobe Express编辑器**：有权访问Express的用户现在可以直接在AEM Assets中使用Adobe Express和Adobe Firefly集成的图像编辑和创建工具，以提高内容重用和加快内容速度。

  ![将元数据表单分配给文件夹](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **分析中的存储使用情况报表**：管理员现在可以查看作为Insights的一部分提供的存储使用情况报表。

  ![存储使用情况洞察](/help/assets/assets/storage-usage-insights.png)

* **搜索第一个主页配置**：现在通过Experience Manager Assets可为组织配置主页体验。 如果选择先搜索作为主页，则可以为您的组织配置搜索栏对齐方式、背景图像和徽标。

  ![搜索第一个配置](/help/assets/assets/search-first-configuration.png)

### 管理员视图的预发行版中的新增功能 {#admin-view-features-prerelease}

**视频预览**：默认情况下，AEM Assets现在会生成所有受支持视频格式的预览演绎版，而无需配置处理配置文件。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] 中的新增功能 {#forms-features}

* **[复选框组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**：基于核心组件的自适应Forms现在可以包含复选框组件。 它允许用户进行二进制选择，选择或取消选择特定选项。 它通常会显示为一个小框，单击或点按该框可在两种状态之间切换：选中和取消选中。 复选框是用于显示yes/no或true/false选项的常见表单元素。

* **[条款和条件组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**：基于核心组件的自适应Forms现在可以包含条款和条件组件。 它允许表单作者在表单中引入特定部分，向用户显示与服务、产品或平台的使用相关的条款、条件或法律协议。 此组件旨在通过提交表单告知用户他们同意遵守的规则、法规和义务。

  ![复选框、条款和条件以及垂直选项卡组件](/help/forms/assets/forms-components.png)

* **[垂直选项卡组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**：基于核心组件的自适应Forms现在可以将表单内容整理到垂直选项卡列表中，提供结构化和可导航的布局。 在表单中使用垂直选项卡可以通过简化导航和改进表单内容的组织来增强整体用户体验，尤其是在表单包含多个部分或复杂信息的情况下。



### [!DNL Forms] 预发行版本中的新增功能 {#prerelease-features-forms}

* **[将自适应Forms连接到Microsoft® SharePoint列表](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**：AEM Forms提供了一个OOTB集成，可用于将表单数据直接提交到SharePoint List，让您能够利用SharePoint的“列表”功能。 您可以将Microsoft SharePoint列表配置为表单数据模型的数据源，并使用 **使用表单数据模型提交** 提交操作以将自适应表单连接到SharePoint列表。

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期采用者计划 {#forms-early-adopter}

* **将自适应表单提交到Adobe Workfront Fusion场景**：Formsas a Cloud Service提供开箱即用的选项，可轻松地将自适应表单与Adobe Workfront连接。 这简化了将自适应表单提交到Adobe Workfront场景的过程，允许您在提交自适应表单时触发Workfront Fusion场景。

* **从右至左语言支持**：基于核心组件构建的自适应Forms现在能够以从右至左(RTL)语言呈现，如阿拉伯语、波斯语和乌尔都语。 全球有超过20亿人使用RTL语言。 通过RTL语言中的表单，您可以扩展自适应表单的覆盖范围，以迎合这些不同的受众并利用RTL市场。 在某些地区，提供当地语言表格也是法律要求。 通过容纳本地语言，您不仅可以向更广泛的受众敞开大门，还可以确保遵守相关法律和法规。

  ![从右至左语言支持](/help/forms/assets/right-to-left-language-support.png)

* **[用 DocAssurance API（Communication API 的一部分）保护文档](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 使您能够通过为文档签名和加密来保护敏感信息。通过加密，可将文档内容转换为无法读取的格式，从而确保只有获得授权的用户可访问。这一层加强的保护不仅防止未经授权地查看宝贵的数据，还能让人安心。利用 Signature API，您的组织可以保护其分发和接收的 Adobe PDF 文档的安全和隐私。此服务使用数字签名和认证确保只有预期的接收者可更改文档。

  您可以通过您的官方电子邮件 ID 向 `aem-forms-early-adopter-program@adobe.com` 发送电子邮件，以加入早期采用者计划并请求对该功能的访问权限。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 现在可以许可WAF流量过滤器规则 {#cdn-waf-license}

流量过滤规则于10月发布，其中包括一条说明：特殊类别的Web应用程序防火墙(WAF)规则将于今年晚些时候提供，以补充Sites和Forms客户已有的规则。 作为更新，现在可以许可WAF-DDoS保护产品。

获得许可后，可以使用Cloud Manager配置管道将这些高级WAF规则部署到CDN中，从而添加额外的一层保护来抵御Web攻击。

阅读关于 [流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)，包括WAF。 与您的AEM客户团队讨论许可WAF-DDoS保护或增强安全性。

### CDN配置早期采用者计划 {#cdn-config-early-adopter}

除了最近发布的 [流量过滤器规则（包括WAF）](/help/security/traffic-filter-rules-including-waf.md)，则有机会使用配置管道来声明和部署其他类型的CDN配置。 我们很乐意了解您的用例，包括：
* 301/302客户端重定向
* 将边缘上的请求代理到任意源
* URL转换
* 设置或修改请求或响应标头
* CDN无法访问AEM时的自定义错误页面
* 通过用户名/密码进行身份验证
* 任何其他有用的CDN配置

发送电子邮件至 **aemcs-cdn-config-adopter@adobe.com** 来自您的官方电子邮件ID以及您的反馈。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。

## 已知问题 {#known-issues}

* 无法提交基于核心组件的自适应Forms。 使用核心组件版本2.0.38 - 2.0.60构建的自适应Forms出现问题。

  要解决此问题。 您可以迁移到自适应表单核心组件版本2.0.62或更高版本。 要为您的环境设置自适应Forms核心组件版本， [设置core.forms.components.version、core.forms.components.af.version和core.wcm.components.version组件的版本](/help/forms/enable-adaptive-forms-core-components.md#2-add-adaptive-forms-core-components-dependencies-to-your-git-repository) 基于Formsas a Cloud Service存储库或AEM原型的项目中的依赖项，以及 [将更改部署到Formsas a Cloud Service环境](/help/forms/enable-adaptive-forms-core-components.md#build-and-deploy-updated-code-on-an-aem-forms-as-a-cloud-service-environment). 您可以在以下位置找到最新版本的自适应Forms核心组件依赖项： [自适应Forms核心组件Git存储库](https://github.com/adobe/aem-core-forms-components#system-requirements).
