---
title: 使用用户映射工具
description: 使用用户映射工具
translation-type: tm+mt
source-git-commit: 664c278494a5ac88362b994946060ab3baa846d8
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# 使用用户映射工具{#user-mapping-tool}

## 概述 {#overview}

作为过渡进入AEM的Cloud Service的一部分，您需要将用户和组从现有的AEM系统移至AEM作为Cloud Service。 这由内容传输工具完成。

对AEM作为Cloud Service的一个重大改变是完全集成地使用AdobeID访问创作层。  这需要使用Adobe Admin Console管理用户和用户组。 AdobeIdentity Management系统(IMS)中集中了用户用户档案信息，该系统可在所有Adobe云应用程序中提供单一登录。 有关详细信息，请参阅Identity Management。 由于此更改，现有用户和用户组需要映射到其IMS ID，以避免重复用户和Cloud Service作者实例上的用户组。

## 重要注意事项{#important-considerations}

有一些例外情况需要考虑。 将记录以下特定案例，并且不会映射有关的用户或组：

1. 如果用户在其jcr节点的`profile/email`字段中没有电子邮件地址。

1. 如果在IMS系统上找不到所使用的组织ID的给定电子邮件（或者，由于其他原因无法检索IMS ID）。

1. 如果用户当前处于禁用状态，则会将其视为与未禁用状态相同。  它将按正常方式进行映射和迁移，并在云实例上保持禁用状态。

## 使用用户映射工具{#using-user-mapping-tool}

用户映射工具使用一个API，它允许它通过电子邮件查找IMS用户并返回其IMS ID。 此API要求用户为其组织创建客户端ID、客户端机密和访问令牌/载体令牌。

请按照以下步骤设置：

1. 使用您的Adobe ID导航到[Adobe开发人员控制台](https://console.adobe.io)。
1. 创建新项目或打开现有项目
1. 添加API
1. 选择用户管理API
1. 创建JWT凭据
1. 生成密钥对或上传公钥（rsa不行）
1. 生成访问令牌（或JWT令牌或载体令牌）。
1. 将所有这些信息(客户端ID、客户端机密、技术帐户ID、技术帐户电子邮件、组织ID、访问令牌)保存在一个安全位置。