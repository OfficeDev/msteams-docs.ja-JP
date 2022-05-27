---
title: Microsoft Graph を使用して、Teams でのプロアクティブなボットのインストールとメッセージングを承認する
description: Teams でのプロアクティブ メッセージングとその実装方法について説明します。 コード サンプルを使用してプロアクティブなアプリのインストールとメッセージングを有効にする方法について説明します。
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: teams プロアクティブ メッセージング チャットのインストール Graph
ms.openlocfilehash: 7a133b91aabe920b109b644331bc6526cd950858
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757704"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>Graph API を使用してメッセージを送信するアプリの事前インストール

## <a name="proactive-messaging-in-teams"></a>Teams でのプロアクティブ メッセージング

プロアクティブ メッセージは、ユーザーとの会話を開始するためにボットによって開始されます。 ウェルカム メッセージの送信、アンケートや投票の実施、組織全体の通知のブロードキャストなど、さまざまな目的に対応しています。 Teams のプロアクティブ メッセージは、**アドホック** または **ダイアログ ベース** の会話として配信できます。

|メッセージの種類 | 説明 |
|----------------|-------------- |
|アドホック プロアクティブ メッセージ| ボットは、会話フローを中断することなくメッセージを挿入します。|
|ダイアログ ベースのプロアクティブ メッセージ | ボットは新しいダイアログ スレッドを作成し、会話を制御し、プロアクティブ メッセージを配信し、閉じて、前のダイアログに制御を返します。|

## <a name="proactive-app-installation-in-teams"></a>Teams でのプロアクティブ アプリのインストール

ボットがユーザーに事前にメッセージを送信するには、個人用アプリとして、またはユーザーがメンバーであるチームにインストールする必要があります。 場合によっては、アプリをインストールしていないユーザーや以前に操作したユーザーに対してプロアクティブにメッセージを送信する必要があります。 たとえば、組織内のすべてのユーザーに重要な情報をメッセージで送信する必要がある場合は、Microsoft Graph APIを使用して、ユーザーのボットをプロアクティブにインストールできます。

## <a name="permissions"></a>アクセス許可

Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) リソースの種類のアクセス許可は、Microsoft Teams プラットフォーム内のすべてのユーザー (個人) またはチーム (チャネル) スコープに対するアプリのインストール ライフサイクルを管理するのに役立ちます。

|アプリケーションのアクセス許可 | 説明|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|Teams アプリは、事前のサインインや使用なしで、任意の *ユーザー* の読み取り、インストール、アップグレード、アンインストールを行うことができます。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|ユーザーがサインインしていない状態で、任意の *チーム* に対して Teams アプリが自分自身を読み取り、インストール、アップグレード、アンインストールすることを許可します。|

これらのアクセス許可を使用するには、次の値を使用して [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加する必要があります。

* **ID**: Azure Active Directory アプリ ID。
* **リソース**: アプリのリソース URL。

> [!NOTE]
>
> * インストールは他のユーザー向けであるため、ボットにはアプリケーションが必要であり、ユーザーが委任したアクセス許可は必要ありません。
>
> * Azure AD テナント管理者は、[アプリケーションに対して明示的に承認を与える](/graph/security-authorization#grant-permissions-to-an-application)必要があります。 アプリケーションにアクセス許可が付与されると、Azure AD テナントのすべてのメンバーに付与されたアクセス許可が付与されます。

## <a name="enable-proactive-app-installation-and-messaging"></a>プロアクティブなボットをインストールしてメッセージングを有効にする

> [!IMPORTANT]
> Microsoft Graph は、組織のアプリ ストアまたは Teams ストアに発行されたアプリのみをインストールできます。

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a>Teams 用のプロアクティブ メッセージング ボットを作成して発行する

開始するには、[組織のアプリ ストア](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org)または [Teams ストア](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)にある[プロアクティブ メッセージング](../../concepts/bots/bot-conversations/bots-conv-proactive.md)機能を備えた [Teams のボット](../../bots/how-to/create-a-bot-for-teams.md) が必要です。

> [!TIP]
> 運用環境対応の [*Company Communicator*](../..//samples/app-templates.md#company-communicator) アプリ テンプレートは、ブロードキャスト メッセージングを許可し、プロアクティブなボット アプリケーションを構築するための優れたスタートです。

### <a name="get-the-teamsappid-for-your-app"></a>アプリの `teamsAppId` を入手する

`teamsAppId` は次の方法で取得できます。

* 組織のアプリ カタログから:

    **Microsoft Graph ページ リファレンス:** [teamsApp リソース タイプ](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

    **HTTP GET** リクエスト:

    ```http
    GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    リクエストは、アプリのカタログで生成されたアプリ ID である `teamsApp` オブジェクト `id` を返す必要があります。 これは、Teams アプリ マニフェストで指定した ID とは異なります。

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

* 個人用スコープ内のユーザーに対してアプリが既にアップロードまたはサイドロードされている場合:

    **Microsoft Graph ページ リファレンス:** [ユーザーにインストールされているアプリを一覧表示する](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **HTTP GET** リクエスト:

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* チーム スコープ内のチャネルに対してアプリが既にアップロードまたはサイドロードされている場合:

    **Microsoft Graph ページ リファレンス:** [チーム内のアプリを一覧表示する](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **HTTP GET** リクエスト:

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > 結果の一覧を絞り込むには、 [**teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) オブジェクトの任意のフィールドをフィルター処理できます。

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>メッセージ受信者に対してボットが現在インストールされているかどうかを確認する

メッセージ受信者に対してボットが現在インストールされているかどうかを確認するには、次のようにします。

**Microsoft Graph ページ リファレンス:** [ユーザーにインストールされているアプリを一覧表示する](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** リクエスト:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

要求は次を返します。

* アプリがインストールされていない場合は空の配列。
* アプリがインストールされている場合は、単一 の [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) オブジェクトを持つ配列。

### <a name="install-your-app"></a>サイトにアプリ パーツをインストールします。

アプリは次のようにインストールできます。

**Microsoft Graph ページ リファレンス:** [ユーザー向けのアプリのインストール](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP POST** リクエスト

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

ユーザーが Microsoft Teams を実行している場合は、アプリのインストールが直ちに行われます。 インストールされているアプリを表示するには、再起動が必要になる場合があります。

### <a name="retrieve-the-conversation-chatid"></a>会話 `chatId` を取得する

ユーザー向けにアプリがインストールされると、ボットはプロアクティブ メッセージを送信するために必要な情報を含む`conversationUpdate` [イベント通知](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)を受信します。

**Microsoft Graph ページ リファレンス:** [チャットの取得](/graph/api/chat-get?view=graph-rest-v1.0&tabs=http&preserve-view=true)

1. アプリの `{teamsAppInstallationId}` が必要です。 お持ちでない場合は、次を使用します。

    **HTTP GET** リクエスト:

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    応答の **id** プロパティは `teamsAppInstallationId` です。

1. 次の要求を行って、`chatId` をフェッチします。

    **HTTP GET** 要求 (アクセス許可—`TeamsAppInstallation.ReadWriteSelfForUser.All`):  

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    応答の **id** プロパティは `chatId` です。

    次のリクエストで `chatId` を取得することもできますが、より広範な `Chat.Read.All` 権限が必要です。

    **HTTP GET** 要求 (アクセス許可—`Chat.Read.All`):

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a>プロアクティブ メッセージを送信する

ボットは、ユーザーまたはチームに対してボットが追加され、すべてのユーザー情報を受信した後に [プロアクティブ メッセージを送信](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) できます。

## <a name="code-snippets"></a>コード スニペット

次のコードは、プロアクティブ メッセージを送信する例を示しています。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public async Task<int> SendNotificationToAllUsersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
   int msgSentCount = 0;

   // Send notification to all the members
   foreach (var conversationReference in _conversationReferences.Values)
   {
       await turnContext.Adapter.ContinueConversationAsync(_configuration["MicrosoftAppId"], conversationReference, BotCallback, cancellationToken);
       msgSentCount++;
   }

   return msgSentCount;
}

private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
{
   await turnContext.SendActivityAsync("Proactive hello.");
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript
server.get('/api/notify', async (req, res) => {
    for (const conversationReference of Object.values(conversationReferences)) {
        await adapter.continueConversationAsync(process.env.MicrosoftAppId, conversationReference, async context => {
            await context.sendActivity('proactive hello');
        });
    }

    res.setHeader('Content-Type', 'text/html');
    res.writeHead(200);
    res.write('<html><body><h1>Proactive messages have been sent.</h1></body></html>');
    res.end();
});
```

---

## <a name="code-sample"></a>コード サンプル

| **サンプルの名前** | **説明** | **.NET** | **Node.js** |
|---------------|--------------|--------|-------------|
| アプリのプロアクティブ インストールとプロアクティブ通知の送信 | このサンプルは、ユーザー向けのアプリのプロアクティブなインストールを使用し、Microsoft Graph API を呼び出してプロアクティブな通知を送信する方法を示しています。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="additional-code-samples"></a>追加のコード サンプル
>
> [!div class="nextstepaction"]
> [**Teams のプロアクティブ メッセージング コード サンプル**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)

## <a name="see-also"></a>関連項目

* [Microsoft Teams のアプリのセットアップ ポリシーを管理する](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [ユーザー SDK v4 にプロアクティブ通知を送信する](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)
