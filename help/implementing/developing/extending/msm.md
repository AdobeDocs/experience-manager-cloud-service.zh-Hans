---
title: 扩展多站点管理器
description: 了解如何扩展多站点管理器的功能。
exl-id: 4b7a23c3-65d1-4784-9dea-32fcceca37d1
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '2435'
ht-degree: 99%

---

# 扩展多站点管理器 {#extending-the-multi-site-manager}

本文档可帮助您了解如何扩展多站点管理器的功能，并涵盖以下主题。

* 了解 MSM Java API 的主要成员 
* 创建可在转出配置中使用的新的同步操作
* 修改默认语言和国家代码

>[!TIP]
>
>本页在文件[重用内容：多站点管理器](/help/sites-cloud/administering/msm/overview.md)提供的上下文中更容易理解。

>[!CAUTION]
>
>多站点管理器及其 API 会在创作网站时使用，因此仅适用于创作环境。

## Java API 概述 {#overview-of-the-java-api}

多站点管理由以下软件包组成：

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.commons](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

主要的 MSM API 对象交互如下（另请参阅[使用的术语](/help/sites-cloud/administering/msm/overview.md#terms-used)）：

![主要 MSM API 对象](assets/msm-api-interaction.png)

* **`Blueprint`**-  `Blueprint`（如 [ Blueprint 配置](/help/sites-cloud/administering/msm/overview.md#source-blueprints-and-blueprint-configurations)）会指定 Live Copy 可以继承内容的页面。

  ![Blueprint](assets/msm-blueprint-interaction.png)

   * 使用 Blueprint 配置 (`Blueprint`) 是可选的，但是：

      * 它允许作者对源使用&#x200B;**转出**&#x200B;选项，以便明确地将修改推送到从该源继承的 Live Copy。
      * 它允许作者使用&#x200B;**创建站点**&#x200B;功能，以便用户轻松地选择语言并配置 Live Copy 的结构。
      * 它定义了任何生成的 Live Copy 的默认转出配置。

* **`LiveRelationship`**-  `LiveRelationship`指定 Live Copy 分支中的资源与其等效源/Blueprint 资源之间的连接（关系）。

   * 这些关系会在实现继承和转出时使用。
   * `LiveRelationship` 对象提供对与关系相关的转出配置 (`RolloutConfig`), `LiveCopy`, 和 `LiveStatus` 对象的访问（引用）。

   * 例如，Live Copy 会在 `/content/copy/us` 中从 `/content/wknd/language-masters` 的源/Blueprint 进行创建。资源 `/content/wknd/language-masters/en/jcr:content` 和 `/content/copy/us/en/jcr:content` 建立关系。

* **`LiveCopy`**-  `LiveCopy`保存 Live Copy 资源与其源/Blueprint 资源之间关系 (`LiveRelationship`) 的配置详细信息。

   * 使用 `LiveCopy` 类来访问页面路径、源/Blueprint 页面的路径、转出配置以及 `LiveCopy` 中是否也包含子页面。

   * 每次使用&#x200B;**创建站点**&#x200B;或&#x200B;**创建 Live Copy** 时，都会创建一个 `LiveCopy` 节点。

* **`LiveStatus`** - `LiveStatus` 对象提供对 `LiveRelationship` 运行时状态的访问。用于查询 Live Copy 的同步状态。

* **`LiveAction`**-  `LiveAction` 是对转出中涉及的每个资源执行的操作。

   * `LiveAction` 仅由 `RolloutConfig` 生成。

* **`LiveActionFactory`**-  `LiveActionFactory` 在给定 `LiveAction` 配置的情况下创建 `LiveAction` 对象。配置作为资源存储在存储库中。

* **`RolloutConfig`**-  `RolloutConfig` 包含 `LiveActions` 的列表，可在触发时使用。`LiveCopy` 继承了 `RolloutConfig`，而结果则显示在 `LiveRelationship` 中。

   * 第一次设置 Live Copy 也会使用 `RolloutConfig`（这会触发 `LiveAction`）。

## 创建新的同步操作 {#creating-a-new-synchronization-action}

您可以创建自定义同步操作，以与您的转出配置一起使用。当[安装的操作](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions)不符合您的特定应用程序要求时，这可能很有用。

为此，请创建两个类：

* 执行操作的 [`com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) 接口的实施。
* 实现 [`com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 接口并创建 `LiveAction` 类实例的 OSGi 组件

`LiveActionFactory` 为给定配置创建 `LiveAction` 类的实例：

* `LiveAction` 类包括以下方法：

   * `getName` - 返回操作的名称

      * 该名称用于指代该操作，例如在推出配置中。

   * `execute` - 执行该操作的任务

* `LiveActionFactory` 类包括以下成员：

   * `LIVE_ACTION_NAME` - 包含关联名称的字段`LiveAction`

      * 此名称必须与 `LiveAction` 类的 `getName` 方法返回的值一致。

   * `createAction` - 创建一个 `LiveAction` 的实例

      * 可选的 `Resource` 参数可用于提供配置信息。

   * `createsAction` - 返回关联的名称`LiveAction`

### 访问 LiveAction 配置节点 {#accessing-the-liveaction-configuration-node}

使用存储库中的 `LiveAction` 配置节点，以存储影响 `LiveAction` 实例的运行时行为的信息。存储库中存储 `LiveAction` 配置的节点在运行时可用于 `LiveActionFactory` 对象。因此，您可以将属性添加到配置节点，并根据需要在 `LiveActionFactory` 实施中使用它们。

例如，`LiveAction` 需要存储 Blueprint 作者的姓名。配置节点的属性包括存储该信息的 Blueprint 页面的属性名称。在运行时，`LiveAction` 会从配置中检索属性名称，然后获取属性值。

[`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) 方法的参数是一个 `Resource` 对象。该 `Resource` 对象表示转出配置中此实时操作的 `cq:LiveSyncAction` 节点。

请参阅文档[创建转出配置](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration)，了解更多信息。

像往常一样，当使用配置节点时，您应该将其调整为 `ValueMap` 对象：

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

### 访问目标节点、源节点和 LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

以下对象作为 `LiveAction` 对象的 `execute` 方法的参数提供：

* 表示 Live Copy 源的 [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) 对象
* 表示 Live Copy 目标的 `Resource` 对象
* Live Copy 的 [`LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) 对象
   * `autoSave` 值表明您的 `LiveAction` 是否应该保存对存储库所做的更改
   * `reset` 值表示转出重置模式。

从这些对象中您可以获得有关 `LiveCopy` 的所有信息。您还可以使用 `Resource` 对象，获取`ResourceResolver`、`Session`和`Node`对象。这些对象对于操作存储库内容非常有用：

在以下代码的第一行中，源是源页面的 `Resource` 对象：

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>`Resource` 参数可能是不适应 `Node` 对象的 `null` 或 `Resources` 对象，如 [`NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/NonExistingResource.html) 对象。

## 创建新的转出配置 {#creating-a-new-rollout-configuration}

当安装的转出配置不符合您的应用程序要求时，您可以采取以下步骤创建转出配置：

* [创建转出配置](#create-the-rollout-configuration)
* [将同步操作添加到转出配置中](#add-synchronization-actions-to-the-rollout-configuration)

然后，在 Blueprint 或 Live Copy 页面上设置转出配置时，您就可以使用新的转出配置。

>[!TIP]
>
>另请参阅[自定义转出的最佳实践](/help/sites-cloud/administering/msm/best-practices.md#customizing-rollouts)。

### 创建转出配置 {#create-the-rollout-configuration}

要创建转出配置，请执行以下操作：

1. 在 `https://<host>:<port>/crx/de` 打开 CRXDE Lite。

1. 导航至 `/apps/msm/<your-project>/rolloutconfigs`，您的项目的 `/libs/msm/wcm/rolloutconfigs` 定制版本。

   * 如果这是您的第一项配置，则必须使用此 `/libs` 分支作为模板来在 `/apps` 下创建新的分支。

1. 在此位置下，创建一个具有以下属性的节点：

   * **姓名**：转出配置的节点名称，例如 `contentCopy` 或者 `workflow`
   * **类型**：`cq:RolloutConfig`

1. 向该节点添加以下属性：

   * **名称**：`jcr:title`
     **类型**：`String`
     **值**：在 UI 中出现的识别标题

   * **名称**：`jcr:description`
     **类型**：`String`
     **值**：可选描述。

   * **名称**：`cq:trigger`
     **类型**：`String`
     **值**：要使用的[转出触发器](/help/sites-cloud/administering/msm/live-copy-sync-config.md#rollout-triggers)
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. 单击&#x200B;**全部保存**。

### 将同步操作添加到转出配置中 {#add-synchronization-actions-to-the-rollout-configuration}

转出配置存储在您在 `/apps/msm/<your-project>/rolloutconfigs` 节点下创建的[转出设置节点](#create-the-rollout-configuration)下。

添加类型为 `cq:LiveSyncAction` 的子节点，将同步操作添加到转出配置中。同步操作节点的顺序决定了操作发生的顺序。

1. 在 CRXDE Lite 中，选择您的[转出配置](#create-the-rollout-configuration)节点，例如 `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`。

1. 创建具有以下节点属性的节点：

   * **名称**：同步操作的节点名称
      * 该名称必须与[同步操作](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions)下表中的&#x200B;**操作名称**&#x200B;相同，如 `contentCopy` 或 `workflow`。
   * **类型**：`cq:LiveSyncAction`

1. 根据需要添加和配置任意数量的同步操作节点。

1. 重新排列操作节点，使其顺序与您希望它们发生的顺序相一致。
   * 最顶层的操作节点首先出现。

## 创建和使用简单的 LiveActionFactory 类 {#creating-and-using-a-simple-liveactionfactory-class}

按照本节中的程序开发一个 `LiveActionFactory`，并在转出配置中使用它。该程序使用 Maven 和 Eclipse 来开发和部署 `LiveActionFactory`：

1. [创建 maven 项目](#create-the-maven-project)并将其导入到 Eclipse 中。
1. [将依赖项添加](#add-dependencies-to-the-pom-file)到 POM 文件。
1. [实施`LiveActionFactory`界面](#implement-liveactionfactory)，并部署 OSGi 包。
1. [创建转出配置](#create-the-example-rollout-configuration)
1. [创建 Live Copy](#create-the-live-copy)。

[Maven 项目和 Java 类的源代码](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)可在公共 Git 存储库中找到。

### 创建 Maven 项目 {#create-the-maven-project}

以下程序要求您已向 Maven 设置文件添加了 `adobe-public` 配置文件。

* 有关 Adobe 公开配置文件的信息，请参阅[获取内容包 Maven 插件](/help/implementing/developing/tools/maven-plugin.md#obtaining-the-content-package-maven-plugin)
* 有关 Maven 设置文件的信息，请参阅 Maven [设置参考](https://maven.apache.org/settings.html)。

1. 打开终端或命令行会话，并将目录更改为指向创建项目的位置。
1. 输入以下命令：

   ```text
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. 在交互式提示处指定以下值：

   * **`groupId`**：`com.adobe.example.msm`
   * **`artifactId`**：`MyLiveActionFactory`
   * **`version`**：`1.0-SNAPSHOT`
   * **`package`**：`MyPackage`
   * **`appsFolderName`**：`myapp`
   * **`artifactName`**：`MyLiveActionFactory package`
   * **`packageGroup`**：`myPackages`

1. 启动 Eclipse 并[导入 Maven 项目](/help/implementing/developing/tools/eclipse.md#import-the-maven-project-into-eclipse)。

### 将依赖项添加到 POM 文件。 {#add-dependencies-to-the-pom-file}

添加依赖项，以便 Eclipse 编译器可以引用在 `LiveActionFactory` 代码中使用的类。

1. 从 Eclipse Project Explorer 打开文件 `MyLiveActionFactory/pom.xml`。

1. 在编辑器中，单击`pom.xml`选项卡并找到 `project/dependencyManagement/dependencies` 部分。

1. 在 `dependencyManagement` 元素中添加以下 XML元素，然后保存文件。

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

1. 在 `MyLiveActionFactory-bundle/pom.xml` 从 **Project Explorer**&#x200B;打开捆绑包的 POM 文件。

1. 在编辑器中，单击 `pom.xml` 选项卡，并找到项目/依赖项部分。在依赖项元素中添加以下 XML元素，然后保存文件：

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

### 实施 LiveActionFactory {#implement-liveactionfactory}

以下 `LiveActionFactory` 类实施了一个 `LiveAction`，其中记录有关源页面和目标页面的消息，并将 `cq:lastModifiedBy` 属性从源节点复制到目标节点。该实时操作的名称是 `exampleLiveAction`。

1. 在 Eclipse Project 资源管理器中，右键单击 `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` 包，然后单击&#x200B;**新建** -> **类**。

1. 对于&#x200B;**名称**&#x200B;输入 `ExampleLiveActionFactory`，然后单击&#x200B;**完成**。

1. 打开 `ExampleLiveActionFactory.java` 文件，将内容替换为以下代码，然后保存文件。

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

1. 使用终端或命令会话，将目录更改为 `MyLiveActionFactory` 目录（Maven 项目目录）。然后，输入以下命令：

   ```shell
   mvn -PautoInstallPackage clean install
   ```

1. AEM `error.log` 文件应指示捆绑包已启动，并在 `https://<host>:<port>/system/console/status-slinglogs` 中的日志中可见。

   ```text
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### 创建示例转出配置 {#create-the-example-rollout-configuration}

使用您创建的 `LiveActionFactory` 创建 MSM 转出配置：

1. 使用以下属性，使用标准程序创建和配置[转出配置：](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration)

   * **标题**：转出配置示例
   * **名称**：examplerolloutconfig
   * **cq:trigger**：`publish`

### 将实时操作添加到转出配置示例中 {#add-the-live-action-to-the-example-rollout-configuration}

配置您在上一个程序中创建的转出配置，以便它可以使用 `ExampleLiveActionFactory` 类。

1. 打开 CRXDE Lite。

1. 在 `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content` 下创建以下节点：

   * **名称**：`exampleLiveAction`
   * **类型**：`cq:LiveSyncAction`

1. 单击&#x200B;**全部保存**。

1. 选择 `exampleLiveAction` 节点，并添加一个属性，以向 `ExampleLiveAction` 类指示`cq:LastModifiedBy`属性应从源节点复制到目标节点。

   * **名称**：`repLastModBy`
   * **类型**：`Boolean`
   * **值**：`true`

1. 单击&#x200B;**全部保存**。

### 创建 Live Copy {#create-the-live-copy}

使用您的转出配置创建 WKND 参考站点英语/产品分支的 [Live Copy：](/help/sites-cloud/administering/msm/creating-live-copies.md#creating-a-live-copy-of-a-page)

* **源**：`/content/wknd/language-masters/en/products`

* **转出配置**：转出配置示例

激活源分支的&#x200B;**产品**（英文）页面，观察 `LiveAction` 类生成的日志消息：

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

## 更改语言名称和默认国家/地区 {#changing-language-names-and-default-countries}

AEM 使用一组默认的语言和国家/地区代码。

* 默认语言代码是 ISO-639-1 定义的由两个小写字母组成的代码。
* 默认的国家/地区代码是由 ISO 3166 定义的小写或大写形式的由两个字母组成的代码。

MSM 使用存储的语言和国家/地区代码列表来确定与页面语言版本名称关联的国家/地区名称。如果需要，您可以更改列表的以下方面：

* 语言标题
* 国家/地区名称
* 语言的默认国家/地区（对于代码等，例如 `en`, `de`）

语言列表存储在 `/libs/wcm/core/resources/languages` 节点下。每个子节点都代表一种语言或一种语言国家/地区：

* 节点的名称是语言代码（如 `en` 或 `de`），或 language_country 代码（例如 `en_us` 或 `de_ch`）。

* 节点的 `language` 属性存储代码语言的全名。
* 节点的 `country` 属性存储代码国家/地区的全名。
* 当节点名称仅由语言代码组成时（例如 `en`），国家属性是 `*`，而额外的`defaultCountry`属性会存储语言国家/地区的代码，以指示要使用的国家/地区。

![语言定义](assets/msm-language-manager.png)

若要修改语言：

1. 打开 CRXDE Lite。
1. 选择 `/apps` 文件夹并单击&#x200B;**创建**，然后选择&#x200B;**创建文件夹**。

1. 命名新文件夹`wcm`。

1. 重复上一步，以创建 `/apps/wcm/core` 文件夹树。在 `core` 中创建一个类型为 `sling:Folder` 的节点，称为 `resources`。

1. 右键单击 `/libs/wcm/core/resources/languages` 节点并单击 **复制**。
1. 右键单击 `/apps/wcm/core/resources` 文件夹并单击&#x200B;**粘贴**。根据需要修改子节点。
1. 单击&#x200B;**全部保存**。
1. 单击&#x200B;**工具**、**操作**、**Web Console**。在此控制台中单击 **OSGi**，然后单击&#x200B;**配置**。
1. 找到并单击 **Day CQ WCM 语言管理器**，并将&#x200B;**语言列表**&#x200B;的值更改为 `/apps/wcm/core/resources/languages`，然后单击&#x200B;**保存**。

   ![Day CQ WCM 语言管理器](assets/msm-language-manager.png)

## 在页面属性上配置 MSM 锁 {#configuring-msm-locks-on-page-properties}

创建自定义页面属性时，您可能需要考虑新属性是否适合转出到任何 Live Copy。

例如，如果添加两个新的页面属性：

* 联系电子邮件:

   * 该属性不需要转出，因为它在每个国家/地区（或品牌等）中都会有所不同。

* 主要视觉风格：

   * 项目要求是要转出该属性，因为它（通常）对所有国家/地区（或品牌等）都是通用的。

那么您需要确保：

* 联系电子邮件:

   * 被排除在转出属性之外。
   * 请参阅文档[配置 Live Copy 同步](/help/sites-cloud/administering/msm/live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization)，了解更多信息。

* 主要视觉风格：

   * 请确保除非取消继承，否则不允许编辑此属性。
   * 还要确保您可以恢复继承。这是通过单击链接/断开的链接来控制的，这些链接可进行切换，以指示连接的状态。

页面属性是否要转出，因此在编辑时是否要取消/恢复继承，由对话框属性控制：

* `cq-msm-lockable`

   * 这会在对话框中创建链节符号。
   * 这只允许在继承被取消（链接断开）时进行编辑。
   * 这仅适用于资源的第一个子级
      * **类型**：`String`
      * **值**：持有对价属性的名称，与属性值相当`name`
         * 例如，请参阅
           `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

当定义了 `cq-msm-lockable` 时，断开/闭合链的操作会通过以下方式与 MSM 相互作用：

* 如果 `cq-msm-lockable` 的值为：

   * **相对**（例如，`myProperty` 或 `./myProperty`）

      * 断开链会添加和删除来自 `cq:propertyInheritanceCancelled` 的属性。

   * **绝对**（例如，`/image`）

      * 断开链会通过将 `cq:LiveSyncCancelled` mixin 添加到 `./image`，并将 `cq:isCancelledForChildren` 设置为 `true` 来取消继承。

      * 关闭链会恢复继承。

>[!NOTE]
>
>`cq-msm-lockable` 适用于要编辑的资源的第一个子级别，并且无论该值定义为绝对值还是相对值，它在任何更深级别的祖先上都不起作用。

>[!NOTE]
>
>当您重新启用继承时，Live Copy 页面属性不会自动与源属性同步。如果需要，您可以手动请求同步。
