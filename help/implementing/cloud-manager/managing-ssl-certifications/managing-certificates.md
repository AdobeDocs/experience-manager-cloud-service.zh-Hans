---
title: 管理 SSL 证书
description: 了解如何使用Cloud Manager检查SSL证书的状态，以及如何编辑、替换、更新和删除这些证书。
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
source-git-commit: 6cc1620d139db3804325c118d0874c5f94cb23a4
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# 管理 SSL 证书 {#managing-ssl-certificates}

了解如何使用Cloud Manager检查SSL证书的状态，以及如何编辑、替换、更新和删除这些证书。

## 检查SSL证书的状态 {#checking-status-an-ssl-certificate}

可以从SSL证书页面一目了然地了解SSL证书的状态。

* **绿色**  — 此状态表示您的证书在当前日期起至少60天内有效。

* **橙色**  — 此状态表示您的证书将在60天内过期。
   * 现在是时候确保您有计划通过Cloud Manager UI续订并替换您的证书，以避免可能的站点访问或中断。
   * Cloud Manager将在UI中发送常规通知，以提醒您证书即将过期。

* **红色**  — 此状态表示SSL证书已过期。

## 预先存在的CDN配置 {#pre-existing-cdn}

如果您的SSL证书已预先存在CDN配置，则 **SSL证书** 页面，鼓励您通过UI添加这些配置，以便它们在Cloud Manager中可见且可配置。

使用UI迁移所有预先存在的环境配置后，该消息会消失。 消息可能需要1-2个工作日才能消失。

请参阅该文档 [添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 以了解更多详细信息。

在 **IP允许列表** 和 **环境** 页面，用于为IP允许列表或自定义域名预先存在CDN配置的环境。

## 更新SSL证书 {#update-ssl-certificate}

当证书过期时，任何正在与过期证书一起使用的域将不再有效。 通过以下步骤更新证书可确保域继续按需要工作。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。
1. 导航到 **环境** 屏幕 **概述** 页面。
1. 导航到 **SSL证书** 屏幕 **环境** 屏幕。
1. 您将看到一个表格，其中包含已成功安装到程序中的每个SSL证书的行。 单击您要更新的证书行最右侧的省略号按钮，然后选择 **查看和更新**.
1. 将显示证书详细信息，并且可以进行更新。

>[!NOTE]
>
>用户必须是 **业务所有者** 或 **部署管理器** 角色，以便在Cloud Manager中更新SSL证书。

## 替换SSL证书 {#replace-ssl-certificate}

可以按照与部分中所述相同的步骤替换SSL证书 [更新SSL证书。](#update-ssl-certificate)

## 删除 SSL 证书 {#deleting-an-ssl-certificate}

从Cloud Manager中删除证书是一项无法撤消的永久性操作。 作为最佳实践，Adobe建议先将SSL文件保存在本地，然后再在Cloud Manager中删除它们。

Cloud Manager将不允许您删除一个SSL证书，该证书具有一个或多个与其关联的域。 删除SSL证书之前，必须删除所有关联的域。 请参阅该文档 [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) 以了解更多。

按照以下步骤删除SSL证书。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。
1. 导航到 **环境** 屏幕 **概述** 页面。
1. 导航到 **SSL证书** 屏幕 **环境** 屏幕。
1. 您将看到一个表格，其中包含已成功安装到程序中的每个SSL证书的行。 单击您要删除的证书行最右侧的省略号按钮，然后选择 **删除**.
1. 在 **删除SSL证书** 对话框。

>[!NOTE]
>
>用户必须是 **业务所有者** 或 **部署管理器** 角色，以便在Cloud Manager中删除SSL证书。
