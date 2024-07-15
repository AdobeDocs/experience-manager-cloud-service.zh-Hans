---
title: 内容片段 – 关于删除的注意事项
description: 在 AEM 中定义内容片段删除策略之前，请查看这些重要注意事项。内容片段是用于投放 headless 内容的强大工具，必须仔细考虑删除这些片段的影响。
feature: Content Fragments
role: User, Developer, Architect
exl-id: d1726bff-3aa8-4758-bee7-0cacea1f660a
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 92%

---

# 关于删除内容片段的注意事项 {#delete-considerations-content-fragments}

在 AEM 中定义用于删除内容片段的策略之前，请查看这些重要的注意事项。内容片段是用于投放 headless 内容的强大工具，必须仔细考虑删除这些片段的影响。

## 权限 – 删除或不删除 {#permissions-delete-or-not-delete}

删除内容的功能非常强大，但可能很敏感，许多行业都需要限制和控制这些权限的分配方式。

关于删除权限，内容片段必须考虑在两个级别：

1. **内容片段作为单个实体。**

   * **用例**：必须编辑/更新内容片段的用户 — **并删除整个片段**。
   * **权限**：可通过“用户”和/或“组管理”分配“删除”权限。

2. **构成内容片段的多个子实体；例如，变体、子节点。**

   内容片段编辑器的基本操作要求可以删除此类临时子元素。例如，在处理变量时；在编辑元数据或管理关联的内容时，也可以。

   * **用例**：必须编辑/更新内容片段的用户 — **不允许删除整个片段**。
   * **权限**：请参阅[仅编辑器功能需要的权限](#permissions-required-for-editor-functionality-only)。

>[!NOTE]
>
>另请参阅“如何在 AEM 中审核用户管理操作”。

## 仅编辑器功能需要的权限 {#permissions-required-for-editor-functionality-only}

必须为需要编辑／更新内容片段但&#x200B;**不允许删除整个片段**&#x200B;的用户分配特定权限，因为内容片段编辑器的基本操作要求可删除临时的子元素。

例如，在处理变量时；在编辑元数据或管理关联的内容时，也可以。

>[!NOTE]
>
>在通过“用户”和/或“组管理”分配的“删除”权限中包括编辑/更新内容片段所需的删除权限。

编辑/更新片段所需的权限必须应用于包含内容片段的节点或适当的父节点（在 `/content/dam` 下的任何级别）。将权限分配给此类父节点时，权限将应用于该分支中的所有节点。

例如，容纳所有内容片段的文件夹，如：

* `/content/dam/contentfragments`

>[!CAUTION]
>
>还可在 `/content/dam` 上设置权限，因为所有内容片段都存储在此处。
>
>但是，此操作将相同的删除权限还应用于&#x200B;*所有*&#x200B;其他资源类型。

允许特定用户和/或组编辑/更新内容片段的前提权限为：

>[!NOTE]
>
>此列表显示所需的所有权限，而不只是删除权限。

* 对于内容片段节点或文件夹：

   * `jcr:addChildNodes`、`jcr:modifyProperties`

* 对于 `jcr:content`所有内容片段的节点：

   * `jcr:addChildNodes`、`jcr:modifyProperties` 和 `jcr:removeChildNodes`

* 对于所有内容片段的 `jcr:content` 下的所有节点：

   * `jcr:addChildNodes`、`jcr:modifyProperties`、`jcr:removeChildNodes` 和 `jcr:removeNode`
