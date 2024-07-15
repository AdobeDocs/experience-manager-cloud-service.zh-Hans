---
title: 用于通用编辑器的SecurBank示例应用程序
description: 使用SecurBank应用程序了解具有实践经验的通用编辑器，该应用程序旨在展示通用编辑器的强大功能、灵活性和可用性，以加快内容创建。
exl-id: 97e1395f-b51e-4cee-b1d0-2466a08f96af
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 1%

---

# 用于通用编辑器的SecurBank示例应用程序 {#securbank}

使用SecurBank应用程序了解具有实践经验的通用编辑器，该应用程序旨在展示通用编辑器的强大功能、灵活性和可用性，以加快内容创建。

## 先决条件 {#prerequisites}

* 您必须分配给&#x200B;**AEM管理员** [产品配置文件](/help/journey-onboarding/assign-profiles-aem.md)，才能安装SecurBank应用。
* 您必须安装[Node.js](https://nodejs.org)版本20或更高版本，才能进行本地开发。

## 安装SecurBank {#installation}

SecurBank应用程序的安装很简单，但由于涉及AEM as a Cloud Service的许多领域，因此需要执行多个步骤。 以下是主要步骤的概述。

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

   * 选择&#x200B;**解决方案和加载项**&#x200B;时使用默认选项。
   * 有关如何创建沙盒程序的详细信息，请参阅文档[创建沙盒程序。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)

### 克隆程序的Git存储库，并使用SecurBank AEM项目内容进行更新。 {#clone-and-update}

1. 创建项目后，请将其打开，然后在&#x200B;**存储库**&#x200B;选项卡上，点按或单击&#x200B;**访问存储库信息**&#x200B;按钮以打开&#x200B;**存储库信息**&#x200B;对话框，并查看访问沙盒环境的Git存储库所需的凭据。

   * 有关如何访问存储库信息的详细信息，请参阅文档[访问存储库。](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. 使用&#x200B;**存储库信息**&#x200B;对话框中的凭据，在本地计算机上克隆存储库。

1. 找到本地克隆的文件夹，打开它并删除隐藏文件/点文件以外的所有内容。

1. 通过单击&#x200B;**代码**，然后在下拉列表中&#x200B;**下载ZIP**，从GitHub [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank)中检索最新的SecurBank AEM项目代码。

1. 在本地文件系统上解压缩zip文件的内容，并将其移动到沙盒程序的本地克隆的现为空的文件夹中。

1. 使用终端，切换到克隆项目的文件夹并提交所有内容并将其推送到Git。

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### 运行管道以部署SecurBank AEM项目。 {#run-pipeline}

将SecurBank的AEM项目提交到沙盒存储库后，便可以部署管道了。

1. 返回到Cloud Manager中沙盒程序的&#x200B;**概述**&#x200B;选项卡，并运行全栈非生产管道。

   * 取消选中管道运行的所有选项。
   * 有关运行管道的详细信息，请参阅文档[管理管道。](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)

### 检索Cloud Manager凭据以进行本地Web应用程序开发。 {#retrieve-credentials}

在运行SecurBank应用程序之前，您需要Cloud Manager凭据才能将应用程序连接到Cloud Manager。

1. 在管道运行时，返回到Cloud Manager中的&#x200B;**概述**&#x200B;选项卡，点按或单击环境名称旁边的省略号按钮，然后选择&#x200B;**Developer Console**。

1. 在Developer Console中，选择&#x200B;**集成**&#x200B;选项卡，然后选择&#x200B;**本地令牌**&#x200B;选项卡，然后点按或单击&#x200B;**获取本地开发令牌**。

1. 使用访问令牌生成了JSON文件。 仅将令牌本身（其余JSON不是必需的）复制到安全位置，以供在关闭Developer Console并返回到Cloud Manager之前的后续步骤中使用。

1. 返回到Cloud Manager中的&#x200B;**概述**&#x200B;选项卡上，右键单击环境的URL以复制该URL并将其保存在安全位置以供将来步骤使用。

### 下载并配置SecurBank Web应用程序。 {#download-web-app}

现在，您可以下载并配置SecurBank Web应用程序。

1. 通过单击&#x200B;**代码**，然后在下拉菜单中单击&#x200B;**下载ZIP**，从GitHub [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events)中检索最新的SecurBank应用代码。

1. 在本地文件系统上解压缩zip文件的内容。

1. 启动首选代码编辑器，并在`summit-2024-l425-ue-z-final-with-events/react-app/.env`处的SecurBank应用程序项目中打开隐藏的环境文件。

1. 对`.env`文件进行以下更改并保存更改。

   * 对于`REACT_APP_HOST_URI`，粘贴您环境先前复制的URL的值。
   * 对于`REACT_APP_DEV_TOKEN`，粘贴先前复制的本地开发令牌的值。

### 运行SecurBank Web应用程序。 {#run-web-app}

通过在Cloud Manager和本地设置一切，您可以运行SecurBank Web应用程序。

1. 在本地计算机的命令行中，导航到您下载并解压缩的SecurBank应用程序项目的`react-app`文件夹。

1. 在`react-app`文件夹中，使用`node -i`命令安装SecurBank应用程序。

1. 安装后，使用`npm start`命令启动SecurBank应用程序。

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

   * 并打开一个浏览器窗口，显示URL `https://localhost:3000`。

      * 请注意，这用于开发目的，因此不提供有效证书。 因此，您可能需要通知浏览器允许其访问页面。

恭喜！现在，您应会看到已在浏览器中成功运行SecurBank应用程序。

如果内容尚未显示，请确保已成功完成您运行的&#x200B;**部署到开发**&#x200B;管道。

浏览器中的![SecurBank应用](assets/securbank.png)
