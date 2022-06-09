---
title: 存储库浏览器
seo-title: Repository Browser
description: 存储库浏览器为创作层、发布层和预览层上的所有环境提供了对存储库的只读视图。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: b4d28a0c827fb07d6f731118078ecdf448e2f58b
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 2%

---

# 存储库浏览器 {#repository-browser}

>[!NOTE]
>
>存储库浏览器在AEM版本6582及更高版本上可用。

>[!INFO]
>
>您还可以观看 [这个剪辑](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) 有关如何使用存储库浏览器调试AEMas a Cloud Service的快速视频介绍。

## 简介 {#introduction}

存储库浏览器是一个开发人员工具，它为创作层、发布层和预览层上的所有环境提供了对存储库的只读视图。 它旨在便于查看内容结构，以便更便于查看或调试内容。

可从开发人员控制台访问，以用于浏览所选环境的创作实例或发布实例的存储库。

### 访问先决条件 {#access-prerequisites}

必须满足以下条件才能访问开发人员控制台或存储库浏览器

要访问开发人员控制台，请执行以下操作：

* 对于生产程序，用户必须具有 **Cloud Manager — 开发人员角色** Admin Console
* 对于沙盒程序，具有产品用户档案且有权访问AEMas a Cloud Service的任何用户均可使用该程序。

要访问存储库浏览器，请执行以下操作：

* 用户必须具有 **Cloud Manager — 开发人员** 在Admin Console中查看创作和发布实例的角色。
* 此外，对于作者而言，具有AEM Users产品配置文件的用户可以以最低的读取权限查看存储库浏览器；浏览存储库时，将遵守用户的权限。 具有AEM管理员产品配置文件的用户可以查看具有完全读取访问权限的存储库浏览器。

有关设置用户权限的更多信息，请参阅 [Cloud Manager文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### 启动存储库浏览器 {#launching-the-repository-browser}

可以按照以下步骤启动存储库浏览器。

1. 在Cloud Manager中，单击所选环境旁边的三个圆点，然后选择 **开发人员控制台**

   ![repbrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 接下来，单击 **存储库浏览器** 选项卡
1. 通过单击 **面板** 下拉列表。

   ![repbrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 通过单击 **打开存储库浏览器** 进一步下链接。 这将启动与所选层的代表性实例（面板）对应的浏览器。 这将启动与所选层的代表性实例（面板）对应的浏览器。 请注意，您无法控制所启动层的特定面板。

## 功能 {#features}

### 导航层次结构 {#navigate-the-hierarchy}

您可以使用左侧导航窗格在内容层次结构中进行分析。 单击每个文件夹或节点将显示其子项。 文件夹结构反映Sling资源树，该树是JCR节点树的超集。

![repbrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

<!-- Alexandru: temporarily commenting this out, please don't delete. 

Alternatively, you can navigate directly to a path by entering it in the **Path** field, as shown below. This will also expand its location in the content hierarcy view on the left.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

Whenever you click a folder on the left, the Path field automatically populates with its location. This is useful for copying and pasting the value for later usage.

Additionally, when you click on a folder, the URL is dynamically modified to include the path to that folder. This allows for bookmarkable URLs.

-->

对于发布，默认情况下，存储库浏览器将仅显示公共内容，因此某些文件夹(如 `/conf` 或 `/home` 将不可见。

要使这些位置可见，您需要按照以下步骤操作。

1. 单击所选环境旁边的三个圆点，然后选择 **管理访问权限**

   ![repbrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. 找到您的发布实例，然后单击该实例

   ![repbrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. 为发布管理员创建新的产品配置文件。 在以下示例中，它称为 **开发 — AEM管理员发布**

   ![repbrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. 将相应的用户（对应于应能够导航具有完全访问权限的发布存储库浏览器的用户）添加到新产品配置文件

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 等待几分钟，然后打开 **AEM作者** 控制台
1. 将与新产品配置文件对应的组添加为管理员组的成员。 您可以通过单击 **工具 — 安全 — 创作组**，然后单击 **管理员** 群组。 然后，按如下所示添加群组

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. 激活 **管理员** 和新 **开发 — AEM管理员发布** 群组，以便在发布时可用

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. 作为一项良好的安全实践，请删除 **开发 — AEM管理员发布** 组 **作者** 这样，新组便被隔离以发布

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. 访问发布实例的存储库浏览器时，所有文件夹都可见，包括 `/home` 和 `/conf`.

### 查看JCR属性 {#view-jcr-properties}

单击某个节点将在导航浏览器的右侧窗格中显示其JCR属性。 以下是 `experience-fragments` 节点。

![repbrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### 查看内容 {#view-content}

您可以使用存储库浏览器通过单击导航窗格中的资源来查看内容。 这将在浏览器右侧以相应资源命名的选项卡下打开预览。

![repbrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

预览功能当前适用于以下列表中的图像类型：

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* webp
* bmp
* x图标
* tiff

对于以下基于文本的mime类型：

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### 下载内容 {#download-content}

您还可以使用存储库浏览器下载内容。 在以下示例中，您可以按 **下载** 下载链接 `jcr:data` 与选定节点关联。 通过导航到包含属性定义的节点，此功能可用于所有二进制属性。

![repbrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
