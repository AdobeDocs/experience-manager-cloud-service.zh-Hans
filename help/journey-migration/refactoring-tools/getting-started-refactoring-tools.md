---
title: 重构工具快速入门
description: 了解如何开始使用AEM as a Cloud Service中的重构工具
exl-id: 84394bdd-2b92-4f5d-b08a-7dc2c681baa4
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 4%

---

# 重构工具快速入门 {#getting-started-refactoring-tools}

## 可用性 {#availability}

<!-- Alexandru: duplicate contextualhelp id, drafting this for now

>[!CONTEXTUALHELP]
>id="aemcloud_rs_upload"
>title="Download"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html?lang=zh-Hans" text="Release Notes"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="Software Distribution Portal"

-->

## 运行重构工具 {#running-refactoring-tools}

使用重构工具迁移代码，以便与AEM as a Cloud Service兼容。

1. 如果尚未创建CAM项目，请参阅[在CAM中创建和管理项目](/help/journey-migration/cloud-acceleration-manager/using-cam/getting-started-cam.md#create-project)。
1. 单击&#x200B;**代码重构**&#x200B;卡以上传源代码。

   ![图像](/help/journey-migration/refactoring-tools/assets/rscam1.png)

1. 首次访问&#x200B;**Source代码视图**&#x200B;时，您将看到一个空状态，提示您上传源代码。

   ![图像](/help/journey-migration/refactoring-tools/assets/rscam2.png)

## 上传Source代码 {#uploading}

当客户首次访问&#x200B;**重构工具**&#x200B;时，**Source代码视图**&#x200B;中会显示空状态。 按照以下步骤上传您的项目并开始检查流程：

1. **访问项目上传页面**\
   单击处于空状态的&#x200B;**项目上传**&#x200B;按钮以开始上传过程。

   ![图像](/help/journey-migration/refactoring-tools/assets/rscam3.png)

1. **上传您的Source代码**
   - 在上传对话框中，选择您的源代码ZIP文件。
   - 单击&#x200B;**上传**&#x200B;开始。
   - 上传进度将显示在对话框中。 持续时间取决于项目的大小。

   ![图像](/help/journey-migration/refactoring-tools/assets/rscam4.png)

1. **检查进程**
   - 上载后，**检查进程**&#x200B;将在后台自动开始。
   - **Source代码视图**&#x200B;现在将显示您上传的项目及其检查状态。

1. **检查状态**&#x200B;检查过程旨在通过减少手动配置的开销来简化重构工具的执行。

   检查将显示以下状态之一：
   - **正在运行** — 检查正在进行中。
   - **就绪** — 检查已完成；您现在可以运行重构工具。
   - **失败** — 出现错误。 单击项目以查看检查报告并解决所有问题。

   ![图像](/help/journey-migration/refactoring-tools/assets/rscam5.png)

>[!NOTE]
>
>上传新项目将删除现有项目。 在继续之前，请确保已保存所有必需的数据。

>[!NOTE]
>
>仅当源代码上载成功时，才能执行重构作业。

## 重构作业 {#refactoring-jobs}

单击&#x200B;**重构作业**&#x200B;选项卡时，您将看到现有作业的列表。 如果尚未创建作业，则将显示空状态以提示创建作业。

![图像](/help/journey-migration/refactoring-tools/assets/rscam6.png)

### 1.创建新的重构作业

- 单击&#x200B;**新建作业**&#x200B;按钮。
- 选择所需的重构工具。
- 单击&#x200B;**开始**&#x200B;以启动重构过程。

![图像](/help/journey-migration/refactoring-tools/assets/rscam7.png)

>[!NOTE]
>
>您可以使用&#x200B;**所有工具一起**&#x200B;选项触发单个重构作业或一次性执行所有可用工具。

### 2.作业状态

- **正在运行** — 作业当前正在进行中。 状态会在完成或失败时自动更新。
- **已完成** — 作业已成功完成。 您现在可以查看结果或下载重构的代码。
- **失败** — 作业遇到错误。 单击作业可查看详细的日志并排查问题。

![图像](/help/journey-migration/refactoring-tools/assets/rscam8.png)

当作业成功完成时，**下载**&#x200B;按钮将变为可用，允许您检索：

- **重构的项目**：这是应用转换后的更新代码。 客户可以为其项目下载最新的代码。
- **活动日志**：在作业执行期间，该工具执行的所有步骤和所做的更改都将作为此过程的一部分记录。
- **调查结果报告**：此报告包含工具未完全执行但仍需要处理的项。 此处记录所有此类更改。

![图像](/help/journey-migration/refactoring-tools/assets/rscam9.png)

>[!NOTE]
>
>每项作业最多可能需要1小时才能完成。 如果状态未更新，请联系Adobe支持部门。
