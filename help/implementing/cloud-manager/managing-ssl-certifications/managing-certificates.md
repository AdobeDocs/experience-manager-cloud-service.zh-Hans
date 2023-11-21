---
title: 管理 SSL 证书
description: 了解如何使用 Cloud Manager 检查 SSL 证书的状态，以及如何编辑、替换、更新和删除这些证书。
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 78%

---


# 管理 SSL 证书 {#managing-ssl-certificates}

了解如何使用 Cloud Manager 检查 SSL 证书的状态，以及如何编辑、替换、更新和删除这些证书。

## 检查 SSL 证书的状态 {#checking-status-an-ssl-certificate}

可以从 SSL 证书页面一眼就了解 SSL 证书的状态。

* **绿色** – 此状态表示您的证书自当前日期起至少 60 天内有效。

* **橙色** – 此状态表示您的证书将在 60 天内到期。
   * 现在需要确保您有计划续订证书并通过 Cloud Manager 用户界面替换该证书，从而避免可能的站点访问中断。
   * Cloud Manager 将在 UI 中定期发送通知，提醒您证书即将到期。

* **红色** – 此状态表示 SSL 证书已过期。

## 更新 SSL 证书 {#update-ssl-certificate}

当证书过期时，与过期证书一起使用的任何域都将不再工作。通过以下步骤更新证书可确保域继续按需工作。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。
1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。
1. 从&#x200B;**环境**&#x200B;页面导航到 **SSL 证书**&#x200B;屏幕。
1. 您可以看到一个表，其中包含已在程序中成功安装的每个SSL证书的行。 单击要更新的证书行最右侧的省略号按钮，然后选择 **查看和更新**.
1. 将显示证书详细信息并可以更新。
1. 运行管道以部署更新的证书。

>[!NOTE]
>
>用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色成员，才能在 Cloud Manager 中更新 SSL 证书。

## 替换 SSL 证书 {#replace-ssl-certificate}

可以按照[更新 SSL 证书](#update-ssl-certificate)一节中描述的相同步骤替换 SSL 证书。

## 删除 SSL 证书 {#deleting-an-ssl-certificate}

从 Cloud Manager 中移除证书是一个无法撤消的永久操作。作为最佳实践，Adobe 建议在 Cloud Manager 中删除 SSL 文件之前，先在本地保存这些文件。

Cloud Manager 不允许您删除具有一个或多个关联域的 SSL 证书。在删除 SSL 证书之前，必须删除所有关联的域。请参阅[管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)，了解更多信息。

按照以下步骤删除 SSL 证书。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。
1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。
1. 从&#x200B;**环境**&#x200B;页面导航到 **SSL 证书**&#x200B;屏幕。
1. 您可以看到一个表，其中包含已在程序中成功安装的每个SSL证书的行。 单击要删除的证书行最右侧的省略号，然后选择 **删除**.
1. 在&#x200B;**删除 SSL 证书**&#x200B;对话框中，确认删除操作。
1. 运行管道以取消部署已删除的证书。

>[!NOTE]
>
>用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色成员，才能在 Cloud Manager 中删除 SSL 证书。

## 预先存在的 CDN 配置 {#pre-existing-cdn}

如果您的SSL证书已有CDN配置，则 **SSL证书** 页面，鼓励您通过UI添加这些配置，以便它们在Cloud Manager中可见和可配置。

使用 UI 迁移所有预先存在的环境配置后，消息将消失。消息可能需要 1 – 2 个工作日才能消失。

请参阅[添加 SSL 证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)，了解更多信息。

**IP 允许列表**&#x200B;和&#x200B;**环境**&#x200B;页面上也提供了类似的消息，这些环境具有 IP 允许列表或自定义域名的预先存在的 CDN 配置。
