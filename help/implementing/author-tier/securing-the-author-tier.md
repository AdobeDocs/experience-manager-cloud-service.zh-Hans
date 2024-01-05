---
title: 保护创作层
description: 了解如何配置网络策略以保护对创作层的访问。
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 31%

---

# 保护创作层 {#securing-the-author-tier}

使用AEMas a Cloud Service创建环境时，默认情况下可以从Internet访问生成的创作层。 可以进一步配置网络策略以保护对创作层的访问。 请参阅 [应用IP允许列表](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html) 以了解更多详细信息。 此过程基于应授予您的创作环境网络访问权限的 IP 范围授权。

要设置这些规则，请从以下位置提交支持工单： [Adobe Admin Console](https://adminconsole.adobe.com/) ，并提供以下所需信息：

* 项目 ID
* 环境 ID
* 要授权的 IP 地址范围

