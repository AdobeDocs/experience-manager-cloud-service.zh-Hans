---
title: 删除现有安装的外部依赖项
description: 安装 [!DNL Workfront for Experience Manager enhanced connector]
feature: Integrations
source-git-commit: b61915a27968b11472ae458d7be3d73f3449fbbe
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 1%

---


# 删除现有安装的外部依赖项 {#remove-external-depedencies}

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

