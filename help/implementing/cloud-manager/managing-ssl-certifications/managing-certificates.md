---
title: 管理 SSL 证书
description: 了解如何使用 Cloud Manager 检查 SSL 证书的状态，以及如何编辑、替换、更新和删除这些证书。
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: d2f05915c0bf0af073db7f070b83f13aeae55252
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 13%

---


# 管理 SSL 证书 {#managing-ssl-certificates}

了解如何使用Cloud Manager检查Adobe托管和客户托管的SSL证书的状态以及如何删除它们。 对于客户管理的证书，您还可以编辑和更新（替换）它们。

## 检查SSL证书的状态 {#checking-status-an-ssl-certificate}

可以从&#x200B;**SSL证书**&#x200B;页面一眼就了解SSL证书的状态。

| SSL证书的状态 | 描述 |
| --- | --- |
| 绿色 | 证书自当前日期起至少14天内有效。 |
| 橙色 | 该证书将在14天内过期。<br>·确保您有计划续订证书并通过Cloud Manager用户界面替换该证书，以避免可能的站点访问中断。<br>· Cloud Manager会在UI中定期发送通知，提醒您证书即将到期。 |
| 红色 | SSL证书已过期。<br>请参阅[更新过期的客户托管的SSL证书](#update-ssl-certificate)或[删除SSL证书](#deleting-an-ssl-certificate)。 |

## 更新过期的客户管理的SSL证书 {#update-ssl-certificate}

当客户管理的证书过期时，与已过期证书一起使用的任何域不再工作。 更新证书可确保域继续按需工作。

用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理器**&#x200B;角色的成员才能完成此任务。

**要更新过期的客户管理的SSL证书，请执行以下操作：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。
1. 从&#x200B;**概述**&#x200B;页面，导航到&#x200B;**环境**&#x200B;屏幕。
1. 从&#x200B;**环境**&#x200B;屏幕，导航到&#x200B;**SSL证书**&#x200B;屏幕。
1. 在要更新的过期客户托管证书的行中，单击最右侧的省略号按钮，然后选择&#x200B;**查看和更新**。

   ![更新过期的客户管理的SSL认证](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. 在&#x200B;**查看和更新SSL证书**&#x200B;对话框中，执行以下操作：

   * （可选）在&#x200B;**证书名称**&#x200B;字段中，键入一个新名称。
   * 在&#x200B;**证书**&#x200B;字段中，粘贴新的证书内容密钥。
   * 在&#x200B;**私钥**&#x200B;字段中，仅当更改证书时才更新此字段。
   * 在&#x200B;**证书链**&#x200B;字段（或信任链）中，粘贴证书链。

1. 单击&#x200B;**更新**&#x200B;以保存更改并自动应用它们。

## 替换过期的客户管理的SSL证书 {#replace-ssl-certificate}

按照[更新过期的SSL证书](#update-ssl-certificate)中描述的相同步骤操作，以替换已过期的客户管理的SSL证书。

## 删除SSL证书 {#deleting-an-ssl-certificate}

从Cloud Manager中删除Adobe托管或客户托管的SSL证书是一个无法撤消的永久操作。 作为最佳实践，Adobe建议在Cloud Manager中删除SSL文件之前，先在本地保存这些文件。

>[!NOTE]
>
>无法删除具有一个或多个关联活动域的Adobe托管SSL证书。 在删除SSL证书之前，必须删除所有关联的活动域。 请参阅[管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)以了解详情。

用户必须是&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理器**&#x200B;角色的成员才能完成此任务。

**要删除SSL证书：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。
1. 从&#x200B;**概述**&#x200B;页面，导航到&#x200B;**环境**&#x200B;屏幕。
1. 从&#x200B;**环境**&#x200B;屏幕，导航到&#x200B;**SSL证书**&#x200B;屏幕。
1. 在要删除的证书的行中，单击最右侧的省略号按钮，然后选择&#x200B;**删除**。
如果“删除”按钮具有如下图所示的信息图标，请参阅上面的注释。

   ![删除带有信息图标的按钮](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. 在&#x200B;**删除SSL证书**&#x200B;对话框中，单击&#x200B;**删除**&#x200B;以确认删除。
1. 运行管道以取消部署已删除的证书。

## 预先存在的CDN配置 {#pre-existing-cdn}

如果您已有SSL证书的CDN配置，**SSL证书**&#x200B;页面将显示一条信息性消息。 它鼓励您通过UI添加这些配置，以便它们在Cloud Manager中可见和可管理。

使用UI迁移所有预先存在的环境配置后，消息将消失。 消息可能需要 1 – 2 个工作日才能消失。

有关详细信息，请参阅[添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。

**IP允许列表**&#x200B;和&#x200B;**环境**&#x200B;页面上也提供了类似的消息，这些环境具有IP允许列表或自定义域名的预先存在的CDN配置。
