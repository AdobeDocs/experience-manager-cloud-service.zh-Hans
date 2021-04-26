---
title: 外部化URL
description: Externalizer是一个OSGi服务，它允许您以编程方式将资源路径转换为外部和绝对URL。
translation-type: tm+mt
source-git-commit: 4c584ceadaa358120d1d4b4cabd7e21ced814b31
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---


# 将URL外部化{#externalizing-urls}

在AEM中，**Externalizer**&#x200B;是一个OSGi服务，它允许您以编程方式转换资源路径(例如，`/path/to/my/page`)，通过预先配置DNS来预装路径，从而将其添加到外部和绝对URL（例如`https://www.mycompany.com/path/to/my/page`）中。

由于AEM作为Cloud Service实例无法知道其外部可见的URL，并且由于有时必须在请求范围之外创建链接，因此此服务提供了一个中心位置来配置这些外部URL并构建它们。

本文介绍如何配置Externalizer服务以及如何使用它。 有关服务的技术详细信息，请参阅[Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html)。

## Externalizer的默认行为和如何覆盖{#default-behavior}

现成的Externalizer服务已设置`author-p12345-e6789.adobeaemcloud.com`和`publish-p12345-e6789.adobeaemcloud.com`等值，这样，在不进行任何干预的情况下，作为Cloud Service安装的AEM将使用您的自定义域。

要覆盖此类值，请使用Cloud Manager环境变量，如文章[将AEM的OSGi配置为Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties)中所述，并设置预定义的`AEM_CDN_DOMAIN_AUTHOR`和`AEM_CDN_DOMAIN_PUBLISH`变量。

## 配置Externalizer服务{#configuring-the-externalizer-service}

Externalizer服务允许您集中定义可用于以编程方式为资源路径添加前缀的域。 Externalizer服务应仅用于具有单个域的应用程序。

>[!NOTE]
>
>与将AEM的任何[OSGi配置应用为Cloud Service时一样，](/help/implementing/deploying/overview.md#osgi-configuration)应对本地开发人员实例执行以下步骤，然后将其提交到您的项目代码进行部署。

要为Externalizer服务定义域映射，请执行以下操作：

1. 通过以下方式导航到Configuration Manager:

   `https://<host>:<port>/system/console/configMgr`

1. 单击&#x200B;**Day CQ Link Externalizer**&#x200B;打开配置对话框。

   ![Externalizer OSGi配置](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >指向配置的直接链接为`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. 定义&#x200B;**域**&#x200B;映射。 映射由唯一名称组成，该名称可用于代码中引用域、空格和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   地点：

   * **`scheme`** 通常是http或https，但可以是其他协议。

      * 建议使用https来强制使用https链接。
      * 如果客户端代码在请求将URL外部化时不覆盖方案，则将使用它。
   * **`server`** 是主机名（域名或ip地址）。
   * **`port`** （可选）是端口号。
   * **`contextpath`** （可选）仅在AEM作为web应用程序安装在其他上下文路径下时才设置。

   例如：`production https://my.production.instance`

   以下映射名称是预定义的，因为AEM依赖它们，因此必须始终设置它们：

   * `local`  — 本地实例
   * `author`  — 创作系统DNS
   * `publish`  — 面向公众的网站DNS

   >[!NOTE]
   >
   >自定义配置允许您添加新的类别，如`production`、`staging`，甚至外部非AEM系统，如`my-internal-webservice`。 避免在项目代码库的不同位置对此类URL进行硬编码很有用。

1. 单击&#x200B;**保存**&#x200B;以保存更改。

### 使用Externalizer服务{#using-the-externalizer-service}

本节介绍如何使用Externalizer服务的几个示例。

>[!NOTE]
>
>不应在HTML的上下文中创建绝对链接。 因此，不应在此类情况下使用此实用程序。

* **要将具有“publish”域的路径外部化，请执行以下操作：**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   假设域映射：

   * `publish https://www.website.com`

   * `myExternalizedUrl` 最后是值：

   * `https://www.website.com/contextpath/my/page.html`

* **要将具有“author”域的路径外部化：**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   假设域映射：

   * `author https://author.website.com`

   * `myExternalizedUrl` 最后是值：

   * `https://author.website.com/contextpath/my/page.html`

* **要将具有“local”域的路径外部化：**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   假设域映射：

   * `local https://publish-3.internal`

   * `myExternalizedUrl` 最后是值：

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>您可以在[Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html)中找到更多示例。
