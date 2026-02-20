---
title: Cloud Manager 2026.1.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2026.1.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 2ea076c42a6406548bf48cd246227fc8ddb3a080
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 43%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2026.1.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2026.1.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2026.1.0的发布日期是2026年1月22日星期四。

下一个计划发布于2026年2月5日星期四。

## 新增功能 — Cloud Manager {#cloud-manager-whats-new}

* **配置管道现在支持托管密钥**

  用户现在可以直接在Cloud Manager配置管道中添加和管理密钥。 这些密钥安全地覆盖管道配置规范中的值，并支持灵活、特定于环境的部署。

  ![查看/编辑所选管道下拉菜单上的变量选项](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-option.png)
  *所选管道的下拉菜单上的“查看/编辑变量”选项。*

  ![变量配置对话框&#x200B;](/help/implementing/cloud-manager/release-notes/assets/view-edit-variables-variablesconfig-dialogbox.png)*变量配置对话框。*

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

### Experience Hub 可扩展性和自定义 {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) 是您进入 AEM 的入口点，可根据组织需求进行自定义。请告知 Adobe 您现有的 AEM UI 扩展，以便他们协助您在 Experience Hub 中轻松启用这些功能。

![Experience Hub 可扩展性和自定义工作流程示意图](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

在 Experience Hub 中嵌入自定义体验，扩展和个性化组织的仪表板。除了 Adobe 的内置构件之外，还可以使用 [UI 可扩展性](https://developer.adobe.com/uix/docs/)框架添加您自己的构件。构建基于 JavaScript 的 UI 应用程序，并将其呈现给您的用户，以满足特定业务需求和工作流程。

是否对 Beta 感兴趣？向 [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) 发送电子邮件，其中包含您的 Adobe OrgID 以及要创建自定义设置的简短说明。

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

2025年12月的Cloud Manager版本没有重大错误修复。


<!-- ## Known issues {#known-issues} -->

