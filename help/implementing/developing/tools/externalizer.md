---
title: 将URL外部化
description: 外部化器是一种OSGi服务，允许您以编程方式将资源路径转换为外部和绝对URL。
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# 将URL外部化 {#externalizing-urls}

在AEM中，**外部化器**&#x200B;是一种OSGi服务，通过为路径添加预配置的DNS作为前缀，该服务允许您以编程方式将资源路径（例如`/path/to/my/page`）转换为外部和绝对URL（例如`https://www.mycompany.com/path/to/my/page`）。

由于AEM as a Cloud Service实例无法知道其外部可见URL，并且有时必须在请求范围之外创建链接，因此此服务提供了一个中心位置来配置并构建这些外部URL。

本文介绍了如何配置Externalizer服务及其使用方法。 有关服务的技术详细信息，请参阅[Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html)。

## 外部化器的默认行为以及如何覆盖 {#default-behavior}

现成的Externalizer服务将几个域标识符映射到与为环境生成的AEM服务URL匹配的绝对URL前缀，例如`author https://author-p12345-e6789.adobeaemcloud.com`和`publish https://publish-p12345-e6789.adobeaemcloud.com`。 其中每个默认域的基本URL均从Cloud Manager定义的环境变量中读取。

作为参考，`com.day.cq.commons.impl.ExternalizerImpl.cfg.json`的默认OSGi配置有效：

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
>OSGi配置中的默认`local`、`author`、`preview`和`publish`外部化器域映射必须使用上面列出的原始`$[env:...]`值保留。
>
>将自定义`com.day.cq.commons.impl.ExternalizerImpl.cfg.json`文件部署到省略了这些现成域映射的AEM as a Cloud Service可能会导致应用程序出现不可预测的行为。

要覆盖`preview`和`publish`值，请使用Cloud Manager环境变量，如[为AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties)配置OSGi并设置预定义的`AEM_CDN_DOMAIN_PUBLISH`和`AEM_CDN_DOMAIN_PREVIEW`变量一文中所述。

## 配置Externalizer服务 {#configuring-the-externalizer-service}

使用Externalizer服务，您可以集中定义可用于以编程方式为资源路径添加前缀的域。 Externalizer服务只应用于具有单个域的应用程序。

>[!NOTE]
>
>与为AEM as a Cloud Service](/help/implementing/deploying/overview.md#osgi-configuration)应用任何[OSGi配置时一样，应在本地开发人员实例上执行以下步骤，然后提交到项目代码以进行部署。

要为Externalizer服务定义域映射，请执行以下操作：

1. 通过以下方式导航到Configuration Manager：

   `https://<host>:<port>/system/console/configMgr`

1. 单击&#x200B;**Day CQ Link Externalizer**&#x200B;以打开配置对话框。

   ![外部化器OSGi配置](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >配置的直接链接是`https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. 定义&#x200B;**域**&#x200B;映射。 映射由唯一名称组成，该名称可在代码中用于引用域、空间和域：

   `<unique-name> [scheme://]server[:port][/contextpath]`

   其中：

   * **`scheme`**&#x200B;通常为http或https，但可以是其他协议。

      * Adobe建议使用https来强制https链接。
      * 如果客户端代码在请求URL外部化时未覆盖方案，则使用此选项。

   * **`server`**&#x200B;是主机名（域名或ip地址）。
   * **`port`** （可选）是端口号。
   * 仅当AEM作为Web应用程序安装在不同的上下文路径下时，才会设置&#x200B;**`contextpath`**（可选）。

   例如：`production https://my.production.instance`

   以下映射名称是预定义名称，必须始终设置为AEM依赖于它们：

   * `local` — 本地实例
   * `author` — 创作系统DNS
   * `publish` — 面向公众的网站DNS

   >[!NOTE]
   >
   >自定义配置允许您添加新类别，如`production`、`staging`，甚至可以添加外部非AEM系统，如`my-internal-webservice`。 避免在项目代码库的不同位置对这些URL进行硬编码很有用。

1. 单击&#x200B;**保存**&#x200B;以保存更改。

### 使用Externalizer服务 {#using-the-externalizer-service}

此部分显示了如何使用Externalizer服务的几个示例。

>[!NOTE]
>
>不应在HTML的上下文中创建绝对链接。 因此，在这种情况下，请勿使用此实用程序。

* **要将具有“发布”域的路径外部化：**

  ```java
  String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
  ```

  假定域映射：

   * `publish https://www.website.com`

   * `myExternalizedUrl`最后得到的值为：

   * `https://www.website.com/contextpath/my/page.html`

* **要将具有“作者”域的路径外部化：**

  ```java
  String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
  ```

  假定域映射：

   * `author https://author.website.com`

   * `myExternalizedUrl`最后得到的值为：

   * `https://author.website.com/contextpath/my/page.html`

* **要将具有“本地”域的路径外部化：**

  ```java
  String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
  ```

  假定域映射：

   * `local https://publish-3.internal`

   * `myExternalizedUrl`最后得到的值为：

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>您可以在[Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html)中找到更多示例。
