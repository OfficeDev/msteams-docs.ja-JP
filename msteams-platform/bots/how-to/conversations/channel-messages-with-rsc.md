---
title: RSC を使用してすべてのチャネル メッセージを受信する
author: surbhigupta12
description: RSC アクセス許可を持つすべてのチャネル メッセージを受信する
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 833bdbc015cf852fcd899ce4e75f742448b89978
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631413"
---
# <a name="receive-all-channel-messages-with-rsc"></a>RSC を使用してすべてのチャネル メッセージを受信する

> [!NOTE]
> この機能は現在、パブリック開発者 [プレビューでのみ利用](../../../resources/dev-preview/developer-preview-intro.md) できます。

リソース固有の同意 (RSC) アクセス許可モデルは、もともと api 用に開発されたTeams Graphボット シナリオに拡張されました。

現在、ボットはユーザー チャネル メッセージを受信できるのは、ユーザー チャネル メッセージが@mentioned。 RSC を使用すると、ボットがチーム内の標準チャネル間でユーザー メッセージを受信する同意をチームの所有者に要求@mentioned。 この機能は、アプリで有効になっている RSC のマニフェストでアクセス許可 `ChannelMessage.Read.Group` をTeamsします。 構成後、チームの所有者はアプリのインストール プロセス中に同意を付与できます。

アプリで RSC を有効にする方法の詳細については、「リソース固有の同意」を参照[Teams。](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)

## <a name="enable-bots-to-receive-all-channel-messages"></a>ボットがすべてのチャネル メッセージを受信可能にする

`ChannelMessage.Read.Group`RSC アクセス許可はボットに拡張されます。 ユーザーの同意を得た場合、このアクセス許可を使用すると、グラフ アプリケーションは会話内のすべてのメッセージを取得し、ボットはメッセージを読み取ることなくすべてのチャネル @mentioned。

## <a name="update-app-manifest"></a>アプリ マニフェストの更新

ボットがすべてのチャネル メッセージを受信するには、プロパティで指定されたアクセス許可Teamsアプリ マニフェストで RSC を `ChannelMessage.Read.Group` 構成する必要 `webApplicationInfo` があります。

![アプリ マニフェストの更新](~/bots/how-to/conversations/Media/appmanifest.png)

オブジェクトの例を次に示 `webApplicationInfo` します。

* **id**: Azure Active Directory (AAD) アプリ ID。 これは、ボット ID と同じものにできます。
* **resource**: 任意の文字列。 このフィールドは RSC で操作を行う必要がありますが、エラー応答を回避するには、値を追加する必要があります。
* **applicationPermissions**: アプリの RSC アクセス許可を指定 `ChannelMessage.Read.Group` する必要があります。 詳細については、「リソース固有 [のアクセス許可」を参照してください](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)。

次のコードは、アプリ マニフェストの例を示しています。

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team-to-test"></a>テストするチームのサイドロード

テストするチームにサイドロードするには、RSC を持つチーム内のすべてのチャネル メッセージが、次の情報を取得せずに受信@mentioned。

1. チームを選択または作成します。
1. 左側のウィンドウから &#x25CF;&#x25CF;&#x25CF; 省略記号を選択します。 ドロップダウン メニューが表示されます。
1. ドロップダウン **メニューから [チーム** の管理] を選択します。 詳細が表示されます。

   ![チームでのアプリの管理](~/bots/how-to/conversations/Media/managingteam.png)

1. **[アプリ]** を選択します。 複数のアプリが表示されます。
1. 右下 **アップロードカスタム アプリを** 選択します。

    ![カスタム アプリのアップロード](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. [開く] ダイアログ ボックスから **アプリ パッケージを** 選択します。
1. [**開く**]を選択します。

    ![アプリ パッケージの選択](~/bots/how-to/conversations/Media/selectapppackage.png)

1. アプリ **の詳細** ポップアップから [追加] を選択して、選択したチームにボットを追加します。

    ![ボットの追加](~/bots/how-to/conversations/Media/addingbot.png)

1. チャネルを選択し、ボットのチャネルにメッセージを入力します。

    ボットは、メッセージを受信せずにメッセージを@mentioned。

    ![ボットがメッセージを受信する](~/bots/how-to/conversations/Media/botreceivingmessage.png)

## <a name="see-also"></a>関連項目

* [ボットの会話](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [リソース固有の同意](/microsoftteams/resource-specific-consent)
* [リソース固有の同意をテストする](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [アップロードカスタム アプリのTeams](~/concepts/deploy-and-publish/apps-upload.md)
