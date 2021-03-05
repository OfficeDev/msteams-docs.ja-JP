---
title: Microsoft Graph を使用して Teams でのプロアクティブ ボットのインストールとメッセージングを承認する
description: Teams でのプロアクティブ メッセージングと実装方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams プロアクティブ メッセージング チャットのインストール Graph
ms.openlocfilehash: ac59f3408096993379cae490cd555d3b913cc827
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449403"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a>Graph API を使用してアプリをプロアクティブにインストールし、メッセージを送信する

>[!IMPORTANT]
> Microsoft Graph と Microsoft Teams のパブリック プレビューは、早期アクセスとフィードバックに利用できます。 このリリースでは広範なテストが実施されましたが、実稼働環境での使用を意図した製品ではありません。

## <a name="proactive-messaging-in-teams"></a>Teams でのプロアクティブ メッセージング

プロアクティブ メッセージはボットによって開始され、ユーザーとの会話を開始します。 ウェルカム メッセージの送信、アンケートや投票の実施、組織全体の通知のブロードキャストなど、さまざまな目的に役立ちます。 Teams のプロアクティブ メッセージは、アドホックまたは **ダイアログ** ベース **の会話として配信** できます。

|メッセージ型 | 説明 |
|----------------|-------------- |
|アドホックプロアクティブ メッセージ| ボットは、会話フローを中断せずにメッセージを対話します。|
|ダイアログ ベースのプロアクティブ メッセージ | ボットは新しいダイアログ スレッドを作成し、会話を制御し、プロアクティブ メッセージを配信し、閉じ、コントロールを前のダイアログに返します。|

「ユーザー [にプロアクティブ通知を送信する SDK v4」を参照してください](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)。

## <a name="proactive-app-installation-in-teams"></a>Teams でのプロアクティブ アプリのインストール

ボットがユーザーに事前にメッセージを送る前に、個人用アプリまたはユーザーがメンバーであるチームにインストールする必要があります。 アプリをインストールしていない、または以前に操作したユーザーに事前にメッセージを送信する必要がある場合があります。 たとえば、組織内のすべてのユーザーに重要な情報をメッセージする必要があります。 このようなシナリオでは、Microsoft Graph API を使用して、ユーザー向けボットを事前にインストールできます。

## <a name="permissions"></a>アクセス許可

Microsoft Graph [teamsAppInstallation リソース](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) の種類のアクセス許可は、Microsoft Teams プラットフォーム内のすべてのユーザー (個人用) スコープまたはチーム (チャネル) スコープのアプリのインストール ライフサイクルを管理するのに役立ちます。

|アプリケーションのアクセス許可 | 説明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Teams アプリは、事前にサインインまたは使用することなく、ユーザーの読み取り、インストール、アップグレード、アンインストールを行えます。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Teams アプリは、事前サインインや使用を行わずに、任意のチームで自身を読み取り、インストール、アップグレード、アンインストールできます。|

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
>Microsoft Graph は、組織のアプリ カタログ内または AppSource で発行 [された](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) アプリのみを [インストールできます](https://appsource.microsoft.com/)。

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ Teams 用のプロアクティブ メッセージング ボットを作成して発行する

開始するには、組織のアプリ カタログまたは[AppSource](../../bots/how-to/create-a-bot-for-teams.md)で公開されているプロアクティブ[](../../concepts/deploy-and-publish/overview.md)メッセージング機能を備える[](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)Teams 用ボットが[必要です](https://appsource.microsoft.com/)。 [](../../concepts/bots/bot-conversations/bots-conv-proactive.md)

>[!TIP]
> 実稼働対応の [**Company Communicator**](../..//samples/app-templates.md#company-communicator) アプリ テンプレートはブロードキャスト メッセージングを許可し、プロアクティブボット アプリケーションを構築する良い基盤です。

### <a name="-get-the-teamsappid-for-your-app"></a>✔アプリを `teamsAppId` 取得する

**1.** 次の手順 `teamsAppId` が必要です。

組織 `teamsAppId` のアプリ カタログから取得できます。

**Microsoft Graph ページリファレンス:** [teamsApp リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

要求はオブジェクトを返す必要 `teamsApp` があります。 返されるオブジェクトは、アプリのカタログによって生成されるアプリ ID であり、Teams アプリ マニフェストで指定した `id` ID とは異なります。

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

**Microsoft Graph ページリファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** チーム スコープ内のチャネルに対してアプリがアップロードまたはサイドロードされている場合は、次のように `teamsAppId` 取得できます。

**Microsoft Graph ページリファレンス:** [チーム内のアプリを一覧表示する](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> 結果の一覧を絞り込むには [**、teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) オブジェクトのフィールドをフィルター処理できます。

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ メッセージ受信者にボットが現在インストールされているかどうかを確認する

**Microsoft Graph ページリファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

この要求は、アプリがインストールされていない場合は空の配列、アプリがインストールされている場合は [単一の teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) オブジェクトを持つ配列を返します。

### <a name="-install-your-app"></a>✔ アプリをインストールする

**Microsoft Graph ページリファレンス:** [ユーザー用アプリのインストール](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP POST** 要求:

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

ユーザーが Microsoft Teams を実行している場合、アプリのインストールはすぐに表示されます。 インストールされているアプリを表示するには、再起動が必要になる場合があります。

### <a name="-retrieve-the-conversation-chatid"></a>✔ 会話の **chatId を取得する**

アプリがユーザー用にインストールされている場合、ボットは、プロアクティブ メッセージを送信するために必要な情報を含むイベント `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)通知を受信します。

また `chatId` 、次のように取得することもできます。

**Microsoft Graph ページリファレンス:** [チャットの取得](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

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

## <a name="related-topic-for-teams-administrators"></a>Teams 管理者向け関連トピック
>
> [!div class="nextstepaction"]
> [**Microsoft Teams のアプリのセットアップ ポリシーを管理する**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)

## <a name="view-additional-code-samples"></a>その他のコード サンプルを見る
>
> [!div class="nextstepaction"]
> [**Teams のプロアクティブ メッセージング コード サンプル**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
