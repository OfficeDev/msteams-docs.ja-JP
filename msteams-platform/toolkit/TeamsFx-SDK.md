---
title: TeamsFx SDK
author: surbhigupta
description: このモジュールでは、TeamsFx SDK、コア概念とコード構造、高度なカスタマイズとシナリオについて説明します
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9d870680e146564bb23db0193d2e2b116a249009
ms.sourcegitcommit: 16898eebeddc1bc1ac0d9862b4627c3bb501c109
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2022
ms.locfileid: "68327588"
---
# <a name="teamsfx-sdk"></a>TeamsFx SDK

TeamsFx は、Microsoft Teams シングル サインオン (Teams SSO) を使用し、構成がゼロの単一行ステートメントにクラウド リソースにアクセスすることで、タスクを減らすのに役立ちます。 ブラウザーとNode.js環境で TeamsFx SDK を使用できます。 TeamsFx のコア機能には、クライアント環境とサーバー環境でアクセスできます。 ユーザー認証コードは、次の簡単な方法で記述できます。

* [Teams] タブ
* Teams ボット。
* Azure 関数

## <a name="prerequisites"></a>前提条件

次のツールをインストールし、開発環境を設定する必要があります。

| &nbsp; | インストール | 使用するには... |
   | --- | --- | --- |
   | &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | JavaScript、TypeScript、または SharePoint Framework (SPFx) ビルド環境。 バージョン 1.55 以降を使用してください。 |
   | &nbsp; | [Teams ツールキット](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| アプリのプロジェクト スキャフォールディングを作成する Microsoft Visual Studio Code 拡張機能。 4.0.0 バージョンを使用します。 |
   | &nbsp; | [Node.js](https://nodejs.org/en/download/) | バックエンド JavaScript ランタイム環境。 最新の v16 LTS リリースを使用します。|
   | &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams を使用して、チャット、会議、通話用のアプリを通じて共同作業を行うすべてのユーザーと 1 か所で共同作業を行うことができます。|
   | &nbsp; | [Microsoft&nbsp;Edge](https://www.microsoft.com/edge) (推奨) または [Google Chrome](https://www.google.com/chrome/) | 開発者ツールを備えたブラウザー。 |

> [!NOTE]
> プロジェクトに依存関係として `botbuilder` 関連の [パッケージ](https://github.com/Microsoft/botbuilder-js#packages) がインストールされている場合は、それらが同じバージョンであることを確認してください。

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

## <a name="teamsfx-core-functionalities"></a>TeamsFx のコア機能

### <a name="teamsfx-class"></a>TeamsFx クラス

既定では、TeamsFx クラス インスタンスは、環境変数からすべての TeamsFx 設定にアクセスします。 また、カスタマイズした構成値を設定して、既定値をオーバーライドすることもできます。 詳細については、「[構成をオーバーライドする](#override-configuration)」 を確認してください。
TeamsFx インスタンスを作成するときは、ID の種類も指定する必要があります。
ID には次の 2 種類があります:

* **ユーザー ID**: Teams の現在のユーザーを表します。
* **アプリケーション ID**: アプリケーション自体を表します。

    > [!NOTE]
    > これら 2 つの ID の種類では、TeamsFx コンストラクターとメソッドは同じではありません。

ユーザー ID とアプリケーション ID の詳細については、次のセクションを参照してください。

<details>
<summary><b> ユーザー ID </b></summary>

| コマンド | 説明 |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| アプリケーションは、現在の Teams ユーザーとして認証されます。 |
| `TeamsFx:setSsoToken()`| Node.js 環境のユーザー ID (ブラウザーなし)。 |
| `TeamsFx:getUserInfo()` | ユーザーの基礎情報を取得する。 |
| `TeamsFx:login()` | これは、SSO を使用して特定の OAuth スコープのアクセス トークンを取得する場合に、ユーザーが同意プロセスを実行できるようにするために使用されます。 |

> [!NOTE]
> 現在の Teams ユーザーに代わってリソースにアクセスできます。
</details>

<details>
<summary><b> アプリケーション ID </b></summary>

| コマンド | 説明 |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| Application  is authenticated as an application. The permission usually needs administrator's approval.|
| `TeamsFx:getCredential()`| ID の種類に自動的に対応する資格情報インスタンスが提供されます。 |

> [!NOTE]
> リソースの管理者の同意が必要です。
</details>

### <a name="credential"></a>Credential

TeamsFx を初期化するには、必要な ID の種類を選択する必要があります。 ID の種類を指定した後 SDK では、さまざまな種類の資格情報クラスが使用されます。 これらは ID を表し、対応する認証フローによってアクセス トークンを取得します。 資格情報クラスは、特定のスコープにアクセス トークンを提供するように設計された Azure ライブラリ API で広く使用されるインターフェイスを実装 `TokenCredential` します。 他の API は、クレデンシャル呼び出し `TeamsFx:getCredential()` に依存して `TokenCredential` のインスタンスを取得します。 資格情報と認証フローに関連するクラスの詳細については、「 [資格情報フォルダー」を](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential)参照してください。

認証を簡略化するための資格情報クラスは 3 つあります。 各資格情報クラスター ゲットに対応するシナリオは次のとおりです。

<details>
<summary><b> ブラウザー環境のユーザー ID </b></summary>

`TeamsUserCredential` は、現在 Teams ユーザーの ID を表します。 初めてユーザーの資格情報が認証されると、Teams SSO はトークン交換のために On-Behalf-Of フローを実行します。 SDK では、ブラウザー環境でユーザー ID を選択するときに、この資格情報が使用されます。

必要な構成は次のとおりです `initiateLoginEndpoint` `clientId`。
</details>

<details>
<summary><b> Node.js環境のユーザー ID </b></summary>

`OnBehalfOfUserCredential` は On-Behalf-Of フローを使用し、Azure 関数またはボットのシナリオで Teams SSO トークンを必要とします。 TeamsFx SDK では、Node.js環境でユーザー ID を選択するときに、次の資格情報が使用されます。

必要な構成: `authorityHost`、`tenantId`、`clientId`、`clientSecret`、`certificateContent`。
</details>

<details>
<summary><b> Node.js環境での App Identity </b></summary>

`AppCredential` は、アプリ ID を表します。 アプリ ID は、ユーザーが関与していない場合 (時間トリガーの自動化ジョブなど) で使用できます。 TeamsFx SDK では、Node.js環境でアプリ ID を選択するときに、次の資格情報が使用されます。

必要な構成: `tenantId`、`clientId`、`clientSecret`、`certificateContent`。
</details>

### <a name="bot-sso"></a>Bot SSO

ボット関連のクラスは、[ボット フォルダー](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot)の下に格納されます。

`TeamsBotSsoPrompt` はボット フレームワークと統合されます。 これにより、ボット アプリケーションを開発し、ボット SSO を使用する場合の認証プロセスが簡略化されます。

必要な構成: `initiateLoginEndpoint`、`tenantId`、`clientId`、`applicationIdUri`。

### <a name="supported-functions"></a>サポートされているワークシート関数

TeamsFx SDK provides several functions to ease the configuration for third-party libraries. They're located under [core folder](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core).

* Microsoft Graph サービス: `createMicrosoftGraphClient` および `MsGraphAuthProvider` は、認証された Graph インスタンスの作成に役立ちます。
* SQL: `getTediousConnectionConfig` は面倒な接続構成を返します。

    必要な構成:

  * ユーザー ID を使用する場合は、必須`sqlServerEndpoint``sqlUsername``sqlPassword`です。
  * MSI ID を使用する場合は、必要`sqlServerEndpoint``sqlIdentityId`です。

### <a name="override-configuration"></a>構成をオーバーライドする

新しい `TeamsFx` インスタンスを作成するときにカスタム構成を渡して、既定の構成をオーバーライドしたり、不足している場合に必須フィールドを `environment variables` 設定したりできます。

<details>
<summary><b> タブ プロジェクトの場合 </b> </summary>

Microsoft Visual Studio Code Toolkit を使用してタブ プロジェクトを作成した場合は、事前に構成された環境変数から次の構成値が使用されます。

* authorityHost (REACT_APP_AUTHORITY_HOST)
* tenantId (REACT_APP_TENANT_ID)
* clientId (REACT_APP_CLIENT_ID)
* initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL)
* applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL)
* apiEndpoint (REACT_APP_FUNC_ENDPOINT) // バックエンド関数がある場合にのみ使用
* バックエンド関数がある場合にのみ使用される apiName (REACT_APP_FUNC_NAME) //

</details>

<details>
<summary><b> Azure 関数またはボット プロジェクトの場合 </b></summary>

Visual Studio Code Toolkit を使用して Azure 関数またはボット プロジェクトを作成した場合は、事前に構成された環境変数から次の構成値が使用されます。

* initiateLoginEndpoint (INITIATE_LOGIN_ENDPOINT)
* authorityHost (M365_AUTHORITY_HOST)
* tenantId (M365_TENANT_ID)
* clientId (M365_CLIENT_ID)
* clientSecret (M365_CLIENT_SECRET)
* applicationIdUri (M365_APPLICATION_ID_URI)
* apiEndpoint (API_ENDPOINT)
* sqlServerEndpoint (SQL_ENDPOINT) // は、sql インスタンスがある場合にのみ使用されます
* sqlUsername (SQL_USER_NAME) // は、sql インスタンスがある場合にのみ使用されます
* sqlPassword (SQL_PASSWORD) // は、sql インスタンスがある場合にのみ使用されます
* sqlDatabaseName (SQL_DATABASE_NAME) // は、sql インスタンスがある場合にのみ使用されます
* sqlIdentityId (IDENTITY_ID) // は、sql インスタンスがある場合にのみ使用されます

</details>

### <a name="error-handling"></a>エラー処理

基本的な種類の API エラー応答には `ErrorWithCode`、エラー コードとエラー メッセージが含まれています。 たとえば、特定のエラーを除外するには、次のスニペットを使用します。

```typescript
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

## <a name="microsoft-graph-scenarios"></a>Microsoft Graph のシナリオ

このセクションでは、Microsoft Graph に関連する一般的なシナリオ向けのコード スニペットをいくつか示します。 このようなシナリオでは、ユーザーは異なるエンド (フロントエンド/バックエンド) で異なるアクセス許可を使用して API を呼び出すことができます。

* フロントエンドのユーザー デリゲートアクセス許可 (TeamsUserCredential を使用) <details>
    <summary><b>タブ アプリで Graph API を使用する</b></summary>

    このコード スニペットは、Microsoft Graph を使用 `TeamsFx` して `createMicrosoftGraphClient` ユーザー プロファイルを取得する方法を示しています。 また、. をキャッチして解決 `GraphError`する方法も示します。

    1. 必要なクラスをインポートします。

    ```typescript
    import {
      createMicrosoftGraphClient,
      TeamsFx,
    } from "@microsoft/teamsfx";
    ```

    2. ユーザーの同意を得るために使用 `TeamsFx.login()` します。

    ```typescript
    // Put these code in a call-to-action callback function to avoid browser blocking automatically showing up pop-ups.
    await teamsfx.login(["User.Read"]); // Login with scope
    ```

    3. TeamsFx インスタンスとグラフ クライアントを初期化し、このクライアントによって MS Graph から情報を取得できます。

    ```typescript
    try {
      const teamsfx = new TeamsFx();
      const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
      const profile = await graphClient.api("/me").get();
    } catch (err: unknown) {
      // ErrorWithCode is handled by Graph client
      if (err instanceof GraphError && err.code?.includes(ErrorCode.UiRequiredError)) {
        // Need to show login button to ask for user consent.
      }
    }
    ```

    タブ アプリでGraph APIを使用するサンプルの詳細については、[hello-world-tab サンプル](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab)を参照してください。

    </details>

    <details>
    <summary><b>Microsoft Graph Toolkit との統合</b></summary>

    [Microsoft Graph Toolkit (mgt)](https://aka.ms/mgt) ライブラリは、Microsoft Graph を搭載したさまざまな認証プロバイダーと UI コンポーネントのコレクションです。

    パッケージは`@microsoft/mgt-teamsfx-provider`、クラスを使用`TeamsFx`して`TeamsFxProvider`ユーザーにサインインし、Graph で使用するトークンを取得するクラスを公開します。

    1. 次の必要なパッケージをインストールできます。

    ```bash
    npm install @microsoft/mgt-element @microsoft/mgt-teamsfx-provider @microsoft/teamsfx
    ```

    2. コンポーネント内でプロバイダーを初期化します。

    ```typescript
     // Import the providers and credential at the top of the page
    import {Providers} from '@microsoft/mgt-element';
    import {TeamsFxProvider} from '@microsoft/mgt-teamsfx-provider';
    import {TeamsUserCredential} from "@microsoft/teamsfx";

    const scope = ["User.Read"];
    const teamsfx = new TeamsFx();
    const provider = new TeamsFxProvider(teamsfx, scope);
    Providers.globalProvider = provider;   
    ```

    3. このメソッドを `teamsfx.login(scopes)` 使用して、必要なアクセス トークンを取得できます。

    ```typescript
    // Put these code in a call-to-action callback function to avoid browser blocking automatically showing up pop-ups. 
    await teamsfx.login(this.scope);
    Providers.globalProvider.setState(ProviderState.SignedIn);
    ```

    4. これで、コンテキストを使用して Microsoft Graph にアクセスするReactを使用して、HTML ページまたはメソッドに`render()`任意の`TeamsFx`コンポーネントを追加できるようになりました。

    ```html
    <mgt-person query="me" view="threeLines"></mgt-person>
    ```

    ```typescript
    public render(): void {
    return (
        <div>
            <Person personQuery="me" view={PersonViewType.threelines}></Person>
        </div>
    );
    }    
    ```

    TeamsFx プロバイダーを初期化するサンプルの詳細については、 [Contacts Exporter のサンプルを](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/graph-toolkit-contact-exporter)参照してください。

    </details>

* バックエンドでのユーザー デリゲートアクセス許可 (OnBehalfOfUserCredential を使用) <details>
    <summary><b>ボット アプリケーションでGraph APIを使用する</b></summary>

    このコード スニペットでは、ダイアログを `TeamsBotSsoPrompt` 設定し、サインインしてアクセス トークンを取得する方法を示します。

    1. ダイアログ セットを初期化して追加 `TeamsBotSsoPrompt` します。

    ```typescript
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
    ```

    2. ダイアログを開始し、サインインします。

    ```typescript
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

    ボット アプリケーションで Graph API を使用するサンプルの詳細については、 [bot-sso サンプルを](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/bot-sso)参照してください。

    </details>

    <details>
    <summary><b>メッセージ拡張機能でGraph APIを使用する</b></summary>

    このコード スニペットは、TeamsFx sdk から提供される拡張`TeamsActivityHandler`をオーバーライド`handleTeamsMessagingExtensionQuery`し、アクセス トークンを取得するためにサインインするために使用`handleMessageExtensionQueryWithToken`する方法を示しています。

    ```typescript
    public async handleTeamsMessagingExtensionQuery(context: TurnContext, query: any): Promise<any> {
      return await handleMessageExtensionQueryWithToken(context, null, 'User.Read', 
        async (token: MessageExtensionTokenResponse) => {
          // ... continue to query with access token ...
        });
    }    
    ```

    メッセージ拡張機能で Graph API を使用するサンプルの詳細については、「 [message-extension-sso-sample](https://aka.ms/teamsfx-me-sso-sample)」を参照してください。
    </details>

    <details>
    <summary><b>コマンド ボットでGraph APIを使用する</b></summary>

    このコード スニペットでは、コマンド ボットが Microsoft API を呼び出すように実装 `TeamsFxBotSsoCommandHandler` する方法を示します。

    ```typescript
    import { Activity, TurnContext } from "botbuilder";
    import {
      CommandMessage,
      TriggerPatterns,
      TeamsFx,
      createMicrosoftGraphClient,
      TeamsFxBotSsoCommandHandler,
      TeamsBotSsoPromptTokenResponse,
    } from "@microsoft/teamsfx";

    export class ProfileSsoCommandHandler implements TeamsFxBotSsoCommandHandler {
      triggerPatterns: TriggerPatterns = "profile";

      async handleCommandReceived(
        context: TurnContext,
        message: CommandMessage,
        tokenResponse: TeamsBotSsoPromptTokenResponse,
      ): Promise<string | Partial<Activity> | void> {
        // Init TeamsFx instance with SSO token
        const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

        // Add scope for your Azure AD app. For example: Mail.Read, etc.
        const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
      
        // Call graph api use `graph` instance to get user profile information
        const me = await graphClient.api("/me").get();

        if (me) {
          // Bot will send the user profile info to user
          return `Your command is '${message.text}' and you're logged in as ${me.displayName}`;
        } else {
          return "Could not retrieve profile information from Microsoft Graph.";
        }
      }
    }    
    ```

    コマンド ボットでこのクラスを使用する方法の詳細については、「 [Teams アプリにシングル サインオンを追加する」を](add-single-sign-on.md)参照してください。 また、 [sso コマンド ボットを試すことができる command-bot-with-sso](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/command-bot-with-sso) サンプル プロジェクトもあります。

    </details>

    <details>
    <summary><b>タブ アプリで Azure 関数を呼び出す: On-Behalf-Of フロー</b></summary>

    このコード スニペットでは、Azure Function を呼び出すために使用または`axios`ライブラリを使用`CreateApiClient`する方法と、Azure 関数でGraph APIを呼び出してユーザー プロファイルを取得する方法を示します。

    1. TeamsFx sdk によって提供される Azure 関数を呼び出すために使用 `CreateApiClient` できます。

    ```typescript
    async function callFunction(teamsfx?: TeamsFx) {
      const teamsfx = new TeamsFx();

      // Get the credential.
      const credential = teamsfx.getCredential(); 
      // Create an API client by providing the token and endpoint.
      const apiClient = CreateApiClient(
        teamsfx.getConfig("YOUR_API_ENDPOINT"), // Create an API Client that uses SSO token to authenticate requests
        new BearerTokenAuthProvider(async () =>  (await credential.getToken(""))!.token) // Call API hosted in Azure Functions on behalf of user to inject token to request header
      );

      // Send a GET request to "RELATIVE_API_PATH", "/api/functionName" for example.
      const response = await apiClient.get("RELATIVE_API_PATH");
      return response.data;
    }    
    ```

    ライブラリを使用 `axios` して Azure Function を呼び出すこともできます。

    ```typescript
    async function callFunction(teamsfx?: TeamsFx) {
      const accessToken = await teamsfx.getCredential().getToken(""); // Get SSO token 
      // teamsfx.getConfig("apiEndpoint") will read REACT_APP_FUNC_ENDPOINT environment variable 
      const endpoint = teamsfx.getConfig("apiEndpoint");
      const response = await axios.default.get(endpoint + "/api/" + functionName, {
        headers: {
          authorization: "Bearer " + accessToken.token,
        },
      });
      return response.data;
    }    
    ```

    2. 応答でユーザーに代わって Azure 関数でGraph APIを呼び出します。

    ```typescript
    export default async function run(
      context: Context,
      req: HttpRequest,
      teamsfxContext: TeamsfxContext
    ): Promise<Response> {
      const res: Response = { status: 200, body: {},};
      // ...
      teamsfx = new TeamsFx().setSsoToken(accessToken);
      // Query user's information from the access token.
      try {
        const currentUser: UserInfo = await teamsfx.getUserInfo();
        if (currentUser && currentUser.displayName) {
          res.body.userInfoMessage = `User display name is ${currentUser.displayName}.`;
        } else {
          res.body.userInfoMessage = "No user information was found in access token.";
        }
      } catch (e) {
      }
      // Create a graph client to access user's Microsoft 365 data after user has consented.
      try {
        const graphClient: Client = createMicrosoftGraphClient(teamsfx, [".default"]);
        const profile: any = await graphClient.api("/me").get();
        res.body.graphClientMessage = profile;
      } catch (e) {
      }
      return res;
    }    
    ```

    ボット アプリケーションで Graph API を使用するサンプルの詳細については、  [hello-world-tab-with-backend サンプル](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab-with-backend)を参照してください。

    </details>

* バックエンドでのアプリケーションのアクセス許可 <details>
    <summary><b>Azure Function で証明書ベースの認証を使用する</b></summary>

    このコード スニペットでは、証明書ベースのアプリケーションアクセス許可を使用して、Graph APIの呼び出しに使用できるトークンを取得する方法を示します。

    1. を指定`PEM-encoded key certificate`して初期化`authConfig`できます。

    ```typescript
    const authConfig = {
      clientId: process.env.M365_CLIENT_ID,
      certificateContent: "The content of a PEM-encoded public/private key certificate",
      authorityHost: process.env.M365_AUTHORITY_HOST,
      tenantId: process.env.M365_TENANT_ID,
    };    
    ```

    2. トークンを `authConfig` 取得するために使用できます。

    ```typescript
    const teamsfx = new TeamsFx(IdentityType.App);
    teamsfx.setCustomeConfig(authConfig);
    const token = teamsfx.getCredential().getToken();    
    ```

    </details>

    <details>
    <summary><b>Azure Function でクライアント シークレット認証を使用する</b></summary>

    このコード スニペットでは、クライアント シークレット アプリケーションのアクセス許可を使用して、Graph APIの呼び出しに使用できるトークンを取得する方法を示します。

    1. を指定`client secret`して初期化`authConfig`できます。

    ```typescript
    const authConfig = {
      clientId: process.env.M365_CLIENT_ID,
      clientSecret: process.env.M365_CLIENT_SECRET,
      authorityHost: process.env.M365_AUTHORITY_HOST,
      tenantId: process.env.M365_TENANT_ID,
    };    
    ```

    2. トークンを `authConfig` 取得するために使用できます。

    ```typescript
    const teamsfx = new TeamsFx(IdentityType.App);
    teamsfx.setCustomeConfig(authConfig);
    const token = teamsfx.getCredential().getToken();    
    ```

    ボット アプリケーションで Graph API を使用するサンプルの詳細については、 [hello-world-tab-with-backend サンプル](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab-with-backend)を参照してください。

    </details>

## <a name="other-scenarios"></a>その他のシナリオ

このセクションでは、Microsoft Graph に関連するその他のシナリオのコード スニペットをいくつか示します。 Bot または Azure Function で API クライアントを作成し、Azure Function で SQL データベースにアクセスできます。

  <details>
  <summary><b>Bot または Azure Function で既存の API を呼び出す API クライアントを作成する</b></summary>

  このコード スニペットでは、Bot by で `ApiKeyProvider`既存の API を呼び出す方法を示します。

  ```typescript
  const teamsfx = new TeamsFx();

  // Create an API Key auth provider. In addition to APiKeyProvider, following auth providers are also available:
  // BearerTokenAuthProvider, BasicAuthProvider, CertificateAuthProvider.
  const authProvider = new ApiKeyProvider("YOUR_API_KEY_NAME",
    teamsfx.getConfig("YOUR_API_KEY_VALUE"), // This reads the value of YOUR_API_KEY_VALUE environment variable.
    ApiKeyLocation.Header
  );

  // Create an API client using above auth provider.
  // You can also implement AuthProvider interface and use it here.
  const apiClient = createApiClient(
    teamsfx.getConfig("YOUR_API_ENDPOINT"), // This reads YOUR_API_ENDPOINT environment variable.
    authProvider
  );

  // Send a GET request to "RELATIVE_API_PATH", "/api/apiname" for example.
  const response = await apiClient.get("RELATIVE_API_PATH");  
  ```

  </details>

  <details>
  <summary><b>Azure Function でデータベース SQL にアクセスする</b></summary>

  ライブラリを使用して `tedious` SQL にアクセスし、認証を管理するライブラリを使用 `DefaultTediousConnectionConfiguration` します。 の結果に基づいて、他の SQL ライブラリの `sqlConnectionConfig.getConfig()`接続構成を作成することもできます。

  1. 接続構成を設定します。

  ```typescript
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
  const config2 = await getTediousConnectionConfig(teamsfx, "your database name");  
  ```

  2. データベースに接続します。

  ```typescript
  const connection = new Connection(config);
  connection.on("connect", (error) => {
    if (error) {
      console.log(error);
    }
  });  
  ```

  > [!NOTE]
  > Azure 関数で SQL データベースにアクセスするサンプルの詳細については、 [share-now サンプルを](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/share-now)参照してください。

</details>

## <a name="advanced-customization"></a>高度なカスタマイズ

### <a name="configure-log"></a>ログを構成する

このライブラリを使用する場合は、顧客ログ レベルを設定し、出力をリダイレクトできます。

> [!NOTE]
> ログ記録は既定でオフになっています。ログ レベルを設定して有効にすることができます。

#### <a name="enable-log-by-setting-log-level"></a>ログ レベルを設定してログを有効にする

ログ レベルを設定すると、ログが有効になります。 既定では、ログ情報がコンソールに出力されます。

次のスニペットを使用してログ レベルを設定します。

```typescript
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

> [!NOTE]
> カスタム ロガーまたはログ関数を設定することで、ログ出力をリダイレクトできます。

#### <a name="redirect-by-setting-custom-logger"></a>カスタム ロガーを設定してリダイレクトする

```typescript
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>カスタム ログ関数を設定してリダイレクトする

```typescript
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

> [!NOTE]
> カスタム ロガーを設定しても、ログ関数は有効になりません。

## <a name="upgrade-latest-sdk-version"></a>最新の SDK バージョンをアップグレードする

バージョンの SDK を使用している場合は `loadConfiguration()`、次の手順に従って最新の SDK バージョンにアップグレードできます。

1. `loadConfiguration()` を削除し、`new TeamsFx(IdentityType.User, { ...customConfig })` を使用してカスタマイズされた設定を渡す
2. `new TeamsUserCredential()` を`new TeamsFx()` に置き換えます。
3. `new M365TenantCredential()` を`new TeamsFx(IdentityType.App)` に置き換えます。
4. `new OnBehalfOfUserCredential(ssoToken)` を`new TeamsFx().setSsoToken(ssoToken)` に置き換えます。
5. のインスタンス `TeamsFx` をヘルパー関数に渡して、資格情報インスタンスを置き換えます。

## <a name="next-step"></a>次のステップ

TeamsFx SDK サンプル プロジェクトを使用する方法の詳細 [な](https://github.com/OfficeDev/TeamsFx-Samples) 例について説明します。

## <a name="see-also"></a>関連項目

[Microsoft TeamsFx サンプル ギャラリー](https://github.com/OfficeDev/TeamsFx-Samples)。
