---
title: 如何为收件箱配置搜索过滤器？
description: 了解如何为收件箱项目配置搜索过滤器。
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 1%

---

# 配置收件箱搜索过滤器 {#configure-search-filters-inbox}

您可以为收件箱项目配置搜索过滤器。 将搜索条件基于特定的收件箱列以筛选结果。

例如，要根据“出生日期收件箱”列范围过滤收件箱项目，可以使用“日期范围”谓词定义日期范围。

以下是收件箱的可用谓词类型：

* 范围谓词

* 文本谓词

* 日期范围谓词

* 选项属性谓词

>[!NOTE]
>
>确保您是 `workflow-administrators` 群组来配置收件箱的搜索过滤器。

## 创建或打开自定义配置 {#creating-opening-customized-configuration}

1. 导航到 **[!UICONTROL 工具]**, **[!UICONTROL 常规]**, **[!UICONTROL 搜索Forms]**.

1. 选择 **[!UICONTROL 收件箱搜索边栏]** 配置和点按 **[!UICONTROL 编辑]**.
1. 使用合并谓词配置更改 **[!UICONTROL 编辑搜索Forms]**.
1. 选择 **[!UICONTROL 完成]** 以保存配置。

## 删除自定义配置 {#delete-customized-configuration}

要删除自定义配置，请执行以下操作：

1. 导航到 **[!UICONTROL 工具]**, **[!UICONTROL 常规]**, **[!UICONTROL 搜索Forms]**.

1. 选择 **[!UICONTROL 收件箱搜索边栏]** 配置和点按 **[!UICONTROL 删除]**.

## 配置范围谓词 {#range-predicate}

您可以过滤收件箱项目，以使用范围谓词在收件箱列中搜索数字范围。 您还可以选择包含数字的小数值。

要配置范围谓词，请执行以下操作：

1. 打开 [配置表单](#creating-opening-customized-configuration).
1. 点按 **[!UICONTROL 选择谓词]** 选项卡和拖动 **[!UICONTROL 范围谓词]** 到表单。
1. 在 **[!UICONTROL 设置]** ，选择收件箱列名称以进行搜索，从 **[!UICONTROL 列名称]** 字段。
1. 在 **[!UICONTROL 过滤器标签]** 字段。 选择 **[!UICONTROL 启用小数值]** 复选框以在定义范围时接受数字的小数值。
1. 为配置指定可选描述并点按 **[!UICONTROL 完成]** 来保存它。

配置更改将在您打开“过滤器”页面时反映出来。 您在步骤4中指定的过滤器标签将显示为标签，并带有用于定义最大值和最小值的选项。 按Enter键时， [!DNL Experience Manager] 对步骤3中指定的列名称应用搜索条件，并返回收件箱项目。

>[!NOTE]
>
>文章列出了最新的用户界面选项。 在即将发布的版本中，用户界面上的选项名称将进行更新。

## 配置文本谓词 {#text-predicate}

过滤收件箱项目，以使用“文本谓词”在收件箱列中搜索文本字符串。

要配置文本谓词，请执行以下操作：

1. 打开 [配置表单](#creating-opening-customized-configuration).
1. 点按 **[!UICONTROL 选择谓词]** 选项卡和拖动 **[!UICONTROL 文本谓词]** 到表单。
1. 在 **[!UICONTROL 设置]** ，选择收件箱列名称以进行搜索，从 **[!UICONTROL 列名称]** 字段。
1. 指定在“搜索”文本框中显示的文本作为 **[!UICONTROL 搜索文本框占位符]** 字段。
1. 为配置指定可选描述并点按 **[!UICONTROL 完成]** 来保存它。

配置更改将在您打开“过滤器”页面时反映出来。 按Enter键时， [!DNL Experience Manager] 对步骤3中指定的列名称应用步骤4中指定的搜索文本，并返回收件箱项目。

## 配置日期范围谓词 {#date-range-predicate}

您可以使用“日期范围谓词”筛选收件箱项目，以在“收件箱”列中搜索日期范围。

要配置日期范围谓词，请执行以下操作：

1. 打开 [配置表单](#creating-opening-customized-configuration).
1. 点按 **[!UICONTROL 选择谓词]** 选项卡和拖动 **[!UICONTROL 日期范围谓词]** 到表单。
1. 在 **[!UICONTROL 设置]** ，选择收件箱列名称以进行搜索，从 **[!UICONTROL 列名称]** 字段。
1. 在 **[!UICONTROL 过滤器标签]** 字段。
1. 为过滤器指定开始日期和结束日期标签。
1. 为配置指定可选描述并点按 **[!UICONTROL 完成]** 来保存它。

配置更改将在您打开“过滤器”页面时反映出来。 您在步骤4中指定的过滤器标签将作为日期范围过滤器的标签以及在步骤5中指定的开始日期和结束日期标签一起显示。 [!DNL Experience Manager] 对步骤3中指定的列名称应用搜索条件，并返回收件箱项目。

## 配置自定义列选项谓词 {#custom-column-options-predicate}

您可以使用“自定义列选项”谓词，筛选收件箱项目以在“收件箱”列中搜索自定义选项。

要配置“自定义列选项”谓词，请执行以下操作：

1. 打开 [配置表单](#creating-opening-customized-configuration).
1. 点按 **[!UICONTROL 选择谓词]** 选项卡和拖动 **[!UICONTROL 自定义列选项谓词]** 到表单。
1. 在 **[!UICONTROL 设置]** ，选择收件箱列名称以进行搜索，从 **[!UICONTROL 列名称]** 字段。
1. 在 **[!UICONTROL 过滤器标签]** 字段。
1. 选择 **[!UICONTROL 单选]** 复选框，以便在“收件箱”列上应用过滤器时只能选择一个选项。
1. 在 **[!UICONTROL 添加选项]** 部分：
   1. 选择 **[!UICONTROL 手动]** 以手动定义过滤器搜索选项。 点按 **[!UICONTROL 添加过滤器选项]** 来定义第一个选项。 指定列选项的标签和要搜索的选项值文本。 例如，如果您想要搜索 **女** 作为收件箱列中的值，您可以指定 **F** 作为列选项的标签并添加 **女** 作为选项值文本。 同样，您也可以添加更多过滤器选项。
   1. 选择 **[!UICONTROL JSON路径]** 用于使用JSON文件路径定义选项。 以下是用于定义过滤器选项的JSON文件示例：

      ```JSON
          {
         "options":[
            {
            "text":"Female",
            "value":"F"
            },
            {
            "text":"Male",
            "value":"M"
            }
          ]
        }
      ```

   1. 选择 **[!UICONTROL CRX选项路径]** 用于使用CRX存储库路径定义选项。 点按 **[!UICONTROL 添加选项路径]** 添加多个路径。 以下是定义示例 `Male` 和 `Female` 过滤器选项：

      ```JSON
         <gender jcr:primaryType="sling:OrderedFolder">
                        <male
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Male"
                            value="M"/>
                        <female
                            jcr:primaryType="nt:unstructured"
                            jcr:title="Female"
                            value="F"/>
                    </gender>
      ```

1. 为配置指定可选描述并点按 **[!UICONTROL 完成]** 来保存它。

配置更改将在您打开“过滤器”页面时反映出来。 您在步骤4中指定的过滤器标签将显示为“自定义列选项谓词”的标签。 [!DNL Experience Manager] 对步骤3中指定的列名称应用步骤6中定义的搜索条件，并返回收件箱项目。

以下视频演示了根据 `true` 和 `false` 选项值。

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## 查看基于谓词的搜索过滤器 {#view-search-filters-for-predicates}

您可以根据谓词查看搜索过滤器。 选择 **[!UICONTROL 过滤器]** 的问题。 过滤器显示在左窗格中。 然后，您可以指定搜索条件以过滤收件箱项目。

![过滤器页面](assets/apply-filters.png)

有关管理谓词配置的更多信息，请参阅 [配置搜索Forms](search-forms.md).
