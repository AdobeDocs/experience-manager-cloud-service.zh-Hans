---
title: 中的占位符文本 [!DNL AEM Forms]
description: 占位符文本旨在在控件没有值时帮助用户输入数据。 它可以是示例值或预期格式的简要说明。
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 中的占位符文本 [!DNL AEM Forms] {#placeholder-text-in-aem-forms}

占位符文本表示一个单词或短短语。 它旨在在控件没有值时帮助用户输入数据。 占位符文本可以是示例值或预期格式的简要说明。 占位符文本在用户输入值之前显示，在用户输入或选择值时，会将其删除。

>[!NOTE]
>
>如果指定占位符文本，则其值必须不包含任何新行字符。

![包含和不包含占位符文本的日期组件](assets/dat-picker-place-holder-text.png)

**A.** 包含占位符文本的日期组件 **B.** 不带占位符文本的日期组件

[!DNL AEM Forms] “密码”框、“日期选取器”、“数字”框和文本框字段的支持占位符文本。\
本机HTML5日期小组件不支持占位符文本。 要指定占位符文本，请执行以下操作：

1. 右键单击支持占位符文本的组件，然后单击 **编辑**. 此时将出现“编辑组件”对话框。

1. 打开 **标题和文本** 选项卡。
1. 在 **占位符文本框**. 单击&#x200B;**确定**。

>[!NOTE]
>
>不支持占位符文本 [!DNL Microsoft Internet Explorer 9].

