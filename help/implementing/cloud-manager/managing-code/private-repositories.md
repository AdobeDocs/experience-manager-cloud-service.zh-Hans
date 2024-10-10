---
title: 在Cloud Manager中添加专用GitHub存储库
description: 了解如何设置 Cloud Manager 以使用您自己的专用 GitHub 存储库。
exl-id: 5232bbf5-17a5-4567-add7-cffde531abda
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2fa4abca9823bbc62900023d637429f3fbfd894d
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 42%

---

# 在Cloud Manager中添加专用GitHub存储库 {#private-repositories}

通过设置Cloud Manager以与专用GitHub存储库集成，您可以使用Cloud Manager直接在GitHub中验证代码。 此配置消除了定期将代码与Adobe存储库同步的要求。

<!-- CONSIDER ADDING MORE DETAIL... THE WHY. Some key points about this capability include the following:

* **Direct Integration**: With this setup, you can directly link your private GitHub repositories to Cloud Manager, allowing for seamless code validation, deployment, and CI/CD (Continuous Integration/Continuous Deployment) pipelines without needing to maintain a separate sync process with Adobe's default Git repository.

* **Customization and Autonomy**: Companies often prefer managing their own source code repositories for security, control, and integration purposes. "Build your own GitHub" allows organizations to maintain their internal development processes while leveraging the full functionality of Cloud Manager for building, testing, and deploying AEM (Adobe Experience Manager) applications.

* **Simplified Workflow**: It reduces the overhead of synchronizing code between multiple repositories by allowing Cloud Manager to access the organization's private repository directly, making the development cycle faster and more efficient.

* **CI/CD Pipelines**: Teams can still benefit from Adobe Cloud Manager's automated build, test, and deployment processes, as the integration allows the CI/CD pipelines to pull code from the organization's own GitHub repository.

In essence, a "Build your own GitHub" in Adobe Cloud Manager empowers teams to manage their own GitHub repositories while still using the robust deployment and validation capabilities of Cloud Manager. -->

>[!NOTE]
>
>此功能为公共 GitHub 所独有。不支持自托管 GitHub。

## 配置 {#configuration}

Cloud Manager中专用GitHub存储库的配置包括两个步骤：

1. [将专用GitHub存储库](#add-repo)添加到所选程序。
1. 然后，[验证私有GitHub存储库的所有权](#validate-ownership)。

### 向项目添加专用GitHub存储库 {#add-repo}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择要将专用Git存储库链接到的程序。

1. 在侧面菜单中，在&#x200B;**服务**&#x200B;下，选择![文件夹图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg)**存储库**。

   ![存储库页面](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. 在&#x200B;**存储库**&#x200B;页面的右上角附近，点击&#x200B;**添加存储库**。

1. 在&#x200B;**添加存储库**&#x200B;对话框中，选择&#x200B;**专用存储库**&#x200B;作为存储库类型。

   ![添加自己的存储库](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. 在每个相应的字段中，提供有关存储库的以下详细信息：

   | 字段 | 描述 |
   | --- | --- |
   | 存储库名称 | 为您的新存储库取一个富有表现力的名称。 |
   | 存储库 URL | 专用存储库的URL，必须以`.git`结尾。<br>例如，*`https://github.com/org-name/repo-name.git`*（URL 路径仅用于说明目的）。 |
   | 描述（可选） | 存储库的详细描述。 |

1. 选择&#x200B;**保存**。
现在，您可以[验证私有存储库的所有权](#validate-ownership)。

>[!TIP]
>
>有关在 Cloud Manager 中管理存储库的详细信息，请参阅 [Cloud Manager 存储库](/help/implementing/cloud-manager/managing-code/managing-repositories.md)。



### 验证专用GitHub存储库的所有权 {#validate-ownership}

Cloud Manager 现已知道您的 GitHub 存储库，但它仍需要其访问权限。要授予访问权限，您需要安装 Adobe GitHub 应用程序并验证您是否拥有指定的存储库。

**验证私有GitHub存储库的所有权：**

1. 添加自己的存储库后，请按照&#x200B;**私有存储库所有权验证**&#x200B;对话框中的其余步骤操作。

   ![专用存储库所有权验证](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

   |  | 描述 |
   | --- | --- |
   | **步骤1： GitHub应用程序** | Cloud Manager使用GitHub应用程序与您的私有存储库安全交互。<br>· GitHub组织的所有者必须安装位于`https://github.com/apps/cloud-manager-for-aem`的应用程序并授予对存储库的访问权限。<br>·有关安装和授予访问权限已完成的详细信息，请参阅GitHub文档。 |
   | **步骤2：机密文件** | 要增强安全性，必须在存储库的默认分支中创建机密文件。<br>·单击&#x200B;**生成**，然后单击&#x200B;**确认**。 Cloud Manager在&#x200B;**机密文件内容**&#x200B;文本字段中生成私有文件的内容。<br>·单击![复制图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)以复制该字段中的内容。 秘密文件的内容仅显示一次。 如果在关闭此对话框之前没有复制内容，请重新生成密码。 |

1. 在GitHub存储库的默认分支中创建一个名为的新文件：

   `.well-known/adobe/cloud-manager-challenge`

1. 将机密文件内容粘贴到您刚刚创建的新文件中并保存。

   安装应用程序且存储库中存在机密文件后，请继续执行此步骤。

1. 在&#x200B;**私有存储库所有权验证**&#x200B;对话框中，单击&#x200B;**验证**。

可以按任意顺序安装应用程序并创建机密文件。 但必须先完成这两个步骤，之后才能进行验证。

在验证之前，存储库将会列出红色图标，这表示它尚未经过验证，因此尚无法使用。

![未经验证的存储库](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

**存储库**&#x200B;页面上的表中的&#x200B;**类型**&#x200B;列标识Adobe提供的存储库(**Adobe**)和您自己的专用存储库(**GitHub**)。

如果您需要稍后返回到存储库以完成验证，请在&#x200B;**存储库**&#x200B;页面上，单击代表您刚刚添加的GitHub存储库的行中的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。 在下拉列表中选择&#x200B;**所有权验证**。



## 将专用GitHub存储库与Cloud Manager结合使用 {#using}

在Cloud Manager中验证GitHub存储库后，集成即完成。 您可以将该存储库与Cloud Manager结合使用。

**将专用存储库与 Cloud Manager 结合使用：**

1. 在创建提取请求时，GitHub 检查会自动启动。

   ![GitHub 检查](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. 对于每个提取请求，系统会自动创建[全栈代码质量管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。 每次更新提取请求时，此管道便会启动。

1. 在代码质量检查完成之前，GitHub检查将保持运行状态。 之后，代码质量结果会传播到 GitHub 检查。

   ![GitHub 代码质量检查](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

在合并或关闭拉取请求时，将自动删除创建的全栈代码质量管道。

>[!TIP]
>
>有关运行拉取请求检查时通过GitHub提供的信息的详细信息，请参阅[GitHub检查批注](github-annotations.md)。

>[!TIP]
>
>您可以控制自动创建的管道，验证对专用存储库的每个提取请求。请参阅 [GitHub 检查专用存储库的配置](github-check-config.md)，了解更多信息。



## 将专用存储库与管道关联 {#pipelines}

经过验证的专用存储库可以与[全栈和前端管道相关联](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。



## 限制 {#limitations}

在 Cloud Manager 中使用专用存储库时会受到某些限制。

* 专用存储库不支持 Web 层和配置管道。
* 在生产全栈管道上使用专用存储库时，不会创建和推送任何 Git 标记。
* 如果从您的GitHub组织中删除了AdobeGitHub应用程序，则会删除适用于所有存储库的拉取请求验证功能。
* 当新的提交被推送到选定的分支时，使用专用存储库和提交构建触发器的管道不会自动启动。
* [工件重用功能](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)不适用于专用存储库。
* 使用Cloud Manager中的GitHub检查，无法暂停拉取请求验证。
如果在Cloud Manager中验证GitHub存储库，则Cloud Manager始终会尝试验证为该存储库创建的拉取请求。
