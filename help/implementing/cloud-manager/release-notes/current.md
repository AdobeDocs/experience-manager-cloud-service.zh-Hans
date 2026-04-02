---
title: Cloud Manager 2026.4.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2026.4.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 6c98a27889257a6d8befa04a2b2c4e5a7e6e49f2
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 20%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2026.4.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2026.4.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2026.4.0的发布日期是2026年4月2日星期四。

下一个计划发布于2026年5月7日星期四。


## 新增功能 — Cloud Manager {#cloud-manager-whats-new}

* 用于AI支持的IDE的&#x200B;**Cloud Manager MCP服务器**

  您现在可以使用MCP（模型上下文协议）服务器，该服务器将Cloud Manager公共API公开为启用了AI的IDE（例如光标）的工具。 连接后，您可以使用对话提示列出和管理项目、管道、环境和存储库，帮助您在不离开编辑器的情况下更快地移动。

  请参阅文档[将MCP用于AEM as a Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)。

  请参阅教程[Cloud Manager MCP服务器](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/ai/mcp-servers/cloud-manager#)。

* 使用模块缓存更快地生成&#x200B;**&#x200B;**

  新的构建模型使用模块级缓存仅编译已更改的模块（而不是整个存储库）以缩短构建时间。 它适用于代码质量非生产管道和开发全栈非生产管道。

  请参阅[关于在非生产管道中使用Smart Build](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build)和[添加非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)。

* **自助主机连接检查**

  Cloud Manager现在允许您从环境中运行自助检查。 这些检查将验证主机和端口的可达性，并使用您程序配置的网络路径（包括出口）确认DNS解析。 此功能可帮助您验证高级联网并更快地解决集成问题，而无需打开支持案例或访问Pod。<!-- SKYOPS-23640 -->

  请参阅[网络连接测试](/help/security/network-connectivity-test.md)

* **改进的稳定性、性能和可靠性**

  此版本包括优化和维护更新，这些更新改进了Cloud Manager的稳定性、性能和可靠性。


## Beta 计划 {#private-beta-program}

参与 Cloud Manager 的 beta 计划，在即将推出的功能正式发布之前获得独家访问权限。

>[!IMPORTANT]
>
>Beta版本可能包含缺陷，并“按原样”提供，无任何类型的担保。 Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持（通过Adobe支持服务或其他方式）Beta版。 Adobe建议客户谨慎使用，不要依赖测试版或随附的任何文档或材料的正确功能或性能。 Beta版中的功能和API如有更改，恕不另行通知。 因此，使用测试版完全由客户自行承担风险。

另请参阅[AEM Beta程序](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

目前提供以下机会：

### Edge Delivery Services具有AEM创作和灵活的发布层配置 {#eds-with-aem-authoring}

Cloud Manager引入了两项旨在支持现代交付体系结构的功能。

* 具有AEM创作功能的&#x200B;**Edge Delivery Services**
您现在可以使用Edge Delivery Services交付站点，同时继续在AEM创作模式下创作内容。 根据您的工作流首选项，您可以选择以下创作方法：

   * 基于文档的创作
   * AEM基于创作的创作

有关详细信息，请参阅[在Cloud Manager中创建Edge Delivery站点](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md#one-click-edge-delivery-site)。

* **灵活的发布层配置**
Cloud Manager现在允许您配置项目是否需要发布层。 这种灵活性允许您设置更好地匹配所选交付架构的环境。

有关详细信息，请参阅[灵活发布层(Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier)。

要加入Beta，请使用您的Adobe组织ID和项目ID向[grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com)发送电子邮件。

### 通过模块缓存加快构建速度 {#quick-build-cm-pipelines}

新的构建模型使用模块级缓存仅编译已更改的模块（而不是整个存储库），以缩短构建时间。 适用于生产管道。 您控制哪些生产管道使用&#x200B;**智能生成**。

有关更多信息，请参阅以下内容：

* [在生产管道中使用Smart Build](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#about-smart-build)。
* [添加生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#full-stack-code)。

要加入Beta，请使用您的Adobe组织ID和项目ID向[beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com)发送电子邮件。

<!-- OLD
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

<!-- OLD
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.
-->



## 错误修复 {#bug-fixes}

2026年4月发行的Cloud Manager版本没有重大错误修复。

<!-- ## Known issues {#known-issues} -->

