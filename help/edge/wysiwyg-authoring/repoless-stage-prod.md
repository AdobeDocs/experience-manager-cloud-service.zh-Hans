---
title: 重写暂存和生产环境
description: 了解如何通过不断利用单个代码库为您的暂存和生产环境设置单独的站点。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 709d0661286d023c5cec51be2c51a1123ef7deb6
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---


# 重写暂存和生产环境 {#repoless-stage-prod}

了解如何通过不断利用单个代码库为您的暂存和生产环境设置单独的站点。

## 概述 {#overview}

您可能希望为独立于暂存环境的生产环境设置站点。 为单独的暂存和生产设置设置设置第二个站点类似于多站点管理所需的[设置。](/help/edge/wysiwyg-authoring/repoless-msm.md)实际上，如果需要，它可以与MSM站点结构相结合。

本文档使用单独的暂存环境和生产环境的典型示例。 您可以为所需的任何环境创建单独的环境。

## 配置 {#configuration}

本文档介绍如何使用相同的代码库为您的项目设置单独的生产站点。 下列假设成立。

* 暂存站点已设置，您现在要为生产站点创建配置。
* AEM创作中的内容结构类似。
* 相同的路径映射将用于暂存和生产。

在本例中，我们假设已经为名为wknd的项目（其GitHub存储库也称为wknd）创建了生产站点。

配置单独的生产站点需要两个步骤。

1. [为您的生产环境创建新的Edge Delivery Services站点。](#create-edge-site)
1. [在AEM中为生产站点更新云配置。](#update-cloud-configuration)

### 为您的生产环境创建新的Edge Delivery Services站点 {#create-edge-site}

1. 检索您的身份验证令牌和项目的技术帐户。
   * 有关如何[获取访问令牌](/help/edge/wysiwyg-authoring/repoless.md#access-token)和程序的[技术帐户](/help/edge/wysiwyg-authoring/repoless.md#access-control)的详细信息，请参阅文档&#x200B;**跨站点重用代码**。
1. 通过以下方式调用配置服务来创建新站点。 请考虑：
   * POSTURL中的项目名称必须是您正在创建的新站点名称。 在此示例中，它是`wknd-prod`。
   * `code`配置应与您在初始项目创建时使用的配置相同。
   * `content` > `source` > `url`必须调整为您正在创建的新站点的名称。 在此示例中，它是`wknd-prod`。
   * 即POSTURL中的网站名称必须与`content` > `source` > `url`相同。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
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
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-prod/main",
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
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-prod/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/:/"
           ],
           "includes": [
               "/content/wknd/"
           ]
       }
   }'
   ```

通过调用`https://main--wknd-prod--<your-github-org>.aem.page/config.json`并验证返回的JSON的内容，验证新站点的公共配置是否正常工作。

### 在AEM中为生产站点更新云配置 {#update-cloud-configuration}

必须将您的生产AEM配置为将您在上一部分中创建的新Edge Delivery站点用于专用生产站点。 在此示例中，生产环境中`/content/wknd`下的内容需要知道是否使用您创建的`wknd-prod`站点。

1. 登录到AEM生产实例，然后转到&#x200B;**工具** -> **Cloud Service** -> **Edge Delivery Services配置**。
1. 选择为您的项目自动创建的配置。
1. 点按或单击工具栏中的&#x200B;**属性**。
1. 在&#x200B;**Edge Delivery Services配置**&#x200B;窗口中：
   * 在&#x200B;**组织**&#x200B;字段中提供您的GitHub组织。
   * 将站点名称更改为您在上一部分中创建的站点名称。 在这种情况下，那将为`wknd-prod`。
   * 使用重写配置设置&#x200B;**将项目类型更改为** aem.live。
1. 点按或单击&#x200B;**保存并关闭**。

## 验证设置 {#verify}

现在，您已进行了所有必要的配置更改，请确认一切都按预期运行。

1. 登录您的AEM生产创作实例。
1. 通过转至&#x200B;**导航** -> **站点**&#x200B;来导航到&#x200B;**站点控制台**。
1. 在您的网站中选择一个页面。
1. 点按或单击工具栏中的&#x200B;**编辑**。
1. 确保页面在通用编辑器中正确呈现，并使用与站点根相同的代码。
1. 对页面进行更改并重新发布。
1. 在`https://main--wknd-prod--<your-github-org>.aem.page`访问您的新的Edge Delivery Services网站。

如果您看到所做的更改，则表明您单独的生产站点设置运行正常。
