---
title: 更新 [!DNL Workfront for Experience Manager enhanced connector]
description: 更新 [!DNL Workfront for Experience Manager enhanced connector]
source-git-commit: 34f3cf925a3ea58de176521be459a61f4317eec3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 1%

---

# 更新 [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

[!UICONTROL Experience Manager Assetsas a Cloud Service] 允许您更新 [!DNL Workfront for Experience Manager enhanced connector] 从以前的版本到最新版本。

>[!TIP]
>
>您正在搜索 [!DNL Workfront for Experience Manager enhanced connector] 更新了AEM 6.5文档？ 单击 [此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront).


要更新 [!DNL Workfront for Experience Manager enhanced connector] 到最新版本：

1. 从下载最新版本的增强型连接器 [AdobeSoftware Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip).

1. [访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en) 和从Cloud Manager克隆AEMas a Cloud Service存储库。

1. 使用您选择的IDE打开克隆的Experience Manageras a Cloud Service存储库。

1. 将步骤1中下载的增强型连接器zip文件放置在以下路径中：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果 `resources` 文件夹不存在，请创建文件夹。

1. 在父项中更新增强的连接器版本 `pom.xml`.

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

1. 在中更新依赖项 `all module pom.xml`.

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
   >确保添加 `<scope>` 和 `<systemPath>` 到步骤5和步骤6中的依赖项。

1. 更新 `pom.xml` 嵌入。 添加 [!DNL Workfront for Experience Manager enhanced connector] 包到 `embeddeds` 部分 `pom.xml` 所有子项目。 在所有模块中整合更新 `pom.xml`.

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   嵌入部分的目标设置为 `/apps/<path-to-project-install-folder>/install`. 此JCR路径 `/apps/<path-to-project-install-folder>` 必须包含在 `all/src/main/content/META-INF/vault/filter.xml` 文件。 存储库的筛选规则通常从程序名称派生。 在现有规则中使用文件夹的名称作为目标。

1. [删除对Hoodo分布点的依赖项](remove-external-dependencies.md)，如果有。

1. 将更改推送到存储库。

1. 运行管道以 [将更改部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html).
