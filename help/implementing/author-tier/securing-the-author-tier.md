---
title: 保护创作层
description: 保护创作层
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 53%

---

# 保护创作层 {#securing-the-author-tier}

使用 AEM as a Cloud Service 创建新环境时，默认情况下可以从 Internet 访问生成的创作层。可以进一步配置网络策略，以保护对创作层的访问。 参见 [应用IP允许列表](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=en) 了解更多详细信息。 此过程基于应授予您的创作环境网络访问权限的 IP 范围授权。

要设置这些规则，请提交支持工单，从 [Adobe Admin Console](https://adminconsole.adobe.com/) 包含请求的信息：

* 项目 ID
* 环境 ID
* 要授权的 IP 地址范围

