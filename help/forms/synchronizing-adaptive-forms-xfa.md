---
title: 将自适应Forms与XFA表单模板同步
seo-title: Synchronizing Adaptive Forms with XFA Form Templates
description: 将自适应Forms与XFA/XDP文件同步。
seo-description: Synchronizing Adaptive Forms with XFA/XDP files.
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---


# 将自适应Forms与XFA表单模板同步{#synchronizing-adaptive-forms-with-xfa-form-templates}

## 简介 {#introduction}

您可以基于XFA表单模板创建自适应表单( `*.XDP` 文件)。 通过这种重复利用，您可以保留对现有XFA表单的投资。 有关如何使用XFA表单模板创建自适应表单的信息，请参阅 [根据模板创建自适应表单](creating-adaptive-form.md).

您可以在自适应表单中重复使用XDP文件中的字段。 这些字段称为绑定字段。 绑定字段的属性（如脚本、标签和显示格式）将从XDP文件复制。 您还可以选择覆盖其中某些属性的值。

[!DNL AEM Forms] 提供一种方法，可帮助您保持自适应Forms的字段与随后对XDP文件中的相应字段所做的任何更改保持同步。 本文介绍了如何启用此同步。

![您可以将字段从XFA表单拖动到自适应表单](assets/drag-drop-xfa.gif.gif)

在 [!DNL AEM Forms] 创作环境中，您可以将字段从XFA表单（左）拖到自适应表单（右）

## 前提条件 {#prerequisites}

要使用本文中的信息，建议您熟悉以下方面：

* [创建自适应表单](creating-adaptive-form.md)

* XFA(XML Forms架构)

要使用文章中提供的资产作为示例，请按照下一节中所述下载示例包， [示例包](synchronizing-adaptive-forms-xfa.md#p-sample-package-p).

## 示例包 {#sample-package}

文章使用一个示例来演示如何将自适应表单与更新的XFA表单模板同步。 示例中使用的资产都位于包中，可从 [下载](synchronizing-adaptive-forms-xfa.md#p-downloads-p) 章节。

上传资源包后，您可以在 [!DNL AEM Forms] UI。

使用包管理器安装包： `https://<server>:<port>/crx/packmgr/index.jsp`

资源包包含以下资产：

1. `sample-form.xdp`:以XFA表单模板为例

1. `sample-xfa-af`:基于sample-form.xdp文件的自适应表单。 但是，此自适应表单不包含任何字段。 在下一步中，我们将向此自适应表单添加内容。

### 将内容添加到自适应表单 {#add-content-to-adaptive-form-br}

1. 导航到https://&lt;server>:&lt;port>/aem/forms.html。 如果有疑问，请输入您的凭据。
1. 打开sample-af-xfa以在创作模式下进行编辑。
1. 从侧栏的内容浏览器中，选择数据模型对象选项卡。 将NumericField1和TextField1拖动到自适应表单上。
1. 从 **数值字段** to **AF数值字段。**

>[!NOTE]
>
>在上述步骤中，我们覆盖了XDP文件中字段的属性。 因此，如果稍后修改XDP文件中的相应属性，则不会同步此属性。

## 检测XDP文件中的更改 {#detecting-changes-in-xdp-file}

每当XDP文件或片段中发生任何更改时， [!DNL AEM Forms] UI会标记所有基于XDP文件或片段的自适应Forms。

更新XDP文件后，您需要在 [!DNL AEM Forms] 要标记的更改的UI。

例如，让我们更新 `sample-form.xdp` 文件：

1. 导航到 `https://<server>:<port>/projects.html.` 如果出现提示，请输入您的凭据。
1. 单击左侧的Forms选项卡。
1. 下载 `sample-form.xdp` 文件。 XDP文件将作为 `.zip` 文件，可使用任何文件解压实用程序提取。

1. 打开 `sample-form.xdp` 文件，并更改TextField1字段的标题 **文本字段** to **我的文本字段**.

1. 上传 `sample-form.xdp` 文件返回 [!DNL AEM Forms] UI。

如果XDP文件更新，则在根据XDP文件编辑自适应Forms时，您会在编辑器中看到一个图标。 此图标表示自适应表单与XDP文件不同步。 在下图中，查看侧栏中旁边的图标。

![用于显示自适应表单与XDP文件不同步的图标](assets/sync-af-xfa.png)

## 将自适应Forms与最新的XDP文件同步 {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

当打开与XDP文件不同步的自适应表单以供下次创作时，将显示以下消息： **自适应表单的架构/表单模板已更新。 `Click Here` 以使用新版本重新构建基础。**

单击消息可将自适应表单中的字段与XDP文件中的相应字段同步。

对于本文中使用的示例，请打开 `sample-xfa-af` 创作模式。 消息将向自适应表单的底部显示。

![提示您将自适应表单与XDP文件同步的消息](assets/sync-af-xfa-1.png)

### 更新属性 {#updating-the-properties}

除了作者在自适应表单（从组件对话框中）中显式覆盖的属性之外，所有从XDP文件复制到自适应表单的属性都会进行更新。 服务器日志中提供了已更新的属性列表。

要更新示例自适应表单中的属性，请单击链接(标有 `"Click Here"`)。 TextField1的标题从 **文本字段** to **我的文本字段**.

![update-property](assets/update-property.png)

>[!NOTE]
>
>未更改AF数值字段的标签，因为您已在组件属性对话框中覆盖此属性，如 [将内容添加到自适应Forms](synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p).

### 将新字段从XDP文件添加到自适应表单   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

任何稍后添加到原始XDP文件的字段都会显示在“表单层次结构”选项卡中，您可以将这些新字段拖到自适应表单中。

您无需单击错误消息中的链接，即可更新“表单层次结构”选项卡中的字段。

### 已删除XDP文件中的字段 {#deleted-fields-in-xdp-file}

如果从XDP文件中删除了之前复制到自适应表单的字段，则创作模式下会显示一条错误消息，指出XDP文件中不存在该字段。 在这种情况下，请手动从自适应表单中删除字段或清除 `bindRef` 属性。

以下步骤说明了本文所用示例中资产的使用流程：

1. 更新 `sample-form.xdp` 并删除NumericField1。
1. 上传 `sample-form.xdp` 文件 [!DNL AEM Forms] UI
1. 打开 `sample-xfa-af` 用于创作的自适应表单。 将显示以下错误消息：自适应表单的架构/表单模板已更新。 `Click Here` 以使用新版本重新构建基础。

1. 单击链接(标有“ `Click Here`”)。 将显示一条错误消息，指出XDP文件中不再存在该字段。

![删除XDP文件中的元素时出现错误](assets/no-element-xdp.png)

删除的字段还带有一个图标，用于指示字段中的错误。

![字段中的错误图标](assets/error-field.png)

>[!NOTE]
>
>自适应表单中绑定不正确（无效）的字段 `bindRef` 值)也会被视为已删除的字段。 如果作者未修复这些错误并发布自适应表单，则该字段将被视为正常的未绑定自适应表单字段，并包含在输出XML文件的未绑定部分中。

## 下载 {#downloads}

本文示例的内容包

[获取文件](assets/sample-xfa-af-sync-1.0.zip)
