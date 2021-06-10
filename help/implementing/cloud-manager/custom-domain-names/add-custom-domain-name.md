---
title: 添加自定义域名
description: 添加自定义域名
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 1eb9423b0128c952bc16cf0b8dff95b0e86964a0
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# 添加自定义域名{#adding-cdn}

用户必须是业务所有者或部署管理器，才能在Cloud Manager中添加自定义域名。

## 重要注意事项{#important-considerations}

* 在添加自定义域名之前，必须向您的程序安装包含自定义域名的有效SSL证书。 请参阅[添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)以了解更多信息。

* 当当前正在运行的管道已附加到这些环境时，无法将域名添加到这些环境。

* 一次只能添加一个域名。 但是，域不能包含通配符。 不支持创作端的自定义域。

* AEM as aCloud Service不支持通配符域。

* 每个Cloud Manager环境最多可托管每个环境250个自定义域。

* 同一域名不能在多个环境中使用。

## 从“域设置”页面{#adding-cdn-settings}添加自定义域名

请按照以下步骤从“域设置”页面添加自定义域名：

1. 从&#x200B;**概述**&#x200B;页面导航到&#x200B;**Environments**&#x200B;屏幕。

1. 单击左侧导航菜单中的&#x200B;**域设置**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 单击&#x200B;**添加域**&#x200B;按钮以打开&#x200B;**添加域名**&#x200B;对话框。

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 在&#x200B;**域名**&#x200B;中输入自定义域名。

   >[!NOTE]
   >在域中输入时，不应包含`http://`、`https://`或空格。

1. 选择其发布服务将与域名关联的&#x200B;**Environment**。

1. 选择服务作为&#x200B;**Publish**&#x200B;或&#x200B;**Preview**。

   >[!NOTE]
   >现在，Cloud Manager中支持发布和预览服务的站点程序的自定义域名。 每个Cloud Manager环境最多可托管每个环境250个自定义域。 要了解有关预览服务的更多信息，请参阅[预览服务](/help/implementing/cloud-manager/manage-environments.md#preview-service)。

1. 从下拉菜单中选择&#x200B;**域SSL证书**，然后选择&#x200B;**继续**。

1. **将显示“添** 加域”对话框。这会将您转到环境的域名验证屏幕。 请参阅[添加TXT记录](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)以了解更多信息。

   按照提供的说明来证明您环境的域所有权：

1. 单击&#x200B;**创建**。
1. CDN部署需要有效的SSL证书和成功的TXT验证。 状态&#x200B;**已验证和已部署**表示。
导航至[检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) ，以了解有关各种状态以及如何寻址的更多信息。

   >[!NOTE]
   >由于DNS传播延迟，DNS校样可能需要长达数小时才能识别。 Cloud Manager将验证所有权并更新状态，这些状态可在域设置表中查看。 有关更多详细信息，请参阅检查域名状态。

## 从“环境”页面{#adding-cdn-environments}添加自定义域名

1. 导航到所关注环境的“环境详细信息”页面。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用“域名”(Domain Names)表格顶部的输入字段提交自定义域名，并从下拉列表中选择SSL证书。 单击&#x200B;**+ Add**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 选中&#x200B;**添加域名**&#x200B;对话框中的字段，然后单击&#x200B;**继续**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >在域中输入时，请勿包含`http://`、`https://`或空格。

1. 此时会显示“Domain Name Verification for your Environment”屏幕。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   请参阅[域验证](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)以了解更多信息。 按照提供的说明来证明您环境的域所有权。

1. 单击&#x200B;**创建**。

1. 自定义域名部署需要有效的SSL证书和成功的TXT验证。 状态&#x200B;**已验证和已部署**&#x200B;表示。

此时，您的自定义域名已准备就绪，可供测试，并且`CNAME`会指向该域名。 请参阅[域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) ，了解有关各种状态以及如何寻址的更多信息。

>[!NOTE]
>由于DNS传播延迟，DNS校样可能需要长达数小时才能识别。 Cloud Manager将验证所有权并更新状态，这些状态可在域设置表中查看。 请参阅检查域名状态以了解更多信息。
