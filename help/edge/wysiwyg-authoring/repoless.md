---
title: 跨 Sites 重用代码
description: 如果您有许多相似的网站，这些网站的外观和行为大致相同，但内容不同，那么您可以了解如何在一个重写模型中跨多个网站共享代码。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 2%

---

# 跨 Sites 重用代码 {#repoless}

如果您有许多相似的网站，这些网站的外观和行为大致相同，但内容不同，那么您可以了解如何在一个重写模型中跨多个网站共享代码。

## 一个用于多个站点的代码库 {#one-codebase}

默认情况下，AEM会与您的代码存储库紧密绑定，从而满足大多数用例的要求。 但是，您可能具有多个主要内容不同的网站，但这些网站可以利用相同的代码库。

AEM支持从同一代码库运行多个站点，而不是创建多个GitHub存储库并在专用GitHub存储库之外运行每个站点，同时保持同步。

这种简化的设置免除了代码复制的需要，也称为[“repoless”](https://www.aem.live/docs/repoless)，因为除了您的第一个站点之外，其他所有站点都不需要自己的GitHub存储库。

如果您的项目需要跨站点重新使用代码的可重复灵活性，则可以激活该功能。

无论您最终希望以策略方式创建多少个站点，都必须创建您的第一个站点，该站点将用作您的基础站点。 本文档说明如何创建您的第一个站点以供重复使用。

## 先决条件 {#prerequisites}

要利用此功能，请确保您已完成以下操作。

* 按照文档[使用Edge Delivery Services进行WYSIWYG创作的开发人员快速入门指南](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)，已完全设置您的网站。
* 您至少正在运行AEM as a Cloud Service 2024.08 。

您还需要请求Adobe为您配置以下项目。 通过您的Slack渠道联系或提出支持问题以请求Adobe做出这些更改：

* 请求为您的环境激活[aem.live配置服务](https://www.aem.live/docs/config-service-setup#prerequisites)，并配置为管理员。
* 请求通过Adobe为您的项目启用可拒绝功能。
* 请求Adobe为您创建组织。

## 激活重写功能 {#activate}

要激活项目的重写功能，需要执行多个步骤。

1. [检索访问令牌](#access-token)
1. [设置配置服务](#config-service)
1. [添加站点配置和技术帐户](#access-control)
1. [更新AEM配置](#update-aem)
1. [验证站点](#authenticate-site)

这些步骤以站点`https://wknd.site`为例。 适当地替换您自己的代码。

### 检索访问令牌 {#access-token}

您首先需要访问令牌才能使用配置服务并将其配置为可重用用例。

1. 转到`https://admin.hlx.page/login`并使用`login_adobe`地址登录Adobe身份提供程序。
1. 您将被转发到`https://admin.hlx.page/profile`。
1. 通过使用浏览器的开发人员工具，从`admin.hlx.page`页面设置的JSON Web令牌Cookie中复制`x-auth-token`的值。

获取访问令牌后，即可在cURL请求的标头中按以下格式传递。

```text
--header 'x-auth-token: <your-token>'
```

### 为站点配置添加路径映射并设置技术帐户 {#access-control}

您需要创建站点配置并将其添加到路径映射中。

1. 在站点的根目录下创建一个新页面，然后选择&#x200B;[**配置**&#x200B;模板](/help/edge/wysiwyg-authoring/tabular-data.md#other)。
   * 您可以将配置留空，只保留预定义的`key`和`value`列。 您只需创建它。
1. 使用类似于以下内容的cURL命令，在公共配置中创建到站点配置的映射。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/<your-site-content>/:/",
               "/content/<your-site-content>/configuration:/.helix/config.json"
      ],
           "includes": [
               "/content/<your-site-content>/"
           ]
       }
   }'
   ```
1. 验证是否已设置公共配置以及是否可以使用类似于以下内容的cURL命令。

   ```text
   curl 'https://main--<your-aem-project>--<your-github-org>.aem.live/config.json'
   ```

映射站点配置后，您可以通过定义技术帐户来配置访问控制，使其具有发布权限。

1. 登录到AEM创作实例，然后转到&#x200B;**工具** -> **Cloud Services** -> **Edge Delivery Services配置**，选择为您的站点自动创建的配置，然后点按或单击工具栏中的&#x200B;**属性**。

1. 在&#x200B;**Edge Delivery Services配置**&#x200B;窗口中，选择&#x200B;**身份验证**&#x200B;选项卡，并复制&#x200B;**技术帐户ID**&#x200B;的值。

   * 它类似于`<tech-account-id>@techacct.adobe.com`
   * 对于单个AEM创作环境中的所有站点，技术帐户是相同的。

1. 使用类似于以下内容的cURL命令，使用您复制的技术帐户ID为您的重写配置设置技术帐户。

   * 调整`admin`块以定义应具有网站的完全管理访问权限的用户。
      * 它是一个电子邮件地址数组。
      * 可使用通配符`*`。
      * 有关详细信息，请参阅文档[为作者配置身份验证](https://www.aem.live/docs/authentication-setup-authoring#default-roles)。

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/access.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "admin": {
           "role": {
               "admin": [
                   "<email>@<domain>.<tld>"
               ],
               "config_admin": [
                   "<tech-account-id>@techacct.adobe.com"
               ]
           },
           "requireAuth": "auto"
       }
   }'
   ```

由于您现在使用配置服务，因此可从Git存储库中删除`fstab.yaml`和`paths.json`。

>[!NOTE]
>
>通过使用配置服务并通过`config.json`公开路径映射，将忽略`path.json`文件。

在将AEM配置为可重复使用后，您必须使用配置服务并提供包含路径映射的有效`config.json`。

### 更新AEM配置 {#update-aem}

现在，您已准备好对AEM中的Edge Delivery Services进行必要的更改。

1. 登录到AEM创作实例，然后转到&#x200B;**工具** -> **Cloud Services** -> **Edge Delivery Services配置**，选择为您的站点自动创建的配置，然后点按或单击工具栏中的&#x200B;**属性**。
1. 在&#x200B;**Edge Delivery Services配置**&#x200B;窗口中，将项目类型更改为&#x200B;**aem.live并设置**，然后点按或单击&#x200B;**保存并关闭**。
   ![Edge Delivery Services配置](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. 使用通用编辑器返回您的站点，并确保该站点仍然正确呈现。
1. 修改部分内容并重新发布。
1. 访问您在`https://main--<your-aem-project>--<your-github-org>.aem.page/`发布的网站，并确认更改已正确反映。

您的项目现已设置为可重复使用。

## 后续步骤 {#next-steps}

现在，您的基础站点已配置为可重复使用，您可以创建其他利用相同代码库的站点。 根据您的用例，请参阅以下文档。

* [无重复多 Site 管理](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [无重复阶段和生产环境](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)
* [用于内容创作的站点身份验证](/help/edge/wysiwyg-authoring/site-authentication.md)

## 疑难解答 {#troubleshooting}

在配置可重用用例后，最常见的问题是：通用编辑器中的页面不再呈现，或者您收到白色页面或一般AEM as a Cloud Service错误消息。 在这种情况下：

* 查看已渲染页面的源。
   * 是否实际呈现了一些内容(包含`scripts.js`、`aem.js`和编辑器相关JSON文件的正确HTML标头)？
* 检查创作实例的AEM `error.log`是否存在异常。
   * 最常见的问题是页面组件因404错误而失败。
   * 无法加载`config.json or paths.json`
   * `component-definition.json`等 无法加载
