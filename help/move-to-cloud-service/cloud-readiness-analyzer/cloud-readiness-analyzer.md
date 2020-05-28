---
title: 评估移向云服务的复杂性
description: 评估移向云服务的复杂性
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 云就绪性分析器 {#accesing-complexity}

## 概述 {#overview}

云就绪性分析器(CRA)允许您通过检测以下模式检查现有AEM实例是否准备好迁移到云服务：

* 使用云服务当前不支持的AEM 6.x功能

* 违反将受移动到云服务影响的特定规则

>[!NOTE]
>CRA的输出加快了对转向云服务所需开发工作的评估。

## 设置云就绪性分析器 {#setting-up-cra}

CRA以包形式发布，可处理来自XX及更高版本的任何源AEM版本，探索转向云服务。

它可在软件分发门户上找到，并可使用包管理器进行安装。

### 使用云就绪性分析器 {#using-cra}

>[!NOTE]
> CRA可以在任何环境运行，包括本地开发实例。

>[重要]
>但是，为了提高检测率并避免关键业务实例的任何速度减慢，建议在登台环境上运行它，该登台尽可能接近用户应用程序、内容和配置的生产实例

### 在云就绪性分析器上查看输出 {#viewing-output-cra}


1. 通过使用浏览至Adobe Experience Manager Web Console **配置，导航到AEM Web** Console `https://serveraddress:serverport/system/console/configMgr`。

1. 选择状态——云就绪性分析器，如下图所示。

1. 您还可以通过基于反应文本或常规JSON界面视图输出。

>[!NOTE]
> 有关这些 [方法的更多详](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) 细信息，请参阅图案检测器。) CRA准备就绪后，需要添加此部分。

## 云就绪性的后续步骤 {#the-next-steps}

要获取有关您准备使用云服务的更多信息，Adobe需要评估CRA的输出。

请按照以下步骤发送回文件：

1. 导航到AEM Web Console并下载xx文件，如下图所示。

1. 打开DayCare票证，通过以下方式将文件发送到Adobe:
   1. 在标题为“云就绪性分析器输出”的 **日托中记录支持票证**
   1. 将输出文件附加到票证

