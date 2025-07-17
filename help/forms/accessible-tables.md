---
title: 在HTML5表单中创建可访问的复杂表
description: 了解如何在HTML5表单中创建无障碍的表。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: HTML5 Forms,Mobile Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 在HTML5表单中创建可访问的复杂表 {#create-accessible-complex-tables-in-html-forms}

<span class="preview"> HTML5 Forms功能作为提前访问计划的一部分提供。 要请求访问，请将您的官方（工作）电子邮件ID通过电子邮件发送到aem-forms-ea@adobe.com。
</span>

HTML5 Forms中表的默认实施使用HTML DIV元素来呈现表。 渲染包括使用ARIA角色来满足辅助功能要求。

为避免屏幕阅读器出现辅助功能问题（该屏幕阅读器不完全支持与数据表一起使用的ARIA角色），HTML5 Forms为表提供了替代演绎版。 这些表基于Designer中引入的新表格式，该格式还支持：

* 行标题
* 行跨度

要在HTML5 Forms中使用新格式，请将表标记为复杂表。 要将表标记为复杂，请在表子表单的XML源中添加`extras`标记，如下所示：

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

标记为&#x200B;*complexTable*&#x200B;的表遵循本机HTML演绎版，并为某些屏幕阅读器提供更好的辅助功能支持。  要创建行范围，请选择同一列中表的连续单元格，右键单击选定内容，然后单击&#x200B;**[!UICONTROL 合并单元格]**。

>[!NOTE]
>
>创建行范围仅适用于最左侧的单元格。

要将行标记为行标题，请选择行中的所有单元格，右键单击选定内容，然后单击&#x200B;**[!UICONTROL 标记标题]**。

要将单元格标记为列标题，请选择列中的任意单元格，右键单击选定内容，然后单击&#x200B;**[!UICONTROL 标记标题]**。

新&#x200B;*AccessibleTable*&#x200B;格式的限制：

* 如果在表中使用rowspan，则不支持可增长的字段
* 不支持嵌套表（表单元格中的表）
* 仅对标题行和标题单元格支持rowspan
* 仅支持常规表
* 不支持在rowspan > 1的表中进行数据预填充
