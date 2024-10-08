---
title: 更新 [!DNL Workfront for Experience Manager enhanced connector]
description: 更新 [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 09276b4d-a7c8-4927-8c0a-40eda48e55a7
feature: Workfront Integrations and Apps
role: Admin
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%

---

# 更新[!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

| [搜索最佳实践](/help/assets/search-best-practices.md) | [元数据最佳实践](/help/assets/metadata-best-practices.md) | [Content Hub](/help/assets/product-overview.md) | 具有OpenAPI功能的[Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets开发人员文档](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

[!UICONTROL Experience Manager Assetsas a Cloud Service]允许您将[!DNL Workfront for Experience Manager enhanced connector]从以前的版本更新到最新的版本。

>[!TIP]
>
>您是否正在搜索AEM 6.5的[!DNL Workfront for Experience Manager enhanced connector]更新文档？ 单击[此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-connector-install.html?lang=en##update-enhanced-connector-for-workfront)。


要将[!DNL Workfront for Experience Manager enhanced connector]更新到最新版本，请执行以下操作：

1. 从[Adobe软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/workfront-tools.ui.apps.zip)下载增强型连接器的最新版本。

1. [访问](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/accessing-repos.html?lang=en)并从Cloud Manager克隆AEM as a Cloud Service存储库。

1. 使用您选择的IDE打开克隆的Experience Manageras a Cloud Service存储库。

1. 将步骤1中下载的增强型连接器zip文件放在以下路径中：

   ```TXT
      /ui.apps/src/main/resources/<zip file>
   ```

   >[!NOTE]
   >
   >如果`resources`文件夹不存在，请创建该文件夹。

1. 更新父`pom.xml`中的增强型连接器版本。

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

1. 更新`all module pom.xml`中的依赖项。

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
   >请确保在步骤5和步骤6中将`<scope>`和`<systemPath>`添加到依赖项。

1. 更新`pom.xml`嵌入。 将[!DNL Workfront for Experience Manager enhanced connector]包添加到所有子项目的`pom.xml`的`embeddeds`部分。 将更新合并到所有模块`pom.xml`中。

   ```XML
   <!-- Workfront Tools -->
   <embedded>
      <groupId>digital.hoodoo</groupId>
      <artifactId>workfront-tools.ui.apps</artifactId>
      <type>zip</type>
      <target>/apps/<path-to-project-install-folder>/install</target>
   </embedded>
   ```

   嵌入节的目标设置为`/apps/<path-to-project-install-folder>/install`。 此JCR路径`/apps/<path-to-project-install-folder>`必须包含在`all/src/main/content/META-INF/vault/filter.xml`文件的筛选器规则中。 存储库的过滤器规则通常派生自项目名称。 使用文件夹名称作为现有规则中的目标。

1. [删除Hoodoo分发点上的依赖项](remove-external-dependencies.md)（如果有）。

1. 将更改推送到存储库。

1. 运行管道以[将更改部署到Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code.html)。
