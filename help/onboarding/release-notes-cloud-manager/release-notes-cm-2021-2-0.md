---
title: AEM中Cloud Manager作为Cloud Service版本2021.2.0的发行说明
description: AEM中Cloud Manager作为Cloud Service版本2021.2.0的发行说明
translation-type: tm+mt
source-git-commit: 32557b3f25e4d4f4cb652f19cff4dae58638e07b
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 2%

---


# Adobe Experience Manager中Cloud Manager作为Cloud Service 2021.2.0 {#release-notes}的发行说明

本页概述了AEM中作为Cloud Service 2021.2.0的Cloud Manager发行说明。

## 发布日期 {#release-date}

AEM中Cloud Manager作为Cloud Service 2021.2.0的发布日期为2021年2月11日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* Assets客户现在可以通过Cloud Manager UI以自助方式选择何时何地部署其Brand Portal实例。 对于具有资产解决方案的常规（非沙箱）项目，现在可以在生产环境上设置Brand Portal。 在生产环境上只能执行一次设置。

* 在“项目”和“沙箱创建”中使用的AEM Project原型已更新为版本25。

* 在代码扫描过程中识别的已弃用API的列表已得到改进，以包括最新Cloud Service SDK版本中已弃用的其他类和方法。

* SonarQube 用户档案 for Cloud Manager已更新以删除Sonar规则squid:S2142。 这不再与“线程中断检查”冲突。

* Cloud Manager UI将通知暂时无法添加/更新域名的用户，因为关联的环境已连接正在运行的管道，或者当前正在等待批准步骤。

* 现在，将动态删除客户`pom.xml`文件中设置的属性，以避免生成和质量扫描失败。

* Cloud Manager UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则该用户可能暂时无法选择该证书。

* 已添加其他代码质量规则，以解决Cloud Service兼容性问题。

### 错误修复 {#bug-fixes}

* 与域名匹配的SSL证书不再区分大小写。

* 现在，如果证书私钥不符合2048位限制，Cloud Manager用户界面将通知用户，并显示相应的错误消息。

* Cloud Manager UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则用户可能暂时无法选择该证书。

* 在某些情况下，内部问题可能导致环境删除卡住。

* 某些管线故障被错误地报告为管线错误。
