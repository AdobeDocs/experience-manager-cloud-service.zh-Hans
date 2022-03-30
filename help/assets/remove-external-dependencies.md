---
title: 移除现有安装的外部依赖
description: 移除现有安装的外部依赖
feature: Integrations
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
source-git-commit: b71a78696d4b347c97b077d84b455f53a1747a07
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 17%

---

# 移除现有安装的外部依赖 {#remove-external-depedencies}

Adobe建议您为Workfront的现有增强连接器安装执行配置步骤，以删除对Hoodoo分发点的依赖项。

>[!NOTE]
>
>仅当您在2022年3月之前安装了增强的Workfront连接器时，才执行配置步骤。 从2022年3月开始，Workfront的新增强连接器安装不依赖于Hoodoo分发点。

要删除外部依赖项，请执行以下操作：

1. 从父存储库中删除以下Hoodo存储库配置 `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. 从 `settings.xml` 文件，可在 `./cloudmanager/maven/settings.xml`:

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

1. 执行 [新安装步骤](workfront-connector-install.md).
