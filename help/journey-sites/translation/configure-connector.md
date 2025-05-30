---
title: 配置翻译连接器 (AEM Site)
description: 了解如何将 AEM 连接到翻译服务。
index: true
hide: false
hidefromtoc: false
exl-id: d1a3eb42-e9e4-4118-9ff7-7aab5519cf0d
solution: Experience Manager Sites
feature: Translation
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '1147'
ht-degree: 100%

---

# 配置翻译连接器 {#configure-connector}

了解如何将 AEM 连接到翻译服务。

## 迄今为止的故事 {#story-so-far}

在 AEM Site 翻译历程的上一个文档 [AEM Site 翻译入门](learn-about.md)中，您已了解如何组织内容以及 AEM 的翻译工具的工作方式，现在应：

* 了解内容结构对翻译的重要性。
* 了解 AEM 如何存储内容。
* 熟悉 AEM 的翻译工具。

本文基于这些基础之上，因此您可以执行第一个配置步骤并设置翻译服务，在该历程中，稍后可使用此服务来翻译内容。

## 目标 {#objective}

本文档可帮助您了解如何设置 AEM 连接器以使用所选翻译服务。阅读本文档后，您应：

* 了解 AEM 中翻译集成框架的重要参数。
* 能够自行建立与翻译服务的连接。

## 翻译集成框架 {#tif}

AEM 的翻译集成框架 (TIF) 与第三方翻译服务集成，以编排 AEM 内容的译文。其中涉及三个基本步骤。

1. 连接到您的翻译服务提供商。
1. 创建翻译集成框架配置。
1. 将配置与您的内容关联。

以下部分更详细地描述了这些步骤。

## 连接到翻译服务提供商 {#connect-translation-provider}

第一步是选择要使用哪项翻译服务。AEM 有多种人工翻译服务和机器翻译服务可供选择。大多数提供商都提供了要安装的翻译程序包。请参阅[其他资源](#additional-resources)部分以查看一系列可用的选项。

>[!NOTE]
>
>翻译专家通常负责选择要使用的翻译服务，而管理员通常负责安装所需的翻译连接器包。

在此历程中，我们使用 AEM 提供的 Microsoft Translator 以及现成的试用许可证。有关此提供商的更多信息，请参阅[其他资源](#additional-resources)部分。

如果您选择其他提供商，您的管理员必须按照翻译服务提供的说明安装连接器包。

>[!NOTE]
>
>在 AEM 中使用现成的 Microsoft Translator 不需要额外的设置，并且无需其他连接器配置即可按原样工作。
>
>如果您选择使用 Microsoft Translator 连接器进行测试，则无需执行以下两个部分中的步骤：[创建翻译集成配置](#create-config)和[将配置与您的内容关联](#associate)。但建议您阅读这两个部分，以便熟悉需要配置首选连接器时要执行的步骤。
>
>Microsoft Translator 连接器的试用许可证不用于生产目的，如果您决定对其进行许可，系统管理员必须执行本文档末尾的[其他资源](#additional-resources)部分中详述的步骤来配置该许可证。

## 创建翻译集成配置 {#create-config}

安装首选翻译服务的连接器包后，您必须为该服务创建翻译集成框架配置。该配置包括以下信息：

* 要使用哪个翻译服务提供商
* 要执行人工翻译还是机器翻译
* 是否翻译与页面关联的其他内容，如标记

要创建翻译配置，请执行以下操作：

1. 在全局导航菜单中，选择&#x200B;**工具** > **云服务** > **翻译云服务**。
1. 在您的内容结构中导航到要创建该配置的位置。这一般为项目专属的位置，但也可为全局位置。
   * 例如，在这种情况下，可以全局创建配置以将其应用于所有内容，或仅用于 WKND 项目。

   ![翻译配置位置](assets/translation-configuration-location.png)

1. 在工具栏中选择&#x200B;**创建**&#x200B;以创建新配置。
1. 在字段中提供以下信息，然后选择&#x200B;**创建**。
   1. 在下拉列表中选择&#x200B;**配置类型**。从列表中选择&#x200B;**翻译集成**。
   1. 为您的配置输入一个&#x200B;**标题**。**标题**&#x200B;在&#x200B;**Cloud Service**&#x200B;控制台中以及页面属性下拉列表中标识该配置。
   1. （可选）键入一个&#x200B;**名称**&#x200B;以用于存储该配置的存储库节点。

   ![创建翻译配置](assets/create-translation-configuration.png)

1. 选择&#x200B;**创建**，随后将显示&#x200B;**编辑配置**&#x200B;窗口，您可在其中配置该配置的各种属性。

1. 由于作为 Site 管理您的内容，因此，请选择 **Site** 选项卡。

![翻译配置属性](assets/translation-configuration.png)

1. 提供以下信息。

   1. **翻译方法** – 根据翻译提供商，选择&#x200B;**机器翻译**&#x200B;或&#x200B;**人工翻译**。在此历程中，我们假设使用机器翻译。
   1. **翻译提供商** – 从列表中选择您为翻译服务安装的连接器。
   1. **内容类别：** – 选择最合适的类别以更好地锁定翻译（仅适用于机器翻译）。
   1. **翻译页面资源** – 选择&#x200B;**使用 Site 翻译工作流**&#x200B;可翻译与 Site 页面关联的资源。
   1. **翻译组件字符串** – 选中此项可翻译组件信息。
   1. **翻译标记** – 选中此项可翻译与页面关联的标记。
   1. **自动执行翻译** – 如果您希望翻译自动发送到翻译服务，请选中此属性。

1. 选择&#x200B;**保存并关闭**。

您现在已配置连接器以使用翻译服务。

## 将配置与您的内容关联 {#associate}

AEM 是一种灵活而强大的工具，它通过多个连接器和多种配置支持多种同步翻译服务。设置此类配置超出了该历程的范围。但这种灵活性意味着，您必须通过将配置与您的内容关联来指定应使用哪些连接器和配置来翻译您的内容。

为此，请导航到内容的语言根。在我们的示例中，这将

```text
/content/<your-project>/en
```

1. 转到全局导航，再转到&#x200B;**导航** > **资源** > **文件**。
1. 在资源控制台中，选择要配置的语言根，然后选择&#x200B;**属性**。
1. 选择&#x200B;**云服务**&#x200B;选项卡。
1. 在&#x200B;**添加配置**&#x200B;下拉列表中的&#x200B;**云服务配置**&#x200B;下，选择您的连接器。安装连接器包后，它将显示在下拉列表中，如[之前所述](#connect-translation-provider)。
1. 在&#x200B;**添加配置**&#x200B;下拉列表中的&#x200B;**云服务配置**&#x200B;下，也选择您的配置。
1. 选择&#x200B;**保存并关闭**。

![选择云服务配置](assets/select-cloud-service-configurations.png)

## 后续内容 {#what-is-next}

现在您已完成 AEM Site 翻译历程的这一部分，您应：

* 了解 AEM 中翻译集成框架的重要参数。
* 能够自行建立与翻译服务的连接。

在此知识的基础上继续您的 AEM Site 翻译历程，接下来查看文档[配置翻译规则](translation-rules.md)，了解如何定义要翻译的内容。

## 其他资源 {#additional-resources}

我们建议您查看文档[配置翻译规则](translation-rules.md)来继续翻译历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续此历程所必需的。

* [配置翻译集成框架](/help/sites-cloud/administering/translation/integration-framework.md) – 查看所选翻译连接器的列表，并了解如何配置翻译集成框架以与第三方翻译服务集成。
* [连接到 Microsoft Translator](/help/sites-cloud/administering/translation/connect-ms-translator.md) – AEM 提供了试用 Microsoft Translation 帐户以进行测试。
