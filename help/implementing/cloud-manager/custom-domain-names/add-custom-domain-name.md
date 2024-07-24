---
title: 添加自定义域名
description: 了解如何使用 Cloud Manager 添加自定义域名。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 06e961febd7cb2ea1d8fca00cb3dee7f7ca893c9
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 35%

---


# 添加自定义域名 {#adding-cdn}

了解如何使用 Cloud Manager 添加自定义域名。

## 要求 {#requirements}

在Cloud Manager中添加自定义域名之前，您必须满足这些要求。

* 在添加自定义域名之前，您必须为要添加的域添加域SSL证书，如文档[添加SSL证书中所述。](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* 您必须具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色才能在Cloud Manager中添加自定义域名。
* 你一定是使用Fastly CDN了。

## 在何处添加自定义域名 {#where}

您可以从 Cloud Manager 中的两个位置添加自定义域名：

* [从“域设置”页面](#adding-cdn-settings)
* [从“环境”页面](#adding-cdn-environments)

添加自定义域名时，将使用最具体且有效的证书为该域提供服务。 如果多个证书具有相同的域，则选择最近更新的证书。 Adobe建议您管理证书，这样就不会有重叠域。

本文档中介绍的步骤基于Fastly。 如果您使用其他CDN，则必须使用您选择使用的CDN配置域。

## 从域设置页面添加自定义域名 {#adding-cdn-settings}

按照以下步骤从&#x200B;**域设置**&#x200B;页面添加自定义域名。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 导航到左侧导航面板中的选择&#x200B;**域设置**&#x200B;选项卡。

   ![域设置窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 单击右上角的&#x200B;**添加域**&#x200B;按钮以打开&#x200B;**添加域名**&#x200B;对话框。

   ![“添加域”对话框](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)。

1. 在&#x200B;**域名**&#x200B;选项卡的&#x200B;**域名**&#x200B;字段中输入自定义域名。

   >[!NOTE]
   >
   >输入域时不要包含 `http://`、`https://` 或空格。

1. 选择其服务与域名关联的&#x200B;**环境**。

1. 选择&#x200B;**发布**&#x200B;或&#x200B;**预览**&#x200B;服务。

1. 从下拉列表中选择与域名关联的&#x200B;**域 SSL 证书**，然后选择&#x200B;**继续**。

1. 出现&#x200B;**验证**&#x200B;选项卡。

   ![域名验证](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   * **验证**&#x200B;选项卡描述了配置自定义域名的后续步骤，即创建必要的TXT记录。
   * 您可以立即执行此操作（在对话框中点击或单击&#x200B;**创建**&#x200B;之前），或者在对话框中点击或单击&#x200B;**创建**&#x200B;之后。
   * 下面介绍了选项和后续步骤。

1. 点按或单击&#x200B;**创建**&#x200B;以在Cloud Manager中保存自定义域名。

当您在&#x200B;**添加自定义域**&#x200B;向导的验证步骤中选择&#x200B;**创建**&#x200B;时，Cloud Manager将自动触发TXT验证，因此建议您在Cloud Manager中创建自定义域名时创建TXT记录。 但是，这不是必需的。 对于后续验证，必须主动选择状态旁边的再次验证图标。

在添加TXT条目并经Cloud Manager验证之前，该名称不会处于活动状态。 TXT验证成功由状态&#x200B;**已验证和已部署**&#x200B;指示。

* 请参阅[添加 TXT 记录](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)，了解有关 TXT 记录的更多信息。
* 有关Cloud Manager如何验证自定义域名及其TXT条目的详细信息，请参阅[检查域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。

## 后续步骤 {#next-steps}

在Cloud Manager中创建自定义域名后，您将需要添加TXT条目来验证域的所有权。 继续文档[添加TXT记录](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)以继续设置自定义域名。

## 从环境页面添加自定义域名 {#adding-cdn-environments}

从&#x200B;**环境**&#x200B;页面添加自定义域名的步骤与[从“域设置”页面添加自定义域名的步骤](#adding-cdn-settings)相同，但入口点不同。 按照以下步骤从&#x200B;**环境**&#x200B;页面添加自定义域名。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 导航至&#x200B;**环境详细信息**&#x200B;页面，了解感兴趣的环境。

   ![在“环境详细信息”页面上输入域名](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用&#x200B;**域名**&#x200B;表提交自定义域名。

   1. 输入自定义域名。
   1. 从下拉列表中选择与此名称关联的 SSL 证书。
   1. 单击&#x200B;**+添加**。

   ![添加自定义域名](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 将打开&#x200B;**添加域名**&#x200B;对话框，显示&#x200B;**域名**&#x200B;选项卡。 继续，就像从“域设置”页面添加自定义域名[一样。](#adding-cdn-settings)
