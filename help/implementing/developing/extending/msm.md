---
title: 扩展多站点管理器
description: 了解如何扩展多站点管理器的功能。
source-git-commit: f159f0ef86c2b82da4e7308a0892b4947b6e43fb
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 1%

---


# 扩展多站点管理器 {#extending-the-multi-site-manager}

本文档可帮助您了解如何扩展多站点管理器的功能，并涵盖以下主题。

* 了解MSM Java API的主要成员
* 创建可用于转出配置的新同步操作
* 修改默认语言和国家/地区代码

>[!TIP]
>
>在文档上下文中更容易理解此页面 [重用内容：多站点管理器。](/help/sites-cloud/administering/msm/overview.md)

>[!CAUTION]
>
>多站点管理器及其API在创作网站时使用，因此，它们仅可在创作环境中使用。

## Java API概述 {#overview-of-the-java-api}

多站点管理包含以下包：

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

主MSM API对象进行如下交互（另请参阅部分） [使用的术语](/help/sites-cloud/administering/msm/overview.md#terms-used))：

![主MSM API对象](assets/msm-api-interaction.png)

* **`Blueprint`** - A `Blueprint` (如所示 [Blueprint配置](/help/sites-cloud/administering/msm/overview.md#source-blueprints-and-blueprint-configurations))指定Live Copy可以从其中继承内容的页面。

  ![Blueprint](assets/msm-blueprint-interaction.png)

   * Blueprint配置的使用( `Blueprint`)是可选的，但：

      * 它允许作者使用 **转出** 选项，用于将修改明确推送到从此源继承的活动副本。
      * 它允许作者使用 **创建站点**，允许用户轻松选择语言并配置Live Copy的结构。
      * 它定义了任何生成活动副本的默认转出配置。

* **`LiveRelationship`** - `LiveRelationship` 指定Live Copy分支中的资源与其等效的源/Blueprint资源之间的连接（关系）。

   * 在实现继承和转出时，将使用关系。
   * `LiveRelationship` 对象提供对转出配置的访问（引用） ( `RolloutConfig`)， `LiveCopy`、和 `LiveStatus` 与关系相关的对象。

   * 例如，Live Copy是在中创建 `/content/copy/us` 从源/Blueprint访问 `/content/wknd/language-masters`. 资源 `/content/wknd/language-masters/en/jcr:content` 和 `/content/copy/us/en/jcr:content` 形成一种关系。

* **`LiveCopy`** - A `LiveCopy` 保存关系的配置详细信息(`LiveRelationship`)在live copy资源及其源/blueprint资源之间传递。

   * 使用 `LiveCopy` 用于访问页面路径、源/Blueprint页面路径、转出配置和子页面是否也包含在中 `LiveCopy`.

   * A `LiveCopy` 每次创建节点 **创建站点** 或 **创建Live Copy** 已使用。

* **`LiveStatus`** - `LiveStatus` 对象提供对运行时状态的访问 `LiveRelationship`. 用于查询Live Copy的同步状态。

* **`LiveAction`** - A `LiveAction` 是对转出中涉及的每个资源执行的操作。

   * `LiveAction`s仅由生成 `RolloutConfig`s.

* **`LiveActionFactory`** - A `LiveActionFactory` 创建 `LiveAction` 给定对象 `LiveAction` 配置。 配置将作为资源存储在存储库中。

* **`RolloutConfig`** - `RolloutConfig` 保存列表 `LiveActions`，以便在触发时使用。 此 `LiveCopy` 继承 `RolloutConfig` 并且结果将显示在 `LiveRelationship`.

   * 首次设置Live Copy时也会使用 `RolloutConfig` (触发 `LiveAction`s)。

## 创建新同步操作 {#creating-a-new-synchronization-action}

您可以创建要用于转出配置的自定义同步操作。 在以下情况下，这将很有用 [已安装的操作](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions) 不符合您的特定应用程序要求。

为此，请创建两个类：

* 实施 [`com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) 执行该操作的接口。
* 实施的OSGi组件 [`com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 界面并创建实例 `LiveAction` 类

此 `LiveActionFactory` 创建实例 `LiveAction` 给定配置的类：

* `LiveAction` 类包括以下方法：

   * `getName`  — 返回操作的名称

      * 例如，在转出配置中，名称用于引用操作。

   * `execute`  — 执行操作的任务

* `LiveActionFactory` 类包括以下成员：

   * `LIVE_ACTION_NAME`  — 一个字段，其中包含关联用户的名称， `LiveAction`

      * 此名称必须与 `getName` 方法 `LiveAction` 类。

   * `createAction`  — 创建 `LiveAction`

      * 可选 `Resource` 参数可用于提供配置信息。

   * `createsAction`  — 返回关联的的名称 `LiveAction`

### 访问LiveAction配置节点 {#accessing-the-liveaction-configuration-node}

使用 `LiveAction` 存储库中的配置节点，用于存储影响运行时行为的信息。 `LiveAction` 实例。 存储库中用于存储 `LiveAction` 配置适用于 `LiveActionFactory` 运行时对象。 因此，您可以将属性添加到配置节点，并在中使用它们 `LiveActionFactory` 实施。

例如， `LiveAction` 需要存储Blueprint作者的名称。 配置节点的属性包括存储信息的Blueprint页面的属性名称。 在运行时， `LiveAction` 从配置中检索属性名称，然后获取属性值。

的参数 [`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 方法是 `Resource` 对象。 此 `Resource` 对象表示 `cq:LiveSyncAction` 转出配置中此实时操作的节点。

请参阅文档 [创建转出配置](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration) 以了解更多信息。

与通常使用配置节点时一样，您应该将其调整为 `ValueMap` 对象：

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### 访问目标节点、源节点和LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

以下对象作为 `execute` 方法 `LiveAction` 对象：

* A [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) 表示Live Copy源的对象
* A `Resource` 表示Live Copy目标的对象。
* 此 [`LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) live copy的对象
   * 此 `autoSave` 值指示您的 `LiveAction` 应保存对存储库所做的更改
   * 此 `reset` 值表示转出重置模式。

从这些对象中，您可以获取有关 `LiveCopy`. 您也可以使用 `Resource` 要获取的对象 `ResourceResolver`， `Session`、和 `Node` 对象。 这些对象可用于处理存储库内容：

在以下代码的第一行中，源是 `Resource` 源页面的对象：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>此 `Resource` 参数可以是 `null` 或 `Resources` 不适应的对象 `Node` 对象，例如 [`NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/NonExistingResource.html) 对象。

## 创建新的转出配置 {#creating-a-new-rollout-configuration}

如果安装的转出配置不符合您的应用程序要求，您可以按照以下两个步骤创建转出配置：

* [创建转出配置](#create-the-rollout-configuration)
* [将同步操作添加到转出配置](#add-synchronization-actions-to-the-rollout-configuration)

然后，在Blueprint或Live Copy页面上设置转出配置时，您可以使用新的转出配置。

>[!TIP]
>
>另请参阅 [自定义转出的最佳实践](/help/sites-cloud/administering/msm/best-practices.md#customizing-rollouts).

### 创建转出配置 {#create-the-rollout-configuration}

要创建新的转出配置，请执行以下操作：

1. 打开CRXDE Lite于 `https://<host>:<port>/crx/de`.

1. 导航到 `/apps/msm/<your-project>/rolloutconfigs`，您的项目的自定义版本 `/libs/msm/wcm/rolloutconfigs`.

   * 如果这是您的第一个配置，则 `/libs` 分支必须用作模板，才能在下创建新分支 `/apps`.

1. 在此位置下，创建具有以下属性的节点：

   * **名称**：转出配置的节点名称，例如 `contentCopy` 或 `workflow`
   * **类型**： `cq:RolloutConfig`

1. 将以下属性添加到此节点：

   * **名称**: `jcr:title`
     **类型**： `String`
     **值**：将显示在UI中的标识标题

   * **名称**: `jcr:description`
     **类型**： `String`
     **值**：可选描述。

   * **名称**: `cq:trigger`
     **类型**： `String`
     **值**：和 [转出触发器](/help/sites-cloud/administering/msm/live-copy-sync-config.md#rollout-triggers) 将使用
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. 单击 **全部保存**.

### 将同步操作添加到转出配置 {#add-synchronization-actions-to-the-rollout-configuration}

转出配置存储在以下位置 [转出配置节点](#create-the-rollout-configuration) 您在 `/apps/msm/<your-project>/rolloutconfigs` 节点。

添加类型的子节点 `cq:LiveSyncAction` 以将同步操作添加到转出配置。 同步操作节点的顺序决定了操作发生的顺序。

1. 在CRXDE Lite中，选择您的 [转出配置](#create-the-rollout-configuration) 节点，例如 `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`.

1. 创建具有以下节点属性的节点：

   * **名称**：同步操作的节点名称
      * 名称必须与 **操作名称** 在下面的表格中 [同步操作](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions) 例如 `contentCopy` 或 `workflow`.
   * **类型**： `cq:LiveSyncAction`

1. 根据需要添加并配置所需数量的同步操作节点。

1. 重新排列操作节点，使其顺序与您希望它们出现的顺序相匹配。
   * 最顶层的操作节点首先出现。

## 创建和使用简单的LiveActionFactory类 {#creating-and-using-a-simple-liveactionfactory-class}

按照本节中的步骤来开发 `LiveActionFactory` 并在转出配置中使用它。 这些过程使用Maven和Eclipse开发和部署 `LiveActionFactory`：

1. [创建maven项目](#create-the-maven-project) 并将其导入Eclipse。
1. [添加依赖项](#add-dependencies-to-the-pom-file) 到POM文件。
1. [实施 `LiveActionFactory` 界面](#implement-liveactionfactory) 和部署OSGi捆绑包。
1. [创建转出配置](#create-the-example-rollout-configuration).
1. [创建Live Copy](#create-the-live-copy).

[Maven项目和Java类的源代码](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout) 在公共Git存储库中提供。

### 创建Maven项目 {#create-the-maven-project}

以下过程要求您已添加 `adobe-public` 配置文件到您的Maven设置文件。

* 有关adobe-public配置文件的信息，请参阅 [获取内容包Maven插件](/help/implementing/developing/tools/maven-plugin.md#obtaining-the-content-package-maven-plugin)
* 有关Maven设置文件的信息，请参阅Maven [设置参考](https://maven.apache.org/settings.html).

1. 打开终端或命令行会话，并将目录更改为指向创建项目的位置。
1. 输入以下命令：

   ```text
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在交互式提示下指定以下值：

   * **`groupId`**： `com.adobe.example.msm`
   * **`artifactId`**: `MyLiveActionFactory`
   * **`version`**: `1.0-SNAPSHOT`
   * **`package`**: `MyPackage`
   * **`appsFolderName`**: `myapp`
   * **`artifactName`**: `MyLiveActionFactory package`
   * **`packageGroup`**: `myPackages`

1. 启动Eclipse和 [导入Maven项目。](/help/implementing/developing/tools/eclipse.md#import-the-maven-project-into-eclipse)

### 向POM文件添加依赖项 {#add-dependencies-to-the-pom-file}

添加依赖关系，以便Eclipse编译器可以引用在 `LiveActionFactory` 代码。

1. 在Eclipse项目资源管理器中，打开文件 `MyLiveActionFactory/pom.xml`.

1. 在编辑器中，单击 `pom.xml` 选项卡并找到 `project/dependencyManagement/dependencies` 部分。

1. 将以下XML添加到 `dependencyManagement` 元素，然后保存该文件。

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. 从打开包的POM文件 **项目资源管理器** 在 `MyLiveActionFactory-bundle/pom.xml`.

1. 在编辑器中，单击 `pom.xml` 选项卡，并找到项目/依赖关系部分。 在依赖关系元素中添加以下XML，然后保存该文件：

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### 实施LiveActionFactory {#implement-liveactionfactory}

以下各项 `LiveActionFactory` 类实现 `LiveAction` 会记录有关源页面和目标页面的消息，并复制 `cq:lastModifiedBy` 属性从源节点到目标节点。 实时操作的名称为 `exampleLiveAction`.

1. 在Eclipse项目资源管理器中，右键单击 `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` 包并单击 **新建** -> **类**.

1. 对于 **名称**，输入 `ExampleLiveActionFactory` 然后单击 **完成**.

1. 打开 `ExampleLiveActionFactory.java` 文件，使用以下代码替换内容，然后保存文件。

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. 使用终端或命令会话，将目录更改为 `MyLiveActionFactory` 目录（Maven项目目录）。 然后，输入以下命令：

   ```shell
   mvn -PautoInstallPackage clean install
   ```

1. AEM `error.log` 文件应指示捆绑包已启动，并在的日志中可见 `https://<host>:<port>/system/console/status-slinglogs`.

   ```text
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### 创建示例转出配置 {#create-the-example-rollout-configuration}

创建使用的MSM转出配置 `LiveActionFactory` 您创建的项目：

1. 创建和配置 [使用标准过程转出配置](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration) 使用属性：

   * **标题**：示例转出配置
   * **名称**： exampleerolloutconfig
   * **cq：trigger**： `publish`

### 将实时操作添加到示例转出配置 {#add-the-live-action-to-the-example-rollout-configuration}

配置您在上一步中创建的转出配置，以使其使用 `ExampleLiveActionFactory` 类。

1. 打开CRXDE Lite。

1. 在下创建以下节点 `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`：

   * **名称**: `exampleLiveAction`
   * **类型**： `cq:LiveSyncAction`

1. 单击 **全部保存**.

1. 选择 `exampleLiveAction` 节点，并添加一个属性来指示 `ExampleLiveAction` 类 `cq:LastModifiedBy` 属性应该从源复制到目标节点。

   * **名称**: `repLastModBy`
   * **类型**： `Boolean`
   * **值**: `true`

1. 单击 **全部保存**.

### 创建Live Copy {#create-the-live-copy}

[创建Live copy](/help/sites-cloud/administering/msm/creating-live-copies.md#creating-a-live-copy-of-a-page) ，位于WKND参考网站的英语/产品分支上，使用您的转出配置：

* **来源**: `/content/wknd/language-masters/en/products`

* **转出配置**：示例转出配置

激活 **产品** （英语）页面，并观察日志消息 `LiveAction` 类生成：

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

## 更改语言名称和默认国家/地区 {#changing-language-names-and-default-countries}

AEM使用一组默认的语言和国家/地区代码。

* 默认语言代码是ISO-639-1定义的小写形式的双字母代码。
* 默认国家/地区代码是ISO 3166定义的小写或大写形式的双字母代码。

MSM使用存储的语言和国家/地区代码列表来确定与页面的语言版本名称关联的国家/地区名称。 如果需要，可以更改列表的以下方面：

* 语言标题
* 国家/地区名称
* 语言的默认国家/地区(对于代码，如 `en`， `de`，等等)

语言列表存储在 `/libs/wcm/core/resources/languages` 节点。 每个子节点表示一种语言或一种语言国家/地区：

* 节点的名称是语言代码(例如 `en` 或 `de`)或language_country代码(如 `en_us` 或 `de_ch`)。

* 此 `language` 节点的属性存储代码的语言的全名。
* 此 `country` 节点的属性存储代码所在国家/地区的全名。
* 当节点名称仅由语言代码(如 `en`)，则国家/地区属性为 `*`和另一个 `defaultCountry` 属性存储语言 — 国家/地区的代码以指示要使用的国家/地区。

![语言定义](assets/msm-language-manager.png)

要修改语言，请执行以下操作：

1. 打开CRXDE Lite。
1. 选择 `/apps` 文件夹并单击 **创建**，则 **创建文件夹。**

1. 命名新文件夹 `wcm`.

1. 重复上一步创建 `/apps/wcm/core` 文件夹树。 创建节点类型 `sling:Folder` 在 `core` 已调用 `resources`.

1. 右键单击 `/libs/wcm/core/resources/languages` 节点并单击 **复制**.
1. 右键单击 `/apps/wcm/core/resources` 文件夹并单击 **粘贴**. 根据需要修改子节点。
1. 单击 **全部保存**.
1. 单击 **工具**， **操作** 则 **Web控制台**. 从该控制台单击 **osgi**，则 **配置**.
1. 找到并单击 **Day CQ WCM语言管理器**，并更改的值 **语言列表** 到 `/apps/wcm/core/resources/languages`，然后单击 **保存**.

   ![Day CQ WCM语言管理器](assets/msm-language-manager.png)

## 配置页面属性上的MSM锁定 {#configuring-msm-locks-on-page-properties}

创建自定义页面属性时，您可能需要考虑新属性是否应该有资格转出到任何活动副本。

例如，如果要添加两个新页面属性：

* 联系电子邮件:

   * 此属性不需要推出，因为每个国家/地区（或品牌等）的此属性将不同。

* 关键可视样式：

   * 项目要求是推出此属性，因为此属性（通常）对所有国家/地区（或品牌等）通用。

然后，您需要确保：

* 联系电子邮件:

   * 将从转出属性中排除。
   * 请参阅文档 [配置Live Copy同步](/help/sites-cloud/administering/msm/live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) 以了解更多信息。

* 关键可视样式：

   * 确保除非取消继承，否则不允许编辑此属性。
   * 另外，请确保您随后可以恢复继承。 可通过单击切换以指示连接状态的链/断链链接来控制连接。

页面属性是否需要进行转出，从而需要在编辑时取消/恢复继承，这将由对话框属性进行控制：

* `cq-msm-lockable`

   * 这将在对话框中创建链链接符号。
   * 仅当取消继承（链链接断开）时，才允许进行编辑。
   * 这仅适用于资源的第一个子级别
      * **类型**： `String`
      * **值**：持有正在审议的资产的名称，其价值相当于该资产的价值 `name`
         * 例如，请参阅
           `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

时间 `cq-msm-lockable` 已定义，断开/关闭链将通过以下方式与MSM交互：

* 如果值 `cq-msm-lockable` 为：

   * **相对** (例如， `myProperty` 或 `./myProperty`)

      * 中断该链将添加和从中移除属性 `cq:propertyInheritanceCancelled`.

   * **绝对** (例如， `/image`)

      * 中断链将通过添加以下内容来取消继承 `cq:LiveSyncCancelled` mixin到 `./image` 和设置 `cq:isCancelledForChildren` 到 `true`.

      * 关闭链将恢复继承。

>[!NOTE]
>
>`cq-msm-lockable` 适用于要编辑的资源的第一个子级别，并且该值在任何更深入的级别祖先上不起作用，无论其定义为绝对值还是相对值。

>[!NOTE]
>
>当您重新启用继承时，Live Copy页面属性不会自动与源属性同步。 如果需要，您可以手动请求同步。
