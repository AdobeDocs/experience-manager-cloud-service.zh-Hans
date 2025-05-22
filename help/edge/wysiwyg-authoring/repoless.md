---
title: 跨 Sites 重用代码
description: 如果您有许多类似的 Sites，它们的外观和行为大多相同，但内容不同，请了解如何在无重复模型中跨多个 Sites 共享代码。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '1039'
ht-degree: 100%

---

# 跨 Sites 重用代码 {#repoless}

如果您有许多类似的 Sites，它们的外观和行为大多相同，但内容不同，请了解如何在无重复模型中跨多个 Sites 共享代码。

## 多个 Sites 使用同一个代码库 {#one-codebase}

默认情况下，AEM 与您的代码存储库紧密绑定，这可以满足大多数用例的要求。但是您可能有多个 Sites，且它们的主要区别在于内容，就可以利用相同的代码库。

AEM 支持从同一个代码库运行多个 Sites，而不是创建多个 GitHub 存储库，让每个 Site 在一个专用 GitHub 存储库上运行并保持它们同步。

这样可以简化设置，无需再重复代码，这也称为[“无重复”](https://www.aem.live/docs/repoless)，因为除了第一个 Site 之外的所有其他 Sites 都不需要自己的 GitHub 存储库。

如果您的项目需要跨 Sites 重用代码的“无重复”灵活性，您可以激活该功能。

无论您最终想要以无重复方式创建多少个 Sites，您都必须创建第一个 Site 作为基础 Site。此文档说明了如何创建用于无重复使用的第一个 Site。

## 先决条件 {#prerequisites}

要利用这个功能，请确保您已完成以下任务。

* 您的 Site 已按照文档[使用 Edge Delivery Services 进行所见即所得创作的开发人员入门快速入门指南](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)完成了所有设置。
* 您至少运行 AEM as a Cloud Service 2024.08 版本。

您还需要让 Adobe 为您配置以下几项。通过您的 Slack 频道联系 Adobe，或者提出支持问题，请求 Adobe 进行以下更改：

* 为您的环境激活 [aem.live 配置服务](https://www.aem.live/docs/config-service-setup#prerequisites)，并将您配置为管理员。
* 请 Adobe 为您的程序启用无重复功能。
* 请 Adobe 为您创建组织。

## 激活无重复功能 {#activate}

为您的项目激活无重复功能分为几个步骤。

1. [检索访问令牌](#access-token)
1. [设置配置服务](#config-service)
1. [添加 Site 配置和技术帐户](#access-control)
1. [更新 AEM 配置](#update-aem)
1. [对 Site 进行身份验证](#authenticate-site)

这些步骤以 Site `https://wknd.site` 为例。适当替换成您自己的 Site。

### 检索访问令牌 {#access-token}

您首先需要一个访问令牌才能使用配置服务，并为这个无重复用例进行配置。

1. 前往 `https://admin.hlx.page/login`，然后使用 `login_adobe` 地址通过 Adobe 标识提供者登录。
1. 您将被转至 `https://admin.hlx.page/profile`。
1. 使用浏览器的开发人员工具，从 `admin.hlx.page` 页面设置的 JSON 网页令牌 cookie 中复制 `x-auth-token` 的值。

获得访问令牌后，它就可以按照以下格式传递到 cURL 请求的标头中。

```text
--header 'x-auth-token: <your-token>'
```

### 添加 Site 配置的路径映射，设置技术账户 {#access-control}

您需要创建一个 Site 配置，然后将其添加到您的路径映射中。

1. 在您的 Site 根目录创建一个新页面，然后选择&#x200B;[**配置**&#x200B;模板](/help/edge/wysiwyg-authoring/tabular-data.md#other)。
   * 您可以将配置留空，仅保留预定义的 `key` 和 `value` 两列。您只需创建它。
1. 使用类似以下示例的 cURL 命令创建一个从公开配置到 Site 配置的映射。

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
1. 使用类似如下示例的 cURL 命令验证此公开配置已设置并可用。

   ```text
   curl 'https://main--<your-aem-project>--<your-github-org>.aem.live/config.json'
   ```

映射了 Site 配置后，您可以通过定义技术帐户来配置访问控制，使其具有发布权限。

1. 登录 AEM 创作实例，然后前往&#x200B;**工具** -> **Cloud Services** -> **Edge Delivery Services 配置**，然后选择为您的 Site 自动创建的配置，然后点击或单击工具栏中的&#x200B;**属性**。

1. 在 **Edge Delivery Services 配置**&#x200B;窗口中选择&#x200B;**身份验证**&#x200B;选项卡，然后复制&#x200B;**技术帐户 ID** 的值。

   * 它看起来有点像 `<tech-account-id>@techacct.adobe.com`
   * 同一个 AEM 创作环境中的所有 Sites 的技术帐户都是相同的。

1. 使用您复制的技术帐户 ID，通过类似以下示例的 cURL 命令为您的无重复配置设置技术帐户。

   * 调整 `admin` 块，定义应该对 Site 具有完全管理访问权限的用户。
      * 这是一个电子邮件地址数组。
      * 可以使用通配符 `*`。
      * 查看文档[配置作者的身份验证](https://www.aem.live/docs/authentication-setup-authoring#default-roles)，了解更多信息。

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

由于您现在使用配置服务，因此您可以从您的 Git 存储库删除 `fstab.yaml` 和 `paths.json`。

>[!NOTE]
>
>使用配置服务并通过 `config.json` 公开路径映射后，`path.json` 文件就被忽略。

将 AEM 配置为无重复使用后，您必须使用配置服务并提供带有路径映射的有效的 `config.json`。

### 更新 AEM 配置 {#update-aem}

现在您已准备好对 AEM 中的 Edge Delivery Services 进行必要的更改。

1. 登录 AEM 创作实例，然后前往&#x200B;**工具** -> **Cloud Services** -> **Edge Delivery Services 配置**，然后选择为您的 Site 自动创建的配置，然后点击或单击工具栏中的&#x200B;**属性**。
1. 在 **Edge Delivery Services 配置**&#x200B;窗口中，将项目类型改为&#x200B;**带有无重复配置设置的 aem.live**，然后点击或单击&#x200B;**保存并关闭**。
   ![Edge Delivery Services 配置](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. 使用通用编辑器返回到您的 Site，确保它仍然能够正确渲染。
1. 更改部分内容，然后重新发布。
1. 在 `https://main--<your-aem-project>--<your-github-org>.aem.page/` 访问您发布的 Site，验证是否正确反映了刚才的更改。

现在，您的项目已设置为无重复使用。

## 后续步骤 {#next-steps}

现在您的基础 Site 已配置为无重复使用，您可以创建其他的使用相同代码库的 Sites。根据您的用例参考以下文档。

* [无重复多 Site 管理](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [无重复的暂存和生产环境](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)
* [用于内容创作的 Site 身份验证](/help/edge/wysiwyg-authoring/site-authentication.md)

## 疑难解答 {#troubleshooting}

配置无重复用例后遇到的最常见问题是通用编辑器中的页面不再渲染，或者您会收到空白页面或 AEM as a Cloud Service 的一般性错误消息。在这类情况下：

* 查看所渲染页面的来源。
   * 是否确实渲染了某些内容（HTML 标头是否是正确的 `scripts.js`、`aem.js`，与编辑器相关的 JSON 文件是否正确）？
* 检查作者实例的 AEM `error.log` 是否发生例外。
   * 最常见的问题是页面组件失败并出现 404 错误。
   * 无法加载 `config.json or paths.json`
   * 无法加载 `component-definition.json`等
