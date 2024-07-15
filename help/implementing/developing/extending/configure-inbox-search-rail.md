---
title: 如何配置收件箱的搜索过滤器？
description: 了解如何为收件箱项目配置搜索过滤器。
exl-id: 0e82d7ad-7a82-4d67-8eb8-9af6936652d8
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 1%

---

# 配置收件箱搜索过滤器 {#configure-search-filters-inbox}

您可以配置收件箱项目的搜索过滤器。 根据特定收件箱列筛选结果的搜索条件。

例如，要根据出生日期收件箱列范围筛选收件箱项目，您可以使用日期范围谓词来定义日期范围。

以下是“收件箱”的可用谓词类型：

* 范围谓词

* 文本谓词

* 日期范围谓词

* 选项属性谓词

>[!NOTE]
>
>确保您是`workflow-administrators`组的成员，以便配置收件箱的搜索过滤器。

## 创建或打开自定义配置 {#creating-opening-customized-configuration}

1. 导航到&#x200B;**[!UICONTROL 工具]**、**[!UICONTROL 常规]**、**[!UICONTROL 搜索Forms]**。

1. 选择&#x200B;**[!UICONTROL 收件箱搜索边栏]**&#x200B;配置并选择&#x200B;**[!UICONTROL 编辑]**。
1. 使用&#x200B;**[!UICONTROL 编辑搜索Forms]**&#x200B;合并谓词配置更改。
1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存配置。

## 删除自定义配置 {#delete-customized-configuration}

要删除自定义配置，请执行以下操作：

1. 导航到&#x200B;**[!UICONTROL 工具]**、**[!UICONTROL 常规]**、**[!UICONTROL 搜索Forms]**。

1. 选择&#x200B;**[!UICONTROL 收件箱搜索边栏]**&#x200B;配置并选择&#x200B;**[!UICONTROL 删除]**。

## 配置范围谓词 {#range-predicate}

您可以过滤收件箱项目，以使用“范围谓词”在收件箱列中搜索数字范围。 您还可以选择包含数字的小数值。

配置范围谓词：

1. 打开配置](#creating-opening-customized-configuration)的[表单。
1. 选择&#x200B;**[!UICONTROL 选择谓词]**&#x200B;选项卡并将&#x200B;**[!UICONTROL 范围谓词]**&#x200B;拖到表单中。
1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，从&#x200B;**[!UICONTROL 列名称]**&#x200B;字段中选择作为搜索依据的收件箱列名称。
1. 在&#x200B;**[!UICONTROL 筛选器标签]**&#x200B;字段中指定筛选器的标签。 选中&#x200B;**[!UICONTROL 启用小数值]**&#x200B;复选框以在定义范围时接受数字的小数值。
1. 为配置指定可选描述，然后选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存配置。

当您打开“过滤器”页面时，会反映配置更改。 您在步骤4中指定的过滤器标签显示为标签，并带有定义最大值和最小值的选项。 按Enter键时，[!DNL Experience Manager]将搜索条件应用于步骤3中指定的列名并返回收件箱项目。

>[!NOTE]
>
>本文列出了最新的用户界面选项。 在即将发行的版本中，用户界面上的选项名称将更新。

## 配置文本谓词 {#text-predicate}

筛选收件箱项目，以使用文本谓词在收件箱列中搜索文本字符串。

配置文本谓词：

1. 打开配置](#creating-opening-customized-configuration)的[表单。
1. 选择&#x200B;**[!UICONTROL 选择谓词]**&#x200B;选项卡并将&#x200B;**[!UICONTROL 文本谓词]**&#x200B;拖到表单中。
1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，从&#x200B;**[!UICONTROL 列名称]**&#x200B;字段中选择作为搜索依据的收件箱列名称。
1. 在&#x200B;**[!UICONTROL 搜索文本框占位符]**&#x200B;字段中指定在搜索文本框中作为占位符文本显示的文本。
1. 为配置指定可选描述，然后选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存配置。

当您打开“过滤器”页面时，会反映配置更改。 按Enter键时，[!DNL Experience Manager]将步骤4中指定的搜索文本应用于步骤3中指定的列名并返回收件箱项目。

## 配置日期范围谓词 {#date-range-predicate}

您可以过滤收件箱项目，以使用日期范围谓词在收件箱列中搜索日期范围。

要配置日期范围谓词，请执行以下操作：

1. 打开配置](#creating-opening-customized-configuration)的[表单。
1. 选择&#x200B;**[!UICONTROL 选择谓词]**&#x200B;选项卡并将&#x200B;**[!UICONTROL 日期范围谓词]**&#x200B;拖到表单中。
1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，从&#x200B;**[!UICONTROL 列名称]**&#x200B;字段中选择作为搜索依据的收件箱列名称。
1. 在&#x200B;**[!UICONTROL 筛选器标签]**&#x200B;字段中指定日期范围筛选器的标签。
1. 指定过滤器的开始日期和结束日期标签。
1. 为配置指定可选描述，然后选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存配置。

当您打开“过滤器”页面时，会反映配置更改。 您在步骤4中指定的过滤器标签显示为日期范围过滤器的标签，以及在步骤5中指定的开始日期和结束日期标签。 [!DNL Experience Manager]将搜索条件应用于步骤3中指定的列名称并返回收件箱项目。

## 配置自定义列选项谓词 {#custom-column-options-predicate}

您可以使用自定义列选项谓词筛选收件箱项目以搜索收件箱列中的自定义选项。

要配置自定义列选项谓词：

1. 打开配置](#creating-opening-customized-configuration)的[表单。
1. 选择&#x200B;**[!UICONTROL 选择谓词]**&#x200B;选项卡并将&#x200B;**[!UICONTROL 自定义列选项谓词]**&#x200B;拖到表单中。
1. 在&#x200B;**[!UICONTROL 设置]**&#x200B;选项卡中，从&#x200B;**[!UICONTROL 列名称]**&#x200B;字段中选择作为搜索依据的收件箱列名称。
1. 在&#x200B;**[!UICONTROL 筛选器标签]**&#x200B;字段中指定自定义列选项筛选器的标签。
1. 选中&#x200B;**[!UICONTROL 单选]**&#x200B;复选框以在对“收件箱”列应用筛选器时仅启用一个选项选择。
1. 在&#x200B;**[!UICONTROL 添加选项]**&#x200B;部分中：
   1. 选择&#x200B;**[!UICONTROL 手动]**&#x200B;以手动定义筛选器搜索选项。 选择&#x200B;**[!UICONTROL 添加筛选器选项]**&#x200B;以定义第一个选项。 为要搜索的列选项和选项值文本指定标签。 例如，如果要在“收件箱”列中搜索&#x200B;**Female**&#x200B;作为值，可以指定&#x200B;**F**&#x200B;作为列选项的标签，并添加&#x200B;**Female**&#x200B;作为选项值文本。 同样，您可以添加更多过滤器选项。
   1. 选择&#x200B;**[!UICONTROL JSON路径]**&#x200B;以使用JSON文件路径定义选项。 以下是定义过滤器选项的示例JSON文件：

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

   1. 选择&#x200B;**[!UICONTROL CRX选项路径]**&#x200B;以使用CRX存储库路径定义选项。 选择&#x200B;**[!UICONTROL 添加选项路径]**&#x200B;以添加多个路径。 以下是定义`Male`和`Female`筛选器选项的示例：

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

1. 为配置指定可选描述，然后选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存配置。

当您打开“过滤器”页面时，会反映配置更改。 您在步骤4中指定的过滤器标签将显示为自定义列选项谓词的标签。 [!DNL Experience Manager]将步骤6中定义的搜索条件应用于步骤3中指定的列名称，并返回收件箱项目。

以下视频说明了根据`true`和`false`选项值筛选列的步骤。

>[!VIDEO](https://video.tv.adobe.com/v/335679)

## 查看基于谓词的搜索筛选器 {#view-search-filters-for-predicates}

您可以查看基于谓词的搜索筛选器。 在收件箱页面上选择&#x200B;**[!UICONTROL 筛选器]**。 筛选器显示在左窗格中。 然后，您可以指定搜索条件以筛选收件箱项目。

![筛选器页面](assets/apply-filters.png)

有关管理谓词配置的更多信息，请参阅[配置搜索Forms](search-forms.md)。
