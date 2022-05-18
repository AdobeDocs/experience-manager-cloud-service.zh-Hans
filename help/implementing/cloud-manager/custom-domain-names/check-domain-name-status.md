---
title: 正在检查域名状态
description: 了解如何确定Cloud Manager是否成功验证了您的自定义域名。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: ba0226b5ad3852dd5f72dd7e0ace650035f5ac6a
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# 正在检查域名状态 {#check-status}

您可以在Cloud Manager中确定自定义域名的状态。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **环境** 屏幕 **概述** 页面。

1. 单击 **域设置** 中。

1. 单击 **状态** 图标。

Cloud Manager将通过TXT值验证域所有权，并显示以下状态消息之一。

* **域验证失败** - TXT值缺失或检测到有错误。

   * 按照提供的说明解决问题。
   * 准备就绪后，必须选择 **再次验证** 图标。

* **正在进行域验证**  — 正在进行核查。

   * 此状态通常在您选择 **再次验证** 图标。

* **已验证，部署失败** - TXT验证成功，但CDN部署失败。

   * 在这种情况下，请联系您的Adobe代表。

* **域验证和部署**  — 此状态表示您的自定义域名已准备就绪，可供使用。

   * 此时，您的自定义域名已准备就绪，可供测试，并将其指向Cloud Manager域名。
   * 请参阅该文档 [配置DNS设置](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) 以了解更多。

* **删除**  — 正在删除自定义域名。

* **删除失败**  — 删除自定义域名失败，必须重试。

   * 请参阅该文档 [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) 以了解更多。

在您选择 **保存** 关于 **添加自定义域** 向导。 对于后续的验证，必须主动选择状态旁边的再次验证图标。

## 域名错误 {#domain-error}

本节将介绍您可能看到的错误以及如何解决这些错误。

**未安装域**  — 在TXT记录的域验证期间，即使已检查记录是否已正确更新，您仍会收到此错误。

**错误说明**  — 快速将域锁定到注册该域的初始帐户，任何其他帐户都无需请求权限即可注册子域。 此外，Fastly仅允许您将一个顶域和相关子域分配给一个Fastly服务和帐户。 如果您现有的Fastly帐户将AEM Cloud Service域所使用的相同顶点和子域链接在一起，则会看到此错误。

**错误解决**  — 错误已修复，如下所示：

* 在Cloud Manager中安装域之前，请从现有帐户中删除该域的顶点和子域。 使用此选项可将顶点域和所有子域链接到AEMas a Cloud ServiceFastly帐户。 请参阅 [在Fastly文档中使用域](https://docs.fastly.com/en/guides/working-with-domains) 以了解更多详细信息。

* 如果您的Apex域有多个要链接到不同Fastly帐户的AEMas a Cloud Service网站和非AEMas a Cloud Service网站的子域，请尝试在Cloud Manager中安装该域，如果域安装失败，请使用Fastly创建客户支持票证，以便我们可以代表您跟踪Fastly。

>[!NOTE]
>
>注意：如果未成功安装域，请勿将网站的DNS路由到AEMas a Cloud ServiceIP。

## 针对自定义域名的预先存在的CDN配置 {#pre-existing-cdn}

如果您的自定义域名已预先存在CDN配置，则 **自定义域名** 和 **环境** 页面，鼓励您通过UI添加这些配置，以便它们在Cloud Manager中可见且可配置。

使用UI迁移所有预先存在的环境配置后，该消息会消失。 消息可能需要1-2个工作日才能消失。

请参阅该文档 [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) 以了解更多详细信息。
