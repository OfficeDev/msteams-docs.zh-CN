---
title: 在不同的环境中测试应用行为
author: surbhigupta
description: 在本模块中，了解如何在不同的环境中测试应用行为
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 187219fec76830119e795d1dd60a36b2374c65ac
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617117"
---
# <a name="test-app-behavior-in-different-environment"></a>在不同的环境中测试应用行为

可以与 Microsoft Teams 集成后测试 Teams 应用。 若要测试 Teams 应用，需要在环境中至少创建一个工作区。 可以使用 Teams 工具包测试 Teams 应用：

* **在 Teams 中本地托管**：Teams 工具包通过将 Teams 应用旁加载到 Teams 以在本地环境中进行测试，在本地托管 Teams 应用。

* **Teams 中托管的云**：若要远程测试 Teams 应用，需要使用预配和部署在 Microsoft Azure Active Directory (Azure AD) 上对其进行云托管。 这涉及到将解决方案上传到 Azure AD，然后上传到 Teams。

> [!NOTE]
> 对于生产规模调试和测试，建议遵循你所在公司的指导方针，以确保能够通过自己的流程支持测试、暂存和部署。

## <a name="locally-hosted-environment"></a>本地托管环境

Teams 是基于云的产品，需要其访问的所有服务，才能使用 HTTPS 终结点公开提供。 本地托管是关于旁加载到 Teams 以在本地环境中进行测试。

> [!NOTE]
> 虽然可以使用所选的任何工具进行测试，但我们建议使用 [ngrok](https://ngrok.com/download)

## <a name="cloud-hosted-environment"></a>云托管环境

若要托管开发和生产代码及其 HTTPS 终结点，需要使用 Azure AD 上的预配和部署远程测试团队应用。 需要确保可从文件中的对象`manifest.jason`中[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)列出的 Teams 应用访问所有域

> [!NOTE]
> 若要确保环境安全，请明确说明所引用的确切域和子域，并且这些域必须由你控制。例如，不建议使用 `*.azurewebsites.net`，但建议使用 `contoso.azurewebsites.net`。

## <a name="see-also"></a>另请参阅

* [在本地调试 Microsoft Teams 应用](debug-local.md)
* [调试后台进程](debug-background-process.md)
* [使用 Teams 工具包预配云资源](provision.md)
* [部署到云](deploy.md)
* [预览和自定义 Teams 应用清单](TeamsFx-preview-and-customize-app-manifest.md)
* [管理多个环境](TeamsFx-multi-env.md)
