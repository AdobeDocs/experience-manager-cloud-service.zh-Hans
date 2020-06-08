---
title: 内容片段 - 删除注意事项
description: 内容片段 - 删除注意事项
translation-type: tm+mt
source-git-commit: bb3d90def8855e8dffdc584c0805da120faf7b12
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 12%

---


# 内容片段 - 删除注意事项{#content-fragments-delete-considerations}

## 权限——删除或不删除 {#permissions-delete-or-not-delete}

删除内容的能力强大，但可能很敏感，许多行业需要限制和控制这些权限的分配方式。

关于删除权限，内容片段必须考虑在两个级别：

1. **内容片段作为单个实体。**

   * **用例**: 需要编辑／更新内容片段——并删 **除整个片段的用户**。
   * **权限**: 可以通过用户和／或组管理分配“删除”权限。 <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **构成内容片段的多个子实体； 例如，变量、子节点。**

   内容片段编辑器的基本操作要求可以删除此类临时子元素。 例如，在操作变量时； 编辑元数据或管理关联的内容时也是如此。

   * **用例**: 需要编辑／更新内容片段的用户， **不允许删除整个片段**。
   * **权限**: 请参 [阅仅编辑器功能所需的权限](#permissions-required-for-editor-functionality-only)。

>[!NOTE]
>
>When a user does not have any Delete permissions, the Content Fragment editor operates in *read-only* mode. <!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>另请参阅如何在AEM中审核用户管理操作。 <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## 仅编辑器功能所需的权限 {#permissions-required-for-editor-functionality-only}

对于需要编辑／更新内容片段的用户， **不允许他们删除整个片段**，必须分配特定权限，因为内容片段编辑器的基本操作要求可以删除临时子元素。

例如，在操作变量时； 编辑元数据或管理关联的内容时也是如此。

>[!NOTE]
>
>编辑／更新内容片段所需的删除权限包括在通过用户和／或组管理分配的“删除”权限中。 <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

编辑／更新片段所需的权限需要应用于包含内容片段的节点或相应的父节点(在下的任何级别 `/content/dam`)。 当分配给此类父节点时，该权限将应用于该分支中的所有节点。

例如，将包含所有内容片段的文件夹，如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>也可以设置 `/content/dam` 权限，因为此处存储了所有内容片段。
>
>但是，此操作也会对所有其他资 *产类型* 应用相同的删除权限。

允许特定用户和／或组编辑／更新内容片段的先决条件是：

>[!NOTE]
>
>此列表显示所需的所有权限，而不仅仅是删除权限。

* 对于内容片段节点或文件夹：

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* 对于所 `jcr:content`有内容片段的节点：

   * `jcr:addChildNodes`, `jcr:modifyProperties` and `jcr:removeChildNodes`

* 对于所有内容片段 `jcr:content` 下的所有节点：

   * `jcr:addChildNodes`, `jcr:modifyProperties` 和 `jcr:removeChildNodes``jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
