---
title: 使用页面编辑器发布内容
description: 了解页面编辑器如何发布内容。
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 5871e04d3bd78bdd8df55d42e7619c98ea3f38ca
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 50%

---


# 使用站点编辑器发布内容 {#publishing}

了解页面编辑器如何发布内容。

## 从页面编辑器发布 {#publishing-from-the-page-editor}

如果您在[页面编辑器](/help/sites-cloud/authoring/page-editor/introduction.md)中编辑页面，则可以直接从编辑器中发布该页面。

1. 选择&#x200B;**页面信息**&#x200B;图标以打开相应的菜单，然后选择&#x200B;**发布页面**&#x200B;选项。

   ![通过页面选项发布页面](/help/sites-cloud/authoring/assets/publishing-page-options.png)

1. 根据页面是否包含需要发布的引用：

   * 如果不包含要发布的引用，则会直接发布页面。
   * 如果页面包含需要发布的引用，则会在&#x200B;**发布**&#x200B;向导中列出该内容，从该向导中可以：
      * 指定要与页面一起发布的资产或标记等，然后使用&#x200B;**发布**&#x200B;完成该过程。
      * 使用&#x200B;**取消**&#x200B;中止操作。

   ![使用页面发布引用](/help/sites-cloud/authoring/assets/publishing-references.png)

1. 选择&#x200B;**发布**&#x200B;会将页面复制到发布环境。在页面编辑器中，会显示一个确认发布操作的信息横幅。

   ![发布状态信息横幅](/help/sites-cloud/authoring/assets/publishing-info.png)

   当在控制台中查看同一页面时，将显示更新的发布状态。

   ![Sites 控制台列视图中的页面发布状态](/help/sites-cloud/authoring/assets/publishing-status-console-column.png)

>[!NOTE]
>
>从页面编辑器发布是一种简单的发布方式，即仅发布选定的一个或多个页面，而不发布任何子页面。

>[!NOTE]
>
>无法发布编辑器中按[别名](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced)处理的页面。编辑器中的发布选项仅适用于通过其实际路径访问的页面。

## 从页面编辑器中取消发布 {#unpublishing}

使用页面编辑器编辑页面时，如果要取消发布该页面，请在&#x200B;**页面信息**&#x200B;菜单中选择&#x200B;**取消发布页面**，操作方式与[发布页面](#publishing-from-the-editor)类似。

>[!NOTE]
>
>无法取消发布编辑器中按[别名](/help/sites-cloud/authoring/sites-console/page-properties.md#advanced)处理的页面。编辑器中的发布选项仅适用于通过其实际路径访问的页面。

## 从站点控制台中发布和取消发布 {#publishing-sites-console}

您还可以从站点控制台](/help/sites-cloud/authoring/sites-console/publishing-pages.md)发布[，当您希望发布多个内容页面或计划发布或取消发布时，这非常有用。
