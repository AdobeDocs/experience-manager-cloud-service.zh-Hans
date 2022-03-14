---
title: 删除SSL证书 — 管理SSL证书
description: 删除SSL证书 — 管理SSL证书
exl-id: 43f66871-cca4-4709-95d0-68aa715c0da2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 2%

---

# 删除 SSL 证书 {#deleting-an-ssl-certificate}

>[!IMPORTANT]
>从Cloud Manager中删除证书是一项无法撤消的永久操作。 最佳做法是在Cloud Manager用户界面中删除任何必需的SSL文件之前，将其保存在本地。

要在Cloud Manager中删除SSL证书，用户必须处于业务所有者或部署管理员角色。 Cloud Manager将不允许您删除一个SSL证书，该证书具有一个或多个与其关联的域。  删除SSL证书之前，必须删除所有关联的域。 请参阅 [删除自定义域名](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) 以了解更多。

按照以下步骤删除SSL证书：

1. 导航到 **SSL证书** 屏幕 **环境** 页面。
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. 确定要删除的SSL证书名称所在的行。
1. 选择 **...** 菜单。
1. 选择 **删除**.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. 确认您的提交来源 **删除SSL证书** 对话框。
