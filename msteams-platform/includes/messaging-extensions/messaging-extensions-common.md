## <a name="add-a-messaging-extension-to-your-app"></a>向应用添加消息传递扩展

消息传递扩展是一种云托管服务，可侦听用户请求，然后使用结构化数据（如卡片） [做出响应](~/task-modules-and-cards/what-are-cards.md)。 通过 Bot Framework 对象将服务Microsoft Teams集成在 `Activity` 一起。 Bot Builder SDK 的 Node.js .NET 和扩展可帮助你向应用添加消息传递扩展功能。

![邮件扩展的消息流关系图](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>在 Bot Framework 中注册

如果尚未注册，必须先向用户注册Microsoft Bot Framework。 聊天机器人的 Microsoft 应用 ID 和回调终结点（如该终结点所定义）将在邮件扩展中用于接收和响应用户请求。 请记住为自动程序Microsoft Teams频道。

记录自动程序应用 ID 和应用密码，将需要在应用清单中提供应用 ID。

### <a name="update-your-app-manifest"></a>更新应用清单

与机器人和选项卡一样，更新 [应用的](~/resources/schema/manifest-schema.md#composeextensions) 清单以包含消息传递扩展属性。 这些属性控制邮件扩展在客户端中的显示Microsoft Teams行为。 从清单的 v1.0 开始，支持消息传递扩展。

#### <a name="declare-your-messaging-extension"></a>声明邮件扩展

若要添加邮件扩展，请通过 属性在清单中添加一个新的顶级 JSON `composeExtensions` 结构。 目前，你只能为应用创建单个邮件扩展。

> [!NOTE]
> 清单将消息传递扩展引用为 `composeExtensions` 。 这是为了维护向后兼容性。

扩展定义是具有以下结构的对象：

| 属性名称 | 用途 | 是否必需？ |
|---|---|---|
| `botId` | 使用 Bot Framework 注册的自动程序的唯一 Microsoft 应用 ID。 这通常应该与整个应用应用的 ID Teams相同。 | 是 |
| `scopes` | 一个数组，用于声明此扩展是可添加到还是可同时添加到或 (`personal` `team` 两) 。 | 是 |
| `canUpdateConfiguration` | 启用 **设置** 菜单项。 | 否 |
| `commands` | 此邮件扩展支持的命令数组。 只能使用 10 个命令。 | 是 |

#### <a name="define-commands"></a>定义命令

邮件扩展应声明一个命令，当用户从撰写框中的"更多选项" (&#8943;) 选择你的应用时，将显示此命令。

![邮件扩展中邮件扩展列表的Teams](~/assets/images/compose-extensions/compose-extension-list.png)

在应用清单中，命令项是具有以下结构的对象：

| 属性名称 | 用途 | 是否必需？ | 最低清单版本 |
|---|---|---|---|
| `id` | 分配给此命令的唯一 ID。 用户请求将包含此 ID。 | 是 | 1.0 |
| `title` | 命令名称。 此值显示在 UI 中。 | 是 | 1.0 |
| `description` | 指示此命令所执行操作的帮助文本。 此值显示在 UI 中。 | 是 | 1.0 |
| `type` | 设置命令的类型。 可取值包括 `query` 和 `action`。 如果不存在，则默认值设置为 `query` 。 | 否 | 1.4 |
| `initialRun` | 可选参数，与命令 `query` 一起使用。 如果设置为 **true**，则指示用户一旦在 UI 中选择此命令，就应执行此命令。 | 否 | 1.0 |
| `fetchTask` | 可选参数，与命令 `action` 一起使用。 设置为 **true** 可获取要显示在任务模块 中的自适应卡片或 [Web URL。](~/task-modules-and-cards/what-are-task-modules.md) 当命令的输入是动态的（而不是静态的参数集） `action` 时，会使用此功能。 请注意，如果设置为 **true，** 则忽略命令的静态参数列表。 | 否 | 1.4 |
| `parameters` | 命令的参数静态列表。 | 是 | 1.0 |
| `parameter.name` | 参数的名称。 这将在用户请求中发送到你的服务。 | 是 | 1.0 |
| `parameter.description` | 描述此参数的用途或应提供的值示例。 此值显示在 UI 中。 | 是 | 1.0 |
| `parameter.title` | 简短的用户友好参数标题或标签。 | 是 | 1.0 |
| `parameter.inputType` | 设置为所需的输入类型。 可能的值包括 `text` `textarea` `number` 、、、、、。 `date` `time` `toggle` 默认值设置为 `text` 。 | 否 | 1.4 |
| `context` | 用于定义邮件操作可用的上下文的值的可选数组。 可能的值是 `message` 、 `compose` 或 `commandBox` 。 默认值为“`["compose", "commandBox"]`”。 | 否 | 1.5 |
