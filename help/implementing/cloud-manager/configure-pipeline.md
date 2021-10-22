---
title: 配置CI/CD管线 — Cloud Services
description: 配置CI/CD管线 — Cloud Services
exl-id: d2024b42-9042-46a0-879e-110b214c7285
source-git-commit: f3743451f7aeadae26e8a6814cfbed9667c4a242
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 0%

---

# 配置 CI-CD 管道 {#configure-ci-cd-pipeline}

在Cloud Manager中，有两种类型的管道：

* **生产管道**:

   只有在创建生产和暂存环境集后，才能添加生产管道。

   请参阅 [设置生产管道](configure-pipeline.md#setting-up-the-pipeline) 以了解更多详细信息。

* **非生产管道**:

   非生产管道可从 **概述** 页面。

   请参阅 [仅限非生产和代码质量管道](configure-pipeline.md#non-production-pipelines) 以了解更多详细信息。

   >[!NOTE]
   >要配置管道，必须：
   > * 定义将启动管道的触发器。
   > * 定义控制生产部署的参数。
   > * 配置性能测试参数。


## 设置生产管道 {#setting-up-production-pipeline}

部署管理器负责设置生产管道。

>[!NOTE]
>在程序创建完成、Git存储库至少具有一个分支，并且创建了生产和暂存环境集之前，无法设置生产管道。

在开始部署代码之前，必须先从 [!UICONTROL Cloud Manager].

>[!NOTE]
>
>在初始设置后，可以更改管道设置。

### 添加新的生产管道 {#adding-production-pipeline}

设置程序并使用 [!UICONTROL Cloud Manager] UI，您就可以添加生产管道。

请按照以下步骤配置生产管道的行为和首选项：

1. 导航到 **管道** 卡 **计划概述** 页面。
单击 **+添加** 选择 **添加生产管道**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. **添加生产管道** 对话框。 输入管道名称。

   此外，您还可以设置 **部署触发器** 和 **重要量度失败行为** 从 **部署选项**. 单击 **继续**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-add2.png)


   您可以定义部署触发器以启动管道。

   * **手动**  — 使用UI手动启动管道。
   * **在Git更改时**  — 每当向配置的git分支添加提交时，都会启动CI/CD管道。 即使选择此选项，也始终可以手动启动管道。

      在管道设置或编辑期间，部署管理器可以选择在任何质量门中遇到重要故障时定义管道的行为。

      这对于希望实现更自动化流程的客户非常有用。 可用选项包括：
   您可以定义重要的失败量度行为以启动管道。

   * **每次提问**  — 这是默认设置，需要对任何重要故障进行手动干预。
   * **立即失败**  — 如果选中，则每当发生重要故障时，将取消管道。 这实质上是在模拟用户手动拒绝每个故障。
   * **立即继续**  — 如果选中，则每当发生重要故障时，管道将自动继续。 这实质上是在模拟用户手动批准每次失败。


1. 的 **添加生产管道** 对话框包括标记为 **源代码**. **完整堆栈代码** 中。 您可以选择 **存储库** 和 **Git分支**. 选择生产部署选项，如下所述。 单击 **继续**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-fullstack1.png)

   生产部署选项：

   * **部署到生产之前暂停**:此选项允许部署在生产之前暂停。
   * **已计划**:此选项允许用户启用计划的生产部署。

1. 的 **添加生产管道** 对话框包含第三个标签为 **体验审核**. 此选项为应始终包含在体验审核中的URL路径提供了一个表。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

   >[!IMPORTANT]
   >您必须单击 **添加页面** 定义您自己的自定义链接。 页面路径必须以开头 `/`.
   >![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit2.png)


   单击 **添加新页面** 提供要包含在体验审核中的URL路径。

   例如，如果您希望包含 `https://wknd.site/us/en/about-us.html` 在体验审核中，输入路径 `/us/en/about-us.html` 单击 **保存**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

   表中显示的URL将为：

   `https://publish-p12361-e112003.adobeaemcloud.com/us/en/about-us.html`

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

   最多可包含25行。 如果用户在此部分中未提交页面，则默认情况下网站的主页将包含在体验审核中。

   请参阅 [了解体验审核结果](/help/implementing/cloud-manager/experience-audit-testing.md) 以了解更多详细信息。

   >[!NOTE]
   > 将配置的页面提交到服务，并根据性能、辅助功能、SEO（搜索引擎优化）、最佳实践和PWA（渐进式Web应用程序）测试进行评估。

1. 单击 **保存**. 现在，新创建的生产管道将显示在 **管道** 卡。

   管道显示在主屏幕的卡片上，带有三个操作，如下所示：

   * **添加**  — 允许添加新管道。
   * **访问存储库信息**  — 允许用户获取访问Cloud Manager Git存储库所需的信息。
   * **了解更多**  — 导航到了解CI/CD管道文档资源。

### 编辑生产管道 {#editing-prod-pipeline}

可以通过 **计划概述** 页面。

请按照以下步骤编辑已配置的管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 单击 **...** 从 **管道** 卡片，单击 **编辑**，如下图所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit1.png)

1. 的 **编辑生产管道** 对话框。

   1. 的 **配置** 选项卡 **管道名称**, **部署触发器**&#x200B;和 **重要量度失败行为**.

      >[!NOTE]
      >请参阅 [添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中添加和管理存储库。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit2.png)


   1. 的 **来源** 选项卡提供选中或取消选中的选项 **部署到生产之前暂停** 和 **已计划** 选项 **生产部署选项**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-pipeline-editnotier.png)

   1. 的 **体验审核** 选项，用于更新或添加新页面。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/pipeline-edit4.png)

1. 单击 **更新** 编辑管道后。

### 其他生产管道操作 {#additional-prod-actions}

#### 运行生产管道 {#run-prod}

可以从管道卡运行生产管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 单击 **...** 从 **管道** 卡片，单击 **运行**，如下图所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-run.png)

#### 删除生产管道 {#delete-prod}

可以从管道卡中删除生产管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 单击 **...** 从 **管道** 卡片，单击 **删除**，如下图所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/prod-delete.png)

   >[!NOTE]
   >具有部署管理器角色的用户现在可以通过 **删除** 选项。


## 仅限非生产和代码质量管道 {#non-production-pipelines}

除了部署到暂存和生产的主管道之外，客户还能够设置其他管道，称为非生产管道。
非生产管道有两种类型：

1. 代码质量：在git分支中的代码上运行代码质量扫描。 此管道可执行生成和代码质量步骤。
1. 部署：除了执行构建和代码质量步骤之外，此管道还会将代码部署到选定的非生产环境到AEMas a Cloud Service环境。

### 添加新的非生产管道 {#adding-non-production-pipeline}

在主屏幕上，这些管道将列在新卡中：

1. 访问 **管道** Cloud Manager主屏幕中的信息卡。 单击 **+添加** 选择 **添加非生产管道**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **添加非生产管道**  对话框。 选择要创建的管道类型 **代码质量管道** 或 **部署管道**.

   >[!NOTE]
   >对于部署管道，必须选择部署环境。

   此外，您还可以设置 **部署触发器** 和 **重要量度失败行为** 从 **部署选项**. 单击 **继续**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

1. **完整堆栈代码** 中。 您可以选择 **存储库** 和 **Git分支**. 单击 **保存**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. 现在，新创建的非生产管道将显示在 **管道** 卡。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   管道显示在主屏幕的卡片上，带有三个操作，如下所示：

   * **添加**  — 允许添加新管道。
   * **访问存储库信息**  — 允许用户获取访问Cloud Manager Git存储库所需的信息。
   * **了解更多**  — 导航到了解CI/CD管道文档资源。

### 编辑非生产管道 {#editing-nonprod-pipeline}

可以通过 **管道卡** 从 **计划概述** 页面。

请按照以下步骤编辑配置的非生产管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 选择非生产管道并单击 **...**. 单击 **编辑**，如下图所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit1.png)

1. 的 **编辑生产管道** 对话框。

   1. 的 **配置** 选项卡 **管道名称**, **部署触发器**&#x200B;和 **重要量度失败行为**.

      >[!NOTE]
      >请参阅 [添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中添加和管理存储库。

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit2.png)


   1. 的 **源代码** 选项卡会提供更新 **存储库** 和 **Git分支**.

      ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-edit3.png)

1. 单击 **更新** 编辑完非生产管道后。

### 其他非生产管道操作 {#additional-nonprod-actions}

#### 运行非生产管道 {#run-nonprod}

可以从管道卡运行生产管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 单击 **...** 从 **管道** 卡片，单击 **运行**，如下图所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-run1.png)

#### 删除非生产管道 {#delete-nonprod}

可以从管道卡中删除生产管道：

1. 导航到 **管道** 卡 **计划概述** 页面。

1. 单击 **...** 从 **管道** 卡片，单击 **删除**，如下图所示。

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-delete.png)


## 后续步骤 {#the-next-steps}

配置管道后，您需要部署代码。

请参阅 [部署代码](deploy-code.md) 以了解更多详细信息。
