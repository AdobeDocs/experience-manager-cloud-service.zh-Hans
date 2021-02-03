---
title: 内容片段——配置浏览器
description: 了解如何在配置浏览器中启用某些内容片段功能。
translation-type: tm+mt
source-git-commit: 260578950833b96616a2a3928d206e6f9e0a206a
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 21%

---


# 内容片段——配置浏览器{#content-fragments-configuration-browser}

## 为实例{#enable-content-fragment-functionality-instance}启用内容片段功能

在使用内容片段之前，您需要使用&#x200B;**配置浏览器**&#x200B;来启用：

* **内容片段模型** -必填
* **GraphQL永久查询** -可选

>[!CAUTION]
>
>如果不启用&#x200B;**内容片段模型**，则创建&#x200B;**选项将不可用于创建新模型。**

要启用内容片段功能，您需要：

* 通过配置浏览器启用内容片段功能
* 将配置应用到您的资产文件夹

### 在配置浏览器{#enable-content-fragment-functionality-in-configuration-browser}中启用内容片段功能

要[使用某些内容片段功能](#creating-a-content-fragment-model),**必须首先通过**&#x200B;配置浏览器&#x200B;**启用它们：**

>[!NOTE]
>
>有关详细信息，另请参阅[配置浏览器：](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)。

>[!CAUTION]
>
>子配置（嵌套在配置中的配置）不支持与内容片段一起使用。

1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**配置浏览器**。

1. 使用&#x200B;**创建**&#x200B;打开对话框，其中：

   1. 指定&#x200B;**标题**。
   1. 要启用其使用选择
      * **内容片段模型**
      * **GraphQL永久查询**

      ![定义配置](assets/cfm-conf-01.png)


1. 选择&#x200B;**创建**&#x200B;以保存定义。

<!-- 1. Select the location appropriate to your website. -->

### 将配置应用于您的资产文件夹{#apply-the-configuration-to-your-assets-folder}

为内容片段功能启用配置&#x200B;**global**&#x200B;后，将应用于任何资产文件夹。

要将其他配置（即不包括全局配置）与类似的 Assets 文件夹一起使用，您必须定义连接。这是通过在相应文件夹的“ **文件夹属性** ”的“云服务 **”选项卡中选****** 择相应的配置来完成的。

![应用配置](assets/cfm-conf-02.png)