---
title: 使用Vanilla JS集成内容片段选择器
description: 将内容片段选择器与各种Adobe、非Adobe和第三方应用程序集成。
role: Admin, User, Developer
source-git-commit: 592e443928f2c9c18ac281027026132b1c877ce3
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---

# 使用Vanilla JS集成内容片段选择器 {#integrate-content-fragment-selector-using-vanilla-js}

您可以将任何Adobe或非Adobe应用程序与Adobe Experience Manager (AEM) as a Cloud存储库集成，并从该应用程序中选择内容片段。

集成可通过导入内容片段选择器包并使用Vanilla JavaScript库连接到AEM as a Cloud Service来完成。 编辑应用程序中的`index.html`或任何适当的文件，以：

* 定义身份验证详细信息
* 访问AEM as a Cloud Service存储库
* 配置内容片段选择器显示属性

如果您符合以下条件，则无需定义某些IMS属性即可执行身份验证：

* 正在[Unified Shell](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell)上集成Adobe应用程序
* 已生成用于身份验证的IMS令牌
