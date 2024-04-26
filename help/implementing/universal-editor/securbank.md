---
title: 用于通用编辑器的SecurBank示例应用程序
description: 使用SecurBank应用程序了解具有实践经验的通用编辑器，该应用程序旨在展示通用编辑器的强大功能、灵活性和可用性，以加快内容创建。
source-git-commit: 4b7612f423e4e728911920793e9e0a03757c7c9d
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 1%

---


# 用于通用编辑器的SecurBank示例应用程序 {#securbank}

使用SecurBank应用程序了解具有实践经验的通用编辑器，该应用程序旨在展示通用编辑器的强大功能、灵活性和可用性，以加快内容创建。

## 先决条件 {#prerequisites}

* 您必须被分配到 **AEM管理员** [产品配置文件](/help/journey-onboarding/assign-profiles-aem.md) 以安装SecurBank应用程序。
* 您必须拥有 [Node.js](https://nodejs.org) 版本20或更高版本已安装，用于本地开发。

## 安装SecurBank {#installation}

SecurBank应用程序的安装很简单，但由于涉及AEMas a Cloud Service的许多领域，因此涉及多个步骤。 以下是主要步骤的概述。

1. [在Cloud Manager中创建沙盒程序。](#create-sandbox-program)
1. [克隆程序的Git存储库，并使用SecurBank AEM项目内容进行更新。](#clone-and-update)
1. [运行管道以部署SecurBank AEM项目。](#run-pipeline)
1. [检索Cloud Manager凭据以进行本地Web应用程序开发。](#retrieve-credentials)
1. [下载并配置SecurBank Web应用程序。](#download-web-app)
1. [运行SecurBank Web应用程序。](#run-web-app)

以下各节详细介绍了所需的各项任务。

### 在Cloud Manager中创建沙盒程序。 {#create-sandbox-program}

您需要一个新的Cloud Manager程序，以便安装SecurBank。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 为SecurBank应用程序创建新的沙盒程序。

   * 选择时使用默认选项 **解决方案和加载项**.
   * 有关如何创建沙盒程序的详细信息，请参阅文档 [创建沙盒程序。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)

### 克隆程序的Git存储库，并使用SecurBank AEM项目内容进行更新。 {#clone-and-update}

1. 创建项目后，打开它并在 **存储库** 选项卡，点按或单击 **访问存储库信息** 按钮以打开 **存储库信息** 对话框并查看访问沙盒环境的Git存储库所需的凭据。

   * 有关如何访问存储库信息的详细信息，请参阅文档 [访问存储库。](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. 使用中的凭据 **存储库信息** 对话框，在本地计算机上克隆存储库。

1. 找到本地克隆的文件夹，打开它并删除隐藏文件/点文件以外的所有内容。

1. 在GitHub中检索最新的SecurBank AEM项目代码 [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank) 通过单击 **代码** 然后 **下载ZIP** 在下拉菜单中。

1. 在本地文件系统上解压缩zip文件的内容，并将其移动到沙盒程序的本地克隆的现为空的文件夹中。

1. 使用终端，切换到克隆项目的文件夹并提交所有内容并将其推送到Git。

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### 运行管道以部署SecurBank AEM项目。 {#run-pipeline}

将SecurBank的AEM项目提交到沙盒存储库后，便可以部署管道了。

1. 返回到 **概述** 选项卡，并运行全栈非生产管道。

   * 取消选中管道运行的所有选项。
   * 有关运行管道的更多信息，请参阅文档 [管理管道。](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)

### 检索Cloud Manager凭据以进行本地Web应用程序开发。 {#retrieve-credentials}

在运行SecurBank应用程序之前，您需要Cloud Manager凭据才能将应用程序连接到Cloud Manager。

1. 在管道运行时，返回到 **概述** 选项卡，然后点按或单击环境名称旁边的省略号按钮并选择 **开发人员控制台**.

1. 在开发人员控制台中，选择 **集成** 选项卡，然后 **本地令牌** 选项卡，然后点按或单击 **获取本地开发令牌**.

1. 使用访问令牌生成了JSON文件。 仅将令牌本身（其余JSON不是必需的）复制到安全位置，以供在关闭开发人员控制台并返回到Cloud Manager之前的未来步骤中使用。

1. 返回Cloud Manager，在 **概述** 选项卡，右键单击环境的URL以复制该URL并将其保存在安全位置，以供将来步骤使用。

### 下载并配置SecurBank Web应用程序。 {#download-web-app}

现在，您可以下载并配置SecurBank Web应用程序。

1. 从GitHub中检索最新的SecurBank应用程序代码，网址为 [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events) 通过单击 **代码** 然后 **下载ZIP** 在下拉菜单中。

1. 在本地文件系统上解压缩zip文件的内容。

1. 启动首选代码编辑器，然后在位于的SecurBank应用程序项目中打开隐藏的环境文件 `summit-2024-l425-ue-z-final-with-events/react-app/.env`.

1. 对 `.env` 文件并保存更改。

   * 对象 `REACT_APP_HOST_URI` 粘贴先前复制的环境的URL的值。
   * 对象 `REACT_APP_DEV_TOKEN` 粘贴之前复制的本地开发令牌的值。

### 运行SecurBank Web应用程序。 {#run-web-app}

通过在Cloud Manager和本地设置一切，您可以运行SecurBank Web应用程序。

1. 在本地计算机的命令行中，导航到 `react-app` 您下载并解压缩的SecurBank应用程序项目的文件夹。

1. 在您的 `react-app` 文件夹安装SecurBank应用程序，其中 `node -i` 命令。

1. 安装后，使用启动SecurBank应用程序 `npm start` 命令。

1. 如果安装并启动成功，您将看到：

* 终端中的以下输出。

  ```text
  Compiled successfully!
  
  You can now view securbank in the browser.
  
    Local:            https://localhost:3000
    On Your Network:  https://192.168.1.15:3000
  
  Note that the development build is not optimized.
  To create a production build, use npm run build.
  
  webpack compiled successfully
  ```

   * 并打开一个浏览器窗口以访问该URL `https://localhost:3000`.

      * 请注意，这用于开发目的，因此不提供有效证书。 因此，您可能需要通知浏览器允许其访问页面。

恭喜！现在，您应会看到已在浏览器中成功运行SecurBank应用程序。

如果内容尚未显示，请确保 **部署到开发** 您运行的管道已成功完成。

![浏览器中的SecurBank应用程序](assets/securbank.png)
