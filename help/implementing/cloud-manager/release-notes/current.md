---
title: Cloud Manager 2025.12.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2025.12.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 7c1f1f1022fd63c190a493d312ab1f355859d15a
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 59%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.12.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.12.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2025.12.0的发布日期是2025年12月4日星期四。

下一个计划发布于2026年1月22日星期四。

## 新增功能 — Experience Hub {#experience-hub-whats-new}

* **简化了Experience Hub的访问**

  已删除用户角色选择，并为&#x200B;**预设**&#x200B;选择（内容作者、资产库管理员、管理员和IT）添加了指南。

* **公告**&#x200B;和&#x200B;**产品更新**

  您可以在可用公告之间切换和迭代，也可以取消它们。

* **最近访问**

  添加了对其他页面和资源（包括页面编辑器、资产、项目和管道执行详细信息、安全页面）的支持。

* **项目列表**

  显示贵组织中的AEM Cloud Manager程序，并可快速访问Cloud Manager详细信息页面。

* **AEM 指南**

  适用于已启用AEM Guides加载项的创作环境的快速操作和快捷键。

## 新增功能 — Cloud Manager {#cloud-manager-whats-new}

* **改进的稳定性、性能和可靠性**

  此版本包括优化和维护更新，这些更新改进了Cloud Manager的稳定性、性能和可靠性。

* **专业测试环境**

  >[!NOTE]
  >
  >专业测试环境现已可供购买。 请联系您的Adobe代表以下订单。

  Cloud Manager 现已支持添加名为&#x200B;**专用测试环境**&#x200B;的新环境类型。该环境旨在帮助团队在正式上线之前在接近生产的条件下验证功能。此环境类型不同于&#x200B;*生产 + 预发布*、*开发*&#x200B;或&#x200B;*快速开发*&#x200B;环境，而是专为运行高级验证场景提供的集中空间。

  请参阅[添加专门的测试环境](/help/implementing/cloud-manager/specialized-test-environment.md)。

  ![“添加环境”对话框中选中了“专用测试环境”单选按钮](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

<!--
>[!NOTE]
>
>Adobe has closed beta access requests for Specialized Testing Environments, having reached a sufficient number of participants. The feature is now in preparation for general availability.

If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


* **管道部署的一键式回滚**

  如果最新的客户源代码无法按预期工作，请快速恢复到以前的部署。 无需重新运行完整管道或手动还原提交。<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

  请参阅[在 AEM as a Cloud Service 中还原先前部署的代码](/help/operations/restore-previous-code-deployed.md)。

  另请参阅 [AEM as a Cloud Service 中的内容恢复](/help/operations/restore.md)。

* **Edge Delivery Services的自助WAF设置**

  在Cloud Manager中创建Edge Delivery Services程序时，您可以启用Web应用程序防火墙(WAF)。 此设置会立即保护您的网站免受恶意流量和DDoS攻击，从而减少手动设置工作。

  查看[一键单击即可创建您的第一个Edge Delivery网站](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)。


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

### 使用您自己的 Git (BYOG) {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

客户现在可以将他们的 Azure DevOps Git 存储库加入到 Cloud Manager 中，同时支持现代 Azure DevOps 和旧版 VSTS（Visual Studio Team Services）两种存储库。

* Edge Delivery Services 用户可以使用已加入的存储库来同步和部署网站代码。
* 对于 AEM as a Cloud Service 和 Adobe Managed Services (AMS) 用户，该存储库可以链接到全栈和前端两种管道。

对其他管道类型以及通过代码质量管道进行提取请求验证的支持即将推出。

请参阅[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->

**有关 BYOG 的常见问题解答**

| 问题 | 解答 |
|---|---|
| *需要时，应如何将项目切换回 Adobe 管理的 Git 存储库？* | 切换回来很简单。[更新管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)，使其指向 Adobe 存储库，如果不再需要外部存储库，可将其删除。 |
| *是否可以为不同的环境（例如非生产环境与生产环境）配置不同的存储库，以允许首先在非生产环境中进行测试？* | 是的，可以为不同的环境配置不同的存储库。例如，开发或代码质量管道可以指向外部存储库，生产管道可继续连接到 Adobe 存储库。确保在使用此配置期间两个存储库之间的同步作业保持活跃。 |
| *`IP Allow` 列表等现有设置是否继续有效？* | 是的，现有的 `IP Allow` 列表仍会照常工作。但是如果外部 Git 存储库受到防火墙保护，必要的 [Adobe IP 地址就必须添加到允许列表中](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *所有 GitLab 存储库 URL 都有效吗？使用的存储库 URL 采用此格式 `https://gitlab_dedicated_url.com/path/repo-name.git`，这与文档中的示例不同。* | 是的，任何支持 API V3 或 V4 的 GitLab 存储库都受支持，包括自托管的 GitLab URL，例如[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)中描述的存储库（`https://git-vendor-name.com/org-name/repo-name.git`）。 |


#### 管理访问令牌{#manage-access-tokens}

在 Cloud Manager 中使用&#x200B;**管理访问令牌**&#x200B;功能，可查看、重命名并删除与外部自带 Git 存储库（如 GitHub Enterprise、GitLab、Bitbucket 和 Azure DevOps）关联的访问令牌。

请参阅[管理访问令牌](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


## 错误修复 {#bug-fixes}

2025年12月的Cloud Manager版本没有重大错误修复。


<!-- ## Known issues {#known-issues} -->

