---
title: 无重复多 Site 管理
description: 了解有关如何以无重复方式设置一个项目，制作全部由 Edge Delivery Services 提供支持且使用单一代码库的本地化 Sites 的最佳实践推荐。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: f6b861ed-18e4-4c81-92d2-49fadfe4669a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '1260'
ht-degree: 100%

---

# 无重复多 Site 管理 {#repoless-msm}

了解有关如何以无重复方式设置一个项目，制作全部由 Edge Delivery Services 提供支持且使用单一代码库的本地化 Sites 的最佳实践推荐。

## 概述 {#overview}

[多 Site 管理器 (MSM)](/help/sites-cloud/administering/msm/overview.md) 及其“实时副本”功能可让您在多个地点使用相同的 Site 内容，同时允许各种变体。您可以一次性创作内容，然后创建实时副本。MSM 维护您的源内容与其实时副本之间的实时关系，以便当您更改源内容时，来源和实时副本可以同步。

您可以使用 MSM 为您的品牌创建跨地区和跨语言的完整内容结构，集中进行内容创作。然后，您的每个本地化 Sites 都可以通过 Edge Delivery Services 使用一个中央代码库投放。

## 要求 {#requirements}

要在无重复用例中配置 MSM，您必须首先完成以下任务：

* 此文档假设您已经根据[使用 Edge Delivery Services 进行所见即所得创作的开发人员快速入门指南](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)为您的项目创建了一个 Site。
* 您必须已经[为您的项目启用了无重复功能](/help/edge/wysiwyg-authoring/repoless.md)。

## 用例 {#use-case}

此文档假设您已经为您的项目创建了一个基本的本地化 Site 结构。以在瑞士和德国开展业务的 wknd 品牌为例，它采用了以下结构。

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

`language-masters` 中的内容是本地化 Sites：德国（`de`）和瑞士（`ch`）的实时副本的来源。此文档的目标是创建 Edge Delivery Services Sites，为每一个本地化 Site 都使用相同的代码库。

## 配置 {#configuration}

配置 MSM 无重复用例有几个步骤。

1. [更新 AEM Site 配置](#update-aem-configurations)。
1. [为您的本地化页面创建新的 Edge Delivery Services Sites](#create-edge-sites)。
1. [在 AEM 中为您的本地化 Sites 更新云配置](#update-cloud-configurations)。

### 更新 AEM Site 配置 {#update-aem-configurations}

[配置](/help/implementing/developing/introduction/configurations.md)可被视为用于收集设置组及其相关内容以用于组织目的的工作区。当您在 AEM 中创建 Site 时，会自动为其创建一个配置。

您通常希望在 Sites 之间共享某些内容，例如：

* 从蓝图中的内容创建的模板
* 内容片段模型，持久查询等。

您可以额外创建配置来促进这种共享。在 wknd 用例中，我们需要以下路径的配置。

```text
/content/wknd
/content/wknd/ch
/content/wknd/de
```

也就是说，您将具有蓝图所使用的 wknd 品牌内容根目录 (`/content/wknd`) 的一个配置以及每个本地化 Site（瑞士和德国）所使用的一个配置。

1. 登录您的 AEM 创作实例。
1. 导航至&#x200B;**配置浏览器**，即从&#x200B;**工具** -> **常规** -> **配置浏览器**。
1. 选择为您的项目（在本例中为 wknd）自动创建的配置，然后点击或单击工具栏中的&#x200B;**创建**。
1. 在&#x200B;**创建配置**&#x200B;对话框中，为您的本地化 Site 提供一个描述性的&#x200B;**名称**（例如 `Switzerland`），然后为&#x200B;**标题**&#x200B;使用与本地化尺寸相同的标题（在本例中为 `ch`）。
1. 选择&#x200B;**云配置**&#x200B;功能以及您的项目可能需要的任何其他功能，例如&#x200B;**可编辑模板**。
1. 点击或单击&#x200B;**创建**。

为您需要的每一个本地化 Site 创建配置。在 wknd 的例子中，您需要为 `de` 创建一个配置，同时还要为 `ch` 创建一个配置。

创建了配置后，您需要确保本地化 Sites 使用它们。

1. 登录您的 AEM 创作实例。
1. 导航至&#x200B;**Sites 控制台**，即从&#x200B;**导航**  -> **Sites**。
1. 选择本地化 Site，例如 `Switzerland`。
1. 在工具栏中点击或单击&#x200B;**属性**。
1. 在页面属性窗口中选择&#x200B;**高级**&#x200B;选项卡，然后在&#x200B;**配置**&#x200B;标题下取消选择选项&#x200B;**从 /content/wknd 继承**，其中 `wknd` 是 Site 根目录。
1. 在&#x200B;**云配置**&#x200B;字段中，使用路径浏览器选择您为本地化 Site 创建的配置，例如 `/conf/wknd/ch` 下的 `Switzerland`。
1. 点击或单击&#x200B;**保存并关闭**。

将相应的配置分配给其他本地化 Sites。在 wknd 例子中，您还需要将 `/conf/wknd/de` 配置分配给德国 Site。

### 为您的本地化页面创建新的 Edge Delivery Services Sites {#create-edge-sites}

要将更多 Sites 连接到 Edge Delivery Services 以实现多区域、多语言 Site 设置，您必须为每个 AEM MSM Sites 设置一个新的 aem.live Site。AEM MSM Sites 与 aem.live Sites 之间是 1:1 的关系，具有共享的 Git 存储库和代码库。

在这个例子中，我们将为 wknd 在瑞士的运营创建 Site `wknd-ch`，其本地化内容位于 AEM 路径 `/content/wknd/ch`。

1. 为您的程序检索授权令牌和技术帐户。
   * 请参阅文档&#x200B;**跨 Sites 重用代码**，了解如何为您的程序[获取您的访问令牌](/help/edge/wysiwyg-authoring/repoless.md#access-token)和[技术帐户](/help/edge/wysiwyg-authoring/repoless.md#access-control)。
1. 通过以下方式调用配置服务来创建一个新 Site。请考虑：
   * POST URL 中的项目名称必须是您正在创建的新 Site 名称。在这个例子中，它是 `wknd-ch`。
   * `code` 配置应该与您在初始创建项目时使用的配置相同。
   * `content` > `source`  > `url` 必须根据您正在创建的新 Site 的名称进行调整。在这个例子中，它是 `wknd-ch`。
   * 也就是说，POST URL 中的 Site 名称与 `content` > `source`  > `url` 必须相同。
   * 调整 `admin` 块，定义应该对 Site 具有完全管理访问权限的用户。
      * 这是一个电子邮件地址数组。
      * 可以使用通配符 `*`。
      * 查看文档[配置作者的身份验证](https://www.aem.live/docs/authentication-setup-authoring#default-roles)，了解更多信息。

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
                       "<email>@<domain>.<tld>"
                   ],
                   "config_admin": [
                       "<tech-account-id>@techacct.adobe.com"
                   ]
               },
               "requireAuth": "auto"
           }
       }
   }'
   ```

1. 通过以下方法调用配置服务，为您的新 Site 添加路径映射。

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

1. 调用 `https://main--wknd-ch--<your-github-org>.aem.page/config.json` 验证新 Site 的公共配置是否正常工作，并验证返回的 JSON 的内容。

重复这些步骤，创建其他本地化 Sites。在 wknd 的例子中，您还需要为德国的业务创建一个 `wknd-de` Site。

### 在 AEM 中为您的本地化页面更新云配置 {#update-cloud-configurations}

AEM 中的页面必须配置为将您在上一节中创建的新 Edge Delivery Sites 用于您的本地化 Sites。在这个例子中，`/content/wknd/ch` 中的内容需要知道应使用您创建的 `wknd-ch` Site。`/content/wknd/de` 中的类似内容需要使用 `wknd-de` Site。

1. 登录 AEM 作者实例，然后前往&#x200B;**工具** -> **Cloud Services** -> **Edge Delivery Services 配置**。
1. 选择为您的项目自动创建的配置，然后选择为本地化页面创建的文件夹。在这个例子中是瑞士（`ch`）。
1. 在工具栏中点击或单击&#x200B;**创建** > **配置**。
1. 在 **Edge Delivery Services 配置**&#x200B;窗口中：
   * 在&#x200B;**组织**&#x200B;字段中提供您的 GitHub 组织。
   * 将 Site 名称改为您在上一节中创建的 Site 的名称。在这个例子中是 `wknd-ch`。
   * 将项目类型改为&#x200B;**带有无重复配置设置的 aem.live**。
1. 点击或单击&#x200B;**保存并关闭**。

## 验证您的设置 {#verify}

现在您完成了所有必要的配置更改，请验证一切是否按预期工作。

1. 登录您的 AEM 创作实例。
1. 导航至&#x200B;**Sites 控制台**，即从&#x200B;**导航**  -> **Sites**。
1. 选择本地化 Site，例如 `Switzerland`。
1. 在工具栏中点击或单击&#x200B;**编辑**。
1. 确保页面在通用编辑器中正确呈现，并使用与 Site 根目录相同的代码。
1. 对页面进行更改，然后重新发布。
1. 在 `https://main--wknd-ch--<your-github-org>.aem.page` 访问新的 Edge Delivery Services Site，查看此本地化页面。

如果您能看到所做的更改，就说明您的 MSM 设置正常运行。
