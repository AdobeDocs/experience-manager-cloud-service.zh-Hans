---
title: 重写多站点管理
description: 了解最佳实践建议，了解如何使用利用单个代码库(每个代码库由Edge Delivery Services提供)的本地化站点，以可靠的方式设置项目。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: e25e21984ebadde7076d95c6051b8bfca5b2ce03
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 1%

---


# 重写多站点管理 {#repoless-msm}

了解最佳实践建议，了解如何使用利用单个代码库(每个代码库由Edge Delivery Services提供)的本地化站点，以可靠的方式设置项目。

## 概述 {#overview}

[多站点管理器(MSM)](/help/sites-cloud/administering/msm/overview.md)及其Live Copy功能允许您在多个位置使用相同的站点内容，并允许进行更改。 您可以创作内容一次并创建活动副本。 MSM维护源内容及其活动副本之间的实时关系，以便在您更改源内容时，可以同步源和活动副本。

您可以使用MSM跨区域设置和语言为品牌创建整个内容结构，并集中创作内容。 然后，利用中心代码库，Edge Delivery Services可以交付每个本地化的网站。

## 要求 {#requirements}

要在可重用用例中配置MSM，必须首先完成多项任务。

* 本文档假定您已根据《使用Edge Delivery Services创作WYSIWYG的[开发人员快速入门指南》](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)为项目创建了一个站点。
* 您必须已[为项目启用重写功能。](/help/edge/wysiwyg-authoring/repoless.md)

## 用例 {#use-case}

本文档假设您已经为项目创建了基本的本地化站点结构。 对于在瑞士和德国开展业务的wknd品牌，它使用以下结构。

```text
/content/wknd
/content/wknd/language-masters
/content/wknd/language-masters/en
/content/wknd/language-masters/de
/content/wknd/language-masters/fr
/content/wknd/language-masters/it
/content/wknd/ch
/content/wknd/ch/de
/content/wknd/ch/fr
/content/wknd/ch/it
/content/wknd/ch/en
/content/wknd/de
/content/wknd/de/de
/content/wknd/de/en
```

`language-masters`中的内容是本地化站点的活动副本源：德国(`de`)和瑞士(`ch`)。 本文档的目标是创建Edge Delivery Services站点，这些站点对每个本地化站点都使用相同的代码库。

## 配置 {#configuration}

配置MSM重写使用案例有几个步骤。

1. [更新AEM站点配置。](#update-aem-configurations)
1. [为本地化Edge Delivery Services创建新的页面站点。](#create-edge-sites)
1. [在AEM中为本地化的站点更新云配置。](#update-cloud-configurations)

### 更新AEM站点配置 {#update-aem-configurations}

[配置](/help/implementing/developing/introduction/configurations.md)可视为工作区，可用于收集设置组及其关联内容以进行组织。 在AEM中创建站点时，会自动为其创建配置。

您通常希望在网站之间共享某些内容，例如：

* 从Blueprint中的内容创建的模板
* 内容片段模型、持久、查询等。

您可以创建其他配置来促进此类共享。 对于wknd用例，我们需要配置以下路径。

```text
/content/wknd
/content/wknd/ch
/content/wknd/de
```

也就是说，您将具有由Blueprint使用的wknd品牌内容(`/content/wknd`)的根的配置以及由每个本地化站点（瑞士和德国）使用的配置。

1. 登录您的AEM创作实例。
1. 通过转至&#x200B;**工具** -> **常规** -> **配置浏览器**&#x200B;导航到&#x200B;**配置浏览器**。
1. 选择为您的项目自动创建的配置（在本例中为wknd），然后点按或单击工具栏中的&#x200B;**创建**。
1. 在&#x200B;**创建配置**&#x200B;对话框中，为您的本地化站点（如`Switzerland`）提供描述性&#x200B;**名称**，对于&#x200B;**标题**，使用与本地化大小相同的标题（在此例中为`ch`）。
1. 选择&#x200B;**云配置**&#x200B;功能以及您的项目可能需要的任何其他功能，如&#x200B;**可编辑模板**。
1. 点击或单击“**创建**”。

为您需要的每个本地化站点创建配置。 对于wknd，您需要为`de`创建配置以及`ch`配置。

创建配置后，您需要确保本地化的网站使用它们。

1. 登录您的AEM创作实例。
1. 通过转至&#x200B;**导航** -> **站点**&#x200B;来导航到&#x200B;**站点控制台**。
1. 选择本地化的网站，如`Switzerland`。
1. 点按或单击工具栏中的&#x200B;**属性**。
1. 在页面属性窗口中，选择&#x200B;**高级**&#x200B;选项卡，在&#x200B;**配置**&#x200B;标题下，取消选择&#x200B;**继承自/content/wknd**&#x200B;选项，其中`wknd`是站点根。
1. 在&#x200B;**云配置**&#x200B;字段中，使用路径浏览器选择您为本地化站点创建的配置，如`/conf/wknd/ch`下的`Switzerland`。
1. 点按或单击&#x200B;**保存并关闭**。

将相应的配置分配给其他本地化的站点。 对于wknd，您还需要将`/conf/wknd/de`配置分配给德国站点。

### 为您的本地化Edge Delivery Services创建新的页面站点 {#create-edge-sites}

要将更多站点连接到Edge Delivery Services以进行多区域、多语言站点设置，您必须为每个AEM MSM站点设置新的aem.live站点。 AEM MSM Sites与具有共享Git存储库和代码库的aem.live站点之间存在1:1的关系。

对于此示例，我们将为瑞士存在wknd创建站点`wknd-ch`，其本地化内容位于AEM路径`/content/wknd/ch`下。

1. 检索您的身份验证令牌和项目的技术帐户。
   * 有关如何[获取访问令牌](/help/edge/wysiwyg-authoring/repoless.md#access-token)和程序的[技术帐户](/help/edge/wysiwyg-authoring/repoless.md#access-control)的详细信息，请参阅文档&#x200B;**跨站点重用代码**。
1. 通过以下方式调用配置服务来创建新站点。 请考虑：
   * POSTURL中的项目名称必须是您正在创建的新站点名称。 在此示例中，它是`wknd-ch`。
   * `code`配置应与您在初始项目创建时使用的配置相同。
   * `content` > `source` > `url`必须调整为您正在创建的新站点的名称。 在此示例中，它是`wknd-ch`。
   * 即POSTURL中的网站名称必须与`content` > `source` > `url`相同。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "code": {
           "owner": "<your-github-org>",
           "repo": "wknd",
           "source": {
               "type": "github",
               "url": "https://github.com/<your-github-org>/wknd"
           }
       },
       "content": {
           "source": {
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-ch/main",
               "type": "markup",
               "suffix": ".html"
           }
       },
       "access": {
           "admin": {
               "role": {
                   "admin": [
                       "*@adobe.com"
                   ],
                   "publish": [
                       "<tech-account-id>@techacct.adobe.com"
                   ]
               },
               "requireAuth": "auto"
           }
       }
   }'
   ```

1. 通过对配置服务进行以下调用，为新站点添加路径映射。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/ch/:/"
           ],
           "includes": [
               "/content/wknd/ch/"
           ]
       }
   }'
   ```

1. 通过调用`https://main--wknd-ch--<your-github-org>.aem.page/config.json`并验证返回的JSON的内容，验证新站点的公共配置是否正常工作。

重复这些步骤以创建其他本地化的站点。 对于wknd，您还需要为德语版创建一个`wknd-de`站点。

### 在AEM中为本地化页面更新云配置 {#update-cloud-configurations}

必须将您在AEM中的页面配置为使用您在上一部分中创建的新Edge Delivery站点，以便进行本地化呈现。 在此示例中，`/content/wknd/ch`下的内容需要知道是否使用您创建的`wknd-ch`站点。 同样，`/content/wknd/de`下的内容需要使用`wknd-de`站点。

1. 登录AEM创作实例并转到&#x200B;**工具** -> **Cloud Service** -> **Edge Delivery Services配置**。
1. 选择为您的项目自动创建的配置，然后选择为本地化页面创建的文件夹。 在本例中，就是瑞士(`ch`)。
1. 在工具栏中点按或单击&#x200B;**创建** > **配置**。
1. 在&#x200B;**Edge Delivery Services配置**&#x200B;窗口中：
   * 在&#x200B;**组织**&#x200B;字段中提供您的GitHub组织。
   * 将站点名称更改为您在上一部分中创建的站点名称。 在这种情况下，那将为`wknd-ch`。
   * 使用重写配置设置&#x200B;**将项目类型更改为** aem.live。
1. 点按或单击&#x200B;**保存并关闭**。

## 验证设置 {#verify}

现在，您已进行了所有必要的配置更改，请确认一切都按预期运行。

1. 登录您的AEM创作实例。
1. 通过转至&#x200B;**导航** -> **站点**&#x200B;来导航到&#x200B;**站点控制台**。
1. 选择本地化的网站，如`Switzerland`。
1. 点按或单击工具栏中的&#x200B;**编辑**。
1. 确保页面在通用编辑器中正确呈现，并使用与站点根相同的代码。
1. 对页面进行更改并重新发布。
1. 访问您的新Edge Delivery Services网站以了解该本地化页面，网址为`https://main--wknd-ch--<your-github-org>.aem.page`。

如果看到您所做的更改，则表示MSM设置运行正常。
