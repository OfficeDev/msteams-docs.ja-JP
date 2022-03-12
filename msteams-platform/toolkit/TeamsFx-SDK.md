---
title: TeamsFx SDK
author: MuyangAmigo
description: TeamsFx SDK について
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 1e78827d4105eefb112bef40d059804a94050f2d
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453622"
---
# <a name="teamsfx-sdk-for-typescript-or-javascript"></a>TeamsFx SDK for TypeScript または JavaScript

TeamsFx は、ID の実装とクラウド リソースへのアクセスのタスクを、構成がゼロの単一行ステートメントに減らすことを目的とします。

ライブラリを使用して、次のコマンドを実行します。

* 同様の方法でクライアント環境とサーバー環境のコア機能にアクセスします。
* 簡単な方法でユーザー認証コードを記述します。

## <a name="get-started"></a>作業の開始

TeamsFx SDK は、TeamsFx ツールキットまたは CLI を使用してスキャフォールディングされたプロジェクトで事前構成されています。
詳細については、「アプリ プロジェクトTeams[参照してください](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md)。

### <a name="prerequisites"></a>前提条件

* Node.js以降 `10.x.x` のバージョン。
* プロジェクトに関連パッケージが`botbuilder` [](https://github.com/Microsoft/botbuilder-js#packages) `>= 4.9.3`依存関係としてインストールされている場合は、同じバージョンであり、バージョンが . ([問題 - すべての BOTBUILDER パッケージが同じバージョンである必要があります](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548))

詳細については、以下を参照してください。

* [ソース コード](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)
* [パッケージ (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx)
* [API リファレンス ドキュメント](https://aka.ms/teamsfx-sdk-help)
* [サンプル](https://github.com/OfficeDev/TeamsFx-Samples)

### <a name="install-the-microsoftteamsfx-package"></a>パッケージの `@microsoft/teamsfx` インストール

以下を使用して、TeamsFx SDK for TypeScript または JavaScript をインストールします `npm`。

```bash
npm install @microsoft/teamsfx
```

### <a name="create-and-authenticate-microsoftgraphclient"></a>作成と認証 `MicrosoftGraphClient`

Microsoft Graph API にアクセスするためのグラフ クライアント オブジェクトを作成するには、認証する資格情報が必要です。 SDK には、さまざまな要件を満たす資格情報クラスがいくつか用意されています。 資格情報を使用する前に構成を読み込む必要があります。

* ブラウザー環境では、構成パラメーターを明示的に渡す必要があります。 プロジェクトのスキャフォールReact、使用する環境変数が用意されています。

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
```

* Azure Function のような NodeJS 環境では、 を呼び出すだけでできます `loadConfiguration`。 既定では、環境変数から読み込めます。

```ts
loadConfiguration();
```

#### <a name="using-teams-app-user-credential"></a>アプリTeams資格情報の使用

次のスニペットを使用します。

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential = new TeamsUserCredential();
const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
const profile = await graphClient.api("/me").get();
```

> [!NOTE]
> この資格情報クラスは、ブラウザー アプリケーション (Tab App など) でTeams使用できます。

#### <a name="using-microsoft-365-tenant-credential"></a>テナントMicrosoft 365の使用

Microsoft 365資格情報は、アプリ ユーザーと対話するTeams必要とします。 アプリケーションとして Microsoft Graph呼び出しできます。

次のスニペットを使用します。

```ts
loadConfiguration();
const credential = new M365TenantCredential();
const graphClient = createMicrosoftGraphClient(credential);
const profile = await graphClient.api("/users/{object_id_of_another_people}").get();
```

## <a name="core-concepts-and-code-structure"></a>コア概念とコード構造

### <a name="credentials"></a>資格情報

認証を簡素化するために、資格情報フォルダーの下に [3 つの資格情報](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential) クラスがあります。

資格情報クラスは、 `TokenCredential` Azure ライブラリ API で広く使用されるインターフェイスを実装します。 特定のスコープにアクセス トークンを提供するように設計されています。 次の資格情報クラスは、特定のシナリオで異なる ID を表します。

* `TeamsUserCredential`はTeamsユーザーの ID を表します。 この資格情報を使用すると、最初にユーザーの同意が要求されます。
* `M365TenantCredential`は、Microsoft 365 ID を表します。 通常、ユーザーが時間トリガーオートメーション ジョブのように関与していない場合に使用されます。
* `OnBehalfOfUserCredential` は、フローの代理として使用されます。 アクセス トークンが必要で、さまざまなスコープの新しいトークンを取得できます。 Azure 関数またはボットのシナリオで使用するように設計されています。

### <a name="bots"></a>ボット

ボット関連のクラスは、ボット フォルダー [の下に格納されます](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot)。

`TeamsBotSsoPrompt` ボット フレームワークと統合できます。 ボット アプリケーションを開発するための認証プロセスを簡略化します。

### <a name="helper-functions"></a>ヘルパー関数

TeamsFx SDK には、サード パーティ製ライブラリの構成を容易にするヘルパー関数が提供されています。 これらはコア フォルダーの [下にあります](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core)。

### <a name="error-handling"></a>エラー処理

API エラー応答は、 `ErrorWithCode`エラー コードとエラー メッセージを含むエラー応答です。

たとえば、特定のエラーをフィルター処理するには、次のスニペットを使用できます。

```ts
try {
  const credential = new TeamsUserCredential();
  await credential.login("User.Read");
} catch (err: unknown) {
  if (err instanceof ErrorWithCode && err.code !== ErrorCode.ConsentFailed) {
    throw err;
  } else {
    // Silently fail because user cancels the consent dialog
    return;
  }
}
```

また、資格情報インスタンスが Microsoft Graph などの他のライブラリで使用されている場合は、エラーがキャッチされ、変換される可能性があります。

```ts
try {
  const credential = new TeamsUserCredential();
  const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
  const profile = await graphClient.api("/me").get();
} catch (err: unknown) {
  // ErrorWithCode is handled by Graph client
  if (err instanceof GraphError && err.code?.includes(ErrorCode.UiRequiredError)) {
    this.setState({
      showLoginBtn: true,
    });
  }
}
```

## <a name="scenarios"></a>シナリオ

次のセクションでは、一般的なシナリオのいくつかのコード スニペットを示します。

### <a name="use-graph-api-in-tab-app"></a>タブ アプリGraph API を使用する

Use `TeamsUserCredential` and `createMicrosoftGraphClient`.

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential: any = new TeamsUserCredential();
const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

### <a name="call-azure-function-in-tab-app"></a>タブ アプリで Azure 関数を呼び出す

ライブラリを `axios` 使用して Azure 関数に HTTP 要求を行います。

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential: any = new TeamsUserCredential();
const token = credential.getToken(""); // Get SSO token for the user
// Call API hosted in Azure Functions on behalf of user
const apiConfig = getResourceConfiguration(ResourceType.API);
const response = await axios.default.get(apiConfig.endpoint + "api/httptrigger1", {
  headers: {
    authorization: "Bearer " + token,
  },
});
```

### <a name="access-sql-database-in-azure-function"></a>Azure 関数SQLデータベースへのアクセス

ライブラリを`tedious`使用して、認証を管理するSQLに`DefaultTediousConnectionConfiguration`アクセスし、活用します。
別に`tedious`、 の結果に基づいて、他のSQLライブラリの接続構成を作成できます`sqlConnectionConfig.getConfig()`。

```ts
loadConfiguration();
const sqlConnectConfig = new DefaultTediousConnectionConfiguration();
// If there's only one SQL database
const config = await sqlConnectConfig.getConfig();
// If there are multiple SQL databases
const config2 = await sqlConnectConfig.getConfig("your database name");
const connection = new Connection(config);
connection.on("connect", (error) => {
  if (error) {
    console.log(error);
  }
});
```

### <a name="use-certificate-based-authentication-in-azure-function"></a>Azure 関数で証明書ベースの認証を使用する

```ts
loadConfiguration({
  authentication: {
    clientId: process.env.M365_CLIENT_ID,
    certificateContent: "The content of a PEM-encoded public/private key certificate",
    authorityHost: process.env.M365_AUTHORITY_HOST,
    tenantId: process.env.M365_TENANT_ID,
  },
});
```

### <a name="use-graph-api-in-bot-application"></a>ボット アプリケーションGraph API を使用する

ダイアログ セット `TeamsBotSsoPrompt` に追加します。

```ts
const { ConversationState, MemoryStorage } = require("botbuilder");
const { DialogSet, WaterfallDialog } = require("botbuilder-dialogs");
const { TeamsBotSsoPrompt } = require("@microsoft/teamsfx");

const convoState = new ConversationState(new MemoryStorage());
const dialogState = convoState.createProperty("dialogState");
const dialogs = new DialogSet(dialogState);

loadConfiguration();
dialogs.add(
  new TeamsBotSsoPrompt("TeamsBotSsoPrompt", {
    scopes: ["User.Read"],
  })
);

dialogs.add(
  new WaterfallDialog("taskNeedingLogin", [
    async (step) => {
      return await step.beginDialog("TeamsBotSsoPrompt");
    },
    async (step) => {
      const token = step.result;
      if (token) {
        // ... continue with task needing access token ...
      } else {
        await step.context.sendActivity(`Sorry... We couldn't log you in. Try again later.`);
        return await step.endDialog();
      }
    },
  ])
);
```

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="configure-log"></a>ログの構成

このライブラリを使用する場合は、顧客ログ レベルを設定し、出力をリダイレクトできます。 ログは既定でオフになっています。ログ レベルを設定することで有効にできます。

#### <a name="enable-log-by-setting-log-level"></a>ログ レベルを設定してログを有効にする

ログは、ログ レベルを設定した場合にのみ有効になります。 既定では、ログ情報をコンソールに出力します。

次のスニペットを使用してログ レベルを設定します。

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

カスタム ロガーまたはログ関数を設定すると、ログ出力をリダイレクトできます。

##### <a name="redirect-by-setting-custom-logger"></a>カスタム ロガーを設定してリダイレクトする

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

##### <a name="redirect-by-setting-custom-log-function"></a>カスタム ログ関数を設定してリダイレクトする

> [!NOTE]
> カスタム ロガーを設定した場合、ログ関数は有効ではありません。

```ts
setLogLevel(LogLevel.Info);
// Only log error message to Application Insights in bot application.
setLogFunction((level: LogLevel, message: string) => {
  if (level === LogLevel.Error) {
    this.telemetryClient.trackTrace({
      message: message,
      severityLevel: Severity.Error,
    });
  }
});
```

## <a name="see-also"></a>関連項目

[Microsoft TeamsFx サンプル ギャラリー](https://github.com/OfficeDev/TeamsFx-Samples)
