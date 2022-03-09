---
title: Microsoft Graphを使用して、アクティブボットのインストールとメッセージングを承認Teams
description: プロアクティブ メッセージングについて、Teams実装する方法について説明します。 コード サンプルを使用してプロアクティブ アプリのインストールとメッセージングを有効にする方法について説明します。
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: Teams プロアクティブ メッセージング チャットのインストールGraph
ms.openlocfilehash: 11fb1188cc88c983b1ee958b1df264346af22693
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2022
ms.locfileid: "63398702"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>Graph API を使用してメッセージを送信するアプリの事前インストール

## <a name="proactive-messaging-in-teams"></a>プロアクティブ メッセージング (Teams

プロアクティブ メッセージはボットによって開始され、ユーザーとの会話を開始します。 ウェルカム メッセージの送信、アンケートや投票の実施、組織全体の通知のブロードキャストなど、さまざまな目的に役立ちます。 インプロアクティブ メッセージTeams、アドホックまたはダイアログ ベースの **会話として配信** できます。

|メッセージの種類 | 内容 |
|----------------|-------------- |
|アドホックプロアクティブ メッセージ| ボットは、会話フローを中断せずにメッセージを対話します。|
|ダイアログ ベースのプロアクティブ メッセージ | ボットは新しいダイアログ スレッドを作成し、会話を制御し、プロアクティブ メッセージを配信し、閉じ、コントロールを前のダイアログに返します。|

## <a name="proactive-app-installation-in-teams"></a>アプリのプロアクティブ インストールTeams

ボットがユーザーに事前にメッセージを送る前に、個人用アプリまたはユーザーがメンバーであるチームにインストールする必要があります。 アプリをインストールしていない、または以前に操作したユーザーに事前にメッセージを送信する必要がある場合があります。 たとえば、組織内のすべてのユーザーに重要な情報をメッセージする必要があります。 このようなシナリオでは、Microsoft Graph API を使用して、ユーザー向けボットを事前にインストールできます。

## <a name="permissions"></a>アクセス許可

Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true) リソースの種類のアクセス許可は、Microsoft Teams プラットフォーム内のすべてのユーザー (個人用) スコープまたはチーム (チャネル) スコープのアプリのインストール ライフサイクルを管理するのに役立ちます。

|アプリケーションのアクセス許可 | 内容|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|事前サインインTeams使用せずに、ユーザーが任意のユーザーに対してアプリを読み取り、インストール、アップグレード、アンインストールできます。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|事前サインインTeams使用せずに、アプリが任意のチームで自身を読み取り、インストール、アップグレード、アンインストールできます。|

これらのアクセス許可を使用するには、次の値で [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加する必要があります。

* **id**: アプリ ID Azure Active Directory ID。
* **resource**: アプリのリソース URL。

> [!NOTE]
>
> * インストールは他のユーザー向けなので、ボットにはアプリケーションが必要であり、ユーザーが委任したアクセス許可は必要ではありません。
>
> * テナントAzure ADは、アプリケーション[に明示的にアクセス許可を付与する必要があります](/graph/security-authorization#grant-permissions-to-an-application)。 アプリケーションにアクセス許可が付与された後、テナントのすべてのAzure ADアクセス許可を取得します。

## <a name="enable-proactive-app-installation-and-messaging"></a>プロアクティブ アプリのインストールとメッセージングを有効にする

> [!IMPORTANT]
> Microsoft Graphは、組織のアプリ ストアまたはサイト ストアに発行されたアプリTeamsできます。

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a>ユーザー向けプロアクティブ メッセージング ボットを作成してTeams

開始するには、組織のアプリ ストア[または](../../bots/how-to/create-a-bot-for-teams.md) Teams ストアにあるプロアクティブ メッセージング[](../../concepts/bots/bot-conversations/bots-conv-proactive.md)機能を備えるボットがTeams[があります](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)。[](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org)

> [!TIP]
> 実稼働対応 [*の Company Communicator*](../..//samples/app-templates.md#company-communicator) テンプレートを使用すると、ブロードキャスト メッセージングが許可され、プロアクティブボット アプリケーションを構築できます。

### <a name="get-the-teamsappid-for-your-app"></a>アプリの `teamsAppId` 取得

次の方法で `teamsAppId` 取得できます。

* 組織のアプリ カタログから:

    **Microsoft Graphページ参照:** [teamsApp リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

    **HTTP GET** 要求:

    ```http
    GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    要求は、アプリのカタログ `teamsApp` 生成 `id`アプリ ID であるオブジェクトを返す必要があります。 これは、アプリ マニフェストで指定した ID とはTeamsです。

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

    **Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **HTTP GET** 要求:

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

* チーム スコープ内のチャネルに対してアプリが既にアップロードまたはサイドロードされている場合:

    **Microsoft Graph ページ リファレンス:** [チーム内のアプリを一覧表示する](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **HTTP GET** 要求:

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > 結果の一覧を絞り込むには、teamsApp オブジェクトのフィールドを [**フィルター処理**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) できます。

### <a name="determine-whether-your-bot-is-currently-installed-for-a-message-recipient"></a>メッセージ受信者にボットが現在インストールされているかどうかを確認する

メッセージ受信者に対してボットが現在インストールされているかどうかを確認するには、次のようにします。

**Microsoft Graph ページ リファレンス:** [ユーザー用にインストールされているアプリの一覧](/graph/api/userteamwork-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP GET** 要求:

```http
GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
```

要求は次の値を返します。

* アプリがインストールされていない場合は空の配列。
* アプリがインストールされている場合 [、単一の teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-v1.0&preserve-view=true) オブジェクトを持つ配列。

### <a name="install-your-app"></a>アプリをインストールする

アプリは次のようにインストールできます。

**Microsoft Graph ページ リファレンス:** [ユーザー用アプリのインストール](/graph/api/userteamwork-post-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

**HTTP POST** 要求:

```http
POST https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps
Content-Type: application/json

{
   "teamsApp@odata.bind" : "https://graph.microsoft.com/v1.0/appCatalogs/teamsApps/{teamsAppId}"
}
```

ユーザーが実行中のMicrosoft Teams、アプリのインストールが直ちに行われます。 インストールされているアプリを表示するには、再起動が必要になる場合があります。

### <a name="retrieve-the-conversation-chatid"></a>会話を取得する `chatId`

アプリがユーザー用にインストールされている場合`conversationUpdate`、ボットは、プロアクティブ メッセージを送信するために必要な情報を含むイベント通知を受信します。[](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)

**Microsoft Graph ページ リファレンス:** [チャットの取得](/graph/api/chat-get?view=graph-rest-v1.0&tabs=http&preserve-view=true)

1. アプリが必要です `{teamsAppInstallationId}`。 持ってない場合は、次のコマンドを使用します。

    **HTTP GET** 要求:

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    応答 **の id** プロパティは、 `teamsAppInstallationId`です。

1. フェッチする次の要求を行います `chatId`。

    **HTTP GET 要求** (アクセス許可 — `TeamsAppInstallation.ReadWriteSelfForUser.All`):  

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/teamwork/installedApps/{teamsAppInstallationId}/chat
    ```

    応答 **の id** プロパティは、 `chatId`です。

    次の要求を使用して `chatId` 取得できますが、より広範なアクセス許可が必要 `Chat.Read.All` です。

    **HTTP GET 要求** (アクセス許可 — `Chat.Read.All`):

    ```http
    GET https://graph.microsoft.com/v1.0/users/{user-id}/chats?$filter=installedApps/any(a:a/teamsApp/id eq '{teamsAppId}')
    ```

### <a name="send-proactive-messages"></a>プロアクティブ メッセージを送信する

ボットは、 [ユーザーまたはチーム](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) に対してボットが追加され、すべてのユーザー情報を受信した後に、プロアクティブ メッセージを送信できます。

## <a name="code-snippets"></a>コード スニペット

次のコードは、プロアクティブ メッセージの送信例を示しています。

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
* [ユーザーにプロアクティブ通知を送信する SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)
