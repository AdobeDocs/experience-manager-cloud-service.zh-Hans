---
title: 用于通用编辑器的 SecurBank 应用程序示例
description: 通过使用 SecurBank 应用程序获得实践经验，深入了解通用编辑器，此应用程序旨在展示通用编辑器的强大功能、灵活性和可用性，以加速内容创作。
exl-id: 97e1395f-b51e-4cee-b1d0-2466a08f96af
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 100%

---

# 用于通用编辑器的 SecurBank 应用程序示例 {#securbank}

通过使用 SecurBank 应用程序获得实践经验，深入了解通用编辑器，此应用程序旨在展示通用编辑器的强大功能、灵活性和可用性，以加速内容创作。

## 先决条件 {#prerequisites}

* 您必须被分配到 **AEM 管理员**[产品轮廓](/help/journey-onboarding/assign-profiles-aem.md)，才能安装 SecurBank 应用程序。
* 您必须安装了 [Node.js](https://nodejs.org) 20 或更高版本用于进行本地开发。

## 安装 SecurBank {#installation}

SecurBank 应用程序的安装很简单，但由于它涉及 AEM as a Cloud Service 的许多区域，因此包含许多步骤。以下是主要步骤概述。

1. [在 Cloud Manager 中创建一个沙盒程序](#create-sandbox-program)。
1. [克隆程序的 git 存储库，用 SecurBank AEM 项目内容将其更新](#clone-and-update)。
1. [运行管道，以部署 SecurBank AEM 项目](#run-pipeline)。
1. [检索 Cloud Manager 凭据，用于本地 Web 应用程序开发](#retrieve-credentials)。
1. [下载并配置 SecurBank Web 应用程序](#download-web-app)。
1. [运行 SecurBank Web 应用程序](#run-web-app)。

接下来几节详细说明了几个必须完成的任务。

### 在 Cloud Manager 中创建一个沙盒程序。 {#create-sandbox-program}

您需要一个新的 Cloud Manager 程序，以便在其中安装 SecurBank。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 为 SecurBank 应用程序创建一个新的沙盒程序。

   * 选择&#x200B;**解决方案和附加组件**&#x200B;时使用默认选项。
   * 有关如何创建沙盒程序的详细信息，请参阅文档[创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)。

### 克隆程序的 git 存储库，用 SecurBank AEM 项目内容进行更新。 {#clone-and-update}

1. 程序创建后打开程序，然后在&#x200B;**存储库**&#x200B;选项卡中点击&#x200B;**访问存储库信息**&#x200B;按钮，打开&#x200B;**存储库信息**&#x200B;对话框，查看访问沙盒环境的 git 存储库所需的凭据。

   * 有关如何访问存储库信息的详细信息，请参阅文档[访问存储库](/help/implementing/cloud-manager/managing-code/accessing-repos.md)。

1. 使用&#x200B;**存储库信息**&#x200B;对话框中的凭据，将存储库克隆在您的本地机器上。

1. 找到并打开本地克隆的文件夹，将除了隐藏/点文件之外的所有内容删除。

1. 在 [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank)，从 GitHub 检索最新的 SecurBank AEM 项目代码，点击&#x200B;**代码**，然后在下拉菜单中点击&#x200B;**下载 ZIP**。

1. 在本地文件系统上将 zip 文件的内容解压缩，然后将其移到沙盒程序本地克隆的现在变空的文件夹中。

1. 使用终端，切换到克隆项目的文件夹，提交所有内容，将其推送到 git。

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### 运行管道，以部署 SecurBank AEM 项目。 {#run-pipeline}

将 SecurBank 的 AEM 项目提交到沙盒存储库后，就可以使用管道进行部署。

1. 返回到 Cloud Manager 中沙盒程序的&#x200B;**概述**&#x200B;选项卡，运行全栈非生产管道。

   * 取消勾选管道运行的所有选项。
   * 有关运行管道的更多信息，请参阅文档[管理管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)。

### 检索 Cloud Manager 凭据，用于本地 Web 应用程序开发。 {#retrieve-credentials}

在运行 SecurBank 应用程序之前，您需要 Cloud Manager 凭据才能将此应用程序与 Cloud Manager 连接。

1. 在管道运行时，返回到 Cloud Manager 中的&#x200B;**概述**&#x200B;选项卡，点击环境名称旁边的省略号按钮，然后选择&#x200B;**开发人员控制台**。

1. 在开发人员控制台中选择&#x200B;**集成**&#x200B;选项卡，然后选择&#x200B;**本地令牌**&#x200B;选项卡，点击&#x200B;**获取本地开发令牌**。

1. 通过这个访问令牌生成一个 JSON 文件。在关闭开发人员控制台并返回 Cloud Manager 之前，只需要将令牌（其余的 JSON 不必需）复制到一个安全的位置，以供在后续步骤中使用。

1. 返回到 Cloud Manager，在&#x200B;**概述**&#x200B;选项卡中右键单击环境的 URL，将其复制并保存到一个安全的位置，以供在后续步骤中使用。

### 下载并配置 SecurBank Web 应用程序。 {#download-web-app}

现在您可以下载并配置 SecurBank Web 应用程序。

1. 在 [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events)，从 GitHub 检索最新的 SecurBank 应用程序代码，点击&#x200B;**代码**，然后在下拉菜单中点击&#x200B;**下载 ZIP**。

1. 在您的本地文件系统上将 zip 文件的内容解压缩。

1. 启动您首选的代码编辑器，打开 SecurBank 应用程序项目中的隐藏环境文件，位于：`summit-2024-l425-ue-z-final-with-events/react-app/.env`。

1. 对 `.env` 文件进行以下更改并保存更改。

   * 将刚才复制的环境 URL 的值粘贴给 `REACT_APP_HOST_URI`。
   * 将刚才复制的本地开发令牌的值粘贴给 `REACT_APP_DEV_TOKEN`。

### 运行 SecurBank Web 应用程序。 {#run-web-app}

完成 Cloud Manager 和本地的所有设置后，您可以运行 SecurBank Web 应用程序。

1. 在本地计算机的命令行中，导航到您已下载并解压缩的 SecurBank 应用程序项目的 `react-app` 文件夹。

1. 在您的 `react-app` 文件夹中，通过 `node -i` 命令安装 SecurBank 应用程序。

1. 安装后，通过 `npm start` 命令启动 SecurBank 应用程序。

1. 如果安装和启动成功，您将看到：

* 终端中输出以下内容。

  ```text
  Compiled successfully!
  
  You can now view securbank in the browser.
  
    Local:            https://localhost:3000
    On Your Network:  https://192.168.1.15:3000
  
  Note that the development build is not optimized.
  To create a production build, use npm run build.
  
  webpack compiled successfully
  ```

   * 一个浏览器窗口打开 URL `https://localhost:3000`。

      * 请注意，这是出于开发目的，因此不提供有效的证书。因此您可能需要告知浏览器允许其访问此页面。

恭喜！您现在会看到 SecurBank 应用程序在您的浏览器中成功运行。

如果没有出现内容，请确保您运行的&#x200B;**部署到开发**&#x200B;管道已成功完成。

![浏览器中的 SecurBank 应用程序](assets/securbank.png)

{{ue-headless-auth}}

