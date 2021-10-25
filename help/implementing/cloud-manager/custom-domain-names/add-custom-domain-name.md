---
title: 添加自定义域名
description: 添加自定义域名
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 98c137645351c86da8680a31b4929c588863a981
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# 添加自定义域名 {#adding-cdn}

用户必须是业务所有者或部署管理器，才能在Cloud Manager中添加自定义域名。

必须完成下列步骤，如下表所示：

| 步骤 |  | 责任 | 了解更多信息 |
|--- |--- |--- |---|
| 添加SLL证书 | 添加SLL证书 | 客户 | [添加SSL证书](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| 域验证 | 添加TXT记录 | 客户 | [添加TXT记录](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| 查看域验证状态 |  | 客户 |  |
|  | 状态：域验证失败 | 客户 | [正在检查域名状态](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | 状态：已验证，部署失败 | 联系Adobe代表 | [正在检查域名状态](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| 通过添加CNAME或APEX记录，添加指向AEMas a Cloud Service的DNS记录 | 配置DNS设置 | 客户 | [配置DNS设置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| 检查DNS记录状态 |  | 客户 | [正在检查DNS记录状态](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 状态：未检测到DNS状态 | 客户 | [正在检查DNS记录状态](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 状态：DNS解析不正确 | 客户 |  |


## 重要注意事项 {#important-considerations}

* 在添加自定义域名之前，必须向您的程序安装包含自定义域名的有效SSL证书。 请参阅 [添加SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 以了解更多。

* 当当前正在运行的管道已附加到这些环境时，无法将域名添加到这些环境。

* 一次只能添加一个域名。 不支持创作端的自定义域。

* AEMas a Cloud Service不支持通配符域。

* 每个Cloud Manager环境最多可托管每个环境500个自定义域。

* 同一域名不能在多个环境中使用。

## 从“域设置”页面添加自定义域名 {#adding-cdn-settings}

请按照以下步骤从“域设置”页面添加自定义域名：

1. 导航到 **环境** 屏幕 **概述** 页面。

1. 单击 **域设置** 菜单中。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 单击 **添加域** 按钮打开 **添加域名** 对话框。

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 在 **域名**.

   >[!NOTE]
   >您不应包括 `http://`, `https://`、或空格。

1. 选择 **环境** 其发布服务将与域名关联。

1. 选择服务作为 **发布** 或 **预览**.

   >[!NOTE]
   >现在，Cloud Manager中支持发布和预览服务的站点程序的自定义域名。 每个Cloud Manager环境最多可托管每个环境500个自定义域。 要了解有关预览服务的更多信息，请参阅 [预览服务](/help/implementing/cloud-manager/manage-environments.md#preview-service).

1. 选择 **域SSL证书** 从下拉菜单中，选择 **继续**.

1. **添加域名** 对话框。 这会将您转到环境的域名验证屏幕。 请参阅 [添加TXT记录](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 以了解更多。

   按照提供的说明来证明您环境的域所有权：

1. 单击 **创建**.
1. CDN部署需要有效的SSL证书和成功的TXT验证。 状态指示 **已验证和部署**.
导航到 [检查自定义域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 了解有关各种状态以及解决方法的更多信息。

   >[!NOTE]
   >由于DNS传播延迟，DNS校样可能需要长达数小时才能识别。 Cloud Manager将验证所有权并更新状态，这些状态可在域设置表中查看。 有关更多详细信息，请参阅检查域名状态。

## “从环境添加自定义域名”页 {#adding-cdn-environments}

1. 导航到所关注环境的“环境详细信息”页面。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用“域名”(Domain Names)表格顶部的输入字段提交自定义域名，并从下拉列表中选择SSL证书。 单击 **+添加**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 检查 **添加域名** 对话框，单击 **继续**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >不包括 `http://`, `https://`、或空格。

1. 此时会显示“Domain Name Verification for your Environment”屏幕。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   请参阅 [域验证](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 以了解更多。 按照提供的说明来证明您环境的域所有权。

1. 单击 **创建**.

1. 自定义域名部署需要有效的SSL证书和成功的TXT验证。 状态指示 **已验证和部署**.

此时，您的自定义域名已准备就绪，可供测试，并且 `CNAME` 指向它。 请参阅 [域名状态](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 了解有关各种状态以及解决方法的更多信息。

>[!NOTE]
>由于DNS传播延迟，DNS校样可能需要长达数小时才能识别。 Cloud Manager将验证所有权并更新状态，这些状态可在域设置表中查看。 请参阅检查域名状态以了解更多信息。
