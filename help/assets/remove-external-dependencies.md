---
title: 移除现有安装的外部依赖
description: 移除现有安装的外部依赖
feature: Workfront Integrations and Apps
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
role: Admin
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 17%

---

# 移除现有安装的外部依赖 {#remove-external-depedencies}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Adobe建议您为Workfront的现有增强型连接器安装执行配置步骤，以删除对Hoodoo分发点的依赖项。

>[!NOTE]
>
>仅当您在2022年3月之前安装了Workfront的增强型连接器时，才执行配置步骤。 从2022年3月开始，Workfront的新增强连接器安装不依赖于Hoodoo分发点。

要删除外部依赖项，请执行以下操作：

1. 从父`pom.xml`中删除以下Hoodoo存储库配置：

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. 从`settings.xml`文件（位于`./cloudmanager/maven/settings.xml`）中删除以下服务器配置：

   ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
   ```

1. 执行[新安装步骤](workfront-connector-install.md)。
