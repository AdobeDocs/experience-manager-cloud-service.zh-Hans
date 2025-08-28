---
title: Cloud Manager 2025.8.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2025.8.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 94a20e8e95edf603227bfadd07e4b4c62e6421e6
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 99%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.8.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.8.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2025.8.0 的发布日期是 2025 年 8 月 7 日星期四。

下一个版本计划于 2025 年 9 月 4 日星期四发布。

## 新增功能 {#what-is-new}

* **Adobe Experience Hub 即将推出**

  从 2025 年 8 月 19 日开始，Adobe 开始分阶段向所有 Adobe Experience Manager 用户推出新的 Experience Hub。

  Experience Hub 是一个统一的起点，提供个性化的上下文体验，帮助用户更快地实现目标。推出过程于 2025 年 8 月 26 日结束，届时所有用户均可使用。新的 Experience Hub 可直接在 [experience.adobe.com](https://experience.adobe.com/) 上访问。若要了解详细信息，请参阅[Experience Hub](/help/experience-hub.md)。

* **Edge Delivery Services 许可证可以通过自助方式纳入 HIPAA 计划**

  具有医疗保健或敏感数据需求的组织现在可以通过自助服务的方式使用 Edge Delivery Services，从而确保 HIPAA 合规性，满足严格的监管标准。<!-- CMGR-70016 -->

* **BYOG 现在可用于 Edge Delivery Services**

  Cloud Manager 现在允许您配置外部 Git 存储库，从而实现灵活的代码管理工作流。<!--(CMGR‑69010, CMGR‑70988) --> 它还允许您直接从 Cloud Manager 用户界面中一个选定的分支提取代码，从而减少手动存储库任务。参见[配置 Edge Delivery 网站以使用外部 Git 存储库](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md) <!-- (CMGR‑68085)(CMGR-69015) --> <!-- KT: https://wiki.corp.adobe.com/display/DMSArchitecture/%5B2025%5D+Cloud+Manager+-+Bring+Your+Own+Git+with+EDS -->

* **自动设置新的 Forms 附加组件**

  仅限网站的客户通常需要一种轻量级、低成本的方式来构建营销表单。新的 AEM Forms Sites 附加组件可以在 Sites 计划中添加有限的 Forms 功能，从而满足这一需求。它还创建了一个通往完整的 AEM Forms 产品的清晰升级路径。<!-- (CMGR-64301) --> <!-- KT: CMGR Provisioning Support for AEM Forms Sites Add-On SKU https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3578379797 -->

  附加组件：
   * 附加到 Sites 计划并与其一起部署——无需单独的 Forms 计划或授权。
   * 针对简单的营销表单用例。
   * 在生产计划创建或生产计划编辑过程中出现在&#x200B;**解决方案与附加组件**&#x200B;列表中，前提条件是 IMS 组织必须持有可用的 Forms 附加组件许可证。

     ![表单附加组件](/help/implementing/cloud-manager/release-notes/assets/forms-add-on.png) *您的 IMS 组织中必须有 Forms 附加组件许可证，才可以在计划中添加 Forms 附加组件。*

     ![创建生产程序时解决方案和附加组件中的 Forms 附加组件](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-creating-production-program.png) *在创建程序期间，您可以选择 Sites 解决方案中的 Forms 附加组件。*

     ![编辑生产程序时的 Forms 附加组件](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-editing-production-program.png) *在&#x200B;**编辑程序**中为 Sites 计划选择 Forms 附加组件，然后运行管道，在环境中将其激活。*

     更多信息请参阅[创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。

## Beta 计划 {#private-beta-program}

参与 Cloud Manager 的 beta 计划，在即将推出的功能正式发布之前获得独家访问权限。

目前提供以下机会：

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

### 添加 Edge Delivery 配置管道 {#add-eds-pipeline}

现在，使用 Edge Delivery Services 构建的站点支持配置管道，将此功能扩展到云服务环境之外。您可以使用&#x200B;**配置管道**&#x200B;来管理设置，例如流量过滤规则和 Web 应用程序防火墙 (WAF) 配置（如适用）。请参阅[受支持的配置](/help/operations/config-pipeline.md#configurations)。

**最新的增强功能**

* 现在，Edge Delivery Services 管道在&#x200B;**已部署的代码**&#x200B;列中显示&#x200B;**配置**，这样就能立即识别仅配置的部署。<!-- CMGR‑69681 -->
* 只要程序包含至少一个 Edge Delivery Services 网站和一个映射域，Cloud Manager 就会显示&#x200B;**添加 Edge Delivery 管道**。否则，该选项将显示为禁用，并且工具提示会说明缺少的要求。<!-- CMGR‑69680 -->
* **Edge Delivery** 选项卡显示一个新的 **Edge Delivery 管道**&#x200B;构件，其中列出了每个管道的名称、状态、存储库和分支。<!-- (CMGR-69052) -->

  ![Edge Delivery 管道构件显示管道名称、状态、存储库和分支](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

* **过滤器**&#x200B;面板添加了&#x200B;**投放类型**&#x200B;分区，其中包括&#x200B;**边缘投放**&#x200B;和&#x200B;**发布投放**&#x200B;两个复选框。<!-- (CMGR-69682) -->

  ![过滤器面板显示新的投放类型：边缘投放和发布投放](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

![在“添加管道”下拉列表中添加 Edge Delivery 管道](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *从&#x200B;**程序概览**页面的&#x200B;**管道**卡片中添加 Edge Delivery 管道。*

![添加 Edge Delivery 管道对话框](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *添加 Edge Delivery 管道对话框。*

请参阅[添加 Edge Delivery 管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 相关联的电子邮件地址发送电子邮件至 [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)。


## 错误修复

* 管道现在仅将变量传递到主要的 Edge Delivery Services 域配置，跳过在重新创建管道过程中删除的任何配置。<!-- (CMGR‑70039) -->
* 现在，管道执行可以可靠启动；修复了由于内部资源处理错误而导致某些管道无法启动的问题。<!-- (CMGR‑58167) -->
* 内容复制会验证 Cloud Manager 权限，阻止缺乏部署管理权限或管理员权限的用户启动。<!-- (CMGR‑62097) -->


<!-- ## Known issues {#known-issues} -->

