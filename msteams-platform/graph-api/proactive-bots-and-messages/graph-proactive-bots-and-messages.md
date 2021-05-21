---
title: Microsoft Graphを使用して、アクティブボットのインストールとメッセージングを承認Teams
description: インプリTeamsプロアクティブ メッセージングについて説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams プロアクティブ メッセージング チャットのインストール Graph
ms.openlocfilehash: 06b50e5ab8594c257959430383bab5e355af4e06
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566153"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a>Graph API を使用したアプリの事前インストールとメッセージの送信

>[!IMPORTANT]
> Microsoft GraphおよびMicrosoft Teamsパブリック プレビューは、早期アクセスとフィードバックのために利用できます。 このリリースでは広範なテストが実施されましたが、実稼働環境での使用を意図した製品ではありません。

## <a name="proactive-messaging-in-teams"></a>プロアクティブ メッセージング (Teams

プロアクティブ メッセージはボットによって開始され、ユーザーとの会話を開始します。 ウェルカム メッセージの送信、アンケートや投票の実施、組織全体の通知のブロードキャストなど、さまざまな目的に役立ちます。 インプロアクティブ メッセージTeams、アドホックまたはダイアログ ベース **の会話として配信** できます。

|メッセージ型 | 説明 |
|----------------|-------------- |
|アドホックプロアクティブ メッセージ| ボットは、会話フローを中断せずにメッセージを対話します。|
|ダイアログ ベースのプロアクティブ メッセージ | ボットは新しいダイアログ スレッドを作成し、会話を制御し、プロアクティブ メッセージを配信し、閉じ、コントロールを前のダイアログに返します。|

## <a name="proactive-app-installation-in-teams"></a>アプリのプロアクティブ インストールTeams

ボットがユーザーに事前にメッセージを送る前に、個人用アプリまたはユーザーがメンバーであるチームにインストールする必要があります。 アプリをインストールしていない、または以前に操作したユーザーに事前にメッセージを送信する必要がある場合があります。 たとえば、組織内のすべてのユーザーに重要な情報をメッセージする必要があります。 このようなシナリオでは、Microsoft Graph API を使用して、ユーザー向けボットを事前にインストールできます。

## <a name="permissions"></a>アクセス許可

Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true)リソースの種類のアクセス許可は、Microsoft Teams プラットフォーム内のすべてのユーザー (個人用) スコープまたはチーム (チャネル) スコープのアプリのインストール ライフサイクルを管理するのに役立ちます。

|アプリケーションのアクセス許可 | 説明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|事前サインインTeams使用せずに、アプリがユーザーの読み取り、インストール、アップグレード、アンインストールを行えます。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|事前サインインTeams使用せずに、アプリが任意のチームで自身を読み取り、インストール、アップグレード、アンインストールできます。|

これらのアクセス許可を使用するには、次の値で [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加する必要があります。
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id** — Azure ADアプリ ID。
> * **resource** — アプリのリソース URL。
>
>[!NOTE]
>
> * インストールは他のユーザー向けなので、ボットにはアプリケーションが必要であり、ユーザーが委任したアクセス許可は必要ではありません。
>
> * Azure テナントADは、アプリケーションに明示的に [アクセス許可を付与する必要があります](/graph/security-authorization#grant-permissions-to-an-application)。 アプリケーションにアクセス許可が付与された後、Azure テナントのすべてのADアクセス許可を取得します。

## <a name="enable-proactive-app-installation-and-messaging"></a>プロアクティブ アプリのインストールとメッセージングを有効にする

> [!IMPORTANT]
>Microsoft Graphは、組織のアプリ ストアまたは組織のアプリ ストアに発行されたアプリTeamsできます。

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ プロアクティブ メッセージング ボットを作成して発行Teams

開始するには、組織のアプリ ストア[または](../../bots/how-to/create-a-bot-for-teams.md)Teams ストアにある[](../../concepts/bots/bot-conversations/bots-conv-proactive.md)プロアクティブ メッセージング機能を備えるボットが[](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org)Teams[必要です](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)。

>[!TIP]
> 実稼働対応の [**Company Communicator**](../..//samples/app-templates.md#company-communicator)アプリ テンプレートはブロードキャスト メッセージングを許可し、プロアクティブボット アプリケーションを構築する良い基盤です。

### <a name="-get-the-teamsappid-for-your-app"></a>✔アプリを `teamsAppId` 取得する

**1.** 次の手順 `teamsAppId` が必要です。

組織 `teamsAppId` のアプリ カタログから取得できます。

**Microsoft Graph ページリファレンス:** [teamsApp リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

要求はオブジェクトを返す必要 `teamsApp` があります。 返されるオブジェクトは、アプリのカタログによって生成されるアプリ ID であり、アプリ マニフェストで指定した ID とは `id` Teams異なります。

```json
{
  "value": [
    {
      "id": "b1c5353a-7aca-41b3-830f-27d5218fe0e5",
      "externalId": "f31b1263-ba99-435a-a679-911d24850d7c",
      "name": "Test App",
      "version": "1.0.1",
      "distributionMethod": "Organization"
    }
  ]
}
```

**2.**  個人用スコープ内のユーザーに対してアプリが既にアップロードまたはサイドロードされている場合は、次のように `teamsAppId` 取得できます。

**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** チーム スコープ内のチャネルに対してアプリがアップロードまたはサイドロードされている場合は、次のように `teamsAppId` 取得できます。

**Microsoft Graph ページ リファレンス:** [チーム内のアプリの一覧](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> 結果の一覧を絞り込むには [**、teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) オブジェクトのフィールドをフィルター処理できます。

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ メッセージ受信者にボットが現在インストールされているかどうかを確認する

**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

この要求は、アプリがインストールされていない場合は空の配列、アプリがインストールされている場合は [単一の teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) オブジェクトを持つ配列を返します。

### <a name="-install-your-app"></a>✔ アプリをインストールする

**Microsoft Graph ページ リファレンス:** [ユーザー用アプリのインストール](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP POST** 要求:

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

ユーザーが実行中のMicrosoft Teams、アプリのインストールがすぐに表示されます。 インストールされているアプリを表示するには、再起動が必要になる場合があります。

### <a name="-retrieve-the-conversation-chatid"></a>✔ 会話の **chatId を取得する**

アプリがユーザー用にインストールされている場合、ボットは、プロアクティブ メッセージを送信するために必要な情報を含むイベント `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)通知を受信します。

また `chatId` 、次のように取得することもできます。

**Microsoft Graph ページ リファレンス:** [チャットの取得](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** アプリが必要です `{teamsAppInstallationId}` 。 持ってない場合は、次のコマンドを使用します。

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

応答 **の id** プロパティは、 `teamsAppInstallationId` です。

**2. 次** の要求を行って、 をフェッチします `chatId` 。

**HTTP GET 要求** (アクセス許可 — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

応答 **の id** プロパティは、 `chatId` です。

次の要求を使用 `chatId` して取得できますが、より広範なアクセス許可が必要 `Chat.Read.All` です。

**HTTP GET 要求** (アクセス許可 — `Chat.Read.All` ):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔プロアクティブ メッセージの送信

ボットは、 [ユーザーまたはチーム](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) に対してボットが追加され、すべてのユーザー情報を受信した後に、プロアクティブ メッセージを送信できます。

## <a name="see-also"></a>関連項目

* [**Microsoft Teams のアプリのセットアップ ポリシーを管理する**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [ユーザーにプロアクティブ通知を送信する SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a>その他のコード サンプルを見る
>
> [!div class="nextstepaction"]
> [**Teams のプロアクティブ メッセージング コード サンプル**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)