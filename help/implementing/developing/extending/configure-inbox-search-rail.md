---
title: 如何配置收件箱的搜索过滤器？
description: 了解如何为收件箱项目配置搜索过滤器。
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 1%

---

# 配置收件箱搜索过滤器 {#configure-search-filters-inbox}

您可以为收件箱项目配置搜索过滤器。 根据特定的收件箱列确定搜索条件以筛选结果。

例如，要根据“出生日期”收件箱列范围筛选收件箱项目，您可以使用日期范围谓词来定义日期范围。

以下是收件箱的可用谓词类型：

* 范围谓词

* 文本谓词

* 日期范围谓词

* 选项属性谓词

>[!NOTE]
>
>确保您是 `workflow-administrators` 组，用于配置收件箱的搜索过滤器。

## 创建或打开自定义配置 {#creating-opening-customized-configuration}

1. 导航到 **[!UICONTROL 工具]**， **[!UICONTROL 常规]**， **[!UICONTROL 搜索Forms]**.

1. 选择 **[!UICONTROL 收件箱搜索边栏]** 配置和点按 **[!UICONTROL 编辑]**.
1. 使用以下方式合并谓词配置更改 **[!UICONTROL 编辑搜索Forms]**.
1. 选择 **[!UICONTROL 完成]** 以保存配置。

## 删除自定义配置 {#delete-customized-configuration}

要删除自定义配置，请执行以下操作：

1. 导航到 **[!UICONTROL 工具]**， **[!UICONTROL 常规]**， **[!UICONTROL 搜索Forms]**.

1. 选择 **[!UICONTROL 收件箱搜索边栏]** 配置和点按 **[!UICONTROL 删除]**.

## 配置范围谓词 {#range-predicate}

您可以过滤收件箱项目，以使用范围谓词搜索收件箱列中的数字范围。 您还可以选择包含数字的小数值。

配置范围谓词：

1. 打开 [配置表单](#creating-opening-customized-configuration).
1. 点按 **[!UICONTROL 选择谓词]** 制表符并拖动 **[!UICONTROL 范围谓词]** 到窗体。
1. 在 **[!UICONTROL 设置]** 选项卡，从中选择作为搜索基础的收件箱列名称 **[!UICONTROL 列名称]** 字段。
1. 在中指定过滤器的标签 **[!UICONTROL 筛选标签]** 字段。 选择 **[!UICONTROL 启用小数值]** 此复选框用于在定义范围时接受数字的小数值。
1. 为配置指定可选描述，然后点击 **[!UICONTROL 完成]** 以保存它。

当您打开“过滤器”页面时，配置更改会反映出来。 您在步骤4中指定的过滤器标签显示为标签，并带有定义最大值和最小值的选项。 按Enter键时， [!DNL Experience Manager] 对步骤3中指定的列名称应用搜索条件并返回收件箱项目。

>[!NOTE]
>
>本文列出了最新的用户界面选项。 在即将发行的版本中，用户界面上的选项名称将更新。

## 配置文本谓词 {#text-predicate}

筛选收件箱项目，以使用文本谓词搜索收件箱列中的文本字符串。

配置文本谓词：

1. 打开 [配置表单](#creating-opening-customized-configuration).
1. 点按 **[!UICONTROL 选择谓词]** 制表符并拖动 **[!UICONTROL 文本谓词]** 到窗体。
1. 在 **[!UICONTROL 设置]** 选项卡，从中选择作为搜索基础的收件箱列名称 **[!UICONTROL 列名称]** 字段。
1. 指定在“搜索”文本框中作为占位符文本显示的文本。 **[!UICONTROL 搜索文本框占位符]** 字段。
1. 为配置指定可选描述，然后点击 **[!UICONTROL 完成]** 以保存它。

当您打开“过滤器”页面时，配置更改会反映出来。 按Enter键时， [!DNL Experience Manager] 将步骤4中指定的搜索文本应用于步骤3中指定的列名称，并返回收件箱项目。

## 配置日期范围谓词 {#date-range-predicate}

您可以过滤收件箱项目，以使用日期范围谓词在收件箱列中搜索日期范围。

要配置日期范围谓词，请执行以下操作：

1. 打开 [配置表单](#creating-opening-customized-configuration).
1. 点按 **[!UICONTROL 选择谓词]** 制表符并拖动 **[!UICONTROL 日期范围谓词]** 到窗体。
1. 在 **[!UICONTROL 设置]** 选项卡，从中选择作为搜索基础的收件箱列名称 **[!UICONTROL 列名称]** 字段。
1. 在中指定日期范围过滤器的标签 **[!UICONTROL 筛选标签]** 字段。
1. 指定筛选器的开始日期和结束日期标签。
1. 为配置指定可选描述，然后点击 **[!UICONTROL 完成]** 以保存它。

当您打开“过滤器”页面时，配置更改会反映出来。 您在步骤4中指定的过滤器标签显示为日期范围过滤器的标签，以及在步骤5中指定的开始日期和结束日期标签。 [!DNL Experience Manager] 对步骤3中指定的列名称应用搜索条件并返回收件箱项目。

## 配置自定义列选项谓词 {#custom-column-options-predicate}

您可以使用自定义列选项谓词来筛选收件箱项目，以搜索收件箱列中的自定义选项。

要配置自定义列选项谓词：

1. 打开 [配置表单](#creating-opening-customized-configuration).
1. 点按 **[!UICONTROL 选择谓词]** 制表符并拖动 **[!UICONTROL 自定义列选项谓词]** 到窗体。
1. 在 **[!UICONTROL 设置]** 选项卡，从中选择作为搜索基础的收件箱列名称 **[!UICONTROL 列名称]** 字段。
1. 在中指定自定义列选项过滤器的标签 **[!UICONTROL 筛选标签]** 字段。
1. 选择 **[!UICONTROL 单选]** 此复选框用于启用在收件箱列上应用过滤器时只选择一个选项。
1. 在 **[!UICONTROL 添加选项]** 部分：
   1. 选择 **[!UICONTROL 手动]** 以手动定义过滤器搜索选项。 点按 **[!UICONTROL 添加筛选器选项]** 以定义第一个选项。 为要搜索的列选项和选项值文本指定标签。 例如，如果要搜索 **女性** 作为“收件箱”列中的值，您可以指定 **F** 作为列选项的标签并添加 **女性** 作为选项值文本。 同样，您可以添加更多过滤器选项。
   1. 选择 **[!UICONTROL JSON路径]** 以使用JSON文件路径定义选项。 以下是定义过滤器选项的JSON文件示例：

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

   1. 选择 **[!UICONTROL CRX选项路径]** 以使用CRX存储库路径定义选项。 点按 **[!UICONTROL 添加选项路径]** 以添加多个路径。 以下是一个要定义的示例 `Male` 和 `Female` 筛选器选项：

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

1. 为配置指定可选描述，然后点击 **[!UICONTROL 完成]** 以保存它。

当您打开“过滤器”页面时，配置更改会反映出来。 您在步骤4中指定的过滤器标签显示为自定义列选项谓词的标签。 [!DNL Experience Manager] 将步骤6中定义的搜索条件应用于步骤3中指定的列名称，并返回收件箱项目。

以下视频说明了根据 `true` 和 `false` 选项值。

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## 查看基于谓词的搜索筛选器 {#view-search-filters-for-predicates}

您可以查看基于谓词的搜索过滤器。 选择 **[!UICONTROL 筛选条件]** 在收件箱页面上。 筛选器显示在左窗格中。 然后，您可以指定搜索条件以筛选收件箱项目。

![“过滤器”页面](assets/apply-filters.png)

有关管理谓词配置的更多信息，请参见 [配置搜索Forms](search-forms.md).
