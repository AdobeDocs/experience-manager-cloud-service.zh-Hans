---
title: 使用人工智能工具进行本地开发
description: 了解如何使用项目上下文、代理技能和MCP服务器配置AI编码工具以加速AEM as a Cloud Service开发。
feature: Developing
role: Developer
source-git-commit: 0bc00b6e14be6ba111ac26ce69f07e138ca400e4
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 0%

---


# 使用人工智能工具进行本地开发 {#local-development-with-ai-tools}

>[!IMPORTANT]
>
>本文中介绍的功能是&#x200B;**测试版**。 通过提前访问Adobe正在开发的功能，客户和合作伙伴可以提供反馈（通过电子邮件发送[aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)）并影响产品开发。 它还有助于客户在功能正式发布之前做好采用新功能的准备。
>
>Beta版本可能包含缺陷，并“按原样”提供，无任何类型的担保。 Adobe没有义务维护、更正、更新、更改、修改或以其他方式支持（通过Adobe支持服务或其他方式）Beta版。 Adobe建议客户谨慎使用，不要依赖测试版或随附的任何文档或材料的正确功能或性能。 Beta版中的功能和API如有更改，恕不另行通知。 因此，使用测试版完全由客户自行承担风险。

>[!NOTE]
>
>本文侧重于使用人工智能工具为&#x200B;**AEM Java栈栈开发**&#x200B;进行本地开发。 对于Edge Delivery Services，请参阅[使用AI工具进行开发](https://www.aem.live/developer/ai-coding-agents)。

AI编码代理（Claude Code、Cursor、GitHub Copilot和类似工具）对AEM的底层技术(Java、OSGi、Sling、JCR、HTL)具有广泛了解，但不一定了解用于生成代码和配置或如何调试常见AEM开发问题的最佳实践。

有四个互补组件解决了这个问题：

| 组件 | 用途 |
|---|---|
| **代理.md** | 项目特定的上下文文件，它可以为每个会话的AEM Cloud Service项目中提供AI依据 |
| **代理技能** | 可重复使用的指令集，用于组件创建和Dispatcher配置等重复开发任务 |
| **AEM快速入门本地MCP服务器** | 公开本地AEM SDK实例的实时运行时数据以支持故障排除 |
| **Dispatcher本地MCP服务器** | 启用本地Dispatcher实例的运行时验证和检查 |

>[!NOTE]
>
> 对于本地开发来说，AEM云服务的远程MCP服务器也很有用，但本文未涉及这些服务器。 请参阅[将MCP用于Cloud Service一文](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md)以了解有关它们的更多信息。

## AGENTS.md {#agentsmd}

`AGENTS.md`是一个Markdown文件，位于AEM项目的根目录，人工智能编码工具会在每个会话开始时自动加载，以便通过基本的AEM Cloud Service Java栈栈域专业技能扎根（而不是AEM 6.5或Edge Delivery Services等其他AEM解决方案）。

`AGENTS.md`不是您复制的静态文件 — 它是通过下一节中所述的`ensure-agents-md`技能生成的。 该技能读取您的`pom.xml`以解析项目名称、发现模块并检测已安装的加载项，从而生成针对您的特定项目定制的文件。

>[!NOTE]
>
>`AGENTS.md`一旦存在于项目根目录中，`ensure-agents-md`技能便不再运行。 如果您的项目结构发生更改，请直接编辑该文件。

## 座席技能 {#agent-skills}

技能是用于对多步骤开发工作流进行编码的说明集。 在调用时，人工智能遵循该技能的程序，而不是仅依赖一般知识，产生一致、符合公约的结果。

Adobe将在&#x200B;**[分支上的](https://github.com/adobe/skills/tree/beta/skills/aem/cloud-service/skills)adobe/skills**`beta`存储库中发布AEM as a Cloud Service技能，因为此功能尚未公开发布：

| 技能 | 用途 |
|---|---|
| `ensure-agents-md` | 根据项目的实际模块结构定制的Bootstrap`AGENTS.md`和`CLAUDE.md` |
| `create-component` | 支撑完整的AEM组件：组件定义、对话框XML、HTL模板、Sling模型、单元测试和clientlibs |
| `dispatcher` | AI支持的Dispatcher和Apache HTTPD配置助手，涵盖配置创作、技术咨询、事件响应、性能调整和安全强化 |
| `workflow` | 所有AEM as a Cloud Service工作流技能的单一入口点。 涵盖工作流模型设计、自定义流程步骤和参与者选择器开发、启动器配置、工作流触发和生产支持，包括调试卡住/失败的工作流、使用Cloud Manager日志测试事件、线程池分析以及针对Granite工作流引擎的Sling作业诊断。 |

### 安装技能 {#install-skills}

选择与您的AI编码工具匹配的方法。 一旦安装技能，这些技能即可用于该计算机上的所有项目。

#### Claude码 {#claude-code}

```bash
# Add the Adobe Skills marketplace (one-time setup)
/plugin marketplace add adobe/skills#beta

# Install all available skills
/plugin install aem-cloud-service@adobe-skills
```

#### Npx技能 {#npx-skills}

```bash
# Install all available skills
npx skills add https://github.com/adobe/skills/tree/beta/skills/aem/cloud-service --all
```

#### Upskill（GitHub CLI扩展） {#upskill-github-cli-extension}

```bash
# Install the gh-upskill extension (one-time setup)
gh extension install trieloff/gh-upskill

# Install all available skills
gh upskill adobe/skills --branch beta --path skills/aem/cloud-service --all
```

### 使用secure-agents-md技能 {#use-the-ensure-agents-md-skill}

安装该技能后，在尚未具有`AGENTS.md`的任何AEM Cloud Service项目中打开您的AI助手。 该技能将在处理您的第一个请求之前自动运行，在项目根目录下创建这两个文件，而无需显式调用。

### 使用创建组件技能 {#use-the-create-component-skill}

首次使用时，该技能将从`project`和现有组件中自动检测`package`、`group`和`pom.xml`，要求您确认检测到的值，然后在项目根目录中创建`.aem-skills-config.yaml`。 首次使用前无需手动配置。

如果您希望预创建文件，请将`.aem-skills-config.yaml`置于具有以下结构的项目根目录下：

```yaml
configured: true

project: "wknd"                                    # Check /apps/{project}/ or pom.xml
package: "com.adobe.aem.guides.wknd.core"          # Check core/pom.xml
group: "WKND Components"                           # Check existing component .content.xml files
```

文件位于技能目录之外，技能更新时永远不会覆盖该文件。

在AI聊天中描述组件：

```
Create an AEM component called "Hero Banner"

Dialog specification:
Title (title) - Textfield, mandatory
Subtitle (subtitle) - Textfield
Background Image (backgroundImage) - Fileupload
CTA Text (ctaText) - Textfield
CTA Link (ctaLink) - Pathfield
```

代理会响应字段说明进行确认，然后生成所有组件文件。 支持的模式包括带有复合嵌套项的多字段、条件显示/隐藏逻辑、通过Sling资源合并器进行的核心组件扩展以及使用AEM Mocks的JUnit 5测试。

### 使用Dispatcher技能 {#use-the-dispatcher-skill}

调用任何Dispatcher或Apache HTTPD配置工作的Dispatcher技能。 该技能根据请求的性质将请求路由到六个专业子技能中的一个：

| 子技能 | 用途 |
|---|---|
| `workflow-orchestrator` | 端到端工作，包括设计、配置更改、验证和跟进 |
| `config-authoring` | 具体配置更改：过滤器、缓存规则、重写、主机、标头和场 |
| `technical-advisory` | 概念指导、政策解释和引文支持的建议 |
| `incident-response` | 运行时失败、缓存异常和回归 |
| `performance-tuning` | 缓存效率、延迟和吞吐量优化 |
| `security-hardening` | 曝光回顾和生产强化 |

对于广泛或首次请求，从`workflow-orchestrator`子技能开始。 对于有针对性的工作，请向相应的专家描述具体的关切事项和技能途径。

Dispatcher技能处理编排和咨询指导。 如下所述的Dispatcher MCP服务器提供了该技能在需要本地证据时所使用的七种验证和运行时工具。

## AEM快速入门MCP服务器 {#aem-quickstart-mcp-server}

模型上下文协议(MCP)是一个开放标准，它允许AI编码工具连接到外部数据源和服务。 AEM快速入门MCP服务器是一个内容包，一旦安装在本地AEM SDK实例中，就会将运行时数据直接公开给连接的AI工具，从而使代理能够检索日志、诊断OSGi故障以及检查请求处理，而无需离开IDE。

### 安装内容包 {#install-the-content-package}

从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Abeta)下载内容包，然后使用位于`com.adobe.aem:com.adobe.aem.mcp-server-contribs-content`的包管理器将`/crx/packmgr`安装到本地快速入门中。

**兼容性：**&#x200B;已与AEM SDK `2026.2.24678.20260226T154829Z-260200`及更高版本一起验证。

### 可用工具 {#available-tools}

| 工具 | 描述 |
|---|---|
| `aem-logs` | 检索AEM和OSGi日志条目，这些条目可以按正则表达式模式、日志级别和条目计数筛选 |
| `diagnose-osgi-bundle` | 诊断捆绑包或DS组件未启动的原因；报告缺少包、引用不满足和配置问题 |
| `recent-requests` | 返回最近的HTTP请求，其中具有Sling的完整内部处理跟踪（资源解析、脚本解析、过滤器链），可按路径正则表达式筛选 |

### 配置IDE {#configure-your-ide}

#### 光标 {#cursor}

在光标设置中，添加新的自定义MCP服务器：

```json
"aem-cs-sdk": {
  "type": "streamable-http",
  "url": "http://localhost:4502/bin/mcp",
  "headers": {
    "Authorization": "Basic YWRtaW46YWRtaW4="
  }
}
```

#### GitHub Copilot与IntelliJ IDEA {#github-copilot-with-ihtellij-idea}

导航到&#x200B;**工具> GitHub Copilot >模型上下文协议(MCP)**，然后单击&#x200B;**配置**。 添加：

```json
"aem-cs-sdk": {
  "url": "http://localhost:4502/bin/mcp",
  "requestInit": {
    "headers": {
      "Authorization": "Basic YWRtaW46YWRtaW4="
    }
  }
}
```

#### 其他IDE {#other-ides}

任何MCP客户端都可以指向带有`http://localhost:4502/bin/mcp`标头的`Authorization: Basic YWRtaW46YWRtaW4=`来连接。 使用IDE的MCP设置配置自定义标头。

>[!NOTE]
>
>值`Basic YWRtaW46YWRtaW4=`是`admin:admin`的Base64编码，这是本地Quickstart的默认凭据。 请勿在非本地环境中使用它。

## Dispatcher MCP服务器 {#dispatcher-mcp-server}

Dispatcher MCP服务器与AEM Dispatcher SDK捆绑在一起。 它使AI工具能够针对Docker中本地运行的Dispatcher实例验证Dispatcher和Apache HTTPD配置、跟踪请求处理和检查缓存行为。

与Dispatcher技能不同， Dispatcher MCP服务器仅公开工具：七个MCP工具，无提示或资源。

### 先决条件 {#prerequisites}

- Docker Desktop 4.x或更高版本，已安装并正在运行
- 从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Abeta)下载的AEM Dispatcher SDK

>[!NOTE]
>
>如果您看到`client version 1.43 is too new`，请在外壳程序或`DOCKER_API_VERSION=1.41`中设置`mcp.json`。

### 安装Dispatcher SDK {#install-the-dispatcher-sdk}

**macOS和Linux：**

```bash
chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
./aem-sdk-dispatcher-tools-<version>-unix.sh
cd dispatcher-sdk-<version>
chmod +x ./bin/docker_run_mcp.sh
./bin/docker_run_mcp.sh test
```

**Windows：**

```powershell
Expand-Archive aem-sdk-dispatcher-tools-<version>-windows.zip
```

运行`./bin/docker_run_mcp.sh help`以检索复制粘贴IDE配置，运行`./bin/docker_run_mcp.sh version`以确认捆绑的MCP和SDK版本。 使用`./bin/docker_run_mcp.sh diagnose`调查连接问题。

### 配置光标 {#configure-cursor}

将`aem-dispatcher-mcp`条目添加到`~/.cursor/mcp.json`：

```json
{
  "mcpServers": {
    "aem-dispatcher-mcp": {
      "command": "<path_to_dispatcher_sdk>/bin/docker_run_mcp.sh",
      "env": {
        "DOCKER_API_VERSION": "1.43",
        "AEM_DEPLOYMENT_MODE": "cloud",
        "MCP_LOG_LEVEL": "trace",
        "MCP_LOG_FILE": "/tmp/dispatcher-mcp.log",
        "DISPATCHER_CONFIG_PATH": "<path_to_dispatcher_src>"
      }
    }
  }
}
```

将`<path_to_dispatcher_sdk>`替换为提取的Dispatcher SDK位置，将`<path_to_dispatcher_src>`替换为项目的调度程序`src`目录。 将`DISPATCHER_CONFIG_PATH`设置为包含定义`/docroot`的文件的配置根。 `MCP_LOG_LEVEL`和`MCP_LOG_FILE`是可选的调试设置。 如果您看到`client version 1.43 is too new`，请将`DOCKER_API_VERSION`设置为`1.41`。 如果已配置其他MCP服务器，请添加`aem-dispatcher-mcp`项而不替换它们。 保存后重新启动光标。

其他IDE也可以以类似的方式进行配置。 SDK的`docs/DispatcherMCP.md`包含Claude Desktop和VS代码的完整示例。

### 可用工具 {#available-tools-dispatcher}

| 工具 | 描述 |
|---|---|
| `validate` | 验证Dispatcher和Apache HTTPD配置 |
| `lint` | 运行模式感知静态检查和最佳实践分析 |
| `sdk` | 执行Dispatcher SDK工作流： `validate`、`validate-full`、`three-phase-validate`、`docker-test`、`check-files`、`diff-baseline` |
| `trace_request` | 使用运行时证据跟踪请求行为 |
| `inspect_cache` | 检查目标URL的缓存和docroot行为 |
| `monitor_metrics` | 从Dispatcher和HTTPD日志中读取运行时指标 |
| `tail_logs` | 跟踪相关的Dispatcher和HTTPD运行时日志 |

MCP表面仅有意公开这七种工具；提示和资源保留在技能层中。 在提取的Dispatcher SDK中的`docs/DispatcherMCP.md`中提供了完整的参考文档。
