---
title: Microsoft Graphを使用して、Teamsでのプロアクティブなボットのインストールとメッセージングを承認する
description: Teamsでのプロアクティブなメッセージングと実装方法について説明します。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: チームのプロアクティブなメッセージング チャット のインストール Graph
ms.openlocfilehash: 06b50e5ab8594c257959430383bab5e355af4e06
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566153"
---
# <a name="proactive-installation-of-apps-using-graph-api-and-send-messages"></a>Graph API を使用したアプリの事前インストールとメッセージの送信

>[!IMPORTANT]
> Microsoft GraphおよびMicrosoft Teamsパブリック プレビューは、早期アクセスとフィードバックに利用できます。 このリリースでは、広範囲にわたるテストを実施していますが、運用環境での使用を目的としたものではありません。

## <a name="proactive-messaging-in-teams"></a>Teamsでのプロアクティブなメッセージング

プロアクティブ メッセージは、ユーザーとの会話を開始するためにボットによって開始されます。 歓迎メッセージの送信、アンケートやアンケートの実施、組織全体の通知のブロードキャストなど、さまざまな目的に対応しています。 Teams内のプロアクティブ メッセージは、**アドホック** またはダイアログ **ベースの** 会話として配信できます。

|メッセージ型 | 説明 |
|----------------|-------------- |
|アドホック プロアクティブ メッセージ| ボットは、会話フローを中断せずにメッセージを挿入します。|
|ダイアログ ベースのプロアクティブ メッセージ | ボットは新しいダイアログ スレッドを作成し、会話を制御し、プロアクティブ メッセージを配信し、閉じて、コントロールを前のダイアログに戻します。|

## <a name="proactive-app-installation-in-teams"></a>Teamsでのプロアクティブなアプリのインストール

ボットがユーザーに事前にメッセージを送信するには、そのボットを個人用アプリとしてインストールするか、ユーザーがメンバーであるチームにインストールする必要があります。 アプリをインストールしていない、または以前にアプリと対話していないユーザーに、事前にメッセージを送信する必要がある場合があります。 たとえば、組織の全員に重要な情報を送信する必要があります。 このようなシナリオでは、Microsoft Graph API を使用して、ユーザー用にボットを事前にインストールできます。

## <a name="permissions"></a>アクセス許可

Microsoft Graph [teamsAppApp リソースの種類](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true)のアクセス許可は、Microsoft Teams プラットフォーム内のすべてのユーザー (個人用) またはチーム (チャネル) スコープのアプリのインストール ライフサイクルを管理するのに役立ちます。

|アプリケーションのアクセス許可 | 説明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Teamsアプリは、事前のサインインや使用を行わずに、任意の **ユーザー** のを読み取り、インストール、アップグレード、およびアンインストールできます。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|Teamsアプリは、事前のサインインや使用を行わずに、どの **チーム** でも読み取り、インストール、アップグレード、およびアンインストールを行うことができます。|

これらのアクセス許可を使用するには、次の値を持つ [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加する必要があります。
> [!div class="checklist"]
> [!div class="checklist"]
>
> * **id** — Azure AD アプリ ID。
> * **リソース** — アプリのリソース URL。
>
>[!NOTE]
>
> * インストールは他のユーザー用であるため、ボットにはアプリケーションが必要であり、ユーザーが委任したアクセス許可は必要ありません。
>
> * Azure AD テナント管理者は [、アプリケーションにアクセス許可を明示的に付与する](/graph/security-authorization#grant-permissions-to-an-application)必要があります。 アプリケーションにアクセス許可が付与されると、Azure AD テナントのすべてのメンバーが付与されたアクセス許可を取得します。

## <a name="enable-proactive-app-installation-and-messaging"></a>アプリの事前インストールとメッセージングを有効にする

> [!IMPORTANT]
>Microsoft Graphは、組織のアプリ ストアまたはTeams ストアに公開されているアプリのみをインストールできます。

### <a name="-create-and-publish-your-proactive-messaging-bot-for-teams"></a>✔ Teams用のプロアクティブなメッセージング ボットを作成して公開する

開始するには、[組織のアプリ ストア](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org)または[Teams](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)ストアにある[プロアクティブなメッセージング](../../concepts/bots/bot-conversations/bots-conv-proactive.md)機能を備えた[Teams用のボット](../../bots/how-to/create-a-bot-for-teams.md)が必要です。

>[!TIP]
> 運用準備が整 [**った会社Communicator**](../..//samples/app-templates.md#company-communicator)アプリ テンプレートは、ブロードキャスト メッセージングを可能にし、プロアクティブなボット アプリケーションを構築するための優れた基盤です。

### <a name="-get-the-teamsappid-for-your-app"></a>✔ `teamsAppId` アプリ用の を入手する

**1.** 次の `teamsAppId` ステップに必要です。

`teamsAppId`は、組織のアプリ カタログから取得できます。

**マイクロソフト Graph ページリファレンス:** [チームアプリ リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
```

要求はオブジェクトを返す必要があります `teamsApp` 。 返されるオブジェクト `id` は、アプリのカタログ生成アプリ ID であり、Teams アプリ マニフェストで指定した ID とは異なります。

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

**2.**  アプリが既にアップロードされている場合、またはユーザーのサイドロードがパーソナルスコープにある場合は、次のようにして取得できます `teamsAppId` 。

**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

**3.** チーム スコープ内のチャネルに対してアプリがアップロードまたはサイドロードされている場合は、次のようにして取得できます `teamsAppId` 。

**マイクロソフト Graph ページ リファレンス:** [チーム内のアプリを一覧表示する](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
```

>[!TIP]
> 結果のリストを絞り込むには、 [**チームの任意**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) のフィールドにフィルターを適用できます。

### <a name="-determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>✔ メッセージ受信者に対してボットが現在インストールされているかどうかを確認する

**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

アプリがインストールされていない場合は空の配列を返し、アプリがインストールされている場合は 1 つの [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) オブジェクトを持つ配列を返します。

### <a name="-install-your-app"></a>✔ アプリをインストールする

**マイクロソフト Graph ページ リファレンス:** [ユーザー用のアプリのインストール](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP POST** 要求:

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

ユーザーが実行Microsoft Teams場合、アプリのインストールはすぐに表示されます。 インストールされているアプリを表示するには、再起動が必要な場合があります。

### <a name="-retrieve-the-conversation-chatid"></a>✔ 会話チャット ID を取得 **します**

ユーザーにアプリがインストールされると、 `conversationUpdate` ボットは、プロアクティブ メッセージを送信するために必要な情報を含む [イベント通知](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) を受け取ります。

また `chatId` 、次のように取得することもできます。

**マイクロソフト Graph ページ リファレンス:** [チャットを取得する](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

**1.** アプリが必要です `{teamsAppInstallationId}` 。 このファイルがない場合は、次の手順を実行します。

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

応答の **id** プロパティ `teamsAppInstallationId` は.

**2.** 次の要求を行って `chatId` 、 を取得します。

**HTTP GET** 要求 (アクセス許可 — `TeamsAppInstallation.ReadWriteSelfForUser.All` ):  

```http
GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
```

応答の **id** プロパティ `chatId` は.

`chatId`次の要求を使用して を取得することもできますが、より広範な `Chat.Read.All` アクセス許可が必要です。

**HTTP GET** 要求 (アクセス許可 — `Chat.Read.All` ):

```http
GET https://graph.microsoft.com/beta/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
```

### <a name="-send-proactive-messages"></a>✔ プロアクティブ メッセージを送信する

ボットがユーザーまたはチームに追加され、すべてのユーザー情報を受信した後、ボットは [プロアクティブ メッセージを送信](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) できます。

## <a name="see-also"></a>関連項目

* [**Microsoft Teams のアプリのセットアップ ポリシーを管理する**](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [ユーザーに事前通知を送信 SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)

## <a name="view-additional-code-samples"></a>その他のコード サンプルを見る
>
> [!div class="nextstepaction"]
> [**Teams のプロアクティブ メッセージング コード サンプル**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)