---
title: Microsoft Graphを使用して、アクティブボットのインストールとメッセージングを承認Teams
description: プロアクティブ メッセージングについて、Teams実装する方法について説明します。 コード サンプルを使用してプロアクティブ アプリのインストールとメッセージングを有効にする方法について説明します。
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: Teams プロアクティブ メッセージング チャットのインストール Graph
ms.openlocfilehash: a52d36150ee384841cde73e9a00510cabc31f144
ms.sourcegitcommit: 58fe8a87b988850ae6219c55062ac34cd8bdbf66
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2021
ms.locfileid: "60949580"
---
# <a name="proactive-installation-of-apps-using-graph-api-to-send-messages"></a>Graph API を使用してメッセージを送信するアプリの事前インストール

>[!IMPORTANT]
> Microsoft GraphおよびMicrosoft Teamsパブリック プレビューは、早期アクセスとフィードバックのために利用できます。 このリリースでは広範なテストが実施されましたが、実稼働環境での使用を意図した製品ではありません。

## <a name="proactive-messaging-in-teams"></a>プロアクティブ メッセージング (Teams

プロアクティブ メッセージはボットによって開始され、ユーザーとの会話を開始します。 ウェルカム メッセージの送信、アンケートや投票の実施、組織全体の通知のブロードキャストなど、さまざまな目的に役立ちます。 インプロアクティブ メッセージTeams、アドホックまたはダイアログ ベース **の会話として配信** できます。

|メッセージの種類 | [説明] |
|----------------|-------------- |
|アドホックプロアクティブ メッセージ| ボットは、会話フローを中断せずにメッセージを対話します。|
|ダイアログ ベースのプロアクティブ メッセージ | ボットは新しいダイアログ スレッドを作成し、会話を制御し、プロアクティブ メッセージを配信し、閉じ、コントロールを前のダイアログに返します。|

## <a name="proactive-app-installation-in-teams"></a>アプリのプロアクティブ インストールTeams

ボットがユーザーに事前にメッセージを送る前に、個人用アプリまたはユーザーがメンバーであるチームにインストールする必要があります。 アプリをインストールしていない、または以前に操作したユーザーに事前にメッセージを送信する必要がある場合があります。 たとえば、組織内のすべてのユーザーに重要な情報をメッセージする必要があります。 このようなシナリオでは、Microsoft Graph API を使用して、ユーザー向けボットを事前にインストールできます。

## <a name="permissions"></a>アクセス許可

Microsoft Graph [teamsAppInstallation](/graph/api/resources/teamsappinstallation?view=graph-rest-1.0&preserve-view=true)リソースの種類のアクセス許可は、Microsoft Teams プラットフォーム内のすべてのユーザー (個人用) スコープまたはチーム (チャネル) スコープのアプリのインストール ライフサイクルを管理するのに役立ちます。

|アプリケーションのアクセス許可 | [説明]|
|------------------|---------------------|
|`TeamsAppInstallation.ReadWriteSelfForUser.All`|事前サインインTeams使用せずに、アプリがユーザーの読み取り、インストール、アップグレード、アンインストールを行えます。|
|`TeamsAppInstallation.ReadWriteSelfForTeam.All`|事前サインインTeams使用せずに、アプリが任意のチームで自身を読み取り、インストール、アップグレード、アンインストールできます。|

これらのアクセス許可を使用するには、次の値で [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) キーをアプリ マニフェストに追加する必要があります。

* **id**: アプリ id Azure Active Directory (AAD) アプリ ID。
* **resource**: アプリのリソース URL。

> [!NOTE]
>
> * インストールは他のユーザー向けなので、ボットにはアプリケーションが必要であり、ユーザーが委任したアクセス許可は必要ではありません。
>
> * テナントAADは、アプリケーション[に明示的にアクセス許可を付与する必要があります](/graph/security-authorization#grant-permissions-to-an-application)。 アプリケーションにアクセス許可が付与された後、テナントのすべてのAADアクセス許可を取得します。

## <a name="enable-proactive-app-installation-and-messaging"></a>プロアクティブ アプリのインストールとメッセージングを有効にする

> [!IMPORTANT]
> Microsoft Graphは、組織のアプリ ストアまたは組織のアプリ ストアに発行されたアプリTeamsできます。

### <a name="create-and-publish-your-proactive-messaging-bot-for-teams"></a>ユーザー向けプロアクティブ メッセージング ボットを作成してTeams

開始するには、組織のアプリ ストア[または](../../bots/how-to/create-a-bot-for-teams.md)Teams ストアにある[](../../concepts/bots/bot-conversations/bots-conv-proactive.md)プロアクティブ メッセージング機能を備えるボット[](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-your-org)がTeams[必要です](../../concepts/deploy-and-publish/apps-publish-overview.md#publish-your-app-to-the-teams-store)。

> [!TIP]
> 実稼働対応の [*Company Communicator*](../..//samples/app-templates.md#company-communicator)アプリ テンプレートを使用すると、ブロードキャスト メッセージングが許可され、プロアクティブボット アプリケーションを構築できます。

### <a name="get-the-teamsappid-for-your-app"></a>アプリの `teamsAppId` 取得

次の方法 `teamsAppId` で取得できます。

* 組織のアプリ カタログから:

    **Microsoft Graph ページリファレンス:** [teamsApp リソースの種類](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true)

    **HTTP GET** 要求:

    ```http
    GET https://graph.microsoft.com/v1.0/appCatalogs/teamsApps?$filter=externalId eq '{IdFromManifest}'
    ```

    要求は、アプリのカタログ生成アプリ ID であるオブジェクト `teamsApp` `id` を返す必要があります。 これは、アプリ マニフェストで指定した ID とはTeamsです。

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

    **Microsoft Graph ページ リファレンス:** [チーム内のアプリの一覧](/graph/api/team-list-installedapps?view=graph-rest-v1.0&tabs=http&preserve-view=true)

    **HTTP GET** 要求:

    ```http
    GET https://graph.microsoft.com/v1.0/teams/{team-id}/installedApps?$expand=teamsApp&$filter=teamsApp/externalId eq '{IdFromManifest}'
    ```

    > [!TIP]
    > 結果の一覧を絞り込むには [**、teamsApp**](/graph/api/resources/teamsapp?view=graph-rest-1.0&preserve-view=true) オブジェクトのフィールドをフィルター処理できます。

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

アプリがユーザー用にインストールされている場合、ボットは、プロアクティブ メッセージを送信するために必要な情報を含むイベント `conversationUpdate` [](../../resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)通知を受信します。

**Microsoft Graph ページ リファレンス:** [チャットの取得](/graph/api/chat-get?view=graph-rest-beta&tabs=http&preserve-view=true)

1. アプリが必要です `{teamsAppInstallationId}` 。 持ってない場合は、次のコマンドを使用します。

    **HTTP GET** 要求:

    ```http
    GET https://graph.microsoft.com/beta/users/{user-id}/teamwork/installedApps?$expand=teamsApp&$filter=teamsApp/id eq '{teamsAppId}'
    ```

    応答 **の id** プロパティは、 `teamsAppInstallationId` です。

1. フェッチする次の要求を行います `chatId` 。

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

### <a name="send-proactive-messages"></a>プロアクティブ メッセージを送信する

ボットは、 [ユーザーまたはチーム](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) に対してボットが追加され、すべてのユーザー情報を受信した後に、プロアクティブ メッセージを送信できます。

## <a name="code-sample"></a>コード サンプル

| **サンプル名** | **説明** | **.NET** | **Node.js** |
|---------------|--------------|--------|-------------|
| アプリのプロアクティブ インストールとプロアクティブ通知の送信 | このサンプルでは、ユーザーに対してアプリのプロアクティブ インストールを使用し、Microsoft の API を呼び出してプロアクティブ通知Graph示します。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) |

## <a name="additional-code-samples"></a>追加のコード サンプル
>
> [!div class="nextstepaction"]
> [**Teams のプロアクティブ メッセージング コード サンプル**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)

## <a name="see-also"></a>関連項目

* [Microsoft Teams のアプリのセットアップ ポリシーを管理する](/MicrosoftTeams/teams-app-setup-policies#create-a-custom-app-setup-policy)
* [ユーザーにプロアクティブ通知を送信する SDK v4](/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true)
