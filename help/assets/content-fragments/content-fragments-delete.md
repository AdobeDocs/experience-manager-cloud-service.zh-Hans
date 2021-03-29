---
title: 内容片段 - 删除注意事项
description: 在AEM中定义内容片段删除策略之前，请查看这些重要注意事项。 内容片段是交付无标题内容的强大工具，删除这些内容的含义必须得到仔细考虑。
translation-type: tm+mt
source-git-commit: e7ca6dc841ba777384be74021a27d523d530a956
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 9%

---


# 内容片段 - 删除注意事项 {#content-fragments-delete-considerations}

在AEM中定义内容片段删除策略之前，请查看这些重要注意事项。 内容片段是交付无标题内容的强大工具，删除这些内容的含义必须得到仔细考虑。

## 权限 — 删除或不删除{#permissions-delete-or-not-delete}

删除内容的功能非常强大，但可能非常敏感，许多行业需要限制和控制这些权限的分配方式。

关于删除权限，内容片段必须考虑在两个级别：

1. **内容片段作为单个实体。**

   * **用例**:需要编辑/更新内容片段并删除整 **个片段的用户**。
   * **权限**:可以通过“用户”和/或“组管理”分配“删除”权限。  <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **组成内容片段的多个子实体；例如，variations， sub-nodes。**

   内容片段编辑器的基本操作要求可以删除这种临时子元素。 例如，当操作变量时；此外，在编辑元数据或管理关联的内容时也是如此。

   * **用例**:需要编辑/更新内容片段的用户，不 **允许删除整个片段**。
   * **权限**:请参 [阅仅编辑器功能所需的权限](#permissions-required-for-editor-functionality-only)。

>[!NOTE]
>
>当用户没有任何“删除”权限时，内容片段编辑器以&#x200B;*只读*&#x200B;模式运行。<!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>另请参见How to Audit User Management Operations in AEM。 <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## 仅编辑器功能所需的权限{#permissions-required-for-editor-functionality-only}

对于需要编辑／更新内容片段的用户， **不允许他们删除整个片段**，必须分配特定权限，因为内容片段编辑器的基本操作要求可以删除临时子元素。

例如，当操作变量时；此外，在编辑元数据或管理关联的内容时也是如此。

>[!NOTE]
>
>编辑/更新内容片段所需的删除权限包含在通过用户和/或组管理分配的“删除”权限中。<!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

编辑/更新片段所需的权限需要应用于包含内容片段的节点或相应的父节点（在`/content/dam`下的任何级别）。 当分配给此类父节点时，权限将应用于该分支中的所有节点。

例如，将包含所有内容片段的文件夹，例如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>也可以设置`/content/dam`的权限，因为所有内容片段都存储在此处。
>
>但是，此操作也会将相同的删除权限应用于&#x200B;*all*&#x200B;其他资产类型。

允许特定用户和/或组编辑/更新内容片段的先决条件是：

>[!NOTE]
>
>此列表显示所需的所有权限，而不仅仅是删除权限。

* 对于内容片段节点或文件夹：

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 对于所有内容片段的`jcr:content`节点：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 和  `jcr:removeChildNodes`

* 对于所有内容片段`jcr:content`下的所有节点：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 和 `jcr:removeChildNodes`,  `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
