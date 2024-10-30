---
title: 无管道URL重定向
description: 了解如何在没有访问Git或Cloud Manager管道的情况下声明301或302重定向。
feature: Dispatcher
role: Admin
source-git-commit: 567c75f456f609dbc254753b439151d0f4100bc0
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# 无管道URL重定向 {#pipeline-free-redirects}

>[!NOTE]
>此功能尚未发布。

由于各种原因，组织会重写URL，从而导致301（或302）重定向，这意味着浏览器会被重定向到不同的页面。

这些情况包括：

* 已移除HTML页面，因此用户将被带入替换页面（有时是主页），而不会看到`404 Page Not Found`错误。
* 重命名的HTML页面。
* seo优化。

AEM as a Cloud Service提供了[多种方法来实施客户端重定向](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/url-redirection)，但在以下情况下，本文中所述的策略（管道免费重定向）是很好的选择：

* 维护重定向的人员是业务用户，他们无权将文件更改提交到源代码管理或执行Cloud Manager Web层配置管道。
* 重定向的数量范围从数到数万不等。
* 您需要用户界面的选项，该选项是作为自定义项目创建的，或者通过使用[ACS Commons Rewrite Map Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html)创建的。

此功能的核心是AEM Apache/Dispatcher能够加载（或重新加载）一个或多个已放置在发布存储库中指定位置中的重写映射文件。 请务必注意，文件到达的方式超出了此功能的范围，但您可以考虑以下方法之一：

* 在创作用户界面中将重写映射摄取为资产并进行发布。
* 安装[ACS Commons重写映射管理器](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html)，该管理器包括一个用于管理url映射的用户界面，并且还可以发布重写映射文件。
* 通过编写自定义应用程序实现完全的灵活性。 例如，使用用户界面或命令行界面管理url映射，或者使用表单上传重写映射，然后使用AEM API发布重写映射文件。

>[!NOTE]
> 此功能需要AEM版本&#x200B;**18311或更高版本**。

## 重写映射 {#rewrite-map}

默认情况下，Apache HTTP服务器每300秒重新加载一次重写映射（如果更改）（该值可配置）。 文件格式应遵循[Apache文档](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html#txt)中描述的纯文本键值映射RewriteMap文件格式。

应创建名为`managed-rewrite-maps.yaml`的文件以指定重写映射文件的位置，并且必须使用Cloud Manager全栈栈管道或Web层管道部署该文件一次。 该文件必须在Dispatcher配置的[src/选择加入](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud/src/opt-in)文件夹中创建。 确保使用[灵活模式文件结构](/help/implementing/dispatcher/validation-debug.md#flexible-mode-file-structure)。

您可以使用以下模式对其进行配置：

```
maps:
- name: my.map
  path: <path-in-publish-repository>/redirectmap.txt
```

例如，如果您选择的放置重写映射文件的方法是将它作为名为`mysite-redirectmap.txt`的资源摄取到AEM中，然后发布，则可以在`/content/dam`下指定一个文件夹：

```
maps:
- name: my.map
  path: /content/dam/redirectmaps/mysite-redirectmap.txt
```

接下来，在Apache配置文件（如`rewrites/rewrite.rules`或`<yourfile>.vhost`）中，必须配置名称属性（上述示例中的`my.map`）引用的映射文件。

`RewriteMap`指令应指示使用`sdbm` （简单DBM）格式以数据库管理器(DBM)文件格式存储数据。

其余配置将取决于`redirectmap.txt`的格式。 如下例所示，最简单的格式是在原始url与映射url之间的一对一映射：

```
# RewriteMap from managed rewrite maps
RewriteMap map.foo dbm=sdbm:/tmp/rewrites/my.map
RewriteCond ${map.foo:$1} !=""
RewriteRule ^(.*)$ ${map.foo:$1|/} [L,R=301]
```


## 注意事项 {#considerations}

请牢记以下内容：

* 默认情况下，在加载重写映射时，Apache将启动，而无需等待加载完整映射文件，因此在加载完整映射之前，可能存在临时不一致的情况。 可以更改此设置，以便Apache会等待加载完整映射内容，但Apache需要更长的时间才能启动。 若要更改此行为以便Apache等待，请将`wait:true`添加到`managed-rewrite-maps.yaml`文件。
* 要更改加载之间的频率，请将`ttl: <integer>`添加到`managed-rewrite-maps.yaml`文件中。 例如 `ttl: 120`。
* 对于RewriteMap单个条目，Apache的长度限制为1024。
