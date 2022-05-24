---
title: Teams アプリにシングル サインオンを追加する
author: zyxiaoyuer
description: Teams Toolkitのシングル サインオンの追加について説明します
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 73177f96172e4fd60b7225c2463efb6a057f36c4
ms.sourcegitcommit: 74623035d7c18194e339f566c820e0653bc3d8b6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656846"
---
# <a name="add-single-sign-on-to-teams-app"></a>Teams アプリにシングル サインオンを追加する

Microsoft Teamsは、サインインTeamsユーザー トークンを取得して Microsoft Graphやその他の API にアクセスするためのシングル サインオン機能をアプリケーションに提供します。 Teams Toolkitは、Azure AD のフローの一部と、いくつかの単純な API の背後にある統合を抽象化することで、対話を容易にします。 これにより、シングル サインオン (SSO) 機能をTeams アプリケーションに簡単に追加できます。

チャット、チーム、またはチャネルでユーザーと対話するアプリケーションの場合、SSO はアダプティブ カードとしてマニフェストされ、ユーザーは Azure AD 同意フローを呼び出すために操作できます。

## <a name="enable-sso-support"></a>SSO サポートを有効にする

Teams Toolkitは、次のTeams機能に SSO を追加するのに役立ちます。

* Tab
* Bot
* 通知ボット: サーバーを修正する
* コマンド ボット

### <a name="add-sso-using-visual-studio-code"></a>Visual Studio Code を使用して SSO を追加する

次の手順は、Visual Studio Code のTeams Toolkitを使用して SSO を追加するのに役立ちます

1. **Microsoft Visual Studio Code** を開きます。
2. 左側のナビゲーション バー Teams Toolkit :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/teams-toolkit-sidebar-icon.png" alt-text="sso add sidebar"::: を選択します。
3. **[開発**] で [**機能の追加]** を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-add features.png" alt-text="sso 機能の追加":::

    * コマンド パレットを開き、[**Teams: 機能の追加**] を選択することもできます。

4. **[シングル サインオン**] を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-select features.png" alt-text="sso select":::

### <a name="add-sso-using-teamsfx-cli"></a>TeamsFx CLI を使用して SSO を追加する

**プロジェクトのルート ディレクトリ** でコマンドを実行`teamsfx add sso`できます

> [!Note]
> この機能により、既存のすべての適用可能な機能に対して SSO が有効になります。 後でプロジェクトに機能を追加する場合は、同じ手順に従って SSO を有効にします。

## <a name="customize-your-project-using-teams-toolkit"></a>Teams Toolkitを使用してプロジェクトをカスタマイズする

次の表に、プロジェクトTeams Toolkit加える変更の一覧を示します。

   |**型**|**File**|**用途**|
   |--------|--------|-----------|
   |Create|`aad.template.json` 下 `template/appPackage`|Azure AD アプリケーション マニフェストは、Azure AD アプリを表します。 `template/appPackage` は、ローカル デバッグまたはプロビジョニング ステージ中に Azure AD アプリを登録するのに役立ちます。|
   |変更|`manifest.template.json` 下 `template/appPackage`|`webApplicationInfo` Teams アプリ マニフェスト テンプレートにオブジェクトが追加されます。 SSO を有効にするには、このフィールドが必要Teams。 この変更は、ローカル デバッグまたはプロビジョニングをトリガーするときに有効です。|
   |Create|`auth/tab`|参照コード、認証リダイレクト ページ、ファイル `README.md` は、タブ プロジェクトのこのパスに生成されます。|
   |Create|`auth/bot`|参照コード、認証リダイレクト ページ、ファイル `README.md` は、ボット プロジェクトのこのパスに生成されます。|

> [!Note]
> SSO を追加することで、ローカル デバッグをトリガーするまで、Teams Toolkitはクラウド内の何も変更しません。 コードを更新して、SSO がプロジェクトで動作していることを確認します。

## <a name="update-your-application-to-use-sso"></a>SSO を使用するようにアプリケーションを更新する

次の手順は、アプリケーションで SSO を有効にするのに役立ちます。

> [!NOTE]
> これらの変更は、スキャフォールディングするテンプレートに基づいています。

---
<br>
<br><details>
<summary><b>Tab プロジェクト </b></summary>

1. フォルダー内の`auth/public`コピー`auth-start.html`と `auth-end.htm`** を .`tabs/public/` Teams Toolkitは、Azure AD のリダイレクト フローに対して、これら 2 つのエンドポイントを Azure AD に登録します。

2. [コピー先] の下にある`auth/tab`フォルダーをコピー`sso`します`tabs/src/sso/`。

    * `InitTeamsFx`: ファイルは TeamsFx SDK を初期化し、SDK の初期化後にコンポーネントを開く `GetUserProfile` 関数を実装します。

    * `GetUserProfile`: ファイルは、Microsoft Graph APIを呼び出してユーザー情報を取得する関数を実装します

3. で実行 `npm install @microsoft/teamsfx-react` します `tabs/`。

4. インポート`InitTeamsFx`する次の行を`tabs/src/components/sample/Welcome.tsx`追加します。

    ```Bash

    import { InitTeamsFx } from "../../sso/InitTeamsFx";

    ```

5. コンポーネントをコンポーネント`InitTeamsFx`に`<InitTeamsFx />`置き換えるには、次の行`<AddSSO />`を`AddSso`置き換えます。

</details>
<details>
<summary><b>ボット プロジェクト </b></summary>

1. フォルダーをコピー先にコピー `auth/bot/public` します `bot/src`。 2 つのフォルダーには、認証リダイレクトに使用される HTML ページが含まれています。これらのページにルーティングを追加するには、ファイルを変更 `bot/src/index` する必要があります。

2. フォルダーをコピー先にコピー `auth/bot/sso` します `bot/src`。 2 つのフォルダーには、SSO 実装の参照として次の 3 つのファイルが含まれています。

    * `showUserInfo`: SSO トークンを使用してユーザー情報を取得する関数を実装します。 これに従って、SSO トークンを必要とする独自のメソッドを作成できます。

    * `ssoDialog`: SSO に使用される [ComponentDialog](/javascript/api/botbuilder-dialogs/componentdialog?view=botbuilder-ts-latest&preserve-view=true) を作成します。

    * `teamsSsoBot`: トリガーできるコマンドを使用`ssoDialog`して [TeamsActivityHandler](/javascript/api/botbuilder/teamsactivityhandler?view=botbuilder-ts-latest&preserve-view=true) を作成し、追加`showUserInfo`します。

3. コード サンプルに従って、このファイルに独自のコマンドを `addCommand` 登録します (省略可能)。

4. で実行 `npm install isomorphic-fetch` します `bot/`。

5. package.json で次の行の下`bot/`で実行`npm install copyfiles`し、置き換えます。
  
   ```JSON

   "build": "tsc --build",

    ```

    および 

   ```JSON

   "build": "tsc --build && copyfiles public/*.html lib/",

   ```

   このボット プロジェクトのビルド中に、認証リダイレクトに使用される HTML ページがコピーされます。

6. 次のファイルを追加したら、ファイルに`bot/src/index`新しい`teamsSsoBot`インスタンスを作成する必要があります。 次のコードを置き換えます。

   ```Bash
  
   // Process Teams activity with Bot Framework.
   server.post("/api/messages", async (req, res) => {
   await commandBot.requestHandler(req, res);
   });  

   ```

    および 

   ```Bash

   const handler = new TeamsSsoBot();
   // Process Teams activity with Bot Framework.
   server.post("/api/messages", async (req, res) => {
       await commandBot.requestHandler(req, res, async (context)=> {
           await handler.run(context);
       });
   });

   ```

7. ファイルに HTML ルートを `bot/src/index` 追加します。

   ```Bash

   server.get(
       "/auth-*.html",
       restify.plugins.serveStatic({
           directory: path.join(__dirname, "public"),
       })
   );

   ```

8. インポートする次の行を`bot/src/index`追加し、`path`次の行を追加します。`teamsSsoBot`

   ```Bash

   // For ts:
   import { TeamsSsoBot } from "./sso/teamsSsoBot";
   const path = require("path");

   // For js:
   const { TeamsSsoBot } = require("./sso/teamsSsoBot");
   const path = require("path");

   ```

9. Teams アプリ マニフェストにコマンドを登録します。 ボットの下に`command`次の行を開`templates/appPackage/manifest.template.json`き、`commandLists`追加します。

   ```JSON

   {
       "title": "show",
       "description": "Show user profile using Single Sign On feature"
   }

   ```
</details>
<details>
<summary><b>ボットに新しいコマンドを追加する </b></summary>

> [!NOTE]
> 現在、これらの手順は 、 `command bot`. 最初 `bot`に [bot-sso サンプル](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/bot-sso)を参照してください。

次の手順は、プロジェクトに SSO を追加した後に、新しいコマンドを追加するのに役立ちます。

1. 下に新しいファイル (`todo.ts`または`todo.js`) を`bot/src/`作成し、独自のビジネス ロジックを追加して、Graph APIを呼び出します。

# <a name="typescript"></a>[TypeScript](#tab/typescript)

   ```typescript
   // for TypeScript:
export async function showUserImage(
    context: TurnContext,
    ssoToken: string,
    param: any[]
): Promise<DialogTurnResult> {
    await context.sendActivity("Retrieving user photo from Microsoft Graph ...");

    // Init TeamsFx instance with SSO token
    const teamsfx = new TeamsFx().setSsoToken(ssoToken);

    // Update scope here. For example: Mail.Read, etc.
    const graphClient = createMicrosoftGraphClient(teamsfx, param[0]);
    
    // You can add following code to get your photo:
    // let photoUrl = "";
    // try {
    //   const photo = await graphClient.api("/me/photo/$value").get();
    //   photoUrl = URL.createObjectURL(photo);
    // } catch {
    //   // Could not fetch photo from user's profile, return empty string as placeholder.
    // }
    // if (photoUrl) {
    //   await context.sendActivity(
    //     `You can find your photo here: ${photoUrl}`
    //   );
    // } else {
    //   await context.sendActivity("Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.");
    // }

    return;
}  
   ```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

   ```javaScript
   // for JavaScript:
export async function showUserImage(context, ssoToken, param) {
    await context.sendActivity("Retrieving user photo from Microsoft Graph ...");

    // Init TeamsFx instance with SSO token
    const teamsfx = new TeamsFx().setSsoToken(ssoToken);

    // Update scope here. For example: Mail.Read, etc.
    const graphClient = createMicrosoftGraphClient(teamsfx, param[0]);
    
    // You can add following code to get your photo:
    // let photoUrl = "";
    // try {
    //   const photo = await graphClient.api("/me/photo/$value").get();
    //   photoUrl = URL.createObjectURL(photo);
    // } catch {
    //   // Could not fetch photo from user's profile, return empty string as placeholder.
    // }
    // if (photoUrl) {
    //   await context.sendActivity(
    //     `You can find your photo here: ${photoUrl}`
    //   );
    // } else {
    //   await context.sendActivity("Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.");
    // }

    return;
}
   ```

---

2. 新しいコマンドを登録する

   * で使用する新しいコマンド登録に次の`teamsSsoBot`行を`addCommand`追加します。

     ```bash

     this.dialog.addCommand("ShowUserProfile", "show", showUserInfo);

     ```

   * 上記の行の後に次の行を追加して、新しいコマンド `photo` を登録し、上記で追加したメソッド `showUserImage` にフックアップします。

     ```bash

     // As shown here, you can add your own parameter into the `showUserImage` method
     // You can also use regular expression for the command here
     const scope = ["User.Read"];
     this.dialog.addCommand("ShowUserPhoto", new RegExp("photo\s*.*"), showUserImage, scope);

     ```

3. Teams アプリ マニフェストにコマンドを登録します。 ボットの下に`command`次の行を開`templates/appPackage/manifest.template.json`き、`commandLists`追加します。

   ```JSON

   {
       "title": "photo",
       "description": "Show user photo using Single Sign On feature"
   }

   ```
</details>
<br>

## <a name="debug-your-application"></a>アプリケーションをデバッグする

F5 キーを押してアプリケーションをデバッグします。 Teams Toolkitでは、Azure AD マニフェスト ファイルを使用して、SSO 用の Azure AD アプリケーションを登録します。 ローカル デバッグ機能Teams Toolkitについては、「[Teams アプリをローカルでデバッグ](debug-local.md)する」を参照してください。

## <a name="customize-azure-ad-application-registration"></a>Azure AD アプリケーションの登録をカスタマイズする

[Azure AD アプリ マニフェスト](/azure/active-directory/develop/reference-app-manifest)を使用すると、アプリケーション登録のさまざまな側面をカスタマイズできます。 必要に応じてマニフェストを更新できます。 目的の API にアクセスするための追加の API アクセス許可を含める必要がある場合は、目的の API [にアクセスするための API アクセス許可](https://github.com/OfficeDev/TeamsFx/wiki/#customize-aad-manifest-template)に関するページを参照してください。
Azure Portal で Azure AD アプリケーションを表示するには、「[Azure portalで Azure AD アプリケーションを表示する](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#How-to-view-the-AAD-app-on-the-Azure-portal)」を参照してください。 

## <a name="sso-authentication-concepts"></a>SSO 認証の概念

次の概念は、SSO 認証に役立ちます。

### <a name="working-of-sso-in-teams"></a>Teamsでの SSO の操作

Microsoft Azure Active Directory (Azure AD) でのシングル サインオン (SSO) 認証では、ユーザーがサインイン資格情報を入力する必要がある回数を最小限に抑えるために、認証トークンが自動的に更新されます。 ユーザーがアプリの使用に同意した場合、ユーザーは自動的にサインインするため、別のデバイスで再度同意する必要はありません。

タブとボットTeams SSO サポートのフローが似ています。詳細については、次を参照してください。

1. [タブでのシングル サインオン (SSO) 認証](../tabs/how-to/authentication/auth-aad-sso.md)
2. [Bots でのシングル サインオン (SSO) 認証](../bots/how-to/authentication/auth-aad-sso-bots.md)

### <a name="simplified-sso-with-teamsfx"></a>TeamsFx を使用した SSO の簡略化

TeamsFx は、SSO を使用し、構成がゼロの 1 行のステートメントにクラウド リソースにアクセスすることで、開発者タスクを減らすのに役立ちます。

TeamsFx SDK を使用すると、資格情報を使用して簡単な方法でユーザー認証コードを記述できます。

1. ブラウザー環境のユーザー ID: `TeamsUserCredential` 現在Teamsユーザーの ID を表します。
2. Node.js環境のユーザー ID: `OnBehalfOfUserCredentail` On-Behalf-Of フローと SSO トークンを使用します。
3. Node.js環境のアプリケーション ID: `AppCredential` アプリケーション ID を表します。

TeamsFx SDK の詳細については、次を参照してください。

* [TeamsFx SDK](TeamsFx-SDK.md) または [API リファレンス](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true)
* [Microsoft Teams Framework (TeamsFx) サンプル ギャラリー](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2)

## <a name="see-also"></a>関連項目

* [Teams アプリを構築するためのアカウントを準備する](accounts.md)
