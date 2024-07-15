---
title: 存储库浏览器
seo-title: Repository Browser
description: 存储库浏览器为创作层、发布层和预览层上的所有环境提供到存储库的只读视图。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 9d1b51b465a148551de93f8180b056b8e7752db5
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---

# 存储库浏览器 {#repository-browser}

>[!NOTE]
>
>存储库浏览器在AEM版本6582及更高版本上可用。

>[!INFO]
>
>您还可以观看[此剪辑](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html)，观看有关如何使用存储库浏览器调试AEM as a Cloud Service的快速视频介绍。

## 简介 {#introduction}

存储库浏览器是一种开发人员工具，可为创作、发布和预览层上的所有环境提供到存储库的只读视图。 它旨在方便查看内容结构，以便更轻松地查看或调试内容。

可从[AEM as a Cloud Service Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)访问，它可用于浏览选定环境的创作或发布实例的存储库。

### 访问先决条件 {#access-prerequisites}

要访问AEM as a Cloud Service Developer Console或存储库浏览器，必须满足以下条件

要访问AEM as a Cloud Service Developer Console，请参阅[Developer Console访问权限](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#developer-console-access)。

要访问存储库浏览器，必须满足与AEM as a Cloud Service Developer Console相同的条件（以上指定）。 要查看特定实例的存储库浏览器内容，请执行以下操作：

* 创作实例：具有&#x200B;**创作实例**&#x200B;的AEM Users产品配置文件的用户能够以最低的读取权限查看存储库浏览器；在浏览存储库时，用户的权限将被考虑。 具有AEM管理员产品配置文件的用户可以使用完全读取权限查看存储库浏览器。

* Publish实例：具有&#x200B;**Publish实例**&#x200B;的AEM用户产品配置文件的用户能够以最低的读取权限查看存储库浏览器。 如果没有该产品配置文件集，用户将以匿名用户身份导航，并且由于权限限制，某些路径将不会显示。

有关设置用户权限的更多信息，请参阅[Cloud Manager文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html)。

### 启动存储库浏览器 {#launching-the-repository-browser}

可以按照以下步骤启动存储库浏览器。

1. 在Cloud Manager中，单击所选环境旁边的三个圆点，然后选择&#x200B;**Developer Console**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 接下来，单击&#x200B;**存储库浏览器**&#x200B;选项卡
1. 通过单击&#x200B;**面板**&#x200B;下拉列表选择与作者、发布或预览对应的任何面板。

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 单击下面的&#x200B;**打开存储库浏览器**&#x200B;链接，启动存储库浏览器。 启动与所选层的代表性实例(pod)对应的浏览器。 您无法控制已启动层的特定面板。

## 功能 {#features}

### 在层次结构中导航 {#navigate-the-hierarchy}

您可以使用左侧导航窗格在内容层次结构中导航。 单击每个文件夹或节点会显示其子节点。 文件夹结构反映了Sling资源树，它是JCR节点树的超集。

![报告浏览器3](/help/implementing/developing/tools/assets/repobrowser3.png)

或者，您也可以通过在&#x200B;**路径**&#x200B;字段中输入路径来直接导航到路径，如下所示。 此路径还会扩展其在左侧内容层次结构视图中的位置。

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

单击左侧的文件夹时，“路径”字段会自动填充其位置。 此功能对于复制和粘贴值以供以后使用很有用。

此外，单击文件夹时，URL会动态修改为包含该文件夹的路径。 此功能允许使用可书签的URL。

对于发布，默认情况下，存储库浏览器仅显示公共内容，因此某些文件夹（如`/conf`或`/home`）不可见。

要使这些位置可见，请执行以下操作。

1. 单击所选环境旁边的三个圆点，然后选择&#x200B;**管理访问权限**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. 找到您的发布实例，然后单击它

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. 为发布管理员创建产品配置文件。 在下面的示例中，它名为&#x200B;**DEV - AEM Administrators Publish**

   ![报表浏览器9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. 将相应的用户添加到新的产品配置文件，这些用户应该能够在发布存储库浏览器中拥有完全访问权限

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 等待几分钟，然后打开&#x200B;**AEM作者**&#x200B;控制台
1. 通过单击作者上的&#x200B;**工具 — 安全 — 组**，然后单击&#x200B;**管理员**&#x200B;组，将对应于新产品配置文件的组添加为管理员组的成员。 然后，添加该组，如下所示

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. 激活&#x200B;**管理员**&#x200B;和新的&#x200B;**DEV - AEM Administrators Publish**&#x200B;组，以便它们在发布时可用

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. 作为良好的安全做法，请从&#x200B;**author**&#x200B;上的管理员组中删除新的&#x200B;**DEV - AEM Administrators Publish**&#x200B;组，以便将该新组隔离为发布

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. 访问发布实例的存储库浏览器时，所有文件夹均可见，包括`/home`和`/conf`。

### 查看JCR属性 {#view-jcr-properties}

单击节点会在导航浏览器的右侧窗格中显示其JCR属性。 以下是`experience-fragments`节点的示例。

![报告浏览器4](/help/implementing/developing/tools/assets/repobrowser41.png)

### 查看内容 {#view-content}

您可以使用存储库浏览器查看内容。 单击导航窗格中的资源，以便在浏览器右侧的以相应资源命名的选项卡下打开预览。

![报告浏览器6](/help/implementing/developing/tools/assets/repobrowser61.png)

预览适用于以下图像类型：

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

对于以下基于文本的MIME类型，和：

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### 下载内容 {#download-content}

您还可以使用存储库浏览器下载内容。 在以下示例中，您可以按&#x200B;**下载**&#x200B;链接以下载与所选节点关联的`jcr:data`。 通过导航到包含属性定义的节点，此功能可用于所有二进制属性。

![报告浏览器5](/help/implementing/developing/tools/assets/repobrowser52.png)
