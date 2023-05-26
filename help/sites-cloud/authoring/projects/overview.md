---
title: 项目
description: 通过项目，您可以将资源分组到一个实体中，该实体通过共享的公共环境可轻松管理项目
exl-id: c5f3331e-637f-4816-be83-faf2df59bd5f
source-git-commit: 8ea043b4b6424d6922c41c143ca74fd25ac60cf8
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 51%

---

# 项目 {#projects}

通过项目，您可以将资源分组到一个实体中。 通过一个通用的共享环境，可轻松管理您的项目。 您可以与项目关联的资源类型在AEM中称为“图块”。 拼贴可以包含项目和团队信息、资产、工作流及其他类型的信息，如[项目拼贴](#project-tiles)中详述。

>[!CAUTION]
>
>对于项目中的用户，如果要在使用“项目”功能（如创建项目、创建任务/工作流、查看和管理团队）时查看其他用户/组，这些用户需要拥有 `/home/users` 和 `/home/groups` 的读访问权限。满足这一要求的最简单方法是向 **projects-users** 组授予对 `/home/users` 和 `/home/groups` 的读访问权。

作为用户，您可以执行以下操作：

* 创建项目
* 将内容和资产文件夹关联到项目
* 删除项目
* 从项目中删除内容链接

请参阅以下附加主题：

* [管理项目](/help/sites-cloud/authoring/projects/managing.md)
* [处理任务](/help/sites-cloud/authoring/projects/tasks.md)
* [使用项目工作流](/help/sites-cloud/authoring/projects/workflows.md)

## 项目控制台 {#projects-console}

在项目控制台中，您可以访问和管理AEM中的项目。

![“项目”控制台](/help/sites-cloud/authoring/assets/projects-console.png)

* 选择&#x200B;**时间线**，然后选择一个项目可查看其时间线。
* 单击/点按 **选择** 以进入选择模式。
* 单击 **创建** 以添加项目。
* **切换活动项目** 允许您在所有项目之间切换，并且只切换处于活动状态的项目。
* **显示统计信息视图** 用于查看有关任务完成的项目统计信息。

## 项目拼贴 {#project-tiles}

使用“项目”，您可以将不同类型的信息与项目关联。 这些称为 **磁贴**. 本节将介绍每个图块及其包含的信息类型。

您可以使以下磁贴与项目关联。 以下各节将逐一进行说明：

* 资产和资产收藏集
* 体验
* 链接
* 项目信息
* 团队
* 登录页面
* 电子邮件
* 工作流
* 启动项
* 任务

### 资产 {#assets}

在 **资产** 图块，您可以收集用于特定项目的所有资源。

![“资产”拼贴](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

您可以直接在图块中上传资产。 此外，如果您具有Dynamic Media加载项，则可以创建图像集、旋转集或混合媒体集。

![图像集](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### 资产收藏集 {#asset-collections}

与资源类似，您可以添加 [资产收藏集](/help/assets/manage-collections.md) 直接转到您的项目。 您可以在Assets中定义收藏集。

![资产收藏集](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

通过单击&#x200B;**添加收藏集**&#x200B;并从列表中选择相应的收藏集来添加收藏集。

### 体验 {#experiences}

此 **体验** 通过图块，您可以将移动设备应用程序、网站或发布添加到项目中。

![体验](/help/sites-cloud/authoring/assets/project-experiences.png)

这些图标指示表示的体验类型：网站、移动应用程序或发布。通过点按或单击向下 V 形并点按&#x200B;**添加体验**&#x200B;和选择体验类型来添加体验。

![添加体验](/help/sites-cloud/authoring/assets/projects-add-experience.png)

选择缩略图的路径，并在适用的情况下更改体验的缩略图。体验会在&#x200B;**体验**&#x200B;拼贴中进行分组。

### 链接 {#links}

通过“链接”拼贴，可将外部链接与项目相关联。

![链接](/help/sites-cloud/authoring/assets/project-links.png)

您可以使用易于识别的名称来命名链接并更改其缩略图。

![添加链接](/help/sites-cloud/authoring/assets/projects-add-link.png)

### 项目信息 {#project-info}

“项目信息”拼贴提供有关项目的一般信息，包括描述、项目状态（非活动或活动）、截止日期和成员。 此外，您还可以添加项目缩略图，该缩略图显示在主项目页面上。

![项目信息](/help/sites-cloud/authoring/assets/project-info.png)

您可以从该拼贴和“团队”拼贴中分配和删除团队成员（或者更改其角色）。

![将团队成员添加到项目](/help/sites-cloud/authoring/assets/projects-add-team.png)

### 翻译作业 {#translation-job}

翻译作业拼贴是您开始翻译的位置，也是您查看翻译状态的地方。 要设置翻译，请参阅 [创建翻译项目](/help/assets/translate-assets.md).

![翻译作业](/help/sites-cloud/authoring/assets/projects-translation-job.png)

单击&#x200B;**翻译作业**&#x200B;卡片底部的省略号可查看翻译工作流中的资产。翻译作业列表还会显示资产元数据和标记条目。这些条目指示资产的元数据和标记也会被翻译。

![翻译作业详细信息](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### 团队 {#team}

在此图块中，您可以指定项目团队的成员。 编辑时，您可以输入团队成员的名称并分配用户角色。

![“团队”拼贴](/help/sites-cloud/authoring/assets/projects-team-tile.png)

您可以在团队中添加和删除团队成员。此外，您还可以编辑向团队成员分配的[用户角色](#user-roles-in-a-project)。

![从列表添加团队](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### 工作流 {#workflows}

您可以按照特定工作流分配项目。 如果有任何工作流正在运行，其状态会显示在 **工作流** 在项目中拼贴。

![工作流](/help/sites-cloud/authoring/assets/project-workflows.png)

您可以按照特定工作流分配项目。 根据您选择的项目，您有不同的可用工作流。

有关这些功能的说明，请参见 [使用项目工作流。](/help/sites-cloud/authoring/projects/workflows.md)

### 启动项 {#launches}

“启动项”图块显示已请求的任何启动项。 [请求启动工作流。](/help/sites-cloud/authoring/projects/workflows.md)

![启动项](/help/sites-cloud/authoring/assets/project-launches.png)

### 任务 {#tasks}

任务允许您监控任何与项目相关的任务（包括工作流）的状态。 [处理任务](/help/sites-cloud/authoring/projects/tasks.md)中详细介绍了任务。

![任务](/help/sites-cloud/authoring/assets/projects-tasks.png)

## 项目模板 {#project-templates}

AEM 提供了三种不同的现成模板：

* 简单项目 – 任何不适合其他类别的项目的参考示例（综合）。它包括三个基本角色（所有者、编辑者和观察者）和四个工作流（项目批准、请求启动项、请求登陆页面和请求电子邮件）。
* 媒体项目 – 适用于媒体相关活动的参考示例项目。它包括几个与媒体相关的项目角色（摄影师、编辑者、撰稿人、设计师、所有者和观察者）。它还请求复制工作流来请求和审查文本。
* [翻译项目](/help/sites-cloud/administering/translation/overview.md) – 用于管理翻译相关活动的参考示例。它包括三个基本角色（所有者、编辑者和观察者）。此外，它还包括两个可在工作流用户界面中访问的工作流。

根据您选择的模板，您有不同的可用选项，尤其是关于用户角色和工作流的选项。

## 项目中的用户角色 {#user-roles-in-a-project}

不同的用户角色是在项目模板中设置的，主要原因有二：

1. 权限。用户角色属于列出的三个类别之一：观察者、编辑者、所有者。 例如，摄影师或撰稿人将拥有与编辑者相同的权限。这些权限决定用户可以对项目中的内容执行的操作。
1. 工作流。工作流可确定在项目中向谁分配了任务。 任务可以与项目角色关联。例如，可以将任务分配给摄影师，以便具有摄影师角色的所有团队成员都能获得该任务。

所有项目都支持以下默认角色，以便您管理安全和控制权限：

| 角色 | 描述 | 权限 | 组成员资格 |
|---|---|---|---|
| 观察者 | 具有此角色的用户可以查看项目详细信息，包括项目状态。 | 项目的只读权限 | `workflow-users` 组 |
| 编辑器 | 此角色中的用户可以上传和编辑项目的内容。 | 对项目、相关元数据和相关资产的读写访问权限；上传镜头列表以及审查和批准资产的权限；对 /etc/commerce 的写入权限；对特定项目的修改权限 | workflow-users 组 |
| 所有者 | 具有此角色的用户可以启动项目。所有者可以创建项目、在项目中启动工作，以及将批准的资产移动到“生产”文件夹。所有者还可以查看和执行项目中的所有其他任务。 | `/etc/commerce` 的写入权限 | `dam-users` 组（能够创建项目），project-administrators 组（能够创建项目和移动资产） |

>[!NOTE]
>
>在创建项目并将用户添加各种角色时，将自动创建与项目关联的组以管理关联的权限。例如，名为 Myproject 的项目将有三个组，分别为 **Myproject 所有者**、**Myproject 编辑者**、**Myproject 观察者**。但是，如果删除了项目，这些组不会自动删除。管理员需要在&#x200B;**工具** > **安全** > **组**&#x200B;中手动删除这些组。
