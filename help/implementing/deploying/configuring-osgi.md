---
title: 为Adobe Experience Manager as a Cloud Service配置OSGi
description: 具有机密值和特定于环境的值的OSGi配置
feature: Deploying
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '3317'
ht-degree: 1%

---

# 为Adobe Experience Manager as a Cloud Service配置OSGi {#configuring-osgi-for-aem-as-a-cloud-service}

>[!NOTE]
>
>AEM引入了使用Cloud Manager用户界面在2021.12.0版本中配置标准环境变量的功能。 有关更多信息，请参阅文档。 [此处](/help/implementing/cloud-manager/environment-variables.md).

[osgi](https://www.osgi.org/) 是Adobe Experience Manager (AEM)技术栈栈中的基本元素。 它用于控制AEM的复合捆绑包及其配置。

OSGi提供了标准化的基元，允许从小型、可重用的协作组件构建应用程序。 这些组件可以组合为一个应用程序并进行部署。 这样可以轻松地管理OSGi包，因为它们可以单独停止、安装和启动。 系统会自动处理相互依赖关系。 每个OSGi组件都包含在各种捆绑包中。 欲了解更多信息，请参见 [OSGi规范](https://help.eclipse.org/latest/index.jsp).

您可以通过属于AEM代码项目一部分的配置文件来管理OSGi组件的配置设置。

## OSGi配置文件 {#osgi-configuration-files}

配置更改在AEM项目的代码包中定义(`ui.apps`)作为配置文件(`.cfg.json`)，位于runmode特定配置文件夹下：

`/apps/example/config.<runmode>`

OSGi配置文件的格式基于JSON，使用 `.cfg.json` Apache Sling项目定义的格式。

OSGi配置通过组件的永久标识(PID)来定位OSGi组件，该PID默认为OSGi组件的Java™类名称。 例如，为通过以下方式实施的OSGi服务提供OSGi配置：

`com.example.workflow.impl.ApprovalWorkflow.java`

在以下位置定义OSGi配置文件：

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

遵循 `cfg.json` osgi配置格式。

>[!NOTE]
>
>AEM早期版本支持的OSGi配置文件使用不同的文件格式，例如 `.cfg`， `.config` 和XML `sling:OsgiConfig` 资源定义。 这些格式将被 `.cfg.json` osgi配置格式。

## 运行模式分辨率 {#runmode-resolution}

>[!TIP]
>
>AEM 6.x支持自定义运行模式，但AEMas a Cloud Service不支持。 AEMas a Cloud Service支持 [精确的一组运行模式](./overview.md#runmodes). 必须使用，处理AEMas a Cloud Service环境之间OSGi配置的任何变量 [OSGi配置环境变量](#environment-specific-configuration-values).

可以使用运行模式将特定OSGi配置定位到特定AEM实例。 要使用runmode，请在下创建配置文件夹 `/apps/example` （其中，示例是您的项目名称），格式为：

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

如果配置文件夹名称中定义的运行模式与AEM使用的运行模式匹配，则使用此类文件夹中的任何OSGi配置。

例如，如果AEM使用runmodes author和dev，则配置节点位于 `/apps/example/config.author/` 和 `/apps/example/config.author.dev/` ，而配置节点 `/apps/example/config.publish/` 和 `/apps/example/config.author.stage/` 不应用。

如果同一PID有多个配置适用，则应用匹配运行模式数最多的配置。

此规则的粒度处于PID级别。 这意味着您无法在中为同一PID定义某些属性 `/apps/example/config.author/` 以及中更具体的部分 `/apps/example/config.author.dev/` 相同的PID。 匹配运行模式数最高的配置对整个PID有效。

>[!NOTE]
>
>A `config.preview` OSGi配置文件夹 **无法** 以相同方式声明 `config.publish` 可以声明文件夹。 相反，预览层从发布层的值继承其OSGi配置。

在进行本地开发时，运行架构启动参数 `-r` 用于指定运行架构 OSGI 配置。

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

### 验证运行模式

AEMas a Cloud Service的运行模式根据环境类型和服务进行了良好的定义。 查看 [可用AEMas a Cloud Service运行模式的完整列表](./overview.md#runmodes).

可以通过以下方式验证由运行模式指定的OSGi配置值：

1. 打开AEM as aCloud Service环境的 [开发人员控制台](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html)
1. 选择要检查的服务层，使用 __Pod__ 下拉列表
1. 选择 __状态__ 选项卡
1. 选择 __配置__ 从 __状态转储__ 下拉列表
1. 选择 __获取状态__ 按钮

结果视图将显示选定层的所有OSGi组件配置及其适用的OSGi配置值。 这些值可以与AEM项目源代码中的OSGi配置值交叉引用，位于 `/apps/example/osgiconfig/config.<runmode(s)>`.


要验证是否应用了适当的OSGi配置值，请执行以下操作：

1. 在开发人员控制台的配置输出中
1. 找到 `pid` 表示要验证的OSGi配置；这是AEM项目源代码中的OSGi配置文件的名称。
1. Inspect `properties` 的列表 `pid` 并验证键和值是否与要验证的运行模式的AEM项目源代码中的OSGi配置文件匹配。


## OSGi配置值的类型 {#types-of-osgi-configuration-values}

有三种类型的OSGi配置值可以与Adobe Experience Manager as a Cloud Service一起使用。

1. **内联值**，这些值已硬编码到OSGi配置中并存储在Git中。 例如：

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **密码值**，出于安全原因，这些值不得存储在Git中。 例如：

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **特定于环境的值**，这些值在开发环境之间有所不同，因此无法在运行模式下准确地定位(因为只有一个 `dev` Adobe Experience Manager as a Cloud Service中的运行模式)。 例如：

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   单个OSGi配置文件可以结合使用这些配置值类型的任意组合。 例如：

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## 如何选择适当的OSGi配置值类型 {#how-to-choose-the-appropriate-osgi-configuration-value-type}

OSGi的常见用例使用内联OSGi配置值。 特定于环境的配置仅用于开发环境之间的值不同的特定用例。

![有关如何使用合适的配置值类型的决策树](assets/choose-configuration-value-type_res1.png)

特定于环境的配置扩展了包含内联值的传统、静态定义的OSGi配置，提供了通过Cloud Manager API在外部管理OSGi配置值的功能。 了解何时使用定义内联值并将其存储在Git中的常见传统方法以及何时将值抽象为特定于环境的配置非常重要。

以下指南介绍了何时使用特定于非机密和机密环境的配置：

### 何时使用内联配置值 {#when-to-use-inline-configuration-values}

内联配置值被视为标准方法，应尽可能使用。 内联配置具有以下优势：

* 它们会进行维护，在Git中具有治理和版本历史记录
* 值隐式绑定到代码部署
* 它们不需要任何其他部署考虑或协调

无论何时定义OSGi配置值，都从内联值开始，并且仅当用例需要时才选择机密或特定于环境的配置。

### 何时使用非机密环境特定的配置值 {#when-to-use-non-secret-environment-specific-configuration-values}

仅使用特定于环境的配置(`$[env:ENV_VAR_NAME]`)，对于非机密配置值，如果预览层的值不同或开发环境之间的值不同。 这包括本地开发实例和任何Adobe Experience Manager as a Cloud Service开发环境。 除了为预览层设置唯一值之外，请避免为Adobe Experience Manager as a Cloud Service暂存或生产环境使用非机密环境特定的配置。

* 仅将特定于非机密环境的配置用于发布层和预览层之间不同的配置值，或用于开发环境（包括本地开发实例）之间不同的值。
* 除了预览层必须不同于发布层的方案外，请在OSGi配置中为暂存和生产非机密值使用标准内联值。 因此，不建议使用特定于环境的配置来促进在运行时对暂存环境和生产环境进行配置更改；这些更改应通过源代码管理引入。

### 何时使用特定于机密环境的配置值 {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as a Cloud Service需要使用特定于环境的配置(`$[secret:SECRET_VAR_NAME]`)，用于任何机密的OSGi配置值，例如密码、私有API密钥或任何其他出于安全原因不能存储在Git中的值。

使用特定于密钥环境的配置来存储所有Adobe Experience Manager as a Cloud Service环境（包括暂存环境和生产环境）上的密钥值。

## 创建OSGi配置 {#creating-osgi-configurations}

创建OSGi配置的方法有两种，如下所述。 前者通常用于配置自定义OSGi组件，这些组件具有开发人员已知的OSGi属性和值，而后者则用于AEM提供的OSGi组件。

### 编写OSGi配置 {#writing-osgi-configurations}

JSON格式的OSGi配置文件可以直接在AEM项目中手动编写。 这通常是为已知的OSGi组件（尤其是由定义配置的同一开发人员设计和开发的自定义OSGi组件）创建OSGi配置的最快方法。 此方法还可用于在不同的运行模式文件夹中复制/粘贴和更新同一OSGi组件的配置。

1. 在IDE中，打开 `ui.apps` 项目，找到或创建配置文件夹(`/apps/.../config.<runmode>`)以新OSGi配置需要生效的运行模式为目标
1. 在此配置文件夹中，创建 `<PID>.cfg.json` 文件。 PID是OSGi组件的永久标识。 它通常是OSGi组件实现的完整类名。 例如：
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
请注意，OSGi配置工厂文件名使用 `<factoryPID>-<name>.cfg.json` 命名约定
1. 打开新的 `.cfg.json` 文件，并定义OSGi属性和值对的键/值组合，如下所示 [JSON OSGi配置格式](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).
1. 将更改保存到新 `.cfg.json` 文件
1. 添加新的OSGi配置文件并将其提交到Git

### 使用AEM SDK快速入门生成OSGi配置 {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

AEM SDK快速入门Jar的AEM Web控制台可用于配置OSGi组件，并将OSGi配置导出为JSON。 这对于配置AEM提供的OSGi组件非常有用，在AEM项目中定义OSGi配置的开发人员可能无法很好地了解这些组件的OSGi属性及其值格式。

>[!NOTE]
>
>AEM Web控制台的配置UI不会写入 `.cfg.json` 文件放入存储库。 因此，请注意，当AEM项目定义的OSGi配置可能与生成的配置不同时，此工作流可避免在本地开发期间潜在的意外行为。

1. 登录到AEM SDK快速入门Jar的AEM Web控制台，网址为 `https://<host>:<port>/system/console` 作为管理员用户
1. 导航到 **osgi** > **配置**
1. 要配置，请找到OSGi组件并点按其标题以进行编辑
   ![OSGi 配置](./assets/configuring-osgi/configuration.png)
1. 根据需要通过Web UI编辑OSGi配置属性值
1. 将永久标识(PID)记录到安全位置。 这稍后将用于生成OSGi配置JSON
1. 点按保存
1. 导航到OSGi > OSGi安装程序配置打印机
1. 粘贴步骤5中复制的PID，确保序列化格式设置为“OSGi配置器JSON”
1. 点按打印
1. JSON格式的OSGi配置将显示在序列化配置属性部分中
   ![OSGi安装程序配置打印机](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. 在IDE中，打开 `ui.apps` 项目，找到或创建配置文件夹(`/apps/.../config.<runmode>`)以新OSGi配置需要生效的运行模式为目标。
1. 在此配置文件夹中，创建 `<PID>.cfg.json` 文件。 PID与步骤5中的值相同。
1. 将步骤10中的序列化配置属性粘贴到 `.cfg.json` 文件。
1. 将更改保存到新 `.cfg.json` 文件。
1. 添加新的OSGi配置文件并将其提交到Git。


## OSGi配置属性格式 {#osgi-configuration-property-formats}

### 内联值 {#inline-values}

内联值的格式为标准的名称 — 值对，遵循标准JSON语法。 例如：

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### 特定于环境的配置值 {#environment-specific-configuration-values}

OSGi配置应为打算按环境定义的变量分配占位符：

```
use $[env:ENV_VAR_NAME]
```

客户应仅将此技术用于与其自定义代码相关的OSGi配置属性；不得使用此技术覆盖Adobe定义的OSGi配置。

>[!NOTE]
>
>占位符不能用于 [repoinit语句](/help/implementing/deploying/overview.md#repoinit).

### 密码配置值 {#secret-configuration-values}

OSGi配置应为要按环境定义的密钥分配一个占位符：

```
use $[secret:SECRET_VAR_NAME]
```

### 变量命名 {#variable-naming}

以下内容适用于特定于环境的配置值和机密配置值。

变量名称必须遵循以下规则：

* 最小长度：2
* 最大长度：100
* 必须匹配正则表达式： `[a-zA-Z_][a-zA-Z_0-9]*`

变量值不得超过2048个字符。

>[!CAUTION]
>
>有些规则与对变量名称使用某些前缀有关：
>
>1. 带有前缀的变量名称 `INTERNAL_`， `ADOBE_`，或 `CONST_` 由Adobe保留。 以这些前缀开头的任何客户设置变量都将被忽略。
>
>1. 客户不得引用带有前缀的变量 `INTERNAL_` 或 `ADOBE_` 也不是。
>
>1. 带前缀的环境变量 `AEM_` 由产品定义为供客户使用和设置的公共API。
>   而客户可以使用和设置以前缀开头的环境变量 `AEM_` 他们不应使用此前缀定义自己的变量。

### 默认值 {#default-values}

以下内容适用于特定于环境的配置值和机密配置值。

如果未设置每个环境的值，则运行时不会替换占位符，并且由于没有发生插值，占位符将保留在原位。 为了避免这种情况，可以使用以下语法将默认值作为占位符的一部分提供：

```
$[env:ENV_VAR_NAME;default=<value>]
```

在提供了默认值的情况下，占位符会被替换为每个环境的值（如果提供）或提供的默认值。

### 本地开发 {#local-development}

以下内容适用于特定于环境的配置值和机密配置值。

变量可以在本地环境中定义，以便在运行时由本地AEM接收。 例如，在Linux®上：

```bash
export ENV_VAR_NAME=my_value
```

建议编写简单的bash脚本，以设置配置中使用的环境变量，并在启动AEM之前执行它。 工具如 [https://direnv.net/](https://direnv.net/) 帮助简化该方法。 根据值的类型，如果这些值可以在所有人之间共享，则它们可能会被签入源代码管理。

从文件中读取密钥的值。 因此，对于使用密码的每个占位符，必须创建包含密码值的文本文件。

例如，如果 `$[secret:server_password]` 使用，一个名为 **server_password** 必须创建。 所有这些机密文件必须存储在同一目录和框架属性中 `org.apache.felix.configadmin.plugin.interpolation.secretsdir` 必须使用该本地目录进行配置。

>[!CAUTION]
>
>文本文件不允许使用文件扩展名。
>
>因此，对于上面的示例，必须命名文本文件 **server_password**  — 不带文件扩展名。

此 `org.apache.felix.configadmin.plugin.interpolation.secretsdir` 是Sling框架属性；因此此属性不是在felix控制台(/system/console)中设置的，而是在系统引导时使用的sling.properties文件中设置的。 此文件可在提取的Jar/install文件夹(crx-quickstart/conf)的/conf子目录中找到。

示例：将此行添加到“crx-quickstart/conf/sling.properties”文件的末尾以将“crx-quickstart/secretsdir”配置为机密文件夹：

```
org.apache.felix.configadmin.plugin.interpolation.secretsdir=${sling.home}/secretsdir
```

### 作者与发布配置 {#author-vs-publish-configuration}

如果OSGi属性对于创作与发布所需的值不同：

* 分隔 `config.author` 和 `config.publish` 必须使用OSGi文件夹，如 [“运行模式分辨率”部分](#runmode-resolution).
* 创建独立变量名称有两种选项，应使用：
   * 推荐使用的第一个选项：在所有OSGi文件夹中(如 `config.author` 和 `config.publish`)声明以定义不同的值，请使用相同的变量名称。 例如
     `$[env:ENV_VAR_NAME;default=<value>]`，其中默认值对应于该层的默认值（创作或发布）。 通过设置环境变量时 [Cloud Manager API](#cloud-manager-api-format-for-setting-properties) 或通过客户端，使用“服务”参数区分各个层，如本中所述 [API参考文档](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/). “service”参数会将变量的值绑定到适当的OSGi层。 它可以是“创作”、“发布”或“预览”。
   * 第二个选项，即使用前缀（例如）声明不同的变量 `author_<samevariablename>` 和 `publish_<samevariablename>`

### 配置示例 {#configuration-examples}

在下面的示例中，假设除了暂存环境和生产环境之外，还有三个开发环境。

**示例 1**

目的是OSGi属性的值 `my_var1` 对于暂存环境和生产环境相同，但三个开发环境中的每一个有所不同。

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
config
</td>
<td>
<pre>
{ "my_var1"： "val"， "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" ： "$[env：my_var1]" "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
</table>

**示例 2**

目的是OSGi属性的值 `my_var1` 在暂存、生产和三个开发环境中均不同。 因此，必须调用Cloud Manager API以便为设置值 `my_var1` 每个开发环境。

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
config.stage
</td>
<td>
<pre>
{ "my_var1"： "val1"， "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ "my_var1"： "val2"， "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" ： "$[env：my_var1]" "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
</table>

**示例 3**

目的是OSGi属性的值 `my_var1` 对于暂存、生产和仅其中一个开发环境相同，但对于其他两个开发环境不同。 在这种情况下，必须调用Cloud Manager API来设置值 `my_var1` 适用于每个开发环境，包括应与暂存和生产环境具有相同值的开发环境。 它不会继承文件夹中设置的值 **config**.

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
config
</td>
<td>
<pre>
{ "my_var1"： "val1"， "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" ： "$[env：my_var1]" "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
</table>

完成此任务的另一种方法是为config.dev文件夹中的替换令牌设置默认值，使其与 **config** 文件夹。

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
config
</td>
<td>
<pre>
{ "my_var1"： "val1"， "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1"： "$[env：my_var1；default=val1]" "my_var2"： "abc"， "my_var3"： 500 }
</pre>
</td>
</tr>
</table>

## 用于设置属性的Cloud Manager API格式 {#cloud-manager-api-format-for-setting-properties}

请参阅 [此页面](https://developer.adobe.com/experience-cloud/cloud-manager/docs/) 有关如何配置API的信息。
>[!NOTE]
>
>确保使用的Cloud Manager API分配了“部署管理员 — Cloud Service”角色。 其他角色无法执行以下所有命令。

### 通过API设置值 {#setting-values-via-api}

调用API会将新变量和值部署到云环境，类似于典型的客户代码部署管道。 创作和发布服务将重新启动并引用新值，通常需要几分钟的时间。

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```
]
        {
                "name" : "MY_VAR1",
                "value" : "plaintext value",
                "type" : "string"  <---default
        },
        {
                "name" : "MY_VAR2",
                "value" : "<secret value>",
                "type" : "secretString"
        }
]
```

>[!NOTE]
>默认变量不是通过API设置的，而是在OSGi属性本身中设置的。
>
>请参阅 [此页面](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) 以了解更多信息。

### 通过API获取值 {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

请参阅 [此页面](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) 以了解更多信息。

### 通过API删除值 {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

要删除变量，请将其包含在空值中。

请参阅 [此页面](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) 以了解更多信息。

### 通过命令行获取值 {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### 通过命令行设置值 {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### 通过命令行删除值 {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>请参阅 [此页面](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 有关如何使用Adobe I/OCLI的Cloud Manager插件配置值的更多信息。

### 变量数 {#number-of-variables}

每个环境最多可以声明200个变量。

## 针对密钥和特定于环境的配置值的部署注意事项 {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

由于机密和特定于环境的配置值位于Git之外，因此不属于正式的Adobe Experience Manager as a Cloud Service部署机制，因此客户应该管理、治理并集成到Adobe Experience Manager as a Cloud Service部署过程中。

如上所述，调用API会将新变量和值部署到云环境，类似于典型的客户代码部署管道。 创作和发布服务将重新启动并引用新值，通常需要几分钟的时间。 在此过程中，不会执行Cloud Manager在常规代码部署期间运行的质量审核和测试。

通常，客户在部署在Cloud Manager中依赖于环境变量的代码之前，会调用API来设置环境变量。 在某些情况下，可能需要在部署代码后修改现有变量。

>[!NOTE]
>
>当管道正在使用中(AEM更新或客户部署)时，API可能会失败，具体取决于当时正在执行的端到端管道的部分。 错误响应将指示请求不成功，但不会指示具体原因。

在某些情况下，计划客户代码部署依赖现有变量才能具有新值，而该值不适用于当前代码。 如果这是一个问题，建议以累加方式进行变量修改。 为此，请创建新的变量名称，而不是只更改旧变量的值，这样旧代码永远不会引用新值。 然后，当新客户版本看起来稳定时，您可以选择删除旧值。

同样，由于变量的值未进行版本控制，因此代码回滚可能会导致它引用导致问题的较新值。 前面提到的加性变量策略也会对此有所帮助。

此附加变量策略也可用于灾难恢复情况，在这些情况中，如果需要重新部署前几天生成的代码，则它引用的变量名称和值将保持不变。 这依赖于一种策略，即客户在删除这些旧变量之前等待几天，否则旧代码将没有合适的变量可引用。
