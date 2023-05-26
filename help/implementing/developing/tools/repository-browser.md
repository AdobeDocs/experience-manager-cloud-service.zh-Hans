---
title: 存储库浏览器
seo-title: Repository Browser
description: 存储库浏览器为创作、发布和预览层上的所有环境提供对存储库的只读视图。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: 43429562ea4292f38d3459e03185270ec950a58a
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 2%

---

# 存储库浏览器 {#repository-browser}

>[!NOTE]
>
>存储库浏览器在AEM版本6582及更高版本上可用。

>[!INFO]
>
>您也可以观看 [此剪辑](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) 有关如何使用Repository Browser调试AEMas a Cloud Service的快速视频介绍。

## 简介 {#introduction}

存储库浏览器是一种开发人员工具，可为创作、发布和预览层上的所有环境提供存储库的只读视图。 它旨在方便查看内容结构，以便更轻松地查看或调试内容。

可从开发人员控制台访问，它可用于浏览选定环境的作者或发布实例的存储库。

### 访问先决条件 {#access-prerequisites}

要访问开发人员控制台或存储库浏览器，必须满足以下条件

要访问开发人员控制台，请执行以下操作：

* 对于生产程序，用户必须具有 **Cloud Manager — 开发人员角色** 在Admin Console中
* 对于沙盒程序，它可供具有产品配置文件的任何用户使用，这些配置文件授予他们访问AEMas a Cloud Service的权限。

要访问存储库浏览器，请执行以下操作：

* 用户必须具有 **Cloud Manager — 开发人员** Admin Console中用于查看创作实例和发布实例的角色。
* 此外，对于作者，具有AEM用户产品配置文件的用户能够以最低的读取访问权限查看存储库浏览器；浏览存储库时用户的权限受到尊重。 具有AEM管理员产品配置文件的用户可以使用完全读取权限查看存储库浏览器。

有关设置用户权限的更多信息，请参阅 [Cloud Manager文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### 启动存储库浏览器 {#launching-the-repository-browser}

可以按照以下步骤启动存储库浏览器。

1. 在Cloud Manager中，单击所选环境旁边的三个圆点，然后选择 **开发人员控制台**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 接下来，单击 **存储库浏览器** 选项卡
1. 通过单击 **Pod** 下拉列表。

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 通过单击 **打开存储库浏览器** 链接更靠下方。 这将启动与选定层的代表性实例(pod)对应的浏览器。 这将启动与选定层的代表性实例(pod)对应的浏览器。 请注意，您无法控制已启动层的特定面板。

## 功能 {#features}

### 在层次结构中定位 {#navigate-the-hierarchy}

您可以使用左侧导航窗格来导航内容层次结构。 单击每个文件夹或节点将显示其子项。 文件夹结构反映了Sling资源树，它是JCR节点树的超集。

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

或者，您也可以通过在以下位置输入路径来直接导航到该路径： **路径** 字段，如下所示。 这还将扩展其在左侧内容层次结构视图中的位置。

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

每当您单击左侧的文件夹时，“路径”字段都会自动填充其位置。 这可用于复制和粘贴值以供以后使用。

此外，单击文件夹时，URL会动态修改以包含该文件夹的路径。 这允许使用可书签的URL。

对于发布，默认情况下，存储库浏览器将仅显示公共内容，因此某些文件夹 `/conf` 或 `/home` 将不可见。

要使这些位置可见，您需要遵循以下步骤。

1. 单击所选环境旁边的三个圆点，然后选择 **管理访问权限**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. 找到您的发布实例，然后单击它

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. 为发布管理员创建新的产品配置文件。 在以下示例中，将其称为 **开发 — AEM管理员发布**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. 将相应的用户添加到新产品配置文件，这些用户应该能够以完全访问权限在发布存储库浏览器中导航

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 等待几分钟，然后打开 **AEM创作** 控制台
1. 将对应于新产品配置文件的组添加为管理员组的成员。 您可以通过单击 **工具 — 安全 — 作者群组**，然后单击 **管理员** 组。 然后，添加该组，如下所示

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. 激活 **管理员** 和新的 **开发 — AEM管理员发布** 组，以便它们可在Publish上使用

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. 作为良好的安全实践，请删除新的 **开发 — AEM管理员发布** 上的管理员组中的组 **作者** 所以新组织是孤立的

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. 访问发布实例的存储库浏览器时，所有文件夹均可见，包括 `/home` 和 `/conf`.

### 查看JCR属性 {#view-jcr-properties}

单击节点将在导航浏览器的右侧窗格中显示其JCR属性。 以下示例适用于 `experience-fragments` 节点。

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### 查看内容 {#view-content}

您可以通过单击导航窗格中的资源，使用存储库浏览器查看内容。 这将在浏览器右侧的选项卡下打开预览，该选项卡以相应资源命名。

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

预览当前可用于以下列表中的图像类型：

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* webp
* bmp
* x-icon
* tiff

对于以下基于文本的MIME类型，和：

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### 下载内容 {#download-content}

您还可以使用存储库浏览器下载内容。 在以下示例中，您可以按 **下载** 链接以下载 `jcr:data` 与选定节点相关联。 通过导航到包含属性定义的节点，此功能可用于所有二进制属性。

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
