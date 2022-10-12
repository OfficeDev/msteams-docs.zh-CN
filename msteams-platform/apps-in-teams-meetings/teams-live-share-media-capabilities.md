---
title: Live Share 媒体功能
author: surbhigupta
description: 在本模块中，详细了解 Live Share 媒体功能、挂起和等待点、音频闪烁以及同步视频和音频。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 31b962d747a792b58a9efc9e2c52e42dc841ed18
ms.sourcegitcommit: 0fa0bc081da05b2a241fd8054488d9fd0104e17b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2022
ms.locfileid: "68552489"
---
# <a name="live-share-media-capabilities"></a>Live Share 媒体功能

:::image type="content" source="../assets/images/teams-live-share/live-share-media-capabilities-docs-feature-1.png" alt-text="Teams Live Share 媒体同步":::

视频和音频是现代世界和工作场所的重要部分。 我们收到了广泛的反馈，建议我们还可以采取更多措施来提高在会议中一起观看视频的质量、辅助功能和许可证保护。

Live Share SDK 为仅包含几行代码的任何 HTML `<video>` 和`<audio>`元素启用可靠的 **媒体同步**。 通过在播放器状态和传输控件层同步媒体，可以单独赋予视图和许可证，同时提供通过应用可获得的最高质量。

## <a name="install"></a>安装

若要使用 npm 将最新版本的 SDK 添加到应用程序，请执行以下操作：

```bash
npm install @microsoft/live-share@next --save
npm install @microsoft/live-share-media@next --save
```

OR

若要使用 [Yarn](https://yarnpkg.com/) 将最新版本的 SDK 添加到应用程序，请执行以下操作：

```bash
yarn add @microsoft/live-share@next
yarn add @microsoft/live-share-media@next
```

## <a name="media-sync-overview"></a>媒体同步概述

Live Share SDK 有两个与媒体同步相关的主类：

| 课程                                                                                        | 说明                                                                                                                                       |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [LiveMediaSession](/javascript/api/@microsoft/live-share-media/livemediasession)     | 自定义实时对象，旨在协调独立媒体流中的媒体传输控件和播放状态。                          |
| [MediaPlayerSynchronizer](/javascript/api/@microsoft/live-share-media/mediaplayersynchronizer) | 使用 >a0/> 同步实现 `IMediaPlayer` 接口（包括 HTML5 `<video>` 和 `<audio>` ） `LiveMediaSession`的任何对象。 |

示例：

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
</body>
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, UserMeetingRole } from "@microsoft/live-share";
import { LiveMediaSession } from "@microsoft/live-share-media";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { mediaSession: LiveMediaSession },
};
const { container } = await liveShare.joinContainer(schema);
const { mediaSession } = container.initialObjects;

// Get the player from your document and create synchronizer
const player = document.getElementById("player");
const synchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles = [UserMeetingRole.organizer, UserMeetingRole.presenter];
await mediaSession.initialize(allowedRoles);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, UserMeetingRole } from "@microsoft/live-share";
import { LiveMediaSession, IMediaPlayer, MediaPlayerSynchronizer } from "@microsoft/live-share-media";
import { ContainerSchema } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { mediaSession: LiveMediaSession },
};
const { container } = await liveShare.joinContainer(schema);
const mediaSession = container.initialObjects.mediaSession as LiveMediaSession;

// Get the player from your document and create synchronizer
const player: IMediaPlayer = document.getElementById("player") as HTMLVideoElement;
const synchronizer: MediaPlayerSynchronizer = mediaSession.synchronize(player);

// Define roles you want to allow playback control and start sync
const allowedRoles: UserMeetingRole[] = [UserMeetingRole.organizer, UserMeetingRole.presenter];
await mediaSession.initialize(allowedRoles);
```

---

自动 `LiveMediaSession` 侦听对组播放状态的更改。 `MediaPlayerSynchronizer` 侦听所发出的 `LiveMediaSession` 状态更改，并将其应用于提供的 `IMediaPlayer` 对象，例如 HTML5 `<video>` 或 `<audio>` 元素。 为了避免播放用户未有意启动的状态更改（如缓冲区事件），我们必须通过同步器调用传输控件，而不是直接通过播放器调用传输控件。

示例：

```html
<body>
  <video id="player">
    <source src="YOUR_VIDEO_SRC" type="video/mp4" />
  </video>
  <div class="player-controls">
    <button id="play-button">Play</button>
    <button id="pause-button">Pause</button>
    <button id="restart-button">Restart</button>
    <button id="change-track-button">Change track</button>
  </div>
</body>
```

```javascript
// ...

document.getElementById("play-button").onclick = () => {
  synchronizer.play();
};

document.getElementById("pause-button").onclick = () => {
  synchronizer.pause();
};

document.getElementById("restart-button").onclick = () => {
  synchronizer.seekTo(0);
};

document.getElementById("change-track-button").onclick = () => {
  synchronizer.setTrack({
    trackIdentifier: "SOME_OTHER_VIDEO_SRC",
  });
};
```

> [!NOTE]
> 虽然可以使用该 `LiveMediaSession` 对象手动同步媒体，但通常建议使用该 `MediaPlayerSynchronizer`对象。 根据你在应用中使用的玩家，可能需要创建一个委托填充码，使 Web 播放器的接口与 [IMediaPlayer](/javascript/api/@microsoft/live-share-media/imediaplayer) 接口匹配。

## <a name="suspensions-and-wait-points"></a>挂起和等待点

:::image type="content" source="../assets/images/teams-live-share/live-share-media-out-of-sync.png" alt-text="显示与演示者的暂停同步的屏幕截图。":::

如果要暂时挂起 `LiveMediaSession` 对象的同步，可以使用挂起功能。 默认情况下，[MediaSessionCoordinatorSuspension](/javascript/api/@microsoft/live-share-media/livemediasessioncoordinatorsuspension) 对象是本地对象，当用户可能想要跟进他们错过的内容、休息一下等等时，这很有帮助。 如果用户结束挂起，同步将自动恢复。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
// Suspend the media session coordinator
const suspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { MediaSessionCoordinatorSuspension } from "@microsoft/live-share-media";

// Suspend the media session coordinator
const suspension: MediaSessionCoordinatorSuspension = mediaSession.coordinator.beginSuspension();

// End the suspension when ready
suspension.end();
```

---

开始挂起时，还可以包含可选的 [CoordinationWaitPoint](/javascript/api/@microsoft/live-share-media/coordinationwaitpoint) 参数，该参数允许用户定义所有用户应在其中发生挂起的时间戳。 在所有用户都已结束该等待点的挂起之前，同步不会恢复。

下面是一些等待点特别有用的方案：

- 在视频中的特定点添加测验或调查。
- 等待每个人在视频启动前或缓冲时适当加载视频。
- 允许演示者选择视频中的点进行小组讨论。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
// Suspend the media session coordinator
const waitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension(waitPoint);
// End the suspension when the user readies up
document.getElementById("ready-up-button").onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { MediaSessionCoordinatorSuspension, CoordinationWaitPoint } from "@microsoft/live-share-media";

// Suspend the media session coordinator
const waitPoint: CoordinationWaitPoint = {
  position: 0,
  reason: "ReadyUp", // Optional.
};
const suspension = mediaSession.coordinator.beginSuspension(waitPoint);

// End the suspension when the user readies up
document.getElementById("ready-up-button")!.onclick = () => {
  // Sync will resume when everyone has ended suspension
  suspension.end();
};
```

---

## <a name="audio-ducking"></a>音频闪避

Live Share SDK 支持智能音频闪避。 可以通过将以下内容添加到代码中来使用应用程序中的功能：

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { meeting } from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer;
meeting.registerSpeakingStateChangeHandler((speakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    // If someone in the meeting starts speaking, periodically
    // lower the volume using your MediaPlayerSynchronizer's
    // VolumeLimiter.
    synchronizer.volumeLimiter?.lowerVolume();
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    // If everyone in the meeting stops speaking and the
    // interval timer is active, clear the interval.
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { meeting } from "@microsoft/teams-js";

// ... set up MediaPlayerSynchronizer

// Register speaking state change handler through Teams Client SDK
let volumeTimer: NodeJS.Timeout | undefined;
meeting.registerSpeakingStateChangeHandler((speakingState: meeting.ISpeakingState) => {
  if (speakingState.isSpeakingDetected && !volumeTimer) {
    // If someone in the meeting starts speaking, periodically
    // lower the volume using your MediaPlayerSynchronizer's
    // VolumeLimiter.
    synchronizer.volumeLimiter?.lowerVolume();
    volumeTimer = setInterval(() => {
      synchronizer.volumeLimiter?.lowerVolume();
    }, 250);
  } else if (volumeTimer) {
    // If everyone in the meeting stops speaking and the
    // interval timer is active, clear the interval.
    clearInterval(volumeTimer);
    volumeTimer = undefined;
  }
});
```

---

此外，将以下 [RSC](/microsoftteams/platform/graph-api/rsc/resource-specific-consent) 权限添加到应用清单中：

```json
{
  // ...rest of your manifest here
  "authorization": {
    "permissions": {
      "resourceSpecific": [
        // ...other permissions here
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Chat",
          "type": "Delegated"
        },
        {
          "name": "OnlineMeetingIncomingAudio.Detect.Group",
          "type": "Delegated"
        }
      ]
    }
  }
}
```

> [!NOTE]
> `registerSpeakingStateChangeHandler`用于音频回避的 API 目前仅在 Microsoft Teams 桌面上工作，并按计划运行并满足现在的会议类型。

## <a name="code-samples"></a>代码示例

| 示例名称          | Description                                                                                                                               | JavaScript                                     |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| React 视频          | 演示 LiveMediaSession 对象如何使用 HTML5 视频的基本示例。                                                        | [View](https://aka.ms/liveshare-reactvideo)    |
| React 媒体模板 | 使所有连接的客户端能够一起观看视频、生成共享播放列表、转移在控制的人，并通过视频进行批注。 | [View](https://aka.ms/liveshare-mediatemplate) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [Live Share 画布](teams-live-share-canvas.md)

## <a name="see-also"></a>另请参阅

- [Live Share SDK 常见问题解答](teams-live-share-faq.md)
- [Live Share SDK 参考文档](/javascript/api/@microsoft/live-share/)
- [Live Share 媒体 SDK 参考文档](/javascript/api/@microsoft/live-share-media/)
- [会议中的 Teams 应用](teams-apps-in-meetings.md)
