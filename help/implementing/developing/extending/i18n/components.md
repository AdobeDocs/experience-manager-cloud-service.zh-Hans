---
title: 国际化组件
description: 将组件和对话框国际化，以便它们的UI字符串能够以不同的语言显示
topic-tags: components
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 0276b310-b9a9-44b6-b295-06c51ef17208
source-git-commit: 401685af02c720994d72cd95d36f0cfcdf15d198
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# 国际化组件{#internationalizing-components}

将组件和对话框国际化，以便它们的UI字符串能够以不同的语言显示。 通过为国际化而设计的组件，可以将UI字符串外部化、翻译然后导入存储库。 在运行时，用户的语言首选项或页面区域设置决定了UI中显示的语言。

![i18n-components-1.png](/help/implementing/developing/extending/assets/i18n-comp1.png)

请使用以下流程将组件国际化，并提供不同语言的UI：

1. [使用国际化字符串的代码实施组件。](/help/implementing/developing/extending/i18n/dev.md)您的代码标识要翻译的字符串，并选择要在运行时呈现的语言。
1. [创建词典](/help/implementing/developing/extending/i18n/translator.md#creating-a-dictionary)。
1. [将字典导出](/help/implementing/developing/extending/i18n/translator.md#exporting-a-dictionary)为XLIFF格式，翻译字符串，然后将XLIFF文件导入回AEM。
1. 将字典合并到应用程序的发布管理流程中。

>[!NOTE]
>
>这里介绍的用于国际化组件的方法用于翻译静态字符串。 当需要更改组件字符串时，您应使用传统的翻译工作流。 例如，当作者可以使用组件的“编辑”对话框中的属性编辑UI字符串时，不应使用语言词典对该字符串进行国际化。

## 语言词典 {#language-dictionaries}

AEM国际化框架使用存储库中的词典存储英语字符串及其翻译的其他语言。 该框架使用英语作为默认语言。 字符串使用它们的英文版本进行标识。 通常，国际化框架使用字母数字ID作为UI字符串。 将字符串的英文版本用作ID具有以下几个优势：

* 代码易于阅读。
* 默认语言始终可用。

[翻译工具](/help/implementing/developing/extending/i18n/translator.md)允许您从一个中心位置管理所有字典。

![i18n-components-2](/help/implementing/developing/extending/assets/i18n-comp2.png)

翻译更改需要通过AEM as a Cloud Service中的[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)从Git进行。

### 在系统词典中覆盖字符串 {#overlaying-strings-in-system-dictionaries}

如果您的组件使用AEM系统词典中包含的字符串，请将该字符串复制到您自己的词典中。 所有组件都将使用词典中的字符串。

请注意，无法预测在全部位于`/apps`节点下的词典中复制字符串时使用的翻译。
