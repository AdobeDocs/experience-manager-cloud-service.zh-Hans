---
title: 国际化 UI 字符串
description: AEM提供了一个控制台，用于管理组件UI中使用的文本的各种翻译。
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 14a6516872f842d099b902b9f633b1d6f984266d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# 使用Translator管理词典{#using-translator-to-manage-dictionaries}

AEM提供了一个控制台，用于管理组件UI中使用的文本的各种翻译。 此控制台位于：

`https://<hostname>:<port-number>/libs/cq/i18n/gui/translator.html`

使用翻译工具管理英语字符串及其翻译。 词典在存储库中创建，例如`/apps/myproject/i18n`。

您管理的翻译工具及词典用于以不同语言呈现组件UI。 如果要翻译页面，请参阅[翻译多语言站点的内容](/help/sites-cloud/administering/translation/overview.md)。

## 创建词典 {#creating-a-dictionary}

开发人员可以在AEM中创建i18n词典，以管理本地化的组件字符串。 字典通常是`/apps`中组件代码的一部分。 以下是AEM WKND代码中的一个示例，该示例具有一个在所有WKND组件中使用的键/值对。

```
{
  "&copy; {0} WKND Site Site. All rights reserved." : "&copy; {0} WKND Site Site. Tous droits réservés."
}
```

开发人员可以通过为新字典添加根节点(`sling:Folder`)来创建其他字典，以保存组件字符串的语言定义。

```shell
/apps/myProject/i18n [sling:Folder]
    - de.json [nt:file] [mix:language]
        + jcr:language = de
    - fr.json [nt:file] [mix:language]
        + jcr:language = fr
```

>[!NOTE]
>
>这是[Sling i18n模块](https://sling.apache.org/site/internationalization-support.html)中的结构。

在AEM GitHub存储库中创建词典后，可通过AEM [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)部署词典。

## 字典位置 {#dictionary-locations}

开发人员可以在`/apps`或`/content/cq:i18n`中创建源语言词典。 从AEM原型示例代码开始，初始字典通常位于`/apps`路径中。 如果目标是将相应的字典语言副本也存储在`/apps`中，则必须由开发人员在组件代码中手动创建和维护这些语言副本。

或者，i18n词典的新AEM运行时翻译过程将在`/content/cq:i18n/<projectName>`中创建已翻译词典，无论源词典是否存储在`/apps`或`/content`中。

在哪里查找i18n词典、源和语言副本时，应使用以下标准做出决定：

* `/apps`
   * 带有组件字符串翻译的词典的默认位置，遵循AEM原型和WKND示例代码
   * 每个Sling的最高渲染顺序（[资源捆绑搜索层次结构](https://sling.apache.org/documentation/bundles/internationalization-support-i18n.html#resourcebundle-hierarchies)）
   * 但不可能在运行时编辑或翻译词典，因为`/apps`在AEM as a Cloud Service环境中不可更改

* `/content/cq:i18n`
   * i18n词典的替代位置，如果
      * 需要词典的运行时翻译
      * 运行时编辑字典的功能是必需的
   * 运行时词典翻译将创建语言副本的默认位置。

由于`/apps`在Sling呈现顺序中始终取代`/content`，因此请务必记住，`/apps`和`/content/cq:i18n`中不能同时存在具有相同键/值对的词典，因为`/content/cq:i18n`中的词典将永远不会用于呈现。 如果`/apps`中已存在字典语言副本（即翻译目标），并且目标是使其在AEM as a Cloud Service中的运行时可翻译，则`/apps`中的原始字典语言副本必须移动到`/content/cq:i18n`，或者在`/apps`中删除，并通过翻译源字典在`/content/cq:i18n`中自动重新创建。 此翻译过程将在`/content/cq:i18n`中自动创建语言副本。

## 自动词典创建 {#automatic-creation}

对于包含AEM核心组件的AEM页面和体验片段，新的词典翻译流程还将扫描这些页面或体验片段，以查找应翻译的组件和组件字符串。 然后，系统将在`/content/cq:i18n`中自动创建相应的新词典语言副本。 这不适用于内容片段，因为这些是未使用AEM核心组件的纯结构化内容。

## 导出词典 {#exporting-a-dictionary}

虽然在AEM as a Cloud Service中无法对`/apps`或`/libs`位置中的i18n词典进行运行时翻译，因为这些位置不可变，但仍可在运行时导出这些词典，以便在AEM外部进行异步翻译。

要将词典的源语言字符串导出到XLIFF文件，请执行以下操作：

1. 打开翻译工具`http://<host>:<port>/libs/cq/i18n/gui/translator.html`

   >[!NOTE]
   >
   >该工具只能通过此URL使用，无法从AEM产品UI访问该工具。

1. 使用词典下拉菜单选择要导出的词典。
1. 单击“导出XLIFF翻译”，然后单击“导出完整的`<locale>` xliff”。

## 导入词典 {#importing-a-dictionary}

要将XLIFF文件导入词典以填充词典内容，请执行以下操作：

1. 打开翻译工具`http://<host>:<port>/libs/cq/i18n/gui/translator.html`
1. 单击导入，然后单击XLIFF翻译。
1. 选择要导入的文件，然后单击“确定”。
