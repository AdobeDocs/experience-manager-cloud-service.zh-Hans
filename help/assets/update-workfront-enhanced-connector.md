---
title: 更新 [!DNL Workfront for Experience Manager enhanced connector]
description: 更新 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
source-git-commit: 77aceab8db82082185c931202fc6ea8eee79c11e
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assetsas a Cloud Service] 使您能够更新 [!DNL Workfront for Experience Manager enhanced connector] 从以前的版本到最新的版本。

>[!TIP]
>
>您是否正在搜索 [!DNL Workfront for Experience Manager enhanced connector] AEM 6.5的更新文档？ 单击 [此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


要更新 [!DNL Workfront for Experience Manager enhanced connector] 到最新版本：

1. 从下载最新版本的增强型连接器 [Adobe软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) 和从Cloud Manager克隆AEMas a Cloud Service存储库。

1. 使用您选择的IDE打开克隆的Experience Manageras a Cloud Service存储库。

1. 将步骤1中下载的增强型连接器zip文件放在以下路径中：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果 `resources` 文件夹不存在，请创建文件夹。

1. 更新父级中的增强型连接器版本 `pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <version> updated enhanced connector version number</version>
         <scope>system</scope>
         <systemPath>${project.basedir}/ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

1. 更新中的依赖关系 `all module pom.xml`.

   ```XML
      <dependency>
         <groupId>digital.hoodoo</groupId>
         <artifactId>workfront-tools.ui.apps</artifactId>
         <type>zip</type>
         <scope>system</scope>
         <systemPath>${project.basedir}/../ui.apps/src/main/resources/workfront-tools.ui.apps.zip</systemPath>
      </dependency>
   ```

   >[!NOTE]
   >
   >确保添加 `<scope>` 和 `<systemPath>` 步骤5和步骤6中的依赖关系。

1. 更新 `pom.xml` 嵌入。 添加 [!DNL Workfront for Experience Manager enhanced connector] 包到 `embeddeds` 部分 `pom.xml` 您的所有子项目的URL。 在所有模块中纳入更新 `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   嵌入节的目标设置为 `/apps/<path-to-project-install-folder>/install`. 此JCR路径 `/apps/<path-to-project-install-folder>` 必须包含在的筛选规则中 `all/src/main/content/META-INF/vault/filter.xml` 文件。 存储库的过滤器规则通常派生自项目名称。 使用文件夹名称作为现有规则中的目标。

1. [删除对Hoodoo分发点的依赖关系](remove-external-dependencies.md)，如果有。

1. 将更改推送到存储库。

1. 将管道运行到 [将更改部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
