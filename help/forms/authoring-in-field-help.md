---
title: 如何为AEM自适应Forms字段添加帮助文本？
description: AEM Forms允许您将上下文帮助作为文本或富媒体（包括视频）添加到自适应表单字段和面板。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
role: User
hide: true
hidefromtoc: true
source-git-commit: d661f869f1264e4a2317692ab6fd22263c89e072
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---


# 为表单字段创作上下文帮助{#authoring-in-context-help-for-form-fields}

## 简介 {#introduction}

在某些情况下，最终用户填写表单时不确定如何在特定表单字段中填写详细信息。 为了解决此类问题，自适应Forms支持向表单字段添加文本或富上下文帮助。 它有助于改善表单填写体验并避免最终用户出现任何歧义。

本文介绍了表单作者如何在创作自适应Forms时添加上下文帮助。

## 添加上下文帮助 {#add-in-context-help}

您可以使用侧边栏中“属性”选项卡的“帮助内容”部分中的以下选项指定上下文帮助。

* [简短描述](authoring-in-field-help.md#p-short-description-p)
* [详细描述](authoring-in-field-help.md#p-long-description-p)

![表单字段的上下文帮助](assets/descriptions.png)

>[!NOTE]
>
>长描述将覆盖短描述。 如果同时指定了两者，则只显示详细描述。

### 简短描述 {#short-description}

简短描述字段用于提供有关填写表单字段的快速和简短提示。 将鼠标悬停在简短描述字段中时，该字段中指定的文本将显示为工具提示。

![为表单字段添加上下文帮助的简短说明](assets/tooltip.png)

>[!NOTE]
>
>选择&#x200B;**始终显示简短描述**&#x200B;以永久显示字段下的帮助文本。

![字段下的永久短上下文帮助](assets/short1.png)

### 详细描述 {#long-description}

您可以使用详细描述字段指定长文本或嵌入富媒体内容（包括视频）作为上下文帮助。 例如，下图显示了如何将视频作为上下文帮助进行嵌入。

![添加富媒体作为表单字段的上下文帮助](assets/long-descriptions.png)

添加完整描述是否显示&#x200B;**？字段旁边的**&#x200B;图标。 单击此图标将显示在详细描述部分中添加的内容。

![富媒体上下文帮助示例](assets/photoshop.png)

### 面板级帮助 {#panel-level-help}

除了表单字段的上下文帮助之外，您还可以在面板编辑对话框的“帮助内容”选项卡中指定面板级别的帮助。

![添加表单面板的上下文帮助](assets/panel-level-help.png)

添加面板的帮助是否显示&#x200B;**？面板描述旁边的**&#x200B;图标。 单击图标将显示在面板编辑对话框的“帮助内容”部分中添加的内容。

![表单面板级别](assets/photoshop-1.png)的上下文帮助示例