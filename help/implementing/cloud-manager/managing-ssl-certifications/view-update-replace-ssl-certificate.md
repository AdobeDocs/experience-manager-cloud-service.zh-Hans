---
title: '查看更新和替换SSL证书——管理SSL '
description: 查看更新和替换SSL证书——管理SSL证书
translation-type: tm+mt
source-git-commit: b76a22469f248dde316dcaa514a906fe4361afd1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 查看和更新并替换SSL证书{#view-update-replace-ssl-certificate}

## 查看和更新SSL证书{#view-update}

何时在云管理器UI中使用这些选项：

* 现有证书即将过期。 用户已用证书供应商续订证书，并希望替换即将过期的现有证书。 注意：只有具有相应权限的用户才能进行更新。
* 使用&#x200B;**视图和更新**&#x200B;菜单，只需视图SSL证书详细信息。
* 或者，您也可以更改已用于从此屏幕引用证书的名称。
* 只有具有相应权限的用户才能进行更新。


## 更新即将过期的SSL证书{#update-ssl-certificate}

当证书过期时，任何与过期证书一起使用的域将不再工作。 要更新过期的证书，必须按照下面列出的步骤操作。 这将确保您的域继续按需要工作。 添加新证书将需要使用新证书更新自定义域名，然后域才能根据需要工作。 有关详细信息，请参阅[查看和更新并替换自定义域名](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)。

请按照以下步骤更新SSL证书：

>[!NOTE]
>用户必须处于“业务所有者”或“部署管理器”角色，才能在云管理器中更新SSL证书。

1. 从&#x200B;**环境**&#x200B;页面导航到“SSL证书”屏幕。
1. 您将看到一个表格，其中每个SSL证书都有一行已成功安装在项目中。
1. 通过选择感兴趣行最右端的三个按钮，可以访问每行的菜单选项。
1. 选择&#x200B;**视图和更新**。 可以从此处查看证书详细信息。

## 替换SSL证书{#replace-ssl-certificate}

请按照以下步骤替换SSL证书：

1. 从&#x200B;**环境**&#x200B;页面导航到“SSL证书”屏幕。
1. 您将看到一个表格，其中每个SSL证书都有一行已成功安装在项目中。
1. 通过选择感兴趣行最右端的三个按钮，可以访问每行的菜单选项。
1. 选择&#x200B;**视图和更新**。
1. 要替换证书，请将新内容粘贴到相应的输入字段中，然后单击“保存&#x200B;****”。 您需要解决可能出现的任何错误。

   请参阅[证书错误](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-error)以解决常见问题。