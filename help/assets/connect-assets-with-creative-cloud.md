---
title: 将 AEM Assets 连接到 Creative Cloud
description: 了解如何配置 AEM Assets 并将其连接到 Creative Cloud。连接到已设置到其他IMS组织的Creative Cloud权利，以轻松地使用AEM Assets中的最新Creative Cloud集成，包括Express和Creative Cloud Libraries。
exl-id: 880200fe-94b3-49de-802c-34283f7c71bc
feature: Collaboration
role: User
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 70%

---

# 将 AEM Assets 连接到 Creative Cloud  {#cross-org-entitlements}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

Experience Manager Assets能够连接到已设置到其他IMS组织的Creative Cloud权利，以轻松地使用AEM Assets中的最新Creative Cloud集成，包括Express和Creative Cloud Libraries。

如果您的 Creative Cloud 产品和 AEM Assets 预配给单独的 IMS 组织，则您可连接到其他 Creative Cloud 组织，以便可在这两个解决方案之间执行集成的工作流程。

## 前提条件 {#prerequisites}

* 具有 Experience Manager Assets 的管理员权限

* 在 Creative Cloud 和 Experience Manager 中使用的同一用户 ID 具有对 Creative Cloud 的有效权利。对具有相同电子邮件地址的个人 ID 和 Federated ID 的权利被视为不同的用户 ID。

## 连接到新的 Creative Cloud 组织 {#connect-to-creative-cloud-org}

要连接到新的 Creative Cloud 组织，请执行以下步骤：

1. 导航到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL Creative Cloud]**。

1. 使用&#x200B;**[!UICONTROL 选择新的 Creative Cloud 组织 ID]** 下拉列表选择新的 Creative Cloud 组织。该列表显示所有您有权访问其的组织。选择具有有效 Creative Cloud 权利的组织。

1. 单击&#x200B;**[!UICONTROL 切换组织]**&#x200B;以切换到该新组织。

   ![跨组织权利](assets/cross-org-entitlements.png)

## 限制 {#limitations}

* 您一次可以将 AEM Assets 连接到一个 Creative Cloud 组织。不支持一次连接到多个 Creative Cloud 组织。

* 您在 AEM Assets 中连接到的 Creative Cloud 组织适用于您组织内的所有用户。
