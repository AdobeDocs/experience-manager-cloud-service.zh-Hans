---
title: 添加Edge Delivery管道
description: 了解如何添加Edge Delivery管道以生成代码并将其部署到生产环境。
index: false
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="私人测试版" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md网站#gitlab-bitbucket"
hide: true
hidefromtoc: true
source-git-commit: 169de7971fba829b0d43e64d50a356439b6e57ca
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 38%

---



# 添加Edge Delivery管道 {#configure-production-pipeline}

了解如何配置Edge Delivery管道以生成代码并将其部署到生产环境。 生产管道首先将代码部署到暂存环境。 在获得批准后，它会将相同的代码部署到生产环境。

用户必须具有&#x200B;**[部署管理员](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能配置生产管道。

>[!NOTE]
>
>在发生以下情况之前，无法设置生产管道：
>
>* 项目随即会创建。
>* Git存储库至少有一个分支。
>* 将创建生产和暂存环境。

在开始部署代码之前，请从[!UICONTROL Cloud Manager]配置管道设置。

>[!NOTE]
>
>在初始设置后，您可以[编辑管道设置](managing-pipelines.md)。

## 添加新的Edge Delivery管道 {#adding-production-pipeline}

在设置项目并具有至少一个使用 [!UICONTROL Cloud Manager] UI 的环境后，便可以执行以下步骤来添加非生产管道。

>[!TIP]
>
>在配置前端管道之前，请参阅[AEM快速站点创建历程](/help/journey-sites/quick-site/overview.md)，获取易于使用的AEM快速站点创建工具的端到端指南。 此历程可帮助您简化AEM站点的前端开发，让您无需了解AEM后端即可快速自定义站点。

**要添加新的Edge Delivery管道：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**项目概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;卡并单击&#x200B;**添加**&#x200B;以选择&#x200B;**添加生产管道**。

   ![在“程序管理员”概述中的“管道”信息卡](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. 此时会显示&#x200B;**添加生产管道**&#x200B;对话框。提供&#x200B;**管道名称**，识别您的管道以及以下选项。单击&#x200B;**“继续”**。

   **部署触发器** – 在定义启动管道的部署触发器时，您可以使用以下选项。

   * **手动** — 手动启动管道。
   * **在Git发生更改时** — 只要将承诺添加到配置的Git分支，就会启动CI/CD管道。 利用此选项，您仍能根据需要手动启动管道。

   **重要量度失败行为r** – 在管道设置或编辑期间，**部署管理员**&#x200B;可以选择定义在任何质量审核出现重要失败时的管道行为。可用的选项为：

   * **每次询问** — 默认设置。 它要求对任何重要失败进行手动干预。
   * **立即失败** – 如果选定此选项，则只要发生重要失败，就会取消管道。此过程实际上是在模拟用户手动拒绝每个失败的情况。
   * **立即继续** — 如果选定此选项，则每当发生重要失败时，管道就会自动继续。 此过程实际上是在模拟用户手动批准每个失败的情况。

   ![生产管道配置](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 在&#x200B;**Source代码**&#x200B;选项卡上，选择管道应处理的代码类型。

   * **[配置全栈栈代码管道](#full-stack-code)**
   * **[配置目标部署管道](#targeted-deployment)**

有关管道类型的更多信息，请参阅[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。

根据您选择的源代码类型，完成生产管道创建的步骤有所不同。 按照上面的链接跳到本文档的下一节，完成管道的配置。

