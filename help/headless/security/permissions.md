---
title: '无标题内容的权限注意事项 '
description: 了解使用Adobe Experience Manager进行无头实施的不同权限和ACL注意事项。 了解创作和发布环境所需的不同角色和潜在权限级别。
feature: Content Fragments,GraphQL API
source-git-commit: c5d67e0ece40cdf7a9009436ec90305fe81425a2
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# 无标题内容的权限注意事项

通过无头实施，应解决多个安全和权限方面的问题。 权限和角色的考虑范围很广，这取决于AEM环境 **作者** 或 **发布**. 每个环境包含不同的角色和不同的需求。

## 创作服务注意事项

“创作”服务是内部用户创建、管理和发布内容的位置。 权限取决于管理内容的不同角色。

### 在群组级别管理权限

作为最佳实践，应在AEM的群组中设置权限。 这些组也称为本地组，可在AEM创作环境中管理。

管理组成员资格的最简单方法是使用AdobeIdentity Management系统(IMS)组并分配 [将IMS组到本地AEM组](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/ims-support.html?lang=en#managing-permissions-in-aem).

![管理控制台权限流程](assets/admin-console-aem-group-permissions.png)

在高层面，该过程是：

1. 使用 [Admin Console](https://adminconsole.adobe.com/)
1. 当用户登录时，IMS组会与AEM同步。
1. 将IMS组分配给AEM组。
1. 设置AEM群组的权限。
1. 当用户登录AEM并通过IMS验证后，他们将继承AEM组的权限。

>[!TIP]
>
> 有关管理IMS和AEM用户和组的详细视频演练，请参阅 [此处](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html).

管理 **组** 在AEM中，导航到 **工具** > **安全性** > **群组**.

要在AEM中管理群组的权限，请导航到 **工具** > **安全性** > **权限**.

### DAM用户

在这种情况下，“DAM”表示数字资产管理。 的 **DAM用户** 是AEM中一个开箱即用的组，可用于管理数字资产和内容片段的“日常”用户。 此组提供 **视图**, **添加**, **更新**, **删除**&#x200B;和 **发布** 内容片段和AEM Assets中的所有其他文件。

如果将IMS用于组成员身份，请将相应的IMS组添加为 **DAM用户** 群组。 登录AEM环境时，IMS组的成员将继承DAM用户组的权限。

#### 自定义DAM用户组

最好不要直接修改现成群组的权限。 您也可以创建自己的组，这些组建在 **DAM用户** 群组权限，并进一步限制对不同群组的访问权限 **文件夹** 在AEM Assets。

如需更细的权限，请使用 **权限** 在AEM中控制台，并从 `/content/dam` 到更具体的路径，例如 `/content/dam/mycontentfragments`.

可能需要为此组用户授予创建和编辑内容片段的权限，但不要删除。 要查看和分配用于编辑的权限，但不要删除，请参阅 [内容片段 — 删除注意事项](/help/assets/content-fragments/content-fragments-delete.md).

### 模型编辑器

能够修改 **内容片段模型** 应留给管理员或 **小组** 具有提升权限的用户数量。 修改内容片段模型具有许多下游效果。

>[!CAUTION]
>
>对内容片段模型的修改会更改无头应用程序所依赖的基础GraphQL API。

如果您希望创建一个管理内容片段模型但没有完全管理员访问权限的组，则可以创建具有以下访问控制条目的组：

| 路径 | 权限 | 权限 |
|-----| -------------| ---------|
| `/conf` | **允许** | `jcr:read` |
| `/conf/<config-name>/settings/dam/cfm` | **允许** | `rep:write`, `crx:replicate` |

## 发布服务权限

发布服务被视为“实时”环境，通常是GraphQL API用户与之交互的环境。 内容在创作服务上经过编辑和批准后，会发布到发布服务。 然后，无头应用程序会通过GraphQL API使用发布服务中的已批准内容。

默认情况下，通过AEM发布服务的GraphQL端点公开的内容可供每个人访问，包括未经身份验证的用户。

### 内容权限

通过AEM GraphQL API公开的内容可以使用 [封闭用户组(CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html) 在assets文件夹中设置，以指定哪些AEM用户组（及其成员）可以访问Assets文件夹的内容。

资产CUG的工作方式：

* 首先，拒绝对文件夹和子文件夹的所有访问权限
* 然后，允许读取CUG列表中列出的所有AEM用户组的文件夹和子文件夹

可以对包含通过GraphQL API公开的内容的资产文件夹设置CUG。 在AEM发布中，对资产文件夹的访问应通过用户组进行控制，而不是直接通过用户进行控制。 创建（或重复使用）AEM用户组，以授予对包含由GraphQL API公开的内容的资产文件夹的访问权限。

#### 选择身份验证方案{#publish-permissions-users}

的 [AEM Headless SDK](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) 支持两种类型的身份验证：

* [基于令牌的身份验证](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) 使用绑定到单个技术帐户的服务凭据。
* 使用AEM用户进行基本身份验证。

### 访问GraphQL API

提供 [适当的身份验证凭据](https://github.com/adobe/aem-headless-client-js#create-aemheadless-client) 对于AEM发布服务的GraphQL API端点，包括凭据有权读取的内容以及可匿名访问的内容。 GraphQL API的其他用户无法读取受CUG保护的文件夹中的内容。

