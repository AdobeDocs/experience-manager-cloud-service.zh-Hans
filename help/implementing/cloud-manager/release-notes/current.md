---
title: Cloud Manager 2025.10.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2025.10.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 4acedba631b3732b989794c648079356f9b79fdd
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 62%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.10.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.10.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2025.10.0的发布日期是2025年10月2日星期四。

下一个计划发布于2025年11月6日星期四。

## 新增功能 {#what-is-new}

* **AEM云运行状况评估服务**

  Adobe引入了AEM云运行状况评估服务，这是一个自动的非侵入性检查工具，可让您的AEM as a Cloud Service环境保持优化、安全并与最佳实践保持一致。

  此服务将执行以下操作：

   * 扫描环境以发现性能瓶颈、效率低下和潜在风险。
   * 分析内容结构（Blueprint、活动副本）和自定义配置。
   * 标识过时的依赖项(AEM SDK、第三方库)。
   * 标记代码质量问题（注释错误、模式效率低下）。
   * 通过仪表板（如&#x200B;**操作中心**）提供可操作指导。
   * 通过早期问题检测和补救支持主动优化。

  团队可以持续监控和改进其AEM环境，以实现更平稳的性能、更强的安全性和长期可维护性。

  请参阅[生产和暂存环境的运行状况评估](/help/implementing/cloud-manager/reports/report-health-assessment.md)。

* **配置管道支持**

  现在，使用 Edge Delivery Services 构建的站点支持配置管道，将此功能扩展到云服务环境之外。您可以使用&#x200B;**配置管道**&#x200B;来管理设置，例如流量过滤规则和 Web 应用程序防火墙 (WAF) 配置（如适用）。请参阅[受支持的配置](/help/operations/config-pipeline.md#configurations)。

  Edge Delivery配置管道还通过Cloud Manager管道变量支持密钥。

  请参阅[添加Edge Delivery管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)。

* **域映射 — CDN设置对话框已简化**

  Cloud Manager简化了&#x200B;**将域映射到CDN**&#x200B;流程，以减少混淆并加快配置。 该对话框现在强调&#x200B;**Adobe托管的CDN**（带有“推荐”徽章）。

  ![选中Adobe托管的CDN单选按钮后，将“域映射到CDN”对话框](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-adobe-managed-cdn.png)。

  请参阅[添加域映射](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)。

  该对话框还为&#x200B;**其他CDN提供商**&#x200B;卡提供单个简明的核对清单，重点内容为包含以下内容的指导性内容：

   * 将您的CDN源指向`publish-p<PROGRAM_ID>-e<ENV_ID>.adobeaemcloud.com`。
   * 设置&#x200B;**主机/SNI**&#x200B;以转发原始主机。
   * 添加`X-AEM-Edge-Key`(在Cloud Manager中部署该键后)。
   * 将`X-Forwarded-Host`设置为您的面向客户的域。
   * 在访问AEM之前清除其他`X-Forwarded-*`标头。

  ![选择“将域映射到CDN”对话框中的“其他CDN提供商”单选按钮](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-other-cdn-provider.png)

  <!-- (no redundant `Origin` field or "Learn more" clutter) -->随附的页脚提供了两个有用的链接：主要CDN的配置示例以及指向完整文档的链接。 单击“我已配置我的CDN”的单个确认按钮，即可完成流程。

  查看AEM as a Cloud Service[中的](/help/implementing/dispatcher/cdn.md#point-to-point-CDN)CDN。

<!--
### Staging-Only and Production-Only Pipelines {#staging-production-only-pipelines}

Support for [staging-only and production-only pipelines](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md) has been introduced, enabling you to split full-stack production deployment pipelines into smaller, specialized deployments.

If you are interested in testing this new feature and sharing your feedback, send an email to  `Grp-cloudmanager_splitpipelines@adobe.com` from your email address associated with your Adobe ID. -->


## Beta 计划 {#private-beta-program}

参与 Cloud Manager 的 beta 计划，在即将推出的功能正式发布之前获得独家访问权限。

目前提供以下机会：
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### Experience Hub可扩展性和自定义 {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md)是您进入AEM的入口点，根据贵组织的需求进行自定义。 介绍Adobe中您现有的AEM UI扩展，以便它们可以帮助您在Experience Hub中轻松启用它们。

![Experience Hub可扩展性和自定义工作流程示意图](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

在Experience Hub中嵌入自定义体验，以扩展和个性化贵组织的仪表板。 除了Adobe的内置小组件之外，还可以使用[UI可扩展性](https://developer.adobe.com/uix/docs/)框架添加您自己的小组件。 构建基于JavaScript的UI应用程序，并将其呈现给您的用户，以满足特定于业务的要求和工作流。

对Beta版感兴趣吗？ 向[beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com)发送电子邮件，其中包含您的Adobe OrgID以及要创建的自定义设置的简短说明。

### 通过模块缓存加快构建速度 {#quick-build-cm-pipelines}

新的构建模型使用模块级缓存仅编译已更改的模块（而不是整个存储库）以缩短构建时间。 它适用于代码质量、全栈和仅限暂存的管道。

有兴趣吗？ 使用您的Adobe OrgID和项目ID向[beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com)发送电子邮件。

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->



### 管道部署一键回滚 {#one-click-rollback}

当最新的客户源代码未如预期运行时，可迅速回滚至先前的部署，无需重新运行完整管道或手动回退提交。<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![从“环境”卡片中还原客户源代码](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *上方的“环境”卡片展示了所选环境的&#x200B;**还原**>**先前部署的代码**选项。*

![“还原先前部署的代码”对话框](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*在&#x200B;**还原先前部署的代码**对话框中，查看当前部署的版本以及要还原的目标版本，然后点击&#x200B;**确认***。

![恢复激活](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Manager 会将环境回滚至较早的构建版本，保留内容和配置不变，并在部署完成前将该环境标记为&#x200B;**还原中**。*

![正在使用的源代码版本](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *如上所示，“环境详细信息”视图现已显示当前正在使用的源代码版本。*

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [restorecode@adobe.com](mailto:restorecode@adobe.com)。

请参阅[在 AEM as a Cloud Service 中还原先前部署的代码](/help/operations/restore-previous-code-deployed.md)。

另请参阅 [AEM as a Cloud Service 中的内容恢复](/help/operations/restore.md)。

### 专用测试环境 {#specialized-test-environment}

Cloud Manager 现已支持添加名为&#x200B;**专用测试环境**&#x200B;的新环境类型。该环境旨在帮助团队在正式上线之前在接近生产的条件下验证功能。此环境类型不同于&#x200B;*生产 + 预发布*、*开发*&#x200B;或&#x200B;*快速开发*&#x200B;环境，而是专为运行高级验证场景提供的集中空间。

**最新的增强功能**

* 您现在可以通过更简洁直观的工作流，在非生产管道中配置一个专门的测试环境。这一精简的设置流程可加快配置完成速度，并降低配置出错的风险。
* 现在，专门的测试环境中支持&#x200B;**复制内容**。您现在可以在真实反映生产的隔离开的测试环境中安全地运行&#x200B;**复制内容**。<!-- (CMGR‑68900) -->

请参阅[添加专门的测试环境](/help/implementing/cloud-manager/specialized-test-environment.md)。

![“添加环境”对话框中选中了“专用测试环境”单选按钮](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

>[!NOTE]
>
>Adobe 已关闭针对专用测试环境的 Beta 版访问请求，因为已获得足够多的参与者。该功能目前正在为全面推出做准备。

<!--
If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


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

10月的Cloud Manager版本中没有重大的错误修复。


<!-- ## Known issues {#known-issues} -->

