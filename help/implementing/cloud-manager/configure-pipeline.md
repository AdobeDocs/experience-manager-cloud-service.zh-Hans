---
title: 配置CI/CD管道-Cloud Services
description: 配置CI/CD管道-Cloud Services
translation-type: tm+mt
source-git-commit: 4d5ad99e44446ac40d9798df1c7fabb862065495
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---


# 配置 CI-CD 管道 {#configure-ci-cd-pipeline}

在Cloud Manager中，有两种类型的管道：

* **生产管道**:

   只有创建生产和阶段环境集后，才能添加生产管道。

   有关详细信息，请参阅[设置生产管道](configure-pipeline.md#setting-up-the-pipeline)。

* **非生产渠道**:

   非生产管道可从云管理器的用户界面的&#x200B;**概述**&#x200B;页面添加。

   有关更多详细信息，请参阅[仅非生产和代码质量管道](configure-pipeline.md#non-production-pipelines)。

>[!NOTE]
>要配置管道，您必须：
> * 定义将开始管线的触发器。
> * 定义控制生产部署的参数。
> * 配置性能测试参数。


## 设置生产管道{#setting-up-production-pipeline}

部署管理器负责设置生产管道。

>[!NOTE]
>在项目创建完成、Git存储库至少具有一个分支并且创建了生产和阶段环境集之前，无法设置生产管道。

在开始部署代码之前，必须从[!UICONTROL 云管理器]配置管道设置。

>[!NOTE]
>
>初始设置后，可以更改管线设置。

## 从[!UICONTROL 云管理器] {#configuring-the-pipeline-settings-from-cloud-manager}配置管道设置

在设置项目并使用[!UICONTROL 云管理器] UI至少拥有一个环境后，即可设置部署管道。

按照以下步骤配置管道的行为和首选项：

1. 单击&#x200B;**设置管道**&#x200B;以设置和配置管道。

   ![](assets/set-up-pipeline1.png)

1. 将显示&#x200B;**设置管道**&#x200B;屏幕。 选择分支，然后单击&#x200B;**Next**。

   ![](assets/setup-1.png)

1. 配置部署选项。

   ![](assets/setup-2.png)

   可以定义触发器以开始管线：

   * **手动** -使用UI手动开始管道。
   * **在Git更改中** -只要向配置的git分支添加提交，就会开始CI/CD管道。即使选择此选项，也始终可以手动开始管线。

   在管线设置或编辑过程中，当在任何质量门中遇到重要故障时，部署管理器可以定义管线的行为。

   这对于希望获得更自动化流程的客户非常有用。 可用选项有：

   * **每次询问** -这是默认设置，需要手动干预任何重要故障。
   * **立即失败** -如果选中此选项，则在出现重要故障时将取消管线。这实质上是模拟用户手动拒绝每个失败。
   * **立即继续** -如果选中此项，管线将在出现重要故障时自动继续。这实际上是模拟用户手动批准每个失败。


1. 生产管道设置包括标记为&#x200B;**体验审核**&#x200B;的第三个选项卡。 此选项提供应始终包含在体验审计中的URL路径的表。

   >[!NOTE]
   >必须单击&#x200B;**添加新页面**&#x200B;来定义您自己的自定义链接。

   ![](assets/setup-3.png)

   单击&#x200B;**添加新页面**&#x200B;以提供要包含在体验审核中的URL路径。

   例如，如果要在体验审核中包含`https://wknd.site/us/en/about-us.html`，请在此字段中输入路径`us/en/about-us.html`，然后单击&#x200B;**保存**。

   ![](assets/exp-audit4.png)

   表中显示的URL将为：

   `https://publish-p14253-e43686.adobeaemcloud.com/us/en/about-us.html`

   ![](assets/exp-audit5.png)

   最多可包含25行。 如果用户在此部分中未提交任何页面，则默认情况下，网站的主页将包含在体验审核中。

   有关详细信息，请参阅[了解体验审核结果](/help/implementing/cloud-manager/experience-audit-testing.md)。

   >[!NOTE]
   > 已配置的页面将提交到服务并根据性能、辅助功能、SEO（搜索引擎优化）、最佳实践和PWA（渐进式Web应用程序）测试进行评估。

1. 单击&#x200B;**编辑管道**&#x200B;屏幕中的&#x200B;**保存**。 现在，**概述**&#x200B;页面显示&#x200B;**部署项目卡**。 单击&#x200B;**部署**&#x200B;按钮以部署项目。

   ![](assets/configure-pipeline5.png)


## 仅限非生产和代码质量的管道{#non-production-pipelines}

除了部署到舞台和生产的主管道外，客户还能够建立额外的管道，称为&#x200B;**非生产管道**。 这些管线始终执行构建和代码质量步骤。 它们还可以选择部署到Adobe Managed Services环境。

在主屏幕上，新卡中列出了以下管线：

1. 从Cloud Manager主屏幕访问&#x200B;**非生产管道**&#x200B;拼贴。

   ![](assets/configure-pipeline6.png)

1. 单击&#x200B;**添加**&#x200B;按钮，以指定管道名称、管道类型和Git分支。

   此外，您还可以从管道选项设置部署触发器和重要失败行为。

   ![](assets/non-prod-pipe1.png)

1. 单击&#x200B;**保存**，主屏幕上的卡上将显示管道，其中有三个操作，如下所示：

   ![](assets/configure-pipeline8.png)

   * **编辑** -允许编辑管道设置
   * **构建** -导航到执行页面，从该页面可以执行管道
   * **管理Git**  —— 允许用户获取访问Cloud Manager Git存储库所需的信息

## 后续步骤 {#the-next-steps}

配置管道后，您需要部署代码。

有关详细信息，请参阅[部署代码](deploy-code.md)。
