---
title: 在协作控制应用中为外部客户端配置任务
author: surbhigupta
description: 在本模块中，了解如何在 Microsoft Teams 的协作控制应用中为外部客户端配置任务。
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: bb98ab632b335717a61499600aef01e652fd0dee
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2022
ms.locfileid: "67178873"
---
# <a name="configure-tasks-for-external-clients"></a>为外部客户端配置任务

可分配给不属于组织或无权访问应用程序的用户的外部任务，例如将任务分配给客户。

若要启用，需要执行额外的步骤，将 XML 字符串传递给附加到所需 MDA 窗体上的子网格组件的任务 PCF 控件的每个实例。 XML 字符串是一个参数化查询，允许控件从包含客户信息的表中提取所需的数据。

> [!NOTE]
> 目前，协作控件仅在 [公共开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中可用。

下面是创建外部任务的步骤：

1. 创建新的自定义实体（如客户）或重复使用现有客户实体（如联系人）。

1. 创建包含以下信息的新字段：
    1. 名称
    1. 电子邮件
    1. 父 (查找父表，例如检查) 
    > [!NOTE]
    > 上述创建的客户实体将是任务控件在分配外部任务时从中拉取客户信息的位置。 父字段可确保客户实体链接到检查记录。

1. 生成 Fetch XML 文件以允许 PCF 控件提取正确的客户信息。

    **配置 XML 架构**

    下面是任务配置 Fetch XML 的架构定义。 需要设计任何 Fetch XML 以满足以下要求：

    * 查询结果应返回每个用户对象的以下属性：
      * ID
      * displayname
      * 电子邮件，如果需要，请使用别名。
    * 查询应包含 **@top** 参数，以允许调用方限制结果数。
    * 查询应具有 **@rootEntityId** 参数，以便根据需要仅按相关记录筛选结果。
    * 查询应具有 **@useName** 参数以允许按名称筛选结果
    * 查询应具有 **@useIdentifier** 参数，仅允许提取所选用户。

    **配置 XML 架构和示例**

    XML 架构的配置从客户表中提取数据。 可以调整 `<fetch/>` 节点以指定自己的查询，以显示来自任何其他自定义表的用户。

    > [!NOTE]
    > XML 中的上述实体和属性名称和顺序属性 **采用PublisherPrefix_TableColumn** 格式。

    ```xml
    
    <custom-tasks> 
    <custom-task id="external" name="External" for="guest"> 
    <fetch top="@top"> 
    <entity name="[Name of table, e.g. Crb2891_customer]"> 
    <attribute name="[Name of ID column, e.g. Crb2891_customerid]" alias="id" /> 
    <attribute name="[Name of primary name column, e.g. Crb2891_name]" alias="displayname" /> 
    <attribute name="[Name of email column, e.g. Crb2891_email]" alias="email" /> 
    <order attribute ="[Name of primary name column, e.g. Crb2891_name]" descending="false" /> 
    <filter type="and"> 
    <condition attribute="[Name of parent lookup column, e.g. Crb2891_parent]" operator="eq" value="@rootEntityId" /> 
    <condition attribute="[Name of primary name column, e.g. Crb2891_name]" operator="like" value="@userName" /> 
    <condition attribute="[Name of email column, e.g. Crb2891_email]" operator="like" value="@userIdentifier" /> 
    </filter> 
    </link-entity> 
    </entity> 
    </fetch> 
    </custom-task> 
    </custom-tasks> 
    
    ```

1. 将任务控件绑定到经典窗体设计器中的子格。 选择 **“保存** ”，然后选择 **“切换到经典**”。

1. 在经典窗体设计器中移动，直到找到 **“任务”** 选项卡。双击子网格以打开其属性对话框。

    :::image type="content" source="~/assets/images/collaboration-control/subgrid-property.png" alt-text="“任务属性”对话框":::

1. 在属性对话框中，设置如下图所示的属性：

    :::image type="content" source="~/assets/images/collaboration-control/tasks-property.png" alt-text="任务属性设置":::

1. 转到“控件”选项卡，然后选择“自定义任务”属性上 :::image type="icon" source="~/assets/images/collaboration-control/edit-icon.png" alt-text="的编辑任务"::: ，以添加上面生成的 Fetch XML。

1. 粘贴 Fetch XML

    :::image type="content" source="~/assets/images/collaboration-control/set-fetchproperties.png" alt-text="提取 XML 属性设置":::

    :::image type="content" source="~/assets/images/collaboration-control/custom-tasksproperty.png" alt-text="提取 XML 自定义属性设置":::

1. 在“配置属性”“自定义任务”和“设置属性”窗口中选择“ **确定** ”。

1. 保存和发布。
