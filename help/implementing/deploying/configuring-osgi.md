---
title: 将OSGi配置为AEM云服务
description: '具有机密值和环境特定值的OSGi配置 '
translation-type: tm+mt
source-git-commit: 743a8b4c971bf1d3f22ef12b464c9bb0158d96c0

---


# OSGi配置 {#osgi-configurations}

[OSGi是](https://www.osgi.org/) Adobe Experience Manager(AEM)技术堆栈中的一个基本元素。 它用于控制AEM及其配置的复合捆绑包。

OSGi提供标准化的基元，它允许应用程序由小的、可重用的和协作的组件构建。 这些组件可以组成应用程序并进行部署。 这允许轻松管理OSGi捆绑包，因为可以单独停止、安装和启动它们。 互依关系将自动处理。 每个OSGi组件都包含在各种包中的一个。 有关详细信息，请参阅 [OSGi规范](https://www.osgi.org/Specifications/HomePage)。

您可以通过AEM代码项目中的配置文件管理OSGi组件的配置设置。

## OSGi配置文件 {#osgi-configuration-files}

配置更改在AEM Project的代码包()中定义为运行`ui.apps`模式特定配置文件夹下`.cfg.json`的配置文件():

`/apps/example/config.<runmode>`

OSGi配置文件的格式基于JSON，使用Apache Sling `.cfg.json` 项目定义的格式。

OSGi配置通过OSGi组件的永久身份(PID)目标OSGi组件，该身份默认为OSGi组件的Java类名称。 例如，为通过以下方式实现的OSGi服务提供OSGi配置：

`com.example.workflow.impl.ApprovalWorkflow.java`

OSGi配置文件在以下位置进行定义：

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

遵循 [cfg.json OSGi配置格式]（遵循cfg.json OSGi配置格式）。

> [!NOTE]
>
> 先前版本的AEM支持使用不同文件格式（如。cfg.、.config和XML sling:OsgiConfig资源定义）的OSGi配置文件。 这些格式由cfg.json OSGi配置格式取代。

## 运行模式分辨率 {#runmode-resolution}

通过使用运行模式，可以将特定OSGi配置定向到特定AEM实例。 要使用运行模式，请在(其 `/apps/example` 中是您的项目名称)下创建配置文件夹，格式为：

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

如果配置文件夹名称中定义的运行模式与AEM使用的运行模式匹配，则将使用此类文件夹中的所有OSGi配置。

例如，如果AEM使用运行模式作者和开发，则将应用和中 `/apps/example/config.author/` 的 `/apps/example/config.author.dev/` 配置节点，而不应用和中 `/apps/example/config.publish/` 的配 `/apps/example/config.author.stage/` 置节点。

如果同一PID的多个配置适用，则应用具有最多匹配运行模式的配置。

此规则的粒度在PID级别。 这意味着您不能为同一PID定义某些属性，而 `/apps/example/config.author/` 为同一PID定义更 `/apps/example/config.author.dev/` 多特定属性。  匹配运行模式数目最多的配置对于整个PID是有效的。

本地开发时，可以传入运行模式启动参数，以指定将使用哪个运行模式OSGI配置。

## OSGi配置值的类型 {#types-of-osgi-configuration-values}

有三种OSGi配置值可以与AEM一起用作云服务。

1. **内联值**，即硬编码到OSGi配置并存储在Git中的值。 例如：

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **机密值**，即出于安全原因不应存储在Git中的值。 例如：

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **环境特定值**，这些值是不同开发环境的值，因此无法按运行模式准确定位(因为AEM中作为云服务有 `dev` 单个运行模式)。 例如：

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   请注意，单个OSGi配置文件可以结合使用这些配置值类型的任意组合。 例如：

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## 如何选择适当的OSGi配置值类型 {#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGi的常见情况使用内联OSGi配置值。 环境特定配置仅用于开发环境之间值不同的特定用例。

![](assets/choose-configuration-value-type.png)

环境特定配置扩展了包含内联值的传统静态定义OSGi配置，从而提供了通过Cloud Manager API在外部管理OSGi配置值的能力。 必须了解何时应使用通用的传统方法来定义内联值并将其存储在Git中，而不是将这些值抽象为特定于环境的配置。

以下指导说明何时使用非机密和机密环境特定配置：

### 何时使用内联配置值 {#when-to-use-inline-configuration-values}

内联配置值被视为标准方法，应尽可能使用。 内联配置提供以下优势：

* 它们由Git维护，其管理和版本历史记录在Git中
* 值隐式绑定到代码部署
* 它们不需要任何额外的部署考虑或协调

无论何时定义OSGi配置值(与内联值开始)，只要在用例需要时选择机密或环境特定配置。

### 何时使用非机密环境特定配置值 {#when-to-use-non-secret-environment-specific-configuration-values}

当这些值在开发环境中`$[env:ENV_VAR_NAME]`不同时，仅对非机密配置值使用环境特定配置()。 这包括本地开发实例和任何AEM作为云服务开发环境。 避免将AEM的非机密环境特定配置用作云服务阶段或生产环境。

* 只对不同开发环境（包括本地开发实例）的配置值使用非机密环境特定配置。
* 请改用OSGi配置中的标准内联值作为舞台和生产非机密值。  与此相关，不建议使用环境特定配置以便于在运行时对舞台和生产环境进行配置更改； 这些更改应通过源代码管理引入。

### 何时使用特定于环境的机密配置值 {#when-to-use-secret-environment-specific-configuration-values}

AEM作为云服务，需要对任何机密OSGi配置值(`$[secret:SECRET_VAR_NAME]`如口令、专用API密钥，或出于安全原因无法存储在Git中的任何其他值)使用环境特定配置()。

使用特定于机密环境的配置将机密值作为云服务环境（包括舞台和生产）存储在所有AEM上。

### 将新配置添加到存储库 {#adding-a-new-configuration-to-the-repository}

#### 您需要了解的内容 {#what-you-need-to-know}

要向存储库添加新配置，您需要了解以下内容：

1. 服 **务的永久** 标识(PID)。

   引用Web **控制台** 中的“配置”字段。 该名称在捆绑名称后面的括号中显示(或 **在页面底部** 的“配置信息”中显示)。

   例如，创建一个节点 `com.day.cq.wcm.core.impl.VersionManagerImpl.` 以配置 **AEM WCM版本管理器**。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 是否需要特定运行模式。 创建文件夹：

   * `config` -适用于所有运行模式
   * `config.author` -对于作者环境
   * `config.publish` -对于发布环境
   * `config.<run-mode>` -视情况

1. 是否需要 **配置** 或 **工厂配置** 。
1. 要配置的各个参数； 包括需要重新创建的任何现有参数定义。

   在Web控制台中引用单个参数字段。 每个参数的名称将显示在括号中。

   例如，创建属性
   `versionmanager.createVersionOnActivation` 在激活 **上配置创建版本**。

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. 中是否已存在配置 `/libs`? 要列表实例中的所有配置，请使 **用** CRXDE Lite中的查询工具提交以下SQL查询:

   `select * from sling:OsgiConfig`

   如果是，则可以将此配置复制到 ` /apps/<yourProject>/`新位置，然后在新位置进行自定义。

## 在存储库中创建配置 {#creating-the-configuration-in-the-repository}

要将新配置实际添加到存储库，请执行以下操作：

1. 使用CRXDE Lite导航到：

   ` /apps/<yourProject>`

1. 如果文件夹尚未存在，请 `config` 创建文 `sling:Folder`件夹():

   * `config` -适用于所有运行模式
   * `config.<run-mode>` -特定于特定运行模式

1. 在此文件夹下，创建一个节点：

   * 类型: `sling:OsgiConfig`
   * 名称： 持久身份(PID);

      例如，AEM WCM Version Manager使用 `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >在名称后附加工厂 `-<identifier>` 配置时。
   >
   >如下所示： `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >如果 `<identifier>` 替换为您（必须）输入用来标识实例的自由文本（您不能忽略此信息）; 例如：
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 对于要配置的每个参数，在此节点上创建一个属性：

   * 名称： Web控制台中显示的参数名称； 该名称显示在字段描述末尾的括号中。 例如，供 `Create Version on Activation` 使用 `versionmanager.createVersionOnActivation`
   * 类型： 酌情。
   * 值： 。
   您只需为要配置的参数创建属性，其他人仍将采用AEM设置的默认值。

1. 保存所有更改。

   通过重新启动服务更新节点后，更改会立即应用（与在Web控制台中所做的更改一样）。

>[!CAUTION]
>
>您不得更改路径中的任 `/libs` 何内容。

>[!CAUTION]
>
>配置的完整路径必须正确，才能在启动时读取。


## Source Control中的配置属性格式 {#configuration-property-format-in-source-control}

在上面向存储库添加新配置一节中 [介绍了如何创建新的OSGI配置](#creating-the-configuration-in-the-repository) 属性。 按照以下步骤操作并修改以下子部分中概述的语法：

### 内联值 {#inline-values}

正如人们所期望的，内联值按照标准JSON语法格式化为标准名称——值对。 例如：

```json
 {

 "my_var1": "val",
 "my_var2": "abc",
 "my_var3": 500

}
```

### 环境特定配置值 {#environment-specific-configuration-values}

OSGi配置应为要根据环境定义的变量分配占位符：

```
use $[env:ENV_VAR_NAME]
```

客户只应将此技术用于与其自定义代码相关的OSGI配置属性； 它不应用于覆盖Adobe定义的OSGI配置。

### 机密配置值 {#secret-configuration-values}

OSGi配置应为要根据环境定义的机密分配一个占位符：

```
use $[secret:SECRET_VAR_NAME]
```

### 变量命名 {#variable-naming}

以下内容适用于特定环境和机密配置值。

变量名称应遵循以下规则：

* 最小长度： 2
* 最大长度： 100
* 必须匹配正则表达式： `[a-zA-Z_][a-zA-Z_0-9]*`

变量值不应超过2048个字符。

### 默认值 {#default-values}

以下内容适用于特定环境和机密配置值。

如果未设置每环境值，则在运行时，占位符不会被替换并保留原位，因为未发生插值。 为避免出现此问题，可以使用以下语法将默认值作为占位符的一部分提供：

```
$[env:ENV_VAR_NAME;default=<value>]
```

在提供默认值的情况下，占位符将替换为每环境值（如果提供）或提供的默认值。

### 本地开发 {#local-development}

以下内容适用于特定环境和机密配置值。

变量可以在本地环境中定义，因此在运行时由本地AEM拾取。 例如，在Linux上：

```bash
export ENV_VAR_NAME=my_value
```

建议编写一个简单的bash脚本，它设置配置中使用的环境变量，并在启动AEM之前执行它。 https://direnv.net/等工 [具可](https://direnv.net/) 帮助您简化此方法。 根据值的类型，如果可以在每个人之间共享，则可能会将它们检入到源代码管理中。

机密值从文件中读取。 因此，对于使用机密的每个占位符，需要创建包含机密值的文本文件。

例如，如 `$[secret:server_password]` 果使用，则需要创建 **名为server_password** 的文本文件。 所有这些机密文件都需要存储在同一个目录中，框架属 `org.apache.felix.configadmin.plugin.interpolation.secretsdir` 性需要使用该本地目录进行配置。

### 作者配置与发布配置 {#author-vs-publish-configuration}

如果OSGI属性要求创作值与发布值不同：

* 应使 `config.author` 用 `config.publish` 单独的和OSGi文件夹，如“Runmode Resolution”(运行模式分 [辨率)部分中所述](#runmode-resolution)。
* 应使用独立变量名称。 建议使用前缀，如author_<variablename> 和发布_<variablename> 其中变量名称相同

### 配置示例 {#configuration-examples}

在以下示例中，假定除了舞台和prod环境外，还有3个开发环境。

**示例1**

其目的是使OSGI属性的值在级和 `my_var1` prod上相同，但对于3个开发环境中的每个都不同。

<table>
<tr>
<td>
<b>文件夹</b>
</td>
<td>
<b>myfile.cfg.json的内容</b>
</td>
</tr>
<tr>
<td>
配置
</td>
<td>
<pre>
{ "my_var1": "val", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1": "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

**示例2**

其目的是使OSGI属性的值对 `my_var1` 于舞台、prod和3个开发环境中的每个都不同。 因此，需要调用Cloud Manager API来为每个开发环境 `my_var1` 设置值。

