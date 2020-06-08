---
title: 配置CI/CD管道——云服务
description: 配置CI/CD管道——云服务
translation-type: tm+mt
source-git-commit: e9514d2ba625a7df8a8126f5b0ab74b975eeda51
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 3%

---


# 配置CI-CD管道 {#configure-ci-cd-pipeline}


## 了解流 {#understanding-the-flow}

您可以在Cloud Manager UI中通过“管 **线设置** ”拼贴配 [!UICONTROL 置管道] 。

部署管理器负责设置管道。 执行此操作时，您首先从Git存储库中选 **择分支**。

要配置管道，用户必须：

* 定义将开始管线的触发器。
* 定义控制生产部署的参数。
* 配置性能测试参数。

## 设置管道 {#setting-up-the-pipeline}

>[!CAUTION]
>
>在一个项目创建完成且Git存储库至少有一个分支之前，无法设置管道。

在开始部署代码之前，您必须从云管理器配置渠 [!UICONTROL 道设置]。

>[!NOTE]
>
>初始设置后，可以更改管线设置。

## 从云管理器配置 [!UICONTROL 管道设置] {#configuring-the-pipeline-settings-from-cloud-manager}

一旦您使用Cloud Manager UI设置了项目并且至少拥 [!UICONTROL 有一个环境] ，您就可以设置部署渠道了。

按照以下步骤配置管道的行为和首选项：

1. 单击“ **设置管道** ”(Setup Pipeline)以设置和配置管道。

   ![](assets/set-up-pipeline1.png)

1. 将显 **示“设置管道** ”屏幕。 Select the branch and click **Next**.

   ![](assets/set-up-pipeline2.png)

1. 配置部署选项。

   ![](assets/set-up-pipeline3.png)

   可以定义触发器以开始管线：

   * **手动** -使用UI手动开始管道。
   * **在Git更改中** -只要向配置的git分支添加提交，就会开始CI/CD管道。 即使选择此选项，也始终可以手动开始管线。

   在管线设置或编辑过程中，当在任何质量门中遇到重要故障时，部署管理器可以定义管线的行为。

   这对于希望实现更自动化流程的客户非常有用。 可用选项有：

   * **每次询问** -这是默认设置，需要手动干预任何重要故障。
   * **立即失败** -如果选中此项，则在出现重要故障时将取消管道。 这实质上是模拟用户手动拒绝每个失败。
   * **立即继续** -如果选中此项，则在出现重要故障时管道将自动继续。 这实际上是模拟用户手动批准每个失败。


1. 单击 **下一** 步以访问“ **测试** ”选项卡，为项目定义测试条件。

   ![](assets/set-up-pipeline4.png)

1. 单击&#x200B;**保存**。“概 *述* ”页现在显 **示“部署项目** ”卡。 单击 **“部署** ”按钮以部署项目。

   ![](assets/configure-pipeline5.png)


## 仅限非生产和代码质量的管道

除了部署到舞台和生产的主要管道外，客户还能够建立额外的管道，称 **为非生产管道**。 这些管线始终执行构建和代码质量步骤。 它们还可以选择部署到Adobe Managed Services环境。

在主屏幕上，新卡中列出了以下管线：

1. 从Cloud **Manager主屏幕访问** “非生产管道”拼贴。

   ![](assets/configure-pipeline6.png)

1. 单击“添 **加** ”按钮，指定“管道名称”、“管道类型”和“Git分支”。

   此外，您还可以从管道选项设置部署触发器和重要失败行为。

   ![](assets/non-prod-pipe1.png)

1. 单 **击** “保存”，管线将显示在主屏幕上的卡上，并有三个操作，如下所示：

   ![](assets/configure-pipeline8.png)

   * **编辑** -允许编辑管道设置
   * **构建** -导航到执行页面，可从中执行管道
   * **管理Git** —— 允许用户获取访问Cloud Manager Git存储库所需的信息

## 后续步骤 {#the-next-steps}

配置管道后，您需要部署代码。

有关更多 [详细信息](deploy-code.md) ，请参阅部署代码。
