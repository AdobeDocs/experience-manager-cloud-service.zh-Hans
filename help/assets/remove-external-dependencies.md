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

Adobe建議您針對Workfront的現有增強型聯結器安裝執行設定步驟，移除對Hoodoo散發點的相依性。

>[!NOTE]
>
>僅當您在2022年3月之前安裝Workfront的增強型聯結器時，才執行設定步驟。 自2022年3月起，Workfront新的增強型聯結器安裝不會依賴Hoodoo發佈點。

若要移除外部相依性：

1. 從父系移除下列Hoodoo存放庫設定 `pom.xml`：

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. 從移除下列伺服器設定 `settings.xml` 檔案，位於 `./cloudmanager/maven/settings.xml`：

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

1. 執行 [新安裝步驟](workfront-connector-install.md).
