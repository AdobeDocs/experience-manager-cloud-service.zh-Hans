---
title: 拆分仅阶段管道和仅生产管道
description: 了解如何使用专用管道拆分暂存和生产部署。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
hide: false
hidefromtoc: false
index: true
exl-id: 7d76a87c-122c-4c4d-8071-957bef4c9cf1
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 49%

---

# 仅分离阶段管道和仅生产管道 {#stage-prod-only}

<!-- REMOVED AS PER CQDOC-23086 ON OCTOBER 3, 2025:
badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#staging-production-only-pipelines" -->

您可以使用专用管道拆分暂存和生产部署。

## 概述 {#overview}

暂存环境和生产环境紧密耦合。默认情况下，对它们的部署链接到单一管道。这是一个部署管道，可部署到该程序中的暂存环境和生产环境。 虽然这种耦合通常是合适的，但在某些用例中存在缺点：

* 如果您只想部署到暂存环境，您可以拒绝管道中的&#x200B;**升级到生产**&#x200B;步骤。 但是，执行操作会被标记为已取消。
* 如果您希望将暂存环境中的最新代码部署到生产环境中，则需要重新部署整个管道，其中包括暂存部署，即使那里没有任何代码更改也是如此。
* 部署期间无法更新环境。 在升级到生产环境之前，如果您暂停以在暂存环境中进行几天的测试，则生产环境将会保持锁定状态，且无法更新。 这种场景会造成无法更新[环境变量](/help/implementing/cloud-manager/environment-variables.md)等非依赖型任务。

仅暂存和仅生产管道通过提供专用的部署选项为这些用例提供解决方案。

* **仅暂存部署管道：**&#x200B;仅会部署到暂存环境，部署和测试完成后执行即会结束。仅暂存管道的行为与标准耦合全栈生产管道相同，但没有生产部署步骤（审批、计划、部署）。
* **仅生产部署管道：**&#x200B;通过选择最近成功的阶段执行仅部署到生产环境。 然后将其工件部署到生产中。 仅限生产的管道会重用暂存部署工件，从而绕过构建阶段。

当全栈生产管道运行时，不会执行仅暂存或仅生产管道，反之亦然。如果仅暂存生产管道和全栈生产管道都配置了 **On Git Changes** 触发器，并且指向同一个分支和存储库，则只有仅暂存生产管道会自动启动。仅限生产的管道不会启动 **`On Git Changes`**，因为它们未直接链接到存储库。

仅限生产的管道是手动触发的，因为它们没有直接链接到 **On Git Changes** 的存储库。

这些专用管道提供了更大的灵活性，但应注意以下操作细节和建议。

>[!NOTE]
>
>仅限生产的管道始终会使用仅限暂存的管道中的工件。 即使标准的耦合生产管道在此期间已部署了其他暂存内容，此过程仍然适用。
>
>* 这种情况可能会导致出现不必要的代码回滚。
>* Adobe 建议在您开始使用仅生产和仅暂存管道后，就停止使用标准耦合生产管道。
>* 如果您仍然决定运行标准耦合管道和仅暂存/仅生产管道，请记住重用工件以避免代码回滚。

## 管道创建 {#pipeline-creation}

仅生产和仅暂存管道以与标准耦合的[生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)和[非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)类似的方式创建。请参阅这些文件，了解详细信息。

1. 在&#x200B;**管道**&#x200B;窗口中，单击&#x200B;**添加管道**。

   * 选择&#x200B;**将非生产管道**&#x200B;添加到[创建仅暂存管道](#stage-only)。
   * 选择&#x200B;**将仅生产管道**&#x200B;添加到[创建仅生产管道](#prod-only)。

![创建仅生产/仅暂存管道](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-stage-pipeline.png)

>[!NOTE]
>
>如果相应的管道已经存在，则某些选项可能会变灰。
>
>* 如果仅暂存管道尚不存在，则无法&#x200B;**添加仅生产管道**。
>* 如果标准耦合管道已经存在，则&#x200B;**添加生产管道**&#x200B;将不可用。
>* 每个项目只允许使用一个仅生产和一个仅暂存管道。

### 创建仅暂存管道 {#stage-only}

1. 在&#x200B;**添加非生产管道**&#x200B;对话框中，在&#x200B;**配置**&#x200B;选项卡上，为您的管道选择&#x200B;**部署管道**&#x200B;字段。
1. 在非生产管道名称字段中，输入自由文本名称。
1. 选择所需的部署选项，然后单击&#x200B;**继续**。

   添加非生产管道对话框中的![配置选项卡](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-1.png)

1. 在&#x200B;**Source代码**&#x200B;选项卡上，选择&#x200B;**全栈代码**。 此选项构建和部署整个AEM应用程序(后端、Dispatcher/Web层配置以及存储库中的任何前端模块)。

1. 在&#x200B;**符合条件的部署环境**&#x200B;下拉列表中，选择&#x200B;**暂存**&#x200B;环境作为管道的部署环境。 选择暂存将创建一个专用于暂存环境的管道（生产升级通过单独的管道进行）。

1. 在各自的下拉列表中选择您的&#x200B;**存储库**&#x200B;和&#x200B;**Git分支**，然后单击&#x200B;**继续**。

   在“添加非生产管道”对话框中![Source“代码”选项卡](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-2.png)

1. 在&#x200B;**体验审核**&#x200B;选项卡上，指定的站点URL是Cloud Manager审核页面质量的已发布URL。

1. 在&#x200B;**页面路径**&#x200B;字段中，指定要审核的页面，然后单击&#x200B;**![添加图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)添加页面**。

   体验审核会分析您为性能、可访问性、渐进式Web应用程序、最佳实践、SEO和其他质量检查添加的每个路径。 通过单击![跨大小400图标](https://spectrum.adobe.com/static/icons/ui_18/CrossSize400.svg)，您可以添加多个路径并删除任何路径。

   在“添加非生产管道”对话框中![体验审核选项卡](/help/implementing/cloud-manager/configuring-pipelines/assets/add-non-prod-pipeline-3.png)

1. 单击&#x200B;**保存**。


### 创建仅生产管道 {#prod-only}

1. 在对话框&#x200B;**添加仅生产管道**&#x200B;中，在&#x200B;**管道名称**&#x200B;文本字段中，输入管道的自由文本名称。
1. 在&#x200B;**管道名称**&#x200B;字段中，键入所需的名称。
1. 在&#x200B;**生产部署选项**&#x200B;下，选择&#x200B;**在部署到生产之前暂停**。

   此选项直接在生产步骤之前插入手动审批审核。 管道将停止并等待批准者（例如部署管理器或业务负责人）批准或取消生产部署。

   用于更改控制或最新检查。

1. 单击&#x200B;**保存**&#x200B;以使用这些选项创建仅限生产的管道。

   ![创建仅生产管道](/help/implementing/cloud-manager/configuring-pipelines/assets/add-production-only-pipeline.png)

## 运行仅阶段管道和仅生产管道 {#running}

您可以像启动任何其他管道[一样启动新管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)。 您还可以直接从仅限暂存管道的执行详细信息触发仅限生产的管道。

<!-- * Stage-only and prod-only pipelines offer a new [emergency mode](#emergency-mode) to skip testing.
Prod-only pipeline run can be triggered directly from the execution details of a [stage-only pipeline](#stage-only-run).


### Emergency Mode {#emergency-mode}

When starting production-only and staging-online pipelines, you are prompted to confirm the start and how it starts.

* **Normal Mode** is a standard run and includes stage testing steps.
* **Emergency Mode** skips stage testing steps.

![Emergency Mode](/help/assets/configure-pipelines/emergency-mode.png) -->

### 运行仅舞台管道 {#stage-only-run}

在执行详细信息中，测试步骤之后将显示&#x200B;**提升内部版本**&#x200B;按钮。 单击它可触发仅用于生产的管道，并将该运行的暂存工件部署到生产环境。 该按钮仅在最近一次成功的仅暂存运行时显示。

![仅暂存管道运行](/help/implementing/cloud-manager/configuring-pipelines/assets/stage-only-pipelines-run.png)

单击&#x200B;**提升内部版本**&#x200B;后，将打开一个对话框，供您确认运行相关的仅生产管道。 单击&#x200B;**运行**&#x200B;以启动它。

![提升生成 — 运行管道对话框](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-run.png)

如果不存在任何内容，则设置对话框会提示您创建一个。

![提升生成 — 没有有效的管道对话框](/help/implementing/cloud-manager/configuring-pipelines/assets/promote-build-no-valid-pipeline.png)


### 运行仅生产管道 {#prod-only-run}

对于&#x200B;**仅用于生产**&#x200B;管道，Cloud Manager显示部署到生产环境的源工件。 检查源执行的&#x200B;**工件准备**&#x200B;步骤，然后打开该步骤以查看详细信息和日志。


![工件详细信息](/help/implementing/cloud-manager/configuring-pipelines/assets/prod-only-pipelines-run.png)
