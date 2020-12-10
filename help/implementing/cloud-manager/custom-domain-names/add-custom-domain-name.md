---
title: 添加自定义域名
description: 添加自定义域名
translation-type: tm+mt
source-git-commit: 68a62be11f711e30b87dfc60a85627dceaf06caa
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---


# 添加自定义域名{#adding-cdn}

用户必须是业务所有者或部署管理者，才能在云管理器中添加自定义域名。

## 重要注意事项{#important-considerations}

* 在添加自定义域名之前，必须向项目安装包含自定义域名的有效SSL证书。 请参阅[添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)以了解更多信息。

* 一次只能添加一个域名。 但是，用户可以添加通配符（例如`*.wknd.com`）作为域名，这允许使用单个TXT记录托管多个子域。

* 每个Cloud Manager环境最多可托管每个环境100个自定义域。

* 同一域名不能用于多个环境。

## 从“域设置”页{#adding-cdn-settings}添加自定义域名

请按照以下步骤从“域设置”页面添加自定义域名：

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**环境**&#x200B;屏幕。

1. 单击左侧导航菜单中的&#x200B;**域设置**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 单击&#x200B;**添加域**&#x200B;按钮以打开&#x200B;**添加域名**&#x200B;对话框。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create2.png)

1. 在&#x200B;**域名**&#x200B;中输入自定义域名。

   >[!NOTE]
   >在域中输入时，不应包括`http://`、`https://`或空格。

1. 选择&#x200B;**环境**，其发布服务将与域名关联。

1. 从下拉列表中选择&#x200B;**域SSL证书**&#x200B;并选择&#x200B;**继续**。

1. **将显示“添** 加域名”对话框。这将带您进入环境的域名验证屏幕。 请参阅[添加TXT记录](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)以了解更多信息。
按照提供的说明证明您的环境的域所有权。

1. 单击&#x200B;**创建**。
1. CDN部署需要有效的SSL证书和成功的TXT验证。 状态&#x200B;**已验证和已部署**&#x200B;表示。
1. 导航到检查自定义域名状态，进一步了解各种状态以及地址。

   >[!NOTE]
   >由于DNS传播延迟，DNS验证可能需要花费数小时才能识别。 云管理器将验证所有权并更新状态，该状态可在域设置表中看到。 有关详细信息，请参阅检查域名状态。

## 从环境页{#adding-cdn-environments}添加自定义域名

1. 定位至感兴趣环境的“环境详细信息”页。
1. 使用“域名”表顶部的输入字段提交自定义域名，即SSL证书。 然后选择添加。
1. 这将启动“添加自定义域名”向导并预填充环境名。
1. 输入自定义域名。 注意：在域中输入时，不要包括`http://`、`https://`或空格。 选择继续。
1. 这将带您进入环境的域名验证屏幕。 请参阅[域验证](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)以了解更多信息。 按照提供的说明证明您的环境的域所有权。
1. 选择&#x200B;**继续**。
1. CDN部署需要有效的SSL证书和成功的TXT验证。 状态&#x200B;**已验证和已部署**&#x200B;表示。

此时，您的自定义域名已准备好进行测试，并且`CNAME`将指向它。 请参阅域名状态，进一步了解各种状态以及如何寻址。

>[!NOTE]
>由于DNS传播延迟，DNS验证可能需要花费数小时才能识别。 云管理器将验证所有权并更新状态，该状态可在域设置表中看到。 请参阅检查域名状态以了解更多信息。
