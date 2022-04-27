---
title: 了解如何在应用程序开发人员GitHub、Azure DevOps和 Teams Jenkins 中使用 CI/CD 管道模板
author: MuyangAmigo
description: CI/CD 模板
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 04/20/2022
ms.openlocfilehash: 66560b1f228c32b0faf6569ff0ae536a81dc33c0
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073291"
---
# <a name="set-up-cicd-pipelines"></a>设置 CI/CD 管道

TeamsFx 有助于在生成Teams应用程序时自动执行开发工作流。 以下是可用于设置 CI/CD 管道、创建工作流模板以及使用 GitHub、Azure DevOps、Jenkins 和其他平台自定义 CI/CD 工作流的工具和模板。 若要预配和部署资源，可以使用Teams开发人员门户创建 Azure 服务主体并发布Teams应用。 若要手动发布Teams应用，可以利用[开发人员门户进行Teams](https://dev.teams.microsoft.com/home)。


|工具和模板 | 说明 |
|---|---|
|[TeamsFx-CLI-Action](https://github.com/OfficeDev/teamsfx-cli-action)|GitHub与 TeamsFx CLI 集成的操作。|
|[Visual Studio Code中的Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Visual Studio Code扩展，可帮助你开发Teams应用以及适用于 GitHub、Azure DevOps 和 Jenkins 的自动化工作流。 |
|[TeamsFx CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) | 命令行工具，可帮助你开发Teams应用以及适用于 GitHub、Azure DevOps 和 Jenkins 的自动化工作流。|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) 和 [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| 用于在 GitHub、Azure DevOps 或 Jenkins 之外实现自动化的脚本模板。 |


## <a name="set-up-pipelines"></a>设置管道

可以使用以下平台设置管道：

1. [使用GitHub设置管道](#set-up-pipelines-with-github)
1. [使用Azure DevOps设置管道](#set-up-pipelines-with-azure-devops)
1. [使用 Jenkins 设置管道](#set-up-pipelines-with-jenkins)
1. [为其他平台设置管道](#set-up-pipelines-for-other-platforms)


### <a name="set-up-pipelines-with-github"></a>使用GitHub设置管道

若要设置包含 CI/CD GitHub的管道：

1. 创建工作流模板。

   * Visual Studio Code
   * TeamsFx CLI

1. 自定义 CI/CD 工作流。


## <a name="create-workflow-templates-with-github"></a>使用GitHub创建工作流模板

**使用Visual Studio Code中的Teams Toolkit创建工作流模板**

1. 使用Teams Toolkit创建新的Teams应用项目。
1. 在 **Visual Studio Code** 活动栏中选择Teams Toolkit图标。
1. 选择 **“添加 CI/CD 工作流**”。
1. 从命令提示符中选择环境。
1. 选择 **GitHub** 作为 CI/CD 提供程序。
1. 从以下选项中选择至少一个模板：CI、CD、预配或发布到Teams。
1. 打开模板并自定义适合方案的工作流。
1. 按照以下`.github/workflows`自述文件在GitHub中设置工作流。

**使用 TeamsFx CLI 创建工作流模板**

1. 输入`cd`Teams应用项目目录。
2. 输入 `teamsfx add cicd` 命令以启动交互式命令过程。
3. 从命令提示符中选择环境。
4. 选择 **GitHub** 作为 CI/CD 提供程序。
5. 从以下选项中选择至少一个模板：CI、CD、预配或发布到Teams。
7. 打开模板并自定义适合方案的工作流。
8. 按照以下`.github/workflows`自述文件在GitHub中设置工作流。

> [!NOTE]
> 如果需要添加其他工作流模板，可以按照同一过程在 Visual Studio Code 或 TeamsFx CLI 中创建工作流模板。

### <a name="customize-cicd-workflow"></a>自定义 CI/CD 工作流

可以更改或删除测试脚本以自定义 CI/CD 工作流：

1. 默认情况下，当向分支提交 `main` 新提交时，会触发 CD 工作流。
1. 如果需要，请更改生成脚本。
1. 根据需要删除测试脚本。

### <a name="set-up-pipelines-with-azure-devops"></a>使用Azure DevOps设置管道

若要使用 CI/CD 的Azure DevOps设置管道：

1. 创建工作流模板。

   * Visual Studio Code
   * TeamsFx CLI

1. 自定义 CI/CD 工作流。


## <a name="create-workflow-templates-with-azure-devops"></a>使用Azure DevOps创建工作流模板

**使用Visual Studio Code中的Teams Toolkit创建工作流模板**

1. 使用Teams Toolkit创建新的Teams应用项目。
2. 在 **Visual Studio Code** 活动栏中选择Teams Toolkit图标。
3. 选择 **“添加 CI/CD 工作流**”。
4. 从命令提示符中选择环境。
5. 选择 **Azure DevOps** 作为 CI/CD 提供程序。
6. 从以下选项中选择至少一个模板：CI、CD、预配和发布到Teams。
7. 打开模板并自定义适合方案的工作流。
8. 按照以下`.azure/pipelines`自述文件在Azure DevOps中设置工作流。

**使用 TeamsFx CLI 创建工作流模板**

1. 输入`cd`Teams应用项目目录。
2. 输入 `teamsfx add cicd` 命令以启动交互式命令过程。
3. 从命令提示符中选择环境。
4. 选择 **Azure DevOps** 作为 CI/CD 提供程序。
5. 从以下选项中选择至少一个模板：CI、CD、预配或发布到Teams。
7. 打开模板并自定义适合方案的工作流。
8. 按照以下`.azure/pipelines`自述文件在Azure DevOps中设置工作流。

> [!NOTE]
> 如果需要添加其他工作流模板，可以按照同一过程在 Visual Studio Code 或 TeamsFx CLI 中创建工作流模板。

### <a name="customize-ci-workflow"></a>自定义 CI 工作流

下面是可以对脚本或工作流定义所做的更改：

1. 使用 npm 生成脚本或自定义在自动化代码中生成的方式。
1. 使用 npm 测试脚本，该脚本返回零以获得成功，并更改测试命令。

### <a name="customize-cd-workflow"></a>自定义 CD 工作流

下面是可以对脚本或工作流定义所做的更改：

1. 确保拥有 npm 生成脚本或自定义在自动化代码中生成的方式。
1. 确保你有一个 npm 测试脚本，该脚本返回零以获得成功或更改测试命令。

### <a name="set-up-pipelines-with-jenkins"></a>使用 Jenkins 设置管道

若要使用 Jenkins 为 CI/CD 设置管道，请执行以下操作：

1. 创建工作流模板。

   * Visual Studio Code
   * TeamsFx CLI

1. 自定义 CI/CD 工作流。

## <a name="create-workflow-templates-with-jenkins"></a>使用 Jenkins 创建工作流模板

**使用Visual Studio Code中的Teams Toolkit创建工作流模板**

1. 使用Teams Toolkit创建新的Teams应用项目。
2. 在 **Visual Studio Code** 边栏中选择Teams Toolkit图标。
3. 选择 **“添加 CI/CD 工作流**”。
4. 从命令提示符中选择环境。
5. 选择 **Jenkins** 作为 CI/CD 提供程序。
6. 从以下选项中选择至少一个模板：CI、CD、预配或发布到Teams。
7. 打开模板并自定义适合方案的工作流。
8. 按照以下 `.jenkins/pipelines` 自述文件设置 Jenkins 的工作流。

**使用 TeamsFx CLI 创建工作流模板**

1. 输入`cd`Teams应用项目目录。
2. 输入 `teamsfx add cicd` 命令以启动交互式命令过程。
3. 从命令提示符中选择环境。
4. 选择 **Jenkins** 作为 CI/CD 提供程序。
5. 从以下选项中选择至少一个模板：CI、CD、预配或发布到Teams。
7. 打开模板并自定义适合方案的工作流。
8. 按照以下 `.jenkins/pipelines` 自述文件设置 Jenkins 的工作流。

> [!NOTE]
> 如果需要添加其他工作流模板，可以按照同一过程在 Visual Studio Code 或 TeamsFx CLI 中创建工作流模板。

### <a name="customize-ci-workflow"></a>自定义 CI 工作流

以下是可以对项目所做的一些更改：

1. 更改 CI 流的触发方式。 默认值是在将新更改推送到 **开发** 分支时使用 **pollSCM** 的触发器。
1. 确保拥有 npm 生成脚本或自定义在自动化代码中生成的方式。
1. 确保你有一个 npm 测试脚本，该脚本返回零以获得成功或更改测试命令。


### <a name="customize-cd-workflow"></a>自定义 CD 工作流

执行以下步骤自定义 CD 管道：

1. 更改 CD 流。 默认值是使用将新更改推送到`main`分支时的触发器`pollSCM`。
1. 如有必要，请更改生成脚本。
1. 如果没有测试，请删除测试脚本。


### <a name="set-up-pipelines-for-other-platforms"></a>为其他平台设置管道

可以按照预定义的列出示例 bash 脚本在其他平台上生成和自定义 CI/CD 管道：

* [CI 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

这些脚本基于跨平台 TeamsFx 命令行工具 [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli)。 可以随文档一起 `npm install -g @microsoft/teamsfx-cli` 安装，并按照文 [档](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) 自定义脚本。

> [!NOTE]
>
> * 若要在 CI 模式下启 `@microsoft/teamsfx-cli` 用运行，请启 `CI_ENABLED` 用 `export CI_ENABLED=true`。 在 CI 模式下， `@microsoft/teamsfx-cli` CI/CD 很友好。
> * 若要在非交互模式下启`@microsoft/teamsfx-cli`用运行，请使用命令设置全局配置： `teamsfx config set -g interactive false` 在非交互模式下， `@microsoft/teamsfx-cli` 不提示输入。

确保安全地在环境变量中设置 Azure 和Microsoft 365凭据。 例如，如果使用GitHub作为源代码存储库，请参阅 [Github 机密](https://docs.github.com/en/actions/reference/encrypted-secrets)。


## <a name="provision-and-deploy-resources"></a>预配和部署资源

若要在 CI/CD 中预配和部署面向 Azure 的资源，必须创建供使用的 Azure 服务主体。

执行以下步骤来创建 Azure 服务主体：

1. 在单个租户中注册Microsoft Azure Active Directory (Azure AD) 应用程序。
2. 将角色分配给Azure AD应用程序以访问 Azure 订阅。 建议使用该 `Contributor` 角色。
3. 创建新的Azure AD应用程序机密。

> [!TIP]
> 保存租户 ID、应用程序 ID (AZURE_SERVICE_PRINCIPAL_NAME) 和机密 (AZURE_SERVICE_PRINCIPAL_PASSWORD) 供将来使用。

有关详细信息，请参阅 [Azure 服务主体指南](/azure/active-directory/develop/howto-create-service-principal-portal)。 下面是创建服务主体的三种方法：

* [Microsoft Azure门户](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>使用Teams开发人员门户发布Teams应用

如果有任何与Teams应用的清单文件相关的更改，则可以更新清单并再次发布Teams应用。

若要手动发布Teams应用，可以利用[开发人员门户进行Teams](https://dev.teams.microsoft.com/home)。

执行以下步骤发布应用：

1. 使用相应的帐户登录到[开发人员门户以Teams](https://dev.teams.microsoft.com)。
2. 通过选择 `App -> Import app -> Replace`zip 导入应用包。
3. 在应用列表中选择目标应用。
4. 通过选择 `Publish -> Publish to your org`发布应用。

### <a name="see-also"></a>另请参阅

* [GitHub Actions快速入门](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [创建第一个Azure DevOps管道](/azure/devops/pipelines/create-first-pipeline)
* [创建第一个 Jenkins 管道](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [使用 Microsoft Teams 开发人员门户管理应用](/concepts/build-and-test/teams-developer-portal)
