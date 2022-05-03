---
title: TeamsFx SDK
author: MuyangAmigo
description: TeamsFx SDK について
ms.author: nintan
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d54c3d962ecc9d1fd703bd4126d71564f8358794
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111221"
---
# <a name="teamsfx-sdk"></a>TeamsFx SDK

TeamsFx は、Teams SSO を活用し、構成がゼロの 1 行のステートメントにクラウド リソースにアクセスすることで、開発者タスクを削減するのに役立ちます。 TeamsFx SDK は、ブラウザーと Node.js 環境で使用するように構築されています。一般的なシナリオは次のとおりです。

* Microsoft Teams のタブによる Web アプリケーション
* Azure 関数
* Teams ボット。

TeamsFx SDK を使用すると、次のことができます。

* クライアント環境とサーバー環境のコア機能にアクセスする 
* 簡略化された方法でユーザー認証コードを記述する

## <a name="prerequisites"></a>前提条件

次のツールをインストールし、開発環境を設定します。

* Node.js の最新バージョン
* プロジェクトに依存関係として `botbuilder` 関連の [パッケージ](https://github.com/Microsoft/botbuilder-js#packages) がインストールされている場合は、それらが同じバージョンであることを確認してください。 現在、必要なバージョンは 4.15.0 以降です。詳細については、「 [ボット ビルダー パッケージは同じバージョンである必要があります](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548)」を参照してください。

次に関する実用的な知識が必要です。

* [ソース コード](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)
* [パッケージ (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx)
* [API リファレンス ドキュメント](https://aka.ms/teamsfx-sdk-help)
* [サンプル](https://github.com/OfficeDev/TeamsFx-Samples)

## <a name="get-started"></a>概要

TeamsFx SDK は、TeamsFx ツールキットまたは CLI を使用してスキャフォールディングされたプロジェクトで事前構成されています。
詳細については、「[Teams アプリのアイコンの作成に関するガイダンス](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md)」を参照してください。

### <a name="install-the-microsoftteamsfx-package"></a>`@microsoft/teamsfx` パッケージをインストールします。

`npm` を使用して TeamsFx SDK for TypeScript または JavaScript をインストールします。

```bash
npm install @microsoft/teamsfx
```

### <a name="create-microsoftgraphclient-service"></a>`MicrosoftGraphClient` サービスを作成する

グラフ クライアント オブジェクトを作成し、Microsoft Graph API にアクセスするには、認証用の資格情報が必要です。 SDK には、開発者向けに構成するための API が用意されています。

<br>

<details>
<summary><b>Teams ユーザー (ユーザー ID) に代わって Graph API を呼び出す</b></summary>

次のスニペットを使用します。

```ts
// Equivalent to:
// const teamsfx = new TeamsFx(IdentityType.User, {
//   initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
//   clientId: process.env.REACT_APP_CLIENT_ID,
// }
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
const profile = await graphClient.api("/me").get(); // Get the profile of current user
```

</details>

<br>

<details>
<summary><b>ユーザーなしで Graph API を呼び出す (アプリケーション ID)</b></summary>

Teams ユーザーとの対話は必要ありません。 アプリケーション ID として Microsoft Graphを呼び出すことができます。

次のスニペットを使用します。

```ts
// Equivalent to:
// const teamsfx = new TeamsFx(IdentityType.App, {
//   initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
//   clientId: process.env.REACT_APP_CLIENT_ID,
// });
const teamsfx = new TeamsFx(IdentityType.App);
const graphClient = createMicrosoftGraphClient(teamsfx);
const profile = await graphClient.api("/users/{object_id_of_another_people}").get(); // Get the profile of certain user
```

</details>

<br>

## <a name="core-concepts-and-code-structure"></a>コア概念とコード構造

### <a name="teamsfx-class"></a>TeamsFx クラス

既定では、TeamsFx クラス インスタンスは、環境変数からすべての TeamsFx 設定にアクセスします。 また、カスタマイズした構成値を設定して、既定値をオーバーライドすることもできます。 詳細については、[オーバーライド構成](#override-configuration) を確認してください。 TeamsFx インスタンスを作成するときは、ID の種類も指定する必要があります。 ID には次の 2 種類があります:

* ユーザー ID
* アプリケーション ID

#### <a name="user-identity"></a>ユーザー ID

| コマンド | 説明 |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| アプリケーションは、現在の Teams ユーザーとして認証されます。 |
| `TeamsFx:setSsoToken()`| Node.js 環境のユーザー ID (ブラウザーなし)。 |
| `TeamsFx:getUserInfo()` | ユーザーの基礎情報を取得する。 |
| `TeamsFx:login()` | これは、SSO を使用して特定の OAuth スコープのアクセス トークンを取得する場合に、ユーザーが同意プロセスを実行できるようにするために使用されます。 |

> [!NOTE]
> 現在の Teams ユーザーに代わってリソースにアクセスできます。

#### <a name="application-identity"></a>アプリケーション ID

| コマンド | 説明 |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| アプリケーションはアプリケーションとして認証されます。通常、アクセス許可には管理者の承認が必要です。|
| `TeamsFx:getCredential()`| ID の種類に自動的に対応する資格情報インスタンスが提供されます。 |

> [!NOTE]
> リソースの管理者の同意が必要です。

### <a name="credential"></a>Credential

TeamsFx を初期化するときは、ID の種類を選択する必要があります。 TeamsFx の初期化時に ID の種類を指定した後、SDK はさまざまな種類の資格情報クラスを使用して ID を表し、対応する認証フローによってアクセス トークンを取得します。

認証を簡略化するための資格情報クラスは 3 つあります。 [資格情報フォルダー](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential)。 資格情報クラスは、特定のスコープにアクセス トークンを提供するように設計された、Azure ライブラリ API で広く使用される `TokenCredential` インターフェイスを実装します。 他の API は、クレデンシャル呼び出し `TeamsFx:getCredential()` に依存して `TokenCredential` のインスタンスを取得します。

各資格情報クラスター ゲットに対応するシナリオは次のとおりです。

#### <a name="user-identity-in-browser-environment"></a>ブラウザー環境のユーザー ID
`TeamsUserCredential` は、現在 Teams ユーザーの ID を表します。 この資格情報を使用すると、初めてユーザーの同意が要求されます。 これは、Teams SSO と On-Behalf-Of フローを利用してトークン交換を行います。 SDK では、開発者がブラウザー環境でユーザー ID を選択するときに、この資格情報が使用されます。

必要な構成: `initiateLoginEndpoint`、`clientId`。

#### <a name="user-identity-in-nodejs-environment"></a>Node.js 環境のユーザー ID
`OnBehalfOfUserCredential` は On-Behalf-Of フローを使用し、Teams SSO トークンが必要です。 これは、Azure Function またはボットのシナリオで使用するように設計されています。 SDK は、開発者が Node.js 環境でユーザー ID を選択するときに、この資格情報を使用します。

必要な構成: `authorityHost`、`tenantId`、`clientId`、`clientSecret`、`certificateContent`。

#### <a name="application-identity-in-nodejs-environment"></a>Node.js 環境でのアプリケーション ID
`AppCredential` は、アプリケーション ID を表します。 これは通常、ユーザーが時間トリガーの自動化ジョブのように関与していない場合に使用されます。 SDK は、開発者が Node.js 環境でアプリ ID を選択するときに、この資格情報を使用します。

必要な構成: `tenantId`、`clientId`、`clientSecret`、`certificateContent`。

### <a name="bot-sso"></a>Bot SSO

ボット関連のクラスは、[ボット フォルダー](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot)の下に格納されます。

`TeamsBotSsoPrompt` には、ボット フレームワークとの良好な統合があります。 これにより、ボット アプリケーションを開発し、ボットの SSO を利用する場合の認証プロセスが簡略化されます。

必要な構成: `initiateLoginEndpoint`、`tenantId`、`clientId`、`applicationIdUri`。

### <a name="supported-functions"></a>サポートされているワークシート関数

TeamsFx SDK には、サード パーティ製ライブラリの構成を容易にするためのいくつかの機能が用意されています。 [コア フォルダー](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core) の下にあります。

*  Microsoft Graph サービス: `createMicrosoftGraphClient` および `MsGraphAuthProvider` は、認証された Graph インスタンスの作成に役立ちます。
*  SQL: `getTediousConnectionConfig` は面倒な接続構成を返します。

必要な構成:
* `sqlServerEndpoint`、`sqlUsername`、ユーザー ID を使用する場合は `sqlPassword`
* `sqlServerEndpoint`、MSI ID を使用する場合は `sqlIdentityId`

### <a name="error-handling"></a>エラー処理

API エラー応答は、エラー コードとエラー メッセージを含むエラー応答である `ErrorWithCode` です。 たとえば、特定のエラーを除外するには、次のスニペットを使用します。

```ts
try {
  const teamsfx = new TeamsFx();
  await teamsfx.login("User.Read");
} catch (err: unknown) {
  if (err instanceof ErrorWithCode && err.code !== ErrorCode.ConsentFailed) {
    throw err;
  } else {
    // Silently fail because user cancels the consent dialog
        return;
  }
}
```

資格情報インスタンスが Microsoft Graph などの他のライブラリで使用されている場合、エラーがキャッチされ、変換される可能性があります。

```ts
try {
  const teamsfx = new TeamsFx();
  const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
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

次のセクションでは、一般的なシナリオ向けのコード スニペットをいくつか示します。

<br>

<details>
<summary><b>タブ アプリで Graph API を使用する</b></summary>
 
`TeamsFx` と `createMicrosoftGraphClient` を使用します。

```ts
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

</details>

<br>

<details>
<summary><b>タブ アプリで Azure 関数を呼び出す</b></summary>

`axios` ライブラリを使用して Azure 関数に HTTP 要求を行います。

```ts
const teamsfx = new TeamsFx();
const token = teamsfx.getCredential().getToken(""); // Get SSO token for the use
// Call API hosted in Azure Functions on behalf of user
const apiEndpoint = teamsfx.getConfig("apiEndpoint");
const response = await axios.default.get(apiEndpoint + "api/httptrigger1", {
  headers: {
    authorization: "Bearer " + token,
  },
});
```

</details>

<br>

<details>
<summary><b>Azure Function でデータベース SQL にアクセスする</b></summary>


`tedious`ライブラリを使用して SQL にアクセスし、認証を管理する `DefaultTediousConnectionConfiguration` 機能を利用します。
`tedious`とは別に、`sqlConnectionConfig.getConfig()` の結果に基づいて、他の SQL ライブラリの接続構成を作成することもできます。

```ts
// Equivalent to:
// const sqlConnectConfig = new DefaultTediousConnectionConfiguration({
//    sqlServerEndpoint: process.env.SQL_ENDPOINT,
//    sqlUsername: process.env.SQL_USER_NAME,
//    sqlPassword: process.env.SQL_PASSWORD,
// });
const teamsfx = new TeamsFx();
// If there's only one SQL database
const config = await getTediousConnectionConfig(teamsfx);
// If there are multiple SQL databases
const config2 = await getTediousConnectionConfig(teamsfx "your database name");
const connection = new Connection(config);
connection.on("connect", (error) => {
  if (error) {
    console.log(error);
  }
});
```

</details>

<br>

<details>
<summary><b>Azure Function で証明書ベースの認証を使用する</b></summary>

```ts
const authConfig = {
  clientId: process.env.M365_CLIENT_ID,
  certificateContent: "The content of a PEM-encoded public/private key certificate",
  authorityHost: process.env.M365_AUTHORITY_HOST,
  tenantId: process.env.M365_TENANT_ID,
};
const teamsfx = new TeamsFx(IdentityType.App);
teamsfx.setCustomeConfig({
  certificateContent: "The content of a PEM-encoded public/private key certificate"
});
const token = teamsfx.getCredential().getToken();
```

</details>

<br>

<details>
<summary><b>ボット アプリケーションで Graph API を使用する</b></summary>

ダイアログ セットに `TeamsBotSsoPrompt` を追加します。

```ts
const { ConversationState, MemoryStorage } = require("botbuilder");
const { DialogSet, WaterfallDialog } = require("botbuilder-dialogs");
const { TeamsBotSsoPrompt } = require("@microsoft/teamsfx");

const convoState = new ConversationState(new MemoryStorage());
const dialogState = convoState.createProperty("dialogState");
const dialogs = new DialogSet(dialogState);

const teamsfx = new TeamsFx();
dialogs.add(
  new TeamsBotSsoPrompt(teamsfx, "TeamsBotSsoPrompt", {
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

</details>

<br>

## <a name="advanced-customization"></a>高度なカスタマイズ

### <a name="configure-log"></a>ログを構成する

このライブラリを使用する場合は、顧客ログ レベルを設定し、出力をリダイレクトできます。 ログ記録は既定でオフになっています。ログ レベルを設定して有効にすることができます。

#### <a name="enable-log-by-setting-log-level"></a>ログ レベルを設定してログを有効にする

ログは、ログ レベルを設定した場合にのみ有効になります。 既定では、ログ情報はコンソールに出力されます。

次のスニペットを使用してログ レベルを設定します。

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

カスタム ロガーまたはログ関数を設定することで、ログ出力をリダイレクトできます。

#### <a name="redirect-by-setting-custom-logger"></a>カスタム ロガーを設定してリダイレクトする

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>カスタム ログ関数を設定してリダイレクトする

> [!NOTE]
> カスタム ロガーを設定した場合、ログ関数は有効になりません。

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

## <a name="override-configuration"></a>構成をオーバーライドする
TeamsFx インスタンスを作成するときにカスタム構成を渡して、既定の構成をオーバーライドしたり、環境変数が見つからない場合に必須フィールドを設定したりできます。

- VS Code Toolkit を使用してタブ プロジェクトを作成した場合は、事前構成済みの環境変数から次の構成値が使用されます。
  * authorityHost (REACT_APP_AUTHORITY_HOST)
  * tenantId (REACT_APP_TENANT_ID)
  * clientId (REACT_APP_CLIENT_ID)
  * initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL)
  * applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL)
  * apiEndpoint (REACT_APP_FUNC_ENDPOINT)
  * apiName (REACT_APP_FUNC_NAME)

- VS Code Toolkitを使用して Azure Function / bot プロジェクトを作成した場合は、事前に構成された環境変数から次の構成値が使用されます。
  * initiateLoginEndpoint (INITIATE_LOGIN_ENDPOINT)
  * authorityHost (M365_AUTHORITY_HOST)
  * tenantId (M365_TENANT_ID)
  * clientId (M365_CLIENT_ID)
  * clientSecret (M365_CLIENT_SECRET)
  * applicationIdUri (M365_APPLICATION_ID_URI)
  * apiEndpoint (API_ENDPOINT)
  * sqlServerEndpoint (SQL_ENDPOINT)
  * sqlUsername (SQL_USER_NAME)
  * sqlPassword (SQL_PASSWORD)
  * sqlDatabaseName (SQL_DATABASE_NAME)
  * sqlIdentityId (IDENTITY_ID)

## <a name="upgrade-latest-sdk-version"></a>最新の SDK バージョンをアップグレードする

`loadConfiguration()` を持つバージョンの SDK を使用している場合は、次の手順に従って最新の SDK バージョンにアップグレードできます。
1. `loadConfiguration()` を削除し、`new TeamsFx(IdentityType.User, { ...customConfig })` を使用してカスタマイズされた設定を渡す
2. `new TeamsUserCredential()` を `new TeamsFx()` に置き換え
3. `new M365TenantCredential()` を `new TeamsFx(IdentityType.App)` に置き換え
4. `new OnBehalfOfUserCredential(ssoToken)` を `new TeamsFx().setSsoToken(ssoToken)` に置き換え
5. ヘルパー関数の `TeamsFx` インスタンスを渡して資格情報インスタンスを置き換える

詳細については、「[TeamsFx クラス](#teamsfx-class)」を参照してください。

## <a name="next-step"></a>次のステップ

TeamsFx SDK を使用する方法の詳細な例については、[サンプル](https://github.com/OfficeDev/TeamsFx-Samples) プロジェクトを参照してください。

## <a name="see-also"></a>関連項目

[Microsoft TeamsFx サンプル ギャラリー](https://github.com/OfficeDev/TeamsFx-Samples)。
