---
title: 搜索
description: 使用完备的搜索功能更快速地查找您的内容
exl-id: 8a799e9a-1461-4e79-ae90-1978af6cf0ed
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 100%

---

# 搜索 {#search-feature}

AEM 的创作环境提供了多种内容搜索机制，具体取决于资源类型。

## 搜索基础知识 {#search-basics}

可从顶部工具栏中使用搜索功能：

![“搜索”图标](/help/sites-cloud/authoring/assets/search-icon.png)

使用搜索边栏可以：

* 搜索特定的关键字、路径或标记
* 按照特定于资源的条件进行筛选，例如修改日期、页面状态和文件大小等。
* 定义和使用[保存的搜索](#saved-searches) - 均基于以上条件

>[!NOTE]
>
>显示搜索边栏时，还可以使用热键 `/`（正斜杠）调用搜索。

## 搜索和筛选 {#search-and-filter}

要搜索和筛选您的资源，请执行以下操作：

1. 打开&#x200B;**搜索**（使用工具栏中的放大镜）并输入您的搜索词。将向您提供相关的建议，并且可供您选择：

   ![搜索词](/help/sites-cloud/authoring/assets/search-term.png)

   默认情况下，搜索结果将被限制在您的当前位置（例如控制台和相关的资源类型）：

   ![搜索位置](/help/sites-cloud/authoring/assets/search-term-location.png)

1. 如果需要，您可以删除位置过滤器（选中要删除的过滤器上的 **X**），以在所有控制台/资源类型之间进行筛选。
1. 将会显示结果，并按控制台和相关的资源类型进行分组。

   您可以选择一种特定的资源（用于未来操作），或通过选择所需的资源类型向下展开；例如&#x200B;**查看全部站点**：

   ![搜索结果](/help/sites-cloud/authoring/assets/search-results.png)

1. 如果您需要进一步向下展开，请选择“边栏”符号（左上方）以打开侧面板&#x200B;**过滤器和选项**。

   ![边栏按钮](/help/sites-cloud/authoring/assets/rail-button.png)

   根据资源类型，搜索将显示预定义的搜索/筛选条件选项。

   侧面板允许您选择以下内容：

   * 保存的搜索
   * 搜索目录
   * 标记
   * 搜索条件，例如修改日期、发布状态、LiveCopy 状态

   >[!NOTE]
   >
   >搜索条件可能会视情况而异：
   >
   >* 具体视您选择的资源类型而定；例如，资产和社区条件理所当然是专用的；
   >* 您可以自定义搜索表单实例（对应于在 AEM 中的位置）。


<!--
  >* Your instance as the [Search Forms](/help/sites-administering/search-forms.md) can be customized (appropriate to the location within AEM).
  -->

![搜索侧面板](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 您还可以添加其他搜索词。

1. 使用 **X**（右上方）关闭&#x200B;**搜索**。

>[!NOTE]
>
>在搜索结果中选择某个项目时，搜索条件会持续保留。
>
>当您在搜索结果页面上选择某个项目时，如果使用浏览器后退按钮返回到搜索页面，则搜索条件仍将存在。

## 保存的搜索 {#saved-searches}

除了按照多方面条件进行搜索以外，您还可以保存特定的搜索配置以供日后检索和使用：

1. 定义搜索条件，然后选择&#x200B;**保存**。

   ![保存搜索](/help/sites-cloud/authoring/assets/search-side-panel.png)

1. 指定名称，然后使用&#x200B;**保存**&#x200B;进行确认。

   ![使用名称保存搜索](/help/sites-cloud/authoring/assets/search-save-name.png)

1. 在下次访问搜索面板时，您可以从选择器中选择保存的搜索：

   ![保存的搜索](/help/sites-cloud/authoring/assets/saved-searches.png)

1. 在保存之后，您可以执行以下操作：

   * 使用 **x**（针对保存的搜索的名称）以开始新的查询（保存的搜索本身将不会被删除）。
   * **编辑保存的搜索**，更改搜索条件，然后再次&#x200B;**保存**。

通过选择保存的搜索并单击搜索面板底部的&#x200B;**编辑保存的搜索**，可以修改保存的搜索。

![修改保存的搜索](/help/sites-cloud/authoring/assets/saved-searches-modify.png)
