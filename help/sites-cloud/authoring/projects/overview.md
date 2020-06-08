---
title: 项目
description: 通过“项目”，您可以将资源分组到一个实体中，该实体的通用共享环境使您能够轻松管理项目
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 72%

---


# 项目 {#projects}

通过“项目”，您可以将资源分组到一个实体中。通用共享环境使您能够轻松管理项目。可以与项目关联的资源类型在 AEM 中称为“拼贴”。Tiles may include project and team information, assets, workflows, and other types of information, as described in detail in [Project Tiles.](#project-tiles)

>[!CAUTION]
>
>For users in projects to see other users/groups while using Projects functionality like creating projects, creating tasks/workflows, seeing and managing the team, those users need to have read access on `/home/users` and `/home/groups`. The easiest way to implement this is to give the **projects-users** group read access to `/home/users` and `/home/groups`.

作为用户，您可以执行以下操作：

* 创建项目
* 将内容和资产文件夹关联到项目
* 删除项目
* 从项目中删除内容链接

请参阅以下其他主题：

* [管理项目](/help/sites-cloud/authoring/projects/managing.md)
* [处理任务](/help/sites-cloud/authoring/projects/tasks.md)
* [使用项目工作流](/help/sites-cloud/authoring/projects/workflows.md)

## “项目”控制台{#projects-console}

在“项目”控制台中，您可以访问和管理 AEM 中的项目。

![项目控制台](/help/sites-cloud/authoring/assets/projects-console.png)

* 选择&#x200B;**时间轴**，然后选择一个项目可查看其时间轴。
* 单击/点按&#x200B;**选择**&#x200B;可进入选择模式。
* 单击&#x200B;**创建**&#x200B;可添加项目。
* **切换活动的项目**&#x200B;允许您在所有项目和仅处于活动状态的项目之间切换。
* **显示统计信息视图**&#x200B;允许您查看与任务完成程度相关的项目统计信息。

## 项目拼贴 {#project-tiles}

通过项目，您可以将不同类型的信息与项目关联。这些信息称为&#x200B;**拼贴**。本节介绍了各个拼贴以及它们包含的信息类型。

您可以将以下拼贴与项目关联。以下各部分介绍了每个拼贴：

* 资产和资产收藏集
* 体验
* 链接
* 项目信息
* 团队
* 登陆页面
* 电子邮件
* 工作流
* 启动项
* 任务

### 资产 {#assets}

在&#x200B;**资产**&#x200B;拼贴中，您可以收集用于特定项目的所有资产。

![资源拼贴](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

您可以直接在该拼贴中上传资产。另外，如果您拥有 Dynamic Media 加载项，则可以创建图像集、旋转集或混合媒体集。

![图像集](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### 资产收藏集 {#asset-collections}

与资产类似，您可以直接将资产收藏集添加到项目中。You define collections in Assets. <!--Similar to assets, you can add [asset collections](/help/assets/managing-collections-touch-ui.md) directly to your project. You define collections in Assets.-->

![资产收集](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

单击&#x200B;**添加收藏集**&#x200B;并从列表中选择相应的收藏集，可添加收藏集。

### 体验 {#experiences}

**体验**&#x200B;拼贴允许您将移动设备应用程序、网站或出版物添加到项目中。

![体验](/help/sites-cloud/authoring/assets/project-experiences.png)

这些图标指示表示的体验类型：网站、移动应用程序或出版物。 单击+符号或单击添加体验 **并选择体验类型** ，以添加体验。

![添加体验](/help/sites-cloud/authoring/assets/projects-add-experience.png)

选择缩略图的路径，并在适用的情况下更改体验的缩略图。Experiences are grouped together in the **Experiences** tile.

### 链接 {#links}

“链接”拼贴允许您将外部链接与项目关联。

![链接](/help/sites-cloud/authoring/assets/project-links.png)

您可以使用易于识别的名称来命名链接并更改其缩略图。

![添加链接](/help/sites-cloud/authoring/assets/projects-add-link.png)

### 项目信息 {#project-info}

“项目信息”拼贴提供了项目的一般信息，包括描述、项目状态（非活动或活动）、到期日期和成员。此外，您还可以添加项目缩略图，该缩略图会显示在“项目”主页上。

![项目信息](/help/sites-cloud/authoring/assets/project-info.png)

您可以从该拼贴和“团队”拼贴中分配和删除团队成员（或者更改其角色）。

![将团队成员添加到项目](/help/sites-cloud/authoring/assets/projects-add-team.png)

### 翻译作业 {#translation-job}

在“翻译作业”拼贴中，您可以开始翻译，也可以查看翻译状态。To set up your translation, see Creating Translation Projects. <!--To set up your translation, see [Creating Translation Projects](/help/assets/translation-projects.md).-->

![翻译作业](/help/sites-cloud/authoring/assets/projects-translation-job.png)

Click the ellipsis at the bottom of the **Translation Job** card to view the assets in the translation workflow. 转换作业列表还显示资产元数据和标记的条目。 这些条目指示资产的元数据和标记也会被翻译。

![翻译作业详细信息](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### 团队 {#team}

在此拼贴中，您可以指定项目团队的成员。编辑时，您可以输入团队成员的姓名并分配用户角色。

![团队拼贴](/help/sites-cloud/authoring/assets/projects-team-tile.png)

您可以在团队中添加和删除团队成员。In addition, you can edit the [user role](#user-roles-in-a-project) assigned to the team member.

![从列表添加团队](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### 工作流 {#workflows}

您可以指定项目遵循特定的工作流。当有任何工作流正在运行时，其状态会显示在“项目”的&#x200B;**工作流**&#x200B;拼贴中。

![工作流](/help/sites-cloud/authoring/assets/project-workflows.png)

您可以指定项目遵循特定的工作流。根据您选择的项目，您可以使用不同的工作流。

这些工作流在[使用项目工作流](/help/sites-cloud/authoring/projects/workflows.md)中进行了介绍。

### 启动项 {#launches}

“启动项”拼贴显示使用[请求启动项工作流](/help/sites-cloud/authoring/projects/workflows.md)请求的任何启动项。

![启动项](/help/sites-cloud/authoring/assets/project-launches.png)

### 任务 {#tasks}

“任务”拼贴允许您监测任何项目相关任务（包括工作流）的状态。Tasks are covered in detail at [Working with Tasks](/help/sites-cloud/authoring/projects/tasks.md).

![任务](/help/sites-cloud/authoring/assets/projects-tasks.png)

## 项目模板 {#project-templates}

AEM附带三个不同的现成模板：

* 简单项目——任何不适合其他类别的项目的参考范例（全部捕获）。 它包括三个基本角色（所有者、编辑者和观察者）和四个工作流（项目批准、请求启动项、请求登陆页面和请求电子邮件）。
* 媒体项目——与媒体相关的活动的参考示例项目。 它包括几个与媒体相关的项目角色（摄影师、编辑者、撰稿人、设计师、所有者和观察者）。它还包括两个与媒体内容相关的工作流-请求复制（用于请求和查看文本）和产品照片拍摄（用于管理与产品相关的照片）
* 翻译项目 - 用于管理翻译相关活动的参考示例。它包括三个基本角色（所有者、编辑者和观察者）。It includes two workflows that are accessed in the Workflows user interface. <!--* [A translation project](/help/sites-administering/translation.md) - A reference sample for managing translation related activities. It includes three basic roles (Owners, Editors, and Observers). It includes two workflows that are accessed in the Workflows user interface.-->

根据您选择的模板，您可以使用不同的选项，特别是与用户角色和工作流有关的选项。

## 项目中的用户角色 {#user-roles-in-a-project}

项目模板中设置了不同的用户角色，之所以使用这些用户角色，主要是出于以下两个原因：

1. 权限. 用户角色属于下列三个类别之一：观察者、编辑者、所有者。例如，摄影师或文案人将具有与编辑相同的权限。 权限决定了用户可以对项目中的内容执行的操作。
1. 工作流. 工作流可确定向谁分配了项目中的任务。任务可以与项目角色关联。 例如，可以将某个任务分配给摄影师，这样所有具有摄影师角色的团队成员都将会获取该任务。

所有项目都支持以下默认角色，以便您可以管理安全性和控制权限：

| 角色 | 描述 | 权限 | 组成员资格 |
|---|---|---|---|
| 观察者 | 具有此角色的用户可以查看项目详细信息，包括项目状态。 | 项目的只读权限 | `workflow-users` 组 |
| 编辑者 | 具有此角色的用户可以上传和编辑项目的内容。 | 对项目、相关元数据和相关资产的读写权限； 上传拍摄列表、照片拍摄以及审核和批准资产的权限； /etc.commerce的写入权限； 修改特定项目的权限 | 工作流用户组 |
| 所有者 | 具有此角色的用户可以启动项目。所有者可以创建项目、在项目中启动工作，以及将已批准的资产移动到“生产”文件夹。 所有者还可以查看和执行项目中的所有其他任务。 | Write permission on `/etc/commerce` | `dam-users` 用户组（能够创建项目）项目管理员组（能够移动资产） |

>[!NOTE]
>
>在创建项目并将用户添加各种角色时，将自动创建与项目关联的组以管理关联的权限。例如，名为 Myproject 的项目将有三个组，分别为 **Myproject 所有者**、**Myproject 编辑者**、**Myproject 观察者**。但是，如果删除了项目，这些组不会自动删除。管理员需要在&#x200B;**工具** > **安全** > **组**&#x200B;中手动删除这些组。
