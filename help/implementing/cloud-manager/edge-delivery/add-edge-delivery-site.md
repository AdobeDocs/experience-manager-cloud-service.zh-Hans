---
title: 将 Edge Delivery Site 添加到 Cloud Manager
description: 了解如何将 Edge Delivery Site 添加到您的生产程序或沙盒程序。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 17e842c9-599a-4877-9834-1e7220f508a8
source-git-commit: 7c990e7e42477120c7ce0720bdb6dc7d03308f92
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 95%

---

# 将 Edge Delivery Site 添加到 Cloud Manager {#adding}

>[!IMPORTANT]
>
>了解为什么必须将 Edge Delivery Services Site 加入到 Cloud Manager。
>请参阅[使用 Adobe 推荐的 Edge Delivery Services 路径的好处](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#recommended-path-eds)。

**若要将 Edge Delivery Site 添加到 Cloud Manager：**

1. 在 Cloud Manager 中加入 Edge Delivery Site 之前，请确保您已首先使用 Edge Delivery Services 许可证创建了您的程序。
请参阅[创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。
1. 在 [experiece.adobe.com](https://experience.adobe.com) 登录 Cloud Manager。
1. 在&#x200B;**快速访问**&#x200B;部分，单击 **Experience Manager**。
1. 在左侧面板中点击 **Cloud Manager**。
1. 选择所需的组织。
1. 在&#x200B;**我的程序**&#x200B;控制台上，单击一个程序。
1. 执行下列操作之一：

   * 从&#x200B;**程序概述**&#x200B;页面，单击 **Edge Delivery** 选项卡。然后，单击页面右下角附近的&#x200B;**添加 Edge Delivery Site**。

     ![从 Edge Delivery 选项卡添加 Edge Delivery Site](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)，以显示左侧菜单。
在&#x200B;**服务**&#x200B;标题下，单击 ![Web 页面图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites**。

在页面的右上角附近，单击![链接图标或添加](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Link_18_N.svg) **添加 Edge Delivery Site**。

     ![通过 Edge Delivery Sites 按钮添加 Edge Delivery Site](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. 在&#x200B;**添加 Edge Delivery Site** 对话框中，在必填字段中提供以下信息：

   | 文本字段 | 描述 |
   | - | --- |
   | Site 名称 | 输入您要添加的 Edge Delivery Site 的名称。<br>该名称是 Cloud Manager 内 Site 的唯一标识符。 |
   | Edge Delivery 来源 | 这个值指定了 Edge Delivery Services 中您的网站内容源的 URL 路径。它还将 Cloud Manager 连接到您的实时网站。<br>此 URL 通常包括&#x200B;*分支*、*项目*&#x200B;和&#x200B;*租户*，如下例所示（仅用于说明目的）：<br>`https://main--{site}--{org}.aem.live` |
   | Site 描述（可选） | 输入您要添加的 Edge Delivery Site 的简短描述。<br>描述信息有助于识别和区分 Site，使您在添加的其他 Sites 中更容易管理和识别该 Site。 |

1. 在对话框的右下角，单击&#x200B;**添加**。

1. 在&#x200B;**验证存储库所有权**&#x200B;对话框中，通过执行以下步骤验证存储库的所有权：

   | 步骤数 | 描述 |
   | - | - |
   | **1** | 将路径和名称为 `well-known/adobe/cloudmanager-challenge.txt` 的文件添加到 Git 存储库的 `main` 分支，该分支列在&#x200B;**存储库 URL** 字段中。请&#x200B;*不要*&#x200B;在位置路径的开头添加句点。<br>如有必要，单击![复制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)将路径复制到剪贴板。 |
   | **2** | 将步骤 2 中文本字段中看到的代码添加到您在步骤 1 中刚刚创建的文件中。<br>如有必要，单击![复制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)将代码复制到剪贴板。 |
   | **3** | 在 Git 存储库中为您刚才创建的更改创建一个拉取请求，然后将其合并到 `main` 以提交代码。 |

1. 单击&#x200B;**验证**。

   >[!NOTE]
   >
   >如果您的Edge Delivery Services网站使用Helix身份验证，则无法访问验证质询。 暂时禁用身份验证，完成站点验证，然后重新打开身份验证。



在验证存储库后，它在 Edge Delivery Sites 表中的状态就会更新。内部带有白色复选标记的绿色圆圈表示状态。

在同一个表中，单击![Edge Delivery Site 图标信息](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg)查看 Site 详情。此信息包括经过验证的存储库 URL，以及预览和生产网站 URL。
