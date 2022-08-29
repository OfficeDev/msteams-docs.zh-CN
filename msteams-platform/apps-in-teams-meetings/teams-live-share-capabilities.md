---
title: Live Share 入门
author: surbhigupta
description: 请在本模块中详细了解 Live Share SDK 功能、RSC 权限、临时数据结构。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 35b39f062bcdaf79e0c32d33260dbd0940a4fe2c
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425601"
---
# <a name="live-share-core-capabilities"></a>Live Share 核心功能

Live Share SDK 可以很轻松地添加到会议扩展的 `sidePanel` 和 `meetingStage` 上下文。 本文重点介绍如何将 Live Share SDK 集成到应用和 SDK 的关键功能中。

> [!NOTE]
> 目前，仅支持计划的会议，并且所有参与者都必须在会议日历上。 目前不支持一对一通话、群组呼叫、立即开会等会议类型。

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-dashboard.png" alt-text="Teams Live Share":::

## <a name="install-the-javascript-sdk"></a>安装 JavaScript SDK

[Live Share SDK](https://github.com/microsoft/live-share-sdk) 是在 [npm](https://www.npmjs.com/package/@microsoft/live-share) 上发布的 JavaScript 包，你可以通过 npm 或 Yarn 下载。

### <a name="npm"></a>npm

```bash
npm install @microsoft/live-share --save
```

### <a name="yarn"></a>纱

```bash
yarn add @microsoft/live-share
```

## <a name="register-rsc-permissions"></a>注册 RSC 权限

若要为会议扩展启用 Live Share SDK，必须首先将以下 RSC 权限添加到应用清单中：

```json
{
  // ...rest of your manifest here
  "configurableTabs": [
    {
        "configurationUrl": "https://<<BASE_URI_ORIGIN>>/config",
        "canUpdateConfiguration": false,
        "scopes": [
            "groupchat"
        ],
        "context": [
            "meetingSidePanel",
            "meetingStage"
        ]
    }
  ],
  "validDomains": [
    "<<BASE_URI_ORIGIN>>"
  ],
  "authorization": {
    "permissions": {
      "resourceSpecific": [
        // ...other permissions here
        {
          "name": "LiveShareSession.ReadWrite.Chat",
          "type": "Delegated"
        },
        {
          "name": "LiveShareSession.ReadWrite.Group",
          "type": "Delegated"
        },
        {
          "name": "MeetingStage.Write.Chat",
          "type": "Delegated"
        },
        {
          "name": "ChannelMeetingStage.Write.Group",
          "type": "Delegated"
        }
      ]
    }
  }
}
```

## <a name="join-a-meeting-session"></a>加入会议会话

按照步骤加入与用户会议关联的会话：

1. 初始化 Teams 客户端 SDK。
2. 初始化 [TeamsFluidClient](/javascript/api/@microsoft/live-share/teamsfluidclient)。
3. 定义要同步的数据结构。 例如，`SharedMap`。
4. 加入容器。

示例：

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import * as microsoftTeams from "@microsoft/teams-js";
import { TeamsFluidClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap } from "fluid-framework";

// Initialize the Teams Client SDK
await microsoftTeams.app.initialize();

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

---

这就是设置容器和加入会议会话所需的全部操作。 现在，让我们回顾一下可与 Live Share SDK 一起使用的不同类型的 _分布式数据结构_。

## <a name="fluid-distributed-data-structures"></a>流体分布式数据结构

Live Share SDK 支持 Fluid Framework 中包含的任何[分布式数据结构](https://fluidframework.com/docs/data-structures/overview/)。 下面是对一些可用的不同类型的对象的快速概述：

| 共享对象                                                                       | 说明                                                                                                                             |
| ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [SharedMap](https://fluidframework.com/docs/data-structures/map/)                   | 分布式键值存储。 为给定键设置任何 JSON 可序列化对象，以便为会话中的每个人同步该对象。 |
| [SharedSegmentSequence](https://fluidframework.com/docs/data-structures/sequences/) | 一种类似于列表的数据结构，用于在集位置存储一组项（称为段）。                                               |
| [SharedString](https://fluidframework.com/docs/data-structures/string/)             | 已针对编辑文档文本编辑进行了优化的分布式字符串序列。                                                                |

让我们看看 `SharedMap` 的工作原理。 在此示例中，我们使用 `SharedMap` 生成了播放列表功能。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient } from "@microsoft/live-share";
import { SharedMap } from "fluid-framework";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { playlistMap: SharedMap },
};
const { container } = await client.joinContainer(schema);
const playlistMap = container.initialObjects.playlistMap as SharedMap;

// Register listener for changes to values in the map
playlistMap.on("valueChanged", (changed, local) => {
  const video = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video) {
  // Add video to map
  playlistMap.set(video.id, video);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient } from "@microsoft/live-share";
import { ContainerSchema, SharedMap, IValueChanged } from "fluid-framework";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { exampleMap: SharedMap },
};
const { container } = await client.joinContainer(schema);
const playlistMap = container.initialObjects.playlistMap as SharedMap;

// Declare interface for object being stored in map
interface IVideo {
  id: string;
  url: string;
}

// Register listener for changes to values in the map
playlistMap.on("valueChanged", (changed: IValueChanged, local: boolean) => {
  const video: IVideo | undefined = playlistMap.get(changed.key);
  // Update UI with added video
});

function onClickAddToPlaylist(video: IVideo) {
  // Add video to map
  playlistMap.set(video.id, video);
}
```

---

> [!NOTE]
> 核心 Fluid Framework DDS 对象不支持会议角色验证。 会议中的每个人都可以更改通过这些对象存储的数据。

## <a name="live-share-ephemeral-data-structures"></a>Live Share 临时数据结构

Live Share SDK 包括一组新的临时 `SharedObject` 类，这些类提供不存储在 Fluid 容器中的有状态和无状态对象。 例如，如果要在应用中创建激光笔功能（例如常用的 PowerPoint Live 集成），可以使用我们的 `EphemeralEvent` 或 `EphemeralState` 对象。

| 临时对象                                                             | Description                                                                                                                             |
| ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [EphemeralPresence](/javascript/api/@microsoft/live-share/ephemeralpresence) | 查看哪些用户处于联机状态，为每个用户设置自定义属性，并广播其状态更改。                               |
| [EphemeralEvent](/javascript/api/@microsoft/live-share/ephemeralevent)       | 使用有效负载中的任何自定义数据属性广播单个事件。                                                             |
| [EphemeralState](/javascript/api/@microsoft/live-share/ephemeralstate)       | 与 SharedMap 类似，SharedMap 是一种分布式键值存储，允许基于角色（例如演示者）进行受限状态更改。 |

### <a name="ephemeralpresence-example"></a>EphemeralPresence 示例

该 `EphemeralPresence` 类使跟踪会话中的人员比以往更容易。 调用 `.initialize()` 或 `.updatePresence()` 方法时，可以为该用户分配自定义元数据，例如名称或配置文件图片。 通过侦 `presenceChanged` 听事件，每个客户端接收到最新的 `EphemeralPresenceUser` 对象，将所有状态更新折叠为每个唯 `userId`一的单个记录。

> [!NOTE]
> 分配给每个 `EphemeralPresenceUser` UUID 的默认`userId`值是随机 UUID，不会直接绑定到 AAD 标识。 可以通过将自定义 `userId` 设置为主键来重写此项，如下面的示例所示。

示例：

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import {
  TeamsFluidClient,
  EphemeralPresence,
  PresenceState,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    presence: EphemeralPresence,
  },
};
const { container } = await client.joinContainer(schema);
const presence = container.initialObjects.presence;

// Register listener for changes to presence
presence.on("presenceChanged", (userPresence, local) => {
  // Update UI with presence
});

// Start tracking presence
presence.initialize("YOUR_CUSTOM_USER_ID", {
  name: "Anonymous",
  picture: "DEFAULT_PROFILE_PICTURE_URL",
});

function onUserDidLogIn(userName, profilePicture) {
  presence.updatePresence(PresenceState.online, {
    name: userName,
    picture: profilePicture,
  });
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralPresence, PresenceState, EphemeralPresenceUser } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomUserData {
  name: string;
  picture: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    presence: EphemeralPresence<ICustomUserData>,
  },
};
const { container } = await client.joinContainer(schema);
const presence = container.initialObjects.presence as EphemeralPresence<ICustomUserData>;

// Register listener for changes to presence
presence.on("presenceChanged", (userPresence: EphemeralPresenceUser<ICustomUserData>, local: boolean) => {
  // Update UI with presence
});

// Start tracking presence
presence.initialize("YOUR_CUSTOM_USER_ID", {
  name: "Anonymous",
  picture: "DEFAULT_PROFILE_PICTURE_URL",
});

function onUserDidLogIn(userName: string, profilePicture: string) {
  presence.updatePresence(PresenceState.online, {
    name: userName,
    picture: profilePicture,
  });
}
```

---

### <a name="ephemeralevent-example"></a>EphemeralEvent 示例

`EphemeralEvent` 是向会议中的其他客户端发送简单事件的好方法。 它适用于发送会话通知等场景。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralEvent } from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { notifications: EphemeralEvent },
};
const { container } = await client.joinContainer(schema);
const { notifications } = container.initialObjects;

// Register listener for incoming notifications
notifications.on("received", (event, local) => {
  let notificationToDisplay;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start listening for incoming notifications
await notifications.initialize();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralEvent, IEphemeralEvent } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomEvent extends IEphemeralEvent {
  senderName: string;
  text: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    notifications: EphemeralEvent<ICustomEvent>,
  },
};
const { container } = await client.joinContainer(schema);
const notifications = container.initialObjects.notifications as EphemeralEvent<ICustomEvent>;

// Register listener for incoming notifications
notifications.on("received", (event: ICustomEvent, local: boolean) => {
  let notificationToDisplay: string;
  if (local) {
    notificationToDisplay = `You ${event.text}`;
  } else {
    notificationToDisplay = `${event.senderName} ${event.text}`;
  }
  // Display notification in your UI
});

// Start listening for incoming notifications
await notifications.initialize();

notifications.sendEvent({
  senderName: "LOCAL_USER_NAME",
  text: "joined the session",
});
```

---

### <a name="ephemeraltimer-example"></a>EphemeralTimer 示例

`EphemeralTimer` 启用具有时间限制的方案，例如组冥想计时器或游戏的圆计时器。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralTimer } from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { timer: EphemeralTimer },
};
const { container } = await client.joinContainer(schema);
const { timer } = container.initialObjects;

// Register listener for when the timer starts its countdown
timer.on("started", (config, local) => {
  // Update UI to show timer has started
});

// Register listener for when a paused timer has resumed
timer.on("played", (config, local) => {
  // Update UI to show timer has resumed
});

// Register listener for when a playing timer has paused
timer.on("paused", (config, local) => {
  // Update UI to show timer has paused
});

// Register listener for when a playing timer has finished
timer.on("finished", (config) => {
  // Update UI to show timer is finished
});

// Register listener for the timer progressed by 20 milliseconds
timer.on("onTick", (milliRemaining) => {
  // Update UI to show remaining time
});

// Start synchronizing timer events for users in session
await timer.initialize();

// Start a 60 second timer
const durationInMilliseconds = 1000 * 60;
timer.start(durationInMilliseconds);

// Pause the timer for users in session
timer.pause();

// Resume the timer for users in session
timer.play();
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import {
  TeamsFluidClient,
  EphemeralTimer,
  EphemeralTimerEvents,
  ITimerConfig,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { timer: EphemeralTimer },
};
const { container } = await client.joinContainer(schema);
const timer = container.initialObjects.timer as EphemeralTimer;

// Register listener for when the timer starts its countdown
timer.on(EphemeralTimerEvents.started, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has started
});

// Register listener for when a paused timer has resumed
timer.on(EphemeralTimerEvents.played, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has resumed
});

// Register listener for when a playing timer has paused
timer.on(EphemeralTimerEvents.paused, (config: ITimerConfig, local: boolean) => {
  // Update UI to show timer has paused
});

// Register listener for when a playing timer has finished
timer.on(EphemeralTimerEvents.finished, (config: ITimerConfig) => {
  // Update UI to show timer is finished
});

// Register listener for the timer progressed by 20 milliseconds
timer.on(EphemeralTimerEvents.onTick, (milliRemaining: number) => {
  // Update UI to show remaining time
});

// Start synchronizing timer events
await timer.initialize();

// Start a 60 second timer for users in session
const durationInMilliseconds = 1000 * 60;
timer.start(durationInMilliseconds);

// Pause the timer for users in session
timer.pause();

// Resume the timer for users in session
timer.play();
```

---

## <a name="role-verification-for-ephemeral-data-structures"></a>临时数据结构的角色验证

Teams 中的会议可以包括一对一通话到全体人员会议，也可包括组织中的成员。 临时对象旨在支持角色验证，允许你定义允许为每个临时对象发送消息的角色。 例如，你可以选择仅会议演示者和组织者可以控制视频播放，但仍允许来宾和与会者请求视频以观看下一步。

> [!NOTE]
> 该 `EphemeralPresence` 类不支持角色验证。 该 `EphemeralPresenceUser` 对象有一个 `getRoles` 方法，该方法返回给定用户的会议角色。

使用以下方法 `EphemeralState`的示例：

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import {
  TeamsFluidClient,
  EphemeralState,
  UserMeetingRole,
} from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { appState: EphemeralState },
};
const { container } = await client.joinContainer(schema);
const { appState } = container.initialObjects;

// Register listener for changes to state and corresponding custom data
appState.on("stateChanged", (state, data, local) => {
  // Update local app state
});

// Set roles who can change state and start listening for changes
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.initialize(allowedRoles);

function onSelectEditMode(documentId) {
  appState.changeState("editing", {
    documentId,
  });
}

function onSelectPresentMode(documentId) {
  appState.changeState("presenting", {
    documentId,
    presentingUserId: "LOCAL_USER_ID",
  });
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralState, UserMeetingRole } from "@microsoft/live-share";

// Declare interface for type of custom data for user
interface ICustomState {
  documentId: string;
  presentingUserId?: string;
}

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: {
    appState: EphemeralState<ICustomState>,
  },
};
const { container } = await client.joinContainer(schema);
const appState = container.initialObjects.appState as EphemeralState<ICustomState>;

// Register listener for changes to state and corresponding custom data
appState.on("stateChanged", (state: string, data: ICustomState | undefined, local: boolean) => {
  // Update local app state
});

// Set roles who can change state and start listening for changes
const allowedRoles: UserMeetingRole[] = [UserMeetingRole.organizer, UserMeetingRole.presenter];
appState.initialize(allowedRoles);

function onSelectEditMode(documentId: string) {
  appState.changeState("editing", {
    documentId,
  });
}

function onSelectPresentMode(documentId: string) {
  appState.changeState("presenting", {
    documentId,
    presentingUserId: "LOCAL_USER_ID",
  });
}
```

---

在将角色验证实现到应用之前（特别是 **组织者** 角色），请倾听客户以了解其应用场景。 不能保证会议组织者在会议中存在。 作为常规的法则，在组织内协作时，所有用户要么是 **组织者**，要么是 **演示者**。 如果用户是 **与会者**，这通常是代表会议组织者的有意决定。

## <a name="code-samples"></a>代码示例

| 示例名称 | Description                                                     | JavaScript                                  |
| ----------- | --------------------------------------------------------------- | ------------------------------------------- |
| 投掷骰子 | 启用所有连接的客户端以投掷骰子并查看结果。 | [View](https://aka.ms/liveshare-diceroller) |
| Agile Poker | 使所有连接的客户端都能够玩 Agile Poker 游戏。               | [View](https://aka.ms/liveshare-agilepoker) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [Live Share 媒体功能](teams-live-share-media-capabilities.md)

## <a name="see-also"></a>另请参阅

* [GitHub 存储库](https://github.com/microsoft/live-share-sdk)
* [Live Share SDK 参考文档](/javascript/api/@microsoft/live-share/)
* [Live Share 媒体 SDK 参考文档](/javascript/api/@microsoft/live-share-media/)
* [Live Share 常见问题解答](teams-live-share-faq.md)
* [会议中的 Teams 应用](teams-apps-in-meetings.md)
