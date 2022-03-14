---
title: AEM 2021.2.0版中Cloud Manageras a Cloud Service的发行说明
description: AEM 2021.2.0版中Cloud Manageras a Cloud Service的发行说明
exl-id: 281f9523-dec2-44f1-9459-5a45d48489d9
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 2%

---

# Adobe Experience Manager as a Cloud Service 2021.2.0版中的Cloud Manager发行说明 {#release-notes}

本页概述了AEM 2021.2.0版中Cloud Manager的发行说明。

## 发布日期 {#release-date}

AEM 2021.2.0版中Cloud Manager的发布日期是2021年2月11日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* Assets客户现在可以通过Cloud Manager UI以自助方式选择何时何地部署其Brand Portal实例。 对于具有Assets解决方案的常规（非沙盒）计划，现在可以在生产环境中配置Brand Portal。 在生产环境中只能完成一次配置。

* 项目和沙盒创建中使用的AEM项目原型已更新到版本25。

* 代码扫描过程中标识的已弃用API列表已得到细化，以包含最新Cloud ServiceSDK版本中已弃用的其他类和方法。

* 更新了Cloud Manager的SonarQube配置文件，以删除Sonar规则squid:S2142。 这不再与线程中断检查冲突。

* Cloud Manager UI将通知那些暂时无法添加/更新域名的用户，因为关联的环境要么具有附加在其上的正在运行的管道，要么当前正在等待批准步骤。

* 客户中设置的属性 `pom.xml` 现在将动态删除带有声纳前缀的文件，以避免生成和质量扫描失败。

* Cloud Manager UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则用户可能暂时无法选择该证书。

* 已添加其他代码质量规则以解决Cloud Service兼容性问题。

### 错误修复  {#bug-fixes}

* 将SSL证书与域名匹配不再区分大小写。

* 现在，如果证书私钥不符合2048位限制，Cloud Manager UI将通知用户，并显示相应的错误消息。

* Cloud Manager UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则用户可能暂时无法选择该证书。

* 在某些情况下，内部问题可能会导致环境删除卡住。

* 某些管道故障被错误地报告为管道错误。
