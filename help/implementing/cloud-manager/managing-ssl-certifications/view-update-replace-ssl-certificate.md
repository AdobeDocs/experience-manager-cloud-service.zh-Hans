---
title: '查看更新和替换SSL证书 — 管理SSL '
description: 查看更新和替换SSL证书 — 管理SSL证书
exl-id: 662494b1-a710-4822-97ef-057043ef89ba
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# 查看、更新和替换 SSL 证书  {#view-update-replace-ssl-certificate}

## 查看和更新SSL证书 {#view-update}

何时在Cloud Manager UI中使用这些选项：

* 现有证书即将过期。 用户已使用证书供应商续订证书，并希望替换即将过期的现有证书。 注意：只有具有相应权限的用户才能进行更新。
* 使用 **查看和更新** 菜单，以便您查看SSL证书详细信息。
* 或者，您也可以从此屏幕中更改用于引用证书的名称。
* 只有具有相应权限的用户才能进行更新。


## 更新即将过期的SSL证书 {#update-ssl-certificate}

当证书过期时，任何正在与过期证书一起使用的域将不再有效。 要更新过期的证书，必须按照下面列出的步骤操作。 这将确保您的域可以继续按预期工作。 添加新证书将需要使用新证书更新自定义域名，然后域才能按需工作。 请参阅 [查看、更新和替换自定义域名](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md) 以了解更多详细信息。

请按照以下步骤更新SSL证书：

>[!NOTE]
>要在Cloud Manager中更新SSL证书，用户必须处于业务所有者或部署管理员角色。

1. 从 **环境** 页面。
1. 您将看到一个表格，其中包含已成功安装到程序中的每个SSL证书的行。
1. 通过选择目标行最右端的三个按钮，可访问每行的菜单选项。
1. 选择 **查看和更新**. 可以从此处查看证书详细信息。

## 替换SSL证书 {#replace-ssl-certificate}

按照以下步骤替换SSL证书：

1. 从 **环境** 页面。
1. 您将看到一个表格，其中包含已成功安装到程序中的每个SSL证书的行。
1. 通过选择目标行最右端的三个按钮，可访问每行的菜单选项。
1. 选择 **查看和更新**.
1. 要替换证书，请将新内容粘贴到相应的输入字段中，然后单击 **保存**. 您需要解决可能出现的任何错误。

   请参阅 [证书错误](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-error) 解决常见问题。
