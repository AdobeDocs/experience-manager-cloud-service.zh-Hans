---
title: 与 Adobe Campaign Classic 集成
description: 了解如何将 AEM as a Cloud Service 与 Adobe Campaign Classic 集成，为您的活动创建引人注目的内容。
feature: Administering
role: Admin
exl-id: 23874955-bdf3-41be-8a06-53d2afdd7f2b
source-git-commit: cab630838f5cce3c2a2749c61b0aa7504dc403f7
workflow-type: ht
source-wordcount: '1302'
ht-degree: 100%

---

# 与 Adobe Campaign Classic 集成 {#integrating-campaign-classic}

通过将 AEM as a Cloud Service 与 Adobe Campaign 集成，您可以直接在 AEM as a Cloud Service 中管理电子邮件投放、内容和表单。需要同时完成 Adobe Campaign Classic 和 AEM as a Cloud Service 的配置步骤才可以实现解决方案之间的双向通信。

进行这种集成后，可独立使用 AEM as a Cloud Service 和 Adobe Campaign Classic。营销人员可以在 Adobe Campaign 中创建活动并使用定位，而内容创建者则可以同时在 AEM as a Cloud Service 中进行内容设计。通过集成，AEM 中活动的内容和设计可以由 Campaign 进行定位和交付。

## 集成步骤 {#integration-steps}

AEM 和 Campaign 之间的集成需要在这两种解决方案中完成多个步骤。

1. [在 Campaign 中安装 AEM 集成包。](#install-package)
1. [在 Campaign 中为 AEM 创建一个运算符](#create-operator)
1. [在 AEM 中配置 Campaign 集成](#campaign-integration)
1. [配置 AEM 外部化器](#externalizer)
1. [在 AEM 中配置活动远程用户](#configure-user)
1. [在 Campaign 中配置 AEM 外部账户](#acc-setup)

本文档将详细介绍每一个步骤

## 前提条件 {#prerequisites}

* 具有 Adobe Campaign Classic 管理员访问权限
   * 要执行集成，您需要一个有效的 Adobe Campaign Classic 实例，包括一个已配置的数据库。
   * 如果您需要有关如何设置和配置 Adobe Campaign Classic 的更多详细信息，请参阅 [Adobe Campaign Classic 文档](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html)，特别是《安装和配置指南》。

* 具有对 AEM as a Cloud Service 的管理员访问权限

## 在 Campaign 中安装 AEM 集成包 {#install-package}

Adobe Campaign 中的 **AEM 集成**&#x200B;包含有连接到 AEM 所需的许多标准配置。

1. 作为管理员，使用客户端控制台登录到 Adobe Campaign 实例。

1. 选择&#x200B;**“工具”**>**“高级”**>**“导入软件包...”**。

   ![导入软件包](assets/import-package.png)

1. 单击&#x200B;**“安装标准包”**，然后单击&#x200B;**“下一个”**。

1. 检查&#x200B;**AEM 集成**&#x200B;包。

   ![安装标准包](assets/select-package.png)

1. 单击&#x200B;**“下一个”**，然后单击&#x200B;**“开始”**&#x200B;以开始安装。

   ![安装进度](assets/installation.png)

1. 安装完成后，单击&#x200B;**“关闭”**。

集成包现在已安装。

## 在 Campaign 中为 AEM 创建运算符 {#create-operator}

集成包会自动创建 AEM 用于连接到 Adobe Campaign 的`aemserver`运算符。您必须为此运算符定义一个安全区域并设置密码。

1. 使用客户端控制台以管理员身份登录 Adobe Campaign。

1. 从菜单栏选择&#x200B;**“工具”** -> **“资源管理器”**。

1. 在资源管理器中，导航到&#x200B;**“管理”**>**“访问管理“**＞**”运算符“**&#x200B;节点。

1. 选择`aemserver`运算符。

1. 在运算符的&#x200B;**”编辑“**&#x200B;选项卡上，选择&#x200B;**”访问权限“**&#x200B;子选项卡，然后单击&#x200B;**”修改访问参数...“**&#x200B;链接。

   ![设置安全区域](assets/access-rights.png)

1. 选择适当的安全区域，并根据需要定义受信任的 IP 掩码。

1. 单击&#x200B;**”保存“**。

1. 注销 Adobe Campaign 客户端。

1. 在 Adobe Campaign 服务器的文件系统上，导航到 Campaign 安装位置，并以管理员身份编辑`serverConf.xml`文件。该文件通常位于以下位置：
   * `C:\Program Files\Adobe\Adobe Campaign Classic v7\conf`在 Windows 中。
   * `/usr/local/neolane/nl6/conf/eng` 在 Linux 中。

1. 搜索`securityZone`，并确保为 AEM 运算符的安全区域设置了以下参数。

   * `allowHTTP="true"`
   * `sessionTokenOnly="true"`
   * `allowUserPassword="true"`。

1. 保存文件。

1. 确保安全区域不会被`config-<server name>.xml`文件中的相应设置覆盖。

   * 如果配置文件包含单独的安全区域设置，则将`allowUserPassword`属性更改为`true`。

1. 如果要更改 Adobe Campaign Classic 服务器端口，请将`8080`替换为所需端口。

>[!CAUTION]
>
>默认情况下，没有为运算符配置安全区域。要使 AEM 连接到 Adobe Campaign，您必须按照前面步骤中的详细说明选择一个区域。
>
>Adobe 强烈建议为 AEM 创建一个安全区域，以避免任何安全问题。有关此主题的更多信息，请参阅[ Adobe Campaign Classic 文档。](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/security-zones.html)

1. 在 Campaign 客户端中，返回到`aemserver`运算符并选择&#x200B;**“常规”**&#x200B;选项卡。

1. 单击&#x200B;**“重置密码...”**&#x200B;链接。

1. 指定密码并将其存储在安全位置以供将来使用。

1. 单击&#x200B;**“确定”**&#x200B;以保存`aemserver`运算符的密码。

## 在 AEM 中配置 Campaign 集成 {#campaign-integration}

AEM 使用[您在 Campaign 中设置的运算符](#create-operator)与 Campaign 进行通信

1. 以管理员身份登录到您的 AEM 创作实例。

1. 从全局导航侧栏中，选择&#x200B;**“工具”**>**“Cloud Service”**＞**“传统 Cloud Service”**>**“Adobe Campaign”**，然后单击&#x200B;**“立即配置”**。

   ![配置 Adobe Campaign](assets/configure-campaign-service.png)

1. 在对话框中，通过输入&#x200B;**“标题”**&#x200B;并单击&#x200B;**“创建”**&#x200B;来创建 Campaign 服务配置。

   ![配置 Campaign 对话框](assets/configure-campaign-dialog.png)

1. 会打开新窗口和对话框会，用以编辑配置。 提供必要的信息。

   * **用户名** – 这是在上一步创建的[ Adobe Campaign AEM 集成包运算符。](#create-operator)默认情况下，这是 `aemserver`。
   * **密码** – 这是在上一步创建的 [Adobe Campaign AEM 集成包运算符的密码。](#create-operator)
   * **API 端点** – 这是 Adobe Campaign 实例 URL。

   ![在 AEM 中配置 Adobe Campaign](assets/configure-campaign.png)

1. 选择&#x200B;**“连接到 Adobe Campaign”**&#x200B;以验证连接，然后单击&#x200B;**确定**。

AEM 现在可以与 Adobe Campaign 通信。

>[!NOTE]
>
>确保您的 Adobe Campaign 服务器可以通过 Internet 访问。AEM as a Cloud Service 不能访问专用网络。

## 配置 AEM 外部化器 {#externalizer}

外部化器是 AEM 中的一个 OSGi 服务，它可将资源路径转换为外部和绝对 URL，这是 AEM 提供 Campaign 可以使用的内容所必需的。

1. 以管理员身份登录到 AEM 创作实例。
1. 通过检查[开发人员控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#osgi-services)中 OSGi 服务的状态转储，确认外部化器配置中的发布实例。
1. 如果不正确，请在相应的实例 git 存储库中进行必要的更改，然后[使用云管理器部署配置。](/help/implementing/cloud-manager/deploy-code.md)

```text
Service 3310 - [com.day.cq.commons.externalizer] (pid: com.day.cq.commons.impl.externalizerImpl)",
"  from Bundle 420 - Day Communique 5 Commons Library (com.day.cq.cq-commons), version 5.12.16",
"    component.id: 2149",
"    component.name: com.day.cq.commons.impl.externalizerImpl",
"    externalizer.contextpath: ",
"    externalizer.domains: [local https://author-p17558-e33255-cmstg.adobeaemcloud.com, author https://author-p17558-e33255-cmstg.adobeaemcloud.com,
     publish https://publish-p17558-e33255-cmstg.adobeaemcloud.com]",
"    externalizer.encodedpath: false",
"    externalizer.host: ",
"    feature-origins: [com.day.cq:cq-quickstart:slingosgifeature:cq-platform-model_quickstart_author:6.6.0-V23085]",
"    service.bundleid: 420",
"    service.description: Creates absolute URLs",
"    service.scope: bundle",
"    service.vendor: Adobe Systems Incorporated",
```

>[!NOTE]
>
>发布实例必须可以从 Adobe Campaign 服务器中访问。

## 在 AEM 中配置活动远程用户 {#configure-user}

如要实现 Campaign 与 AEM 之间的通信，您需要在 AEM 中为 `campaign-remote` 用户设置一个密码。

1. 以管理员身份登录 AEM。
1. 在主导航控制台上，单击左栏中的&#x200B;**“工具”**。
1. 然后单击&#x200B;**“安全”**-＞**“用户”**，打开用户管理控制台。
1. 找到`campaign-remote`用户。
1. 选择`campaign-remote`用户，然后单击&#x200B;**“属性”**&#x200B;来编辑用户。
1. 在&#x200B;**“编辑用户设置”**&#x200B;窗口中，单击&#x200B;**“更改密码”**。
1. 为用户提供新密码，并将密码记在安全位置以备将来使用。
1. 单击&#x200B;**“保存”**&#x200B;以保存密码更改。
1. 单击&#x200B;**“保存并关闭”**&#x200B;以将更改保存到`campaign-remote`用户。

## 在 Campaign 中配置 AEM 外部账户 {#acc-setup}

当[在 Campaign 中安装&#x200B;**AEM 集成**&#x200B;包时，](#install-package)会为 AEM 创建一个外部帐户。通过配置此外部帐户，Adobe Campaign 可以连接到 AEM as a Cloud Service，以实现解决方案之间的双向通信。

1. 使用客户端控制台以管理员身份登录 Adobe Campaign。

1. 从菜单栏选择&#x200B;**“工具”** -> **“资源管理器”**。

1. 在资源管理器中，导航到&#x200B;**“管理”** > **“Platform“**＞**”外部账户“**&#x200B;节点。

   ![外部帐户](assets/external-accounts.png)

1. 找到外部 AEM 帐户。默认情况下，它具有以下值：

   * **类型** – AEM
   * –**标签** – AEM 实例
   * **内部名称** – aemInstance

1. 在该帐户的&#x200B;**“常规”**&#x200B;选项卡上，输入您在[设置活动远程用户密码](#set-campaign-remote-password)步骤中定义的用户信息。

   * **服务器** – AEM 作者服务器地址
      * AEM 作者服务器必须可以从 Adobe Campaign Classic 服务器实例中访问。
      * 确保服务器地址的&#x200B;**不是**&#x200B;以尾随斜杠结尾。
   * **帐户** – 默认情况下，这是您在[设置活动远程用户密码](#set-campaign-remote-password)步骤中在 AEM 中设置的`campaign-remote`用户。
   * **密码** – 该密码与在[设置活动远程用户密码](#set-campaign-remote-password)步骤中在 AEM 中设置的`campaign-remote`用户密码相同。

1. 选中&#x200B;**启用**&#x200B;复选框。

1. 单击&#x200B;**保存**。

Adobe Campaign 现在可以与 AEM 通信。

## 后续步骤 {#next-steps}

在配置 Adobe Campaign Classic 和 AEM as a Cloud Service 后，集成现已完成。

您现在可以通过继续阅读[本文档](/help/sites-cloud/authoring/campaign/creating-newsletters.md)学习如何在 Adobe Experience Manager 中创建新闻稿。
