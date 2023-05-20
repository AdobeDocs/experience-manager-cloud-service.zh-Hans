---
title: 项目
description: 專案可讓您將資源群組到一個實體中，其共用的共用環境可讓您輕鬆管理專案
exl-id: c5f3331e-637f-4816-be83-faf2df59bd5f
source-git-commit: 8ea043b4b6424d6922c41c143ca74fd25ac60cf8
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 51%

---

# 项目 {#projects}

專案可讓您將資源分組到一個實體中。 共用的共用環境可讓您輕鬆管理專案。 您可以與專案建立關聯的資源型別在AEM中稱為「圖磚」。 拼贴可以包含项目和团队信息、资产、工作流及其他类型的信息，如[项目拼贴](#project-tiles)中详述。

>[!CAUTION]
>
>对于项目中的用户，如果要在使用“项目”功能（如创建项目、创建任务/工作流、查看和管理团队）时查看其他用户/组，这些用户需要拥有 `/home/users` 和 `/home/groups` 的读访问权限。满足这一要求的最简单方法是向 **projects-users** 组授予对 `/home/users` 和 `/home/groups` 的读访问权。

身為使用者，您可以執行下列動作：

* 建立專案
* 將內容和資產資料夾關聯至專案
* 刪除專案
* 從專案移除內容連結

請參閱下列其他主題：

* [管理项目](/help/sites-cloud/authoring/projects/managing.md)
* [处理任务](/help/sites-cloud/authoring/projects/tasks.md)
* [使用项目工作流](/help/sites-cloud/authoring/projects/workflows.md)

## 專案主控台 {#projects-console}

專案主控台是您在AEM中存取和管理專案的地方。

![“项目”控制台](/help/sites-cloud/authoring/assets/projects-console.png)

* 选择&#x200B;**时间线**，然后选择一个项目可查看其时间线。
* 按一下/點選 **選取** 以進入選取模式。
* 按一下 **建立** 以新增專案。
* **切換使用中專案** 可讓您在所有專案與僅限作用中專案之間切換。
* **顯示統計資料檢視** 可讓您檢視有關任務完成的專案統計資料。

## 專案動態磚 {#project-tiles}

使用「專案」時，您可以將不同型別的資訊與專案建立關聯。 這些稱為 **圖磚**. 本節將說明每個圖磚及其包含的資訊型別。

您可以讓下列圖磚與專案相關聯。 以下各節將逐一說明：

* 資產和資產集合
* 体验
* 链接
* 專案資訊
* 团队
* 登录页面
* 电子邮件
* 工作流
* 启动项
* 任务

### 资产 {#assets}

在 **資產** 圖磚，即可收集您用於特定專案的所有資產。

![“资产”拼贴](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

您直接在圖磚中上傳資產。 此外，如果您有Dynamic Media附加元件，可以建立影像集、迴轉集或混合媒體集。

![图像集](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### 資產集合 {#asset-collections}

與資產類似，您可以新增 [資產集合](/help/assets/manage-collections.md) 直接存取您的專案。 您可以在Assets中定義集合。

![资产收藏集](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

通过单击&#x200B;**添加收藏集**&#x200B;并从列表中选择相应的收藏集来添加收藏集。

### 体验 {#experiences}

此 **體驗** 圖磚可讓您將行動應用程式、網站或出版物新增至專案。

![体验](/help/sites-cloud/authoring/assets/project-experiences.png)

这些图标指示表示的体验类型：网站、移动应用程序或发布。通过点按或单击向下 V 形并点按&#x200B;**添加体验**&#x200B;和选择体验类型来添加体验。

![添加体验](/help/sites-cloud/authoring/assets/projects-add-experience.png)

选择缩略图的路径，并在适用的情况下更改体验的缩略图。体验会在&#x200B;**体验**&#x200B;拼贴中进行分组。

### 链接 {#links}

「連結」圖磚可讓您將外部連結與專案建立關聯。

![链接](/help/sites-cloud/authoring/assets/project-links.png)

您可以使用易于识别的名称来命名链接并更改其缩略图。

![添加链接](/help/sites-cloud/authoring/assets/projects-add-link.png)

### 项目信息 {#project-info}

「專案資訊」表徵圖提供專案的一般資訊，包括描述、專案狀態（非作用中或作用中）、到期日和成員。 此外，您可以新增顯示在主「專案」頁面上的專案縮圖。

![项目信息](/help/sites-cloud/authoring/assets/project-info.png)

您可以从该拼贴和“团队”拼贴中分配和删除团队成员（或者更改其角色）。

![将团队成员添加到项目](/help/sites-cloud/authoring/assets/projects-add-team.png)

### 翻译作业 {#translation-job}

「翻譯工作」表徵圖是您開始翻譯的位置，也是您檢視翻譯狀態的地方。 若要設定翻譯，請參閱 [建立翻譯專案](/help/assets/translate-assets.md).

![翻译作业](/help/sites-cloud/authoring/assets/projects-translation-job.png)

单击&#x200B;**翻译作业**&#x200B;卡片底部的省略号可查看翻译工作流中的资产。翻译作业列表还会显示资产元数据和标记条目。这些条目指示资产的元数据和标记也会被翻译。

![翻译作业详细信息](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### 团队 {#team}

您可以在此圖磚中指定專案團隊的成員。 編輯時，您可以輸入專案團隊成員的名稱並指派使用者角色。

![“团队”拼贴](/help/sites-cloud/authoring/assets/projects-team-tile.png)

您可以在团队中添加和删除团队成员。此外，您还可以编辑向团队成员分配的[用户角色](#user-roles-in-a-project)。

![从列表添加团队](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### 工作流 {#workflows}

您可以指派專案以遵循特定工作流程。 如果有任何工作流程在執行中，其狀態會顯示在 **工作流程** 圖磚（在專案中）。

![工作流](/help/sites-cloud/authoring/assets/project-workflows.png)

您可以指派專案以遵循特定工作流程。 根據您選擇的專案，您有不同的可用工作流程。

這些內容的說明請參閱 [使用專案工作流程。](/help/sites-cloud/authoring/projects/workflows.md)

### 启动项 {#launches}

「啟動」圖磚會顯示任何以請求方式進行的啟動 [請求啟動工作流程。](/help/sites-cloud/authoring/projects/workflows.md)

![启动项](/help/sites-cloud/authoring/assets/project-launches.png)

### 任务 {#tasks}

任務可讓您監控任何專案相關任務的狀態，包括工作流程。 [处理任务](/help/sites-cloud/authoring/projects/tasks.md)中详细介绍了任务。

![任务](/help/sites-cloud/authoring/assets/projects-tasks.png)

## 项目模板 {#project-templates}

AEM 提供了三种不同的现成模板：

* 简单项目 – 任何不适合其他类别的项目的参考示例（综合）。它包括三个基本角色（所有者、编辑者和观察者）和四个工作流（项目批准、请求启动项、请求登陆页面和请求电子邮件）。
* 媒体项目 – 适用于媒体相关活动的参考示例项目。它包括几个与媒体相关的项目角色（摄影师、编辑者、撰稿人、设计师、所有者和观察者）。它还请求复制工作流来请求和审查文本。
* [翻译项目](/help/sites-cloud/administering/translation/overview.md) – 用于管理翻译相关活动的参考示例。它包括三个基本角色（所有者、编辑者和观察者）。此外，它还包括两个可在工作流用户界面中访问的工作流。

根據您選取的範本，您有不同的可用選項，尤其是關於使用者角色和工作流程。

## 專案中的使用者角色 {#user-roles-in-a-project}

不同的使用者角色設定於專案範本中，主要原因有二：

1. 权限。使用者角色屬於列出的三個類別之一：觀察者、編輯者、擁有者。 例如，摄影师或撰稿人将拥有与编辑者相同的权限。這些許可權會決定使用者可以對專案中的內容執行的操作。
1. 工作流。工作流程會決定指派給專案中任務的人員。 任务可以与项目角色关联。例如，可以將任務指派給攝影師，以便所有擁有攝影師角色的團隊成員都能取得任務。

所有專案都支援下列預設角色，可讓您管理安全性及控制許可權：

| 角色 | 描述 | 权限 | 组成员资格 |
|---|---|---|---|
| 观察者 | 具有此角色的使用者可以檢視專案詳細資訊，包括專案狀態。 | 專案的唯讀許可權 | `workflow-users` 组 |
| 编辑器 | 此角色的使用者可以上傳和編輯專案內容。 | 对项目、相关元数据和相关资产的读写访问权限；上传镜头列表以及审查和批准资产的权限；对 /etc/commerce 的写入权限；对特定项目的修改权限 | workflow-users 组 |
| 所有者 | 具有此角色的用户可以启动项目。所有者可以创建项目、在项目中启动工作，以及将批准的资产移动到“生产”文件夹。所有者还可以查看和执行项目中的所有其他任务。 | `/etc/commerce` 的写入权限 | `dam-users` 组（能够创建项目），project-administrators 组（能够创建项目和移动资产） |

>[!NOTE]
>
>在创建项目并将用户添加各种角色时，将自动创建与项目关联的组以管理关联的权限。例如，名为 Myproject 的项目将有三个组，分别为 **Myproject 所有者**、**Myproject 编辑者**、**Myproject 观察者**。但是，如果删除了项目，这些组不会自动删除。管理员需要在&#x200B;**工具** > **安全** > **组**&#x200B;中手动删除这些组。
