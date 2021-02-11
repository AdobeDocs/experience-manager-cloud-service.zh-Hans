---
title: AEM中Cloud Manager作为Cloud Service版本2021.2.0的发行说明
description: AEM中Cloud Manager作为Cloud Service版本2021.2.0的发行说明
translation-type: tm+mt
source-git-commit: bca0519b3f27ee21df41b2292d19e330c4aa5f7d
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---


# 作为Cloud Service2021.2.0 {#release-notes}的Adobe Experience ManagerCloud Manager发行说明

本页概述了AEM中作为Cloud Service2021.2.0的Cloud Manager发行说明。

## 发布日期 {#release-date}

AEM中Cloud Manager作为Cloud Service2021.2.0的发布日期为2021年2月11日。

## Cloud Manager {#cloud-manager}

### 新增功能 {#what-is-new}

* Cloud Manager Production管道现在将包含自定义UI测试功能。

* 资产客户现在可以通过云管理器UI自助选择何时何地部署其品牌门户实例。 对于具有资产解决方案的常规（非沙箱）项目，现在可以在生产环境上设置Brand Portal。 在“生产”环境上只能进行一次设置。

* 项目和沙箱创建中使用的AEM项目原型已更新为版本25。

* 代码扫描过程中标识的已弃用API的列表已得到改进，以包括最新Cloud ServiceSDK版本中已弃用的其他类和方法。

* SonarQueb用户档案, Cloud Manager已更新以删除Sonar规则squid:S2142。 这不再与“线程中断检查”冲突。

* Cloud Manager UI将告知用户暂时无法添加／更新域名，因为关联的环境连接了正在运行的管道，或者当前正在等待批准步骤。

* 现在，将动态删除客户`pom.xml`文件中设置的带声纳前缀的属性，以避免生成和质量扫描失败。

* 云管理器UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则该用户可能暂时无法选择该证书。


### 错误修复 {#bug-fixes}

* 将SSL证书与域名匹配不再区分大小写。

* 现在，如果证书私钥不满足2048位限制，Cloud Manager UI将通知用户并显示相应的错误消息。

* 云管理器UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则该用户可能暂时无法选择该证书。

* 在某些情况下，内部问题可能导致环境删除卡住。

* 某些管线故障被错误报告为管线错误。
