---
title: Cloud Manager 2026.3.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2026.3.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: eb3e826e27e14b8b1da534440f11d43e973130ec
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 20%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2026.3.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2026.3.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2026.3.0的发布日期是2026年3月5日星期四。

下一个计划发布于2026年4月2日星期四。


## 新增功能 — Cloud Manager {#cloud-manager-whats-new}

* **Cloud Manager现在支持**&#x200B;内容副本&#x200B;**导入的**&#x200B;擦除&#x200B;**选项**

  启用&#x200B;**划出**&#x200B;后，Cloud Manager会在开始导入之前删除目标上的现有内容，这样您就可以从头开始，避免与预先存在的内容冲突。 如果您禁用&#x200B;**擦除**，Cloud Manager会在现有目标内容之上导入新内容。 擦除开始前会显示确认提示，Cloud Manager将记录擦除操作和导入详细信息以便进行跟踪。

  另请参阅[复制内容](/help/implementing/developing/tools/content-copy.md#copy-content)。

* **在AEM Experience Hub中支持UI可扩展性**
[AEM Experience Hub](https://experience.adobe.com/experiencemanager)中对UI扩展的支持现已启用，从而让开发人员能够使用Adobe App Builder构建的自定义功能和构件来扩展界面。

  若要了解更多信息，请参阅[AEM Experience Hub](https://developer.adobe.com/uix/docs/services/aem-experience-hub/)。

* **改进的稳定性、性能和可靠性**

  此版本包括优化和维护更新，这些更新改进了Cloud Manager的稳定性、性能和可靠性。


## Beta 计划 {#private-beta-program}

参与 Cloud Manager 的 beta 计划，在即将推出的功能正式发布之前获得独家访问权限。

>[!IMPORTANT]
>
>Beta版本可能包含缺陷，并“按原样”提供，无任何类型的担保。 Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持(通过Adobe支持服务或其他方式)Beta版。 Adobe建议客户谨慎使用，不要依赖测试版或随附的任何文档或材料的正确功能或性能。 Beta版中的功能和API如有更改，恕不另行通知。 因此，使用测试版完全由客户自行承担风险。

另请参阅[AEM Beta程序](/help/release-notes/release-notes-cloud/release-notes-current.md#aem-beta-programs)

目前提供以下机会：
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### 适用于AI支持的IDE的Cloud Manager MCP服务器{#mcp-server-for-cm}

现在，您可以尝试使用一个MCP（模型上下文协议）服务器，该服务器会将Cloud Manager公共API公开为启用了AI的IDE（例如光标）的工具。 连接后，您可以使用对话提示列出和管理项目、管道、环境和存储库，帮助您在不离开编辑器的情况下更快地移动。

请参阅文档[将MCP用于AEM as a Cloud Service](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)。

请参阅教程[Cloud Manager MCP服务器](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-server/cloud-manager#)。

是否对 Beta 感兴趣？使用您的Adobe OrgID和项目ID向[GRP-AEM-CM-MCP-FEEDBACK@adobe.com](mailto:GRP-AEM-CM-MCP-FEEDBACK@adobe.com)发送电子邮件。


<!--
### Experience Hub Extensibility and Customization {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) serves as your entry point to AEM, customized for your organization's needs. Tell Adobe about your existing AEM UI Extensions so they can help you enable them in Experience Hub with minimal effort.

![Diagram of Experience Hub extensibility and customization workflow](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Embed custom experiences in Experience Hub to extend and personalize your organization's dashboard. In addition to Adobe's built-in widgets, add your own using the [UI Extensibility](https://developer.adobe.com/uix/docs/) framework. Build JavaScript-based UI apps and surface them to your users to meet business-specific requirements and workflows. 

Interested in the beta? Email [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) with your Adobe OrgID and a short description of the customization you intend to create.
-->

### 通过模块缓存加快构建速度 {#quick-build-cm-pipelines}

新的构建模型使用模块级缓存仅编译已更改的模块（而不是整个存储库）以缩短构建时间。它适用于代码质量、全栈和仅限暂存的管道。

![编辑非生产管道对话框，其中显示两个生成策略选项，即“完全生成”和“智能生成”](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png)
*显示“完全生成”和“智能生成”这两个生成策略选项的“编辑非生产管道”对话框。*

在&#x200B;**添加/编辑管道**&#x200B;对话框的&#x200B;**Source代码**&#x200B;选项卡下，新增的&#x200B;**生成策略**&#x200B;部分允许您选择以下生成选项之一：

* **完整内部版本** — 每次运行都会在存储库中生成所有模块。
* **智能生成** — 仅生成自上次提交以来更改的模块，这会缩短总体生成时间。

您控制哪些管道使用&#x200B;**智能生成**。 在Beta测试期间，此选项仅对&#x200B;**代码质量**&#x200B;和&#x200B;**开发部署**&#x200B;管道显示。

是否有兴趣？向 [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) 发送电子邮件，其中包含您的 Adobe OrgID 和项目群 ID。

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->

## 错误修复 {#bug-fixes}

* 解决了恢复点API在检索恢复点时可能返回500错误的问题。 现在，端点可正确处理空值，从而确保一致且可靠的响应。 (CMGR-72963)
* Cloud Manager现在接受带或不带`.git`后缀的GitHub存储库URL，使API行为与UI保持一致，并使存储库载入更加灵活。 (CMGR-73296)
* 产品配置文件名称验证现在不区分大小写，可在创建名称仅因大写不同而异的配置文件时防止出错。 (CMGR-74075)
* 您现在可以从同一管道执行中执行多个恢复操作，从而为环境（如暂存和生产）实现顺序恢复，而无需运行新的管道。 (CMGR-73538)


<!-- ## Known issues {#known-issues} -->

