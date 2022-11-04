---
title: 在 Teams 环境中旁加载和测试应用
author: zyxiaoyuer
description: 在本模块中，了解如何在不同环境中旁加载和测试应用
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 721b3a30bcc8c2fa49bb06491f4ab24bbeb844fd
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833000"
---
# <a name="sideload-and-test-app-in-teams-environment"></a>在 Teams 环境中旁加载和测试应用

添加 API 连接后，可以在 Teams 工具包本地环境中测试 API 连接，并将应用程序部署到云。 在 CI/CD 管道中，使用不同的平台进行设置后，需要创建 Azure 服务主体来预配和部署资源。

在本部分中，你将了解

* [在本地环境中测试 API 连接](#test-api-connection-in-local-environment)
* [将应用程序部署到 Azure](#deploy-your-application-to-azure)
* [预配和部署 CI/CD 资源](#provision-and-deploy-cicd-resources)

## <a name="test-api-connection-in-local-environment"></a>在本地环境中测试 API 连接

以下步骤有助于测试 Teams 工具包本地环境中的 API 连接：

 1. **运行 npm 安装**

    在 或 `api` 文件夹下`bot`运行 `npm install` 以安装添加的包。

 2. **将 API 凭据添加到本地应用程序设置**

    Teams 工具包不要求提供凭据，但它在本地应用程序设置文件中保留占位符。 将占位符替换为访问 API 的相应凭据。 本地应用程序设置文件是 `.env.teamsfx.local` 或 `api` 文件夹中的文件`bot`。

 3. **使用 API 客户端发出 API 请求**

    从需要访问 API 的源代码导入 API 客户端：

    ```BASH
    import { yourApiClient } from '{relative path to the generated file}'
    ```

 4. **使用 Axios) 生成 http () 请求以目标 API (**

    生成的 API 客户端是 Axios API 客户端。 使用 Axios 客户端向 API 发出请求。

     > [!Note]
     > [Axios](https://www.npmjs.com/package/axios) 是一种常用的 nodejs 包，可帮助你处理 http () 请求。 有关如何发出 http () 请求的详细信息，请参阅 [Axios 示例文档](https://axios-http.com/docs/example) ，了解如何使 http () 。

## <a name="deploy-your-application-to-azure"></a>将应用程序部署到 Azure

若要将应用程序部署到 Azure，需要将身份验证添加到相应环境的应用程序设置。 例如，API 可能具有 `dev` 和 `prod`的不同凭据。 根据环境需求配置 Teams 工具包。

Teams 工具包配置本地环境。 引导的示例代码包含注释，告知需要配置哪些应用设置。 有关应用程序设置的详细信息，请参阅 [添加应用设置](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings)

## <a name="provision-and-deploy-cicd-resources"></a>预配和部署 CI/CD 资源

如果要在 CI/CD 中预配和部署面向 Azure 的资源，必须创建供使用的 Azure 服务主体。

执行以下步骤来创建 Azure 服务主体：

1. 在单个租户中注册 Microsoft Azure Active Directory (Azure AD) 应用程序。
2. Assign a role to your Azure AD application to access your Azure subscription. The `Contributor` role is recommended.
3. 创建新的 Azure AD 应用程序密钥。

> [!TIP]
> 保存租户 ID、应用程序 ID (AZURE_SERVICE_PRINCIPAL_NAME) 和密钥 (AZURE_SERVICE_PRINCIPAL_PASSWORD) 供未来使用。

有关详细信息，请参阅 [Azure 服务主体指南](/azure/active-directory/develop/howto-create-service-principal-portal)。 下面是创建服务主体的三种方法：

* [Microsoft Azure 门户](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="see-also"></a>另请参阅

[使用 Teams 工具包发布 Teams 应用](publish.md)
