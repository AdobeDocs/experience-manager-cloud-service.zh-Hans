---
title: 外部化URL
description: Externalizer是一种OSGi服务，它允许您以编程方式将资源路径转换为外部URL和绝对URL。
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: 28903c1cbadece9d0ef575cdc0f0d7fd32219538
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# 外部化URL {#externalizing-urls}

在AEM中， **外部器** 是一种OSGi服务，它允许您以编程方式转换资源路径(例如， `/path/to/my/page`)到外部和绝对URL(例如， `https://www.mycompany.com/path/to/my/page`)，方法是使用预配置的DNS来预定路径。

由于AEMas a Cloud Service实例无法知道其外部可见的URL，并且由于有时必须在请求范围之外创建链接，因此此服务提供了一个中心位置来配置这些外部URL并构建它们。

本文介绍如何配置外部器服务及其使用方法。 有关该服务的技术详情，请参阅 [Javaocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## 外部器的默认行为和如何覆盖 {#default-behavior}

现成的Externalizer服务将一些域标识符映射到与为环境生成的AEM服务URL匹配的绝对URL前缀，例如 `author https://author-p12345-e6789.adobeaemcloud.com` 和 `publish https://publish-p12345-e6789.adobeaemcloud.com`. 每个默认域的基本URL均从Cloud Manager定义的环境变量中读取。

对于引用， `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` 有效：

```json
{
   "externalizer.domains": [
      "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
      "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
      "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]",
      "preview $[env:AEM_EXTERNALIZER_PREVIEW;default=http://localhost:4503]"
   ]
}
```

>[!CAUTION]
>
>默认 `local`, `author`, `preview`和 `publish` OSGi配置中的外部器域映射必须保留为原始 `$[env:...]` 上面列出的值。
>
>部署自定义 `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` 文件到AEM的as a Cloud Service，如果忽略这些现成域映射中的任何映射，则可能会导致无法预测的应用程序行为。

覆盖 `preview` 和 `publish` 值，请按照文章中所述使用Cloud Manager环境变量 [为AEMas a Cloud Service配置OSGi](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) 和设置预定义 `AEM_CDN_DOMAIN_PUBLISH` 和 `AEM_CDN_DOMAIN_PREVIEW` 变量。

## 配置外部器服务 {#configuring-the-externalizer-service}

Externalizer服务允许您集中定义可用于以编程方式为资源路径添加前缀的域。 外部器服务应仅用于具有单个域的应用程序。

>[!NOTE]
>
>与应用任何 [AEMas a Cloud Service的OSGi配置，](/help/implementing/deploying/overview.md#osgi-configuration) 应对本地开发人员实例执行以下步骤，然后将其提交到您的项目代码以进行部署。

要为外部器服务定义域映射，请执行以下操作：

1. 通过以下方式导航到配置管理器：

   `https://<host>:<port>/system/console/configMgr`

1. 单击 **Day CQ链接外部器** 打开配置对话框。

   ![外部器OSGi配置](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >配置的直接链接是 `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. 定义 **域** 映射。 映射由唯一名称组成，该名称可在代码中用于引用域、空格和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **`scheme`** 通常为http或https，但可以是其他协议。

      * 建议使用https来强制使用https链接。
      * 如果客户端代码在请求将URL外部化时不覆盖方案，则将使用该URL。
   * **`server`** 是主机名（域名或ip地址）。
   * **`port`** （可选）是端口号。
   * **`contextpath`** （可选）仅当AEM作为Web应用程序安装在其他上下文路径下时才进行设置。

   例如：`production https://my.production.instance`

   以下映射名称是预定义的，且必须始终设置，因为AEM依赖于这些映射名称：

   * `local`  — 本地实例
   * `author`  — 创作系统DNS
   * `publish`  — 面向公众的网站DNS

   >[!NOTE]
   >
   >自定义配置允许您添加新类别，例如 `production`, `staging` 甚至外部非AEM系统，例如 `my-internal-webservice`. 避免在项目代码库中的不同位置对此类URL进行硬编码非常有用。

1. 单击 **保存** 以保存更改。

### 使用外部器服务 {#using-the-externalizer-service}

此部分显示如何使用外部器服务的一些示例。

>[!NOTE]
>
>不应在HTML上下文中创建绝对链接。 因此，在此类情况下不应使用此实用程序。

* **要将路径外部化为“publish”域，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假设域映射：

   * `publish https://www.website.com`

   * `myExternalizedUrl` 最后是值：

   * `https://www.website.com/contextpath/my/page.html`

* **要将路径外部化为“author”域，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假设域映射：

   * `author https://author.website.com`

   * `myExternalizedUrl` 最后是值：

   * `https://author.website.com/contextpath/my/page.html`

* **要将路径外部化为“本地”域，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假设域映射：

   * `local https://publish-3.internal`

   * `myExternalizedUrl` 最后是值：

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>您可以在 [Javaocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
