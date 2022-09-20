---
title: CI/CD 模板
author: MuyangAmigo
description: 在本模块中，了解如何在 GitHub、Azure DevOps 和 Jenkins for Teams 应用程序开发人员CI/CD 模板中使用 CI/CD 管道模板
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 04/20/2022
ms.openlocfilehash: 05f797afcf54cab2d23ee24aae2c4985f3d724f2
ms.sourcegitcommit: dccb48902e08484692ab927415bcd3d61dc50db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2022
ms.locfileid: "67806870"
---
# <a name="set-up-cicd-pipelines"></a>设置 CI/CD 管道

TeamsFx 有助于在构建 Teams 应用程序时自动执行开发工作流。 以下是可用于设置 CI/CD 管道、创建工作流模板以及使用 GitHub、Azure DevOps、Jenkins 和其他平台自定义 CI/CD 工作流的工具和模板。 若要预配和部署资源，可以使用 Teams 开发人员门户创建 Azure 服务主体并发布 Teams 应用。 若要手动发布 Teams 应用，可以利用 [Teams 版开发人员门户](https://dev.teams.microsoft.com/home)。

|工具和模板 | 说明 |
|---|---|
|[TeamsFx-CLI-Action](https://github.com/OfficeDev/teamsfx-cli-action)|与 TeamsFx CLI 集成的 GitHub 操作。|
|[Visual Studio Code 中的 Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Visual Studio Code扩展，可帮助你开发 Teams 应用以及 GitHub、Azure DevOps 和 Jenkins 的自动化工作流。 |
|[TeamsFx CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) | 命令行工具，可帮助你开发 Teams 应用以及适用于 GitHub、Azure DevOps 和 Jenkins 的自动化工作流。|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) 和 [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| 用于 GitHub、Azure DevOps 或 Jenkins 外部自动化的脚本模板。 |

## <a name="set-up-pipelines"></a>设置 CI/CD 管道

可以使用以下平台设置管道：

1. [使用 GitHub 设置管道](#set-up-pipelines-with-github)
1. [使用 Azure DevOps 设置管道](#set-up-pipelines-with-azure-devops)
1. [使用 Jenkins 设置管道](#set-up-pipelines-with-jenkins)
1. [为其他平台设置管道](#set-up-pipelines-for-other-platforms)

## <a name="set-up-pipelines-with-github"></a>使用 GitHub 设置管道

使用 GitHub for CI/CD 设置管道：

* 创建工作流模板。

  * Visual Studio Code
  * TeamsFx CLI

* 自定义 CI/CD 工作流。

### <a name="create-workflow-templates"></a>创建工作流模板

可以使用 GitHub 创建以下工作流模板：

**Visual Studio Code 中的 Teams Toolkit**

1. 使用 Teams 工具包创建新的 Teams 应用项目。

1. 从左窗格中选择 **Teams 工具包** 图标 :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: 。

1. 选择 **“添加功能”**

   :::image type="content" source="../assets/images/teams-toolkit-v2/add-feature.png" alt-text="添加功能":::

1. 选择“**添加 CI/CD 工作流**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/toolkit-ci-cd-workflow.png" alt-text="选择 CI/CD 工作流":::

1. 从命令提示符中选择环境。
1. 选择 **GitHub** 作为 CI/CD 提供程序。
1. 从以下选项中至少选择一个模板：CI、CD、预配或发布到 Teams。
1. 打开模板并自定义适合方案的工作流。
1. 按照 `.github/workflows` 下的 README 文件在 GitHub 中设置工作流。

**TeamsFx CLI**

1. 将 `cd` 输入到 Teams 应用项目目录。
2. 输入 `teamsfx add cicd` 命令以启动交互式命令进程。
3. 从命令提示符中选择环境。
4. 选择 **GitHub** 作为 CI/CD 提供程序。
5. 从以下选项中至少选择一个模板：CI、CD、预配或发布到 Teams。
7. 打开模板并自定义适合方案的工作流。
8. 按照 `.github/workflows` 下的 README 文件在 GitHub 中设置工作流。

> [!NOTE]
> 如果需要添加其他工作流模板，可以按照同一过程在 Visual Studio Code 或 TeamsFx CLI 中创建工作流模板。

### <a name="customize-cicd-workflow"></a>自定义 CI/CD 工作流

可以更改或删除测试脚本以自定义 CI/CD 工作流：

1. 默认情况下，当对 `main` 分支进行新提交时，将触发 CD 工作流。
1. 根据需要更改生成脚本。
1. 根据需要删除测试脚本。

## <a name="set-up-pipelines-with-azure-devops"></a>使用 Azure DevOps 设置管道

使用 Azure DevOps for CI/CD 设置管道：

* 创建工作流模板。

  * Visual Studio Code
  * TeamsFx CLI

* 自定义 CI/CD 工作流。

### <a name="create-workflow-templates"></a>创建工作流模板

可以使用 Azure DevOps 创建以下工作流模板：

**Visual Studio Code 中的 Teams Toolkit**

1. 使用 Teams 工具包创建新的 Teams 应用项目。
2. 从左窗格中选择 **Teams 工具包** 图标 :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: 。
1. 选择“**添加 CI/CD 工作流**”。
1. 从命令提示符中选择环境。
1. 选择 **Azure DevOps** 作为 CI/CD 提供程序。
1. 从以下选项中选择至少一个模板：CI、CD、预配和发布到 Teams。
1. 打开模板并自定义适合方案的工作流。
1. 按照 `.azure/pipelines` 下的 README 文件在 Azure DevOps 中设置工作流。

**TeamsFx CLI**

1. 将 `cd` 输入到 Teams 应用项目目录。
2. 输入 `teamsfx add cicd` 命令以启动交互式命令进程。
3. 从命令提示符中选择环境。
4. 选择 **Azure DevOps** 作为 CI/CD 提供程序。
5. 从以下选项中至少选择一个模板：CI、CD、预配或发布到 Teams。
7. 打开模板并自定义适合方案的工作流。
8. 按照 `.azure/pipelines` 下的 README 文件在 Azure DevOps 中设置工作流。

> [!NOTE]
> 如果需要添加其他工作流模板，可以按照同一过程在 Visual Studio Code 或 TeamsFx CLI 中创建工作流模板。

### <a name="customize-ci-workflow"></a>自定义 CI 工作流

可以对脚本或工作流定义进行以下更改：

1. 使用 npm 生成脚本或自定义在自动化代码中生成的方式。
1. 使用 npm 测试脚本返回零以获得成功，并更改测试命令。

### <a name="customize-cd-workflow"></a>自定义 CD 工作流

可以对脚本或工作流定义进行以下更改：

1. 确保拥有 npm 生成脚本或自定义在自动化代码中生成的方式。
1. 确保有一个 npm 测试脚本，此脚本返回零以获得成功或更改测试命令。

## <a name="set-up-pipelines-with-jenkins"></a>使用 Jenkins 设置管道

使用 Jenkins for CI/CD 设置管道：

* 创建工作流模板。

  * Visual Studio Code
  * TeamsFx CLI

* 自定义 CI/CD 工作流。

### <a name="create-workflow-templates"></a>创建工作流模板

可以使用 Jenkins 创建以下工作流模板：

**Visual Studio Code 中的 Teams Toolkit**

1. 使用 Teams 工具包创建新的 Teams 应用项目。
2. 从左窗格中选择 **Teams 工具包** 图标 :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png"::: 。
3. 选择“**添加 CI/CD 工作流**”。
4. 从命令提示符中选择环境。
5. 选择 **Jenkins** 作为 CI/CD 提供程序。
6. 从以下选项中至少选择一个模板：CI、CD、预配或发布到 Teams。
7. 打开模板并自定义适合方案的工作流。
8. 按照 `.jenkins/pipelines` 下的自述文件，使用 Jenkins 设置工作流。

**TeamsFx CLI**

1. 将 `cd` 输入到 Teams 应用项目目录。
2. 输入 `teamsfx add cicd` 命令以启动交互式命令进程。
3. 从命令提示符中选择环境。
4. 选择 **Jenkins** 作为 CI/CD 提供程序。
5. 从以下选项中至少选择一个模板：CI、CD、预配或发布到 Teams。
7. 打开模板并自定义适合方案的工作流。
8. 按照 `.jenkins/pipelines` 下的自述文件，使用 Jenkins 设置工作流。

> [!NOTE]
> 如果需要添加其他工作流模板，可以按照同一过程在 Visual Studio Code 或 TeamsFx CLI 中创建工作流模板。

### <a name="customize-ci-workflow"></a>自定义 CI 工作流

可以对项目进行以下更改：

1. 更改 CI 流的触发方式。默认情况下，当将新更改推送到 **dev** 分支时，使用 **pollSCM** 的触发器。
1. 确保拥有 npm 生成脚本或自定义在自动化代码中生成的方式。
1. 确保有一个 npm 测试脚本，此脚本返回零以获得成功或更改测试命令。

### <a name="customize-cd-workflow"></a>自定义 CD 工作流

执行以下步骤自定义 CD 管道：

1. 更改 CD 流。默认情况下，是在将新更改推送到 `main` 分支时使用 `pollSCM` 的触发器。
1. 根据需要更改生成脚本。
1. 如果没有测试，请删除测试脚本。

## <a name="set-up-pipelines-for-other-platforms"></a>为其他平台设置管道

可以按照列出的预定义示例 bash 脚本在其他平台上构建和自定义 CI/CD 管道：

* [CI 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD 脚本](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

这些脚本基于跨平台 TeamsFx 命令行工具 [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli)。 可以使用 `npm install -g @microsoft/teamsfx-cli` 进行安装，并按照[文档](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)自定义脚本。

> [!NOTE]
>
> * 如果要启用在 CI 模式下运行的`@microsoft/teamsfx-cli`，请通过 `export CI_ENABLED=true` 打开 `CI_ENABLED`。 在 CI 模式下， `@microsoft/teamsfx-cli` 适用于 CI/CD。
> * 如果要在非交互模式下启用 `@microsoft/teamsfx-cli`，请使用命令设置全局配置： `teamsfx config set -g interactive false` 在非交互模式下， `@microsoft/teamsfx-cli` 不提示输入。

确保安全地在环境变量中设置 Azure 和 Microsoft 365 凭据。 例如，如果使用 GitHub 作为源代码存储库，请参阅 [Github 密钥](https://docs.github.com/en/actions/reference/encrypted-secrets)。

## <a name="provision-and-deploy-resources"></a>预配和部署资源

如果要在 CI/CD 中预配和部署面向 Azure 的资源，必须创建供使用的 Azure 服务主体。

执行以下步骤来创建 Azure 服务主体：

1. 在单个租户中注册 Microsoft Azure Active Directory (Azure AD) 应用程序。
2. 将角色分配给 Azure AD 应用程序以访问 Azure 订阅。建议使用 `Contributor` 角色。
3. 创建新的 Azure AD 应用程序密钥。

> [!TIP]
> 保存租户 ID、应用程序 ID (AZURE_SERVICE_PRINCIPAL_NAME) 和密钥 (AZURE_SERVICE_PRINCIPAL_PASSWORD) 供未来使用。

有关详细信息，请参阅 [Azure 服务主体指南](/azure/active-directory/develop/howto-create-service-principal-portal)。 下面是创建服务主体的三种方法：

* [Microsoft Azure 门户](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>使用 Teams 开发人员门户发布 Teams 应用

如果有任何与 Teams 应用的清单文件相关的更改，可以更新清单并再次发布 Teams 应用。 若要手动发布 Teams 应用，可以利用 [Teams 版开发人员门户](https://dev.teams.microsoft.com/home)。

执行以下步骤发布应用：

1. 使用相应的帐户登录到 [Teams 开发人员门户](https://dev.teams.microsoft.com) 。
2. 以 zip 形式导入应用包，然后选择 `App -> Import app -> Replace`。
3. 在应用列表中选择目标应用。
4. 发布应用，选择 `Publish -> Publish to your org`。

## <a name="see-also"></a>另请参阅

* [GitHub Actions 快速入门](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [创建第一个 Azure DevOps 管道](/azure/devops/pipelines/create-first-pipeline)
* [创建第一个 Jenkins 管道](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [使用 Microsoft Teams 开发人员门户管理应用](../concepts/build-and-test/teams-developer-portal.md)
