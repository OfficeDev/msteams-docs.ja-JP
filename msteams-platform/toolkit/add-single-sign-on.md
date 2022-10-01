---
title: Teams アプリにシングル サインオンを追加する
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit のシングル サインオン (SSO) を追加する方法、SSO のサポートを有効にする方法、SSO を使用するようにアプリケーションを更新する方法について説明します
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 9c221b0903d4541c4b0601e14ea347680140dfb9
ms.sourcegitcommit: 3aaccc48906fc6f6fbf79916af5664bf55537250
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2022
ms.locfileid: "68295964"
---
# <a name="add-single-sign-on-to-teams-app"></a>Teams アプリにシングル サインオンを追加する

Microsoft Teams には、サインインしている Teams ユーザー トークンを取得して Microsoft Graph やその他の API にアクセスするためのシングル サインオン機能がアプリケーションに用意されています。 Teams Toolkit は、Azure AD フローの一部と、いくつかの単純な API の背後にある統合を抽象化することで、対話を容易にします。 これにより、Teams アプリケーションにシングル サインオン (SSO) 機能を簡単に追加できます。

チャット、チーム、またはチャネルでユーザーと対話するアプリケーションの場合、SSO はアダプティブ カードとしてマニフェストされ、ユーザーは Azure AD 同意フローを呼び出すために対話できます。

## <a name="enable-sso-support"></a>SSO サポートを有効にする

Teams Toolkit は、次の Teams 機能に SSO を追加するのに役立ちます。

* Tab
* Bot
* 通知ボット: サーバーを修正する
* コマンド ボット

### <a name="add-sso-using-visual-studio-code"></a>Visual Studio Code を使用して SSO を追加する

次の手順は、Visual Studio Code で Teams Toolkit を使用して SSO を追加するのに役立ちます

1. **Microsoft Visual Studio Code** を開きます。
2. 左側のナビゲーション バーから [Teams Toolkit :::image type="content" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png" alt-text="sso add sidebar"::: ] を選択します。
3. **[開発**] で [**機能の追加]** を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-add features.png" alt-text="sso 機能の追加":::

    * コマンド パレットを開き、[**Teams: 機能の追加]** を選択することもできます。

4. **[シングル サインオン**] を選択します。

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-select features.png" alt-text="sso select":::

### <a name="add-sso-using-teamsfx-cli"></a>TeamsFx CLI を使用して SSO を追加する

**プロジェクトのルート ディレクトリ** でコマンドを実行`teamsfx add sso`できます

> [!Note]
> この機能により、既存のすべての適用可能な機能に対して SSO が有効になります。 後でプロジェクトに機能を追加する場合は、同じ手順に従って SSO を有効にします。

## <a name="customize-your-project-using-teams-toolkit"></a>Teams Toolkit を使用してプロジェクトをカスタマイズする

次の表に、Teams Toolkit がプロジェクトに加える変更の一覧を示します。

   |**Type**|**ファイル**|**用途**|
   |--------|--------|-----------|
   |Create|`aad.template.json` 下 `template/appPackage`|Azure AD アプリケーション マニフェストは、Azure AD アプリを表します。 `template/appPackage` は、ローカル デバッグまたはプロビジョニング ステージ中に Azure AD アプリを登録するのに役立ちます。|
   |変更|`manifest.template.json` 下 `template/appPackage`|Teams アプリ マニフェスト `webApplicationInfo` テンプレートにオブジェクトが追加されます。 Teams では、SSO を有効にするには、このフィールドが必要です。 この変更は、ローカル デバッグまたはプロビジョニングをトリガーするときに有効です。|
   |Create|`auth/tab`|参照コード、認証リダイレクト ページ、および `README.md` ファイルは、タブ プロジェクトのこのパスに生成されます。|
   |Create|`auth/bot`|このパスでは、ボット プロジェクトの参照コード、認証リダイレクト ページ、ファイル `README.md` が生成されます。|

> [!Note]
> SSO を追加することで、ローカル デバッグをトリガーするまで、Teams Toolkit はクラウド内の何も変更しません。 コードを更新して、SSO がプロジェクトで動作していることを確認します。

## <a name="update-your-application-to-use-sso"></a>SSO を使用するようにアプリケーションを更新する

次の手順は、アプリケーションで SSO を有効にするのに役立ちます。

> [!NOTE]
> これらの変更は、スキャフォールディングするテンプレートに基づいています。

---
<br>
<br><details>
<summary><b>Tab プロジェクト </b></summary>

1. フォルダー内の`auth/public`コピー`auth-start.html`と `auth-end.htm`** を .`tabs/public/` Teams Toolkit は、Azure AD のリダイレクト フローに対して、これら 2 つのエンドポイントを Azure AD に登録します。

2. [コピー先] の下にある`auth/tab`フォルダーをコピー`sso`します`tabs/src/sso/`。

    * `InitTeamsFx`: ファイルは TeamsFx SDK を初期化し、SDK の初期化後にコンポーネントを開く `GetUserProfile` 関数を実装します。

    * `GetUserProfile`: ファイルは、Microsoft Graph APIを呼び出してユーザー情報を取得する関数を実装します

3. で実行 `npm install @microsoft/teamsfx-react` します `tabs/`。

4. インポート`InitTeamsFx`する次の行を`tabs/src/components/sample/Welcome.tsx`追加します。

    ```Bash

    import { InitTeamsFx } from "../../sso/InitTeamsFx";

    ```

5. 置換前の行

   `<AddSSO />` を使用 `<InitTeamsFx />` して、コンポーネントを `AddSso` コンポーネントに `InitTeamsFx` 置き換えます。

</details>
<details>
<summary><b>ボット プロジェクト </b></summary>

#### <a name="set-up-the-azure-ad-redirects"></a>Azure AD リダイレクトを設定する

1. フォルダーを移動します`auth/bot/public``bot/src`。 このフォルダーには、ボット アプリケーションがホストする HTML ページが含まれています。 Azure AD でシングル サインオン フローが開始されると、ユーザーは HTML ページにリダイレクトされます。
1. `bot/src/index` HTML ページに適切な`restify`ルートを追加するように変更します。

    ```ts
    const path = require("path");

    server.get(
        "/auth-*.html",
        restify.plugins.serveStatic({
            directory: path.join(__dirname, "public"),
        })
    );
    ```

#### <a name="update-your-app"></a>アプリを更新する

SSO コマンド ハンドラー `ProfileSsoCommandHandler` は、Azure AD トークンを使用して Microsoft Graph を呼び出します。 このトークンは、ログインしている Teams ユーザー トークンを使用して取得されます。 フローは、必要に応じて同意ダイアログを表示するダイアログにまとめされます。

1. フォルダーの下の`auth/bot/sso`ファイルを移動`profileSsoCommandHandler`します`bot/src`。 `ProfileSsoCommandHandler` class は、SSO トークンを使用してユーザー情報を取得し、このメソッドに従って独自の SSO コマンド ハンドラーを作成するための SSO コマンド ハンドラーです。
1. ファイルを開き `package.json` 、teamsfx SDK バージョン>= 1.2.0 であることを確認します
1. フォルダー内で`bot`コマンドを`npm install isomorphic-fetch --save`実行します。
1. ts スクリプトの場合は、フォルダー内で`bot`コマンドを`npm install copyfiles --save-dev`実行し、次の行を次の行に`package.json`置き換えます。

    ```json
    "build": "tsc --build && shx cp -r ./src/adaptiveCards ./lib/src",
    ```

     および 

    ```json
    "build": "tsc --build && shx cp -r ./src/adaptiveCards ./lib/src && copyfiles src/public/*.html lib/",
    ```

    これにより、ボット プロジェクトをビルドするときに認証リダイレクトに使用される HTML ページがコピーされます。

1. SSO 同意フローを機能させるには、ファイル内の次のコードを `bot/src/index` 置き換えます。

    ```ts
    server.post("/api/messages", async (req, res) => {
        await commandBot.requestHandler(req, res);
    });
    ```

     および 

    ```ts
    server.post("/api/messages", async (req, res) => {
        await commandBot.requestHandler(req, res).catch((err) => {
            // Error message including "412" means it is waiting for user's consent, which is a normal process of SSO, sholdn't throw this error.
            if (!err.message.includes("412")) {
                throw err;
            }
        });
    });
    ```

1. たとえば`bot/src/internal/initialize`、SSO 構成と SSO コマンド ハンドラーを追加するためのオプション`ConversationBot`を置き換えます。

    ```ts
    export const commandBot = new ConversationBot({
        ...
        command: {
            enabled: true,
            commands: [new HelloWorldCommandHandler()],
        },
    });
    ```

     および 

    ```ts
    import { ProfileSsoCommandHandler } from "../profileSsoCommandHandler";

    export const commandBot = new ConversationBot({
        ...
        // To learn more about ssoConfig, please refer teamsfx sdk document: https://docs.microsoft.com/microsoftteams/platform/toolkit/teamsfx-sdk
        ssoConfig: {
            aad :{
                scopes:["User.Read"],
            },
        },
        command: {
            enabled: true,
            commands: [new HelloWorldCommandHandler() ],
            ssoCommands: [new ProfileSsoCommandHandler()],
        },
    });
    ```

1. Teams アプリ マニフェストにコマンドを登録します。 ボットの下に`commands`次の行を開`templates/appPackage/manifest.template.json`き、`commandLists`追加します。

    ```json
    {
        "title": "profile",
        "description": "Show user profile using Single Sign On feature"
    }
    ```

#### <a name="add-a-new-sso-command-to-the-bot-optional"></a>ボットに新しい SSO コマンドを追加する (省略可能)

プロジェクトに SSO を正常に追加したら、新しい SSO コマンドを追加できます。

1. 次のような`photoSsoCommandHandler.ts``photoSsoCommandHandler.js`新しいファイルを作成し、独自の `bot/src/` SSO コマンド ハンドラーを追加して、Graph APIを呼び出します。

    ```TypeScript
    // for TypeScript:
    import { Activity, TurnContext, ActivityTypes } from "botbuilder";
    import "isomorphic-fetch";
    import {
        CommandMessage,
        TriggerPatterns,
        TeamsFx,
        createMicrosoftGraphClient,
        TeamsFxBotSsoCommandHandler,
        TeamsBotSsoPromptTokenResponse,
    } from "@microsoft/teamsfx";

    export class PhotoSsoCommandHandler implements TeamsFxBotSsoCommandHandler {
        triggerPatterns: TriggerPatterns = "photo";

        async handleCommandReceived(
            context: TurnContext,
            message: CommandMessage,
            tokenResponse: TeamsBotSsoPromptTokenResponse,
        ): Promise<string | Partial<Activity> | void> {
            await context.sendActivity("Retrieving user information from Microsoft Graph ...");

            const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

            const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);

            let photoUrl = "";
            try {
                const photo = await graphClient.api("/me/photo/$value").get();
                const arrayBuffer = await photo.arrayBuffer();
                const buffer=Buffer.from(arrayBuffer, 'binary');
                photoUrl = "data:image/png;base64," + buffer.toString("base64");
            } catch {
                // Could not fetch photo from user's profile, return empty string as placeholder.
            }
            if (photoUrl) {
                const photoMessage: Partial<Activity> = {
                    type: ActivityTypes.Message, 
                    text: 'This is your photo:', 
                    attachments: [
                        {
                            name: 'photo.png',
                            contentType: 'image/png',
                            contentUrl: photoUrl
                        }
                    ]
                };
                return photoMessage;
            } else {
                return "Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.";
            }
        }
    }
    ```

    ```javascript
    // for JavaScript:
    const { ActivityTypes } = require("botbuilder");
    require("isomorphic-fetch");
    const { createMicrosoftGraphClient, TeamsFx } = require("@microsoft/teamsfx");

    class PhotoSsoCommandHandler {
        triggerPatterns = "photo";

        async handleCommandReceived(context, message, tokenResponse) {
            await context.sendActivity("Retrieving user information from Microsoft Graph ...");

            const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

            const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
        
            let photoUrl = "";
            try {
                const photo = await graphClient.api("/me/photo/$value").get();
                const arrayBuffer = await photo.arrayBuffer();
                const buffer=Buffer.from(arrayBuffer, 'binary');
                photoUrl = "data:image/png;base64," + buffer.toString("base64");
            } catch {
            // Could not fetch photo from user's profile, return empty string as placeholder.
            }
            if (photoUrl) {
                const photoMessage = {
                    type: ActivityTypes.Message, 
                    text: 'This is your photo:', 
                    attachments: [
                        {
                            name: 'photo.png',
                            contentType: 'image/png',
                            contentUrl: photoUrl
                        }
                    ]
                };
                return photoMessage;
            } else {
                return "Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.";
            }
        }
    }

    module.exports = {
        PhotoSsoCommandHandler,
    };

    ```

1. 配列`bot/src/internal/initialize.ts`にインスタンスを追加`PhotoSsoCommandHandler`します`ssoCommands`。

    ```ts
    // for TypeScript:
    import { PhotoSsoCommandHandler } from "../photoSsoCommandHandler";

    export const commandBot = new ConversationBot({
        ...
        command: {
            ...
            ssoCommands: [new ProfileSsoCommandHandler(), new PhotoSsoCommandHandler()],
        },
    });
    ```

    ```javascript
    // for JavaScript:
    ...
    const { PhotoSsoCommandHandler } = require("../photoSsoCommandHandler");

    const commandBot = new ConversationBot({
        ...
        command: {
            ...
            ssoCommands: [new ProfileSsoCommandHandler(), new PhotoSsoCommandHandler()]
        },
    });
    ...

    ```

1. Teams アプリ マニフェストにコマンドを登録します。 ボットの下に`commands`次の行を開`templates/appPackage/manifest.template.json`き、`commandLists`追加します。

    ```JSON

    {
        "title": "photo",
        "description": "Show user photo using Single Sign On feature"
    }

    ```

</details>
<br>

## <a name="debug-your-application"></a>アプリケーションをデバッグする

F5 キーを押してアプリケーションをデバッグします。 Teams Toolkit では、Azure AD マニフェスト ファイルを使用して、SSO 用の Azure AD アプリケーションを登録します。 Teams Toolkit のローカル デバッグ機能については、「 [Teams アプリをローカルでデバッグする](debug-local.md)」を参照してください。

## <a name="customize-azure-ad-application-registration"></a>Azure AD アプリケーションの登録をカスタマイズする

[Azure AD アプリ マニフェスト](/azure/active-directory/develop/reference-app-manifest)を使用すると、アプリケーション登録のさまざまな側面をカスタマイズできます。 必要に応じてマニフェストを更新できます。 目的の API にアクセスするための API アクセス許可をさらに含める必要がある場合は、目的の API [にアクセスするための API アクセス許可](https://github.com/OfficeDev/TeamsFx/wiki/#customize-aad-manifest-template)に関するページを参照してください。
Azure portalで Azure AD アプリケーションを表示するには、「Azure portal[で Azure AD アプリケーションを表示する](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#How-to-view-the-AAD-app-on-the-Azure-portal)」を参照してください。

## <a name="sso-authentication-concepts"></a>SSO 認証の概念

次の概念は、SSO 認証に役立ちます。

### <a name="working-of-sso-in-teams"></a>Teams での SSO の操作

Microsoft Azure Active Directory (Azure AD) でのシングル サインオン (SSO) 認証では、ユーザーがサインイン資格情報を入力する必要がある回数を最小限に抑えるために、認証トークンが自動的に更新されます。 ユーザーがアプリの使用に同意した場合、ユーザーは自動的にサインインするため、別のデバイスで再度同意する必要はありません。

Teams のタブとボットには、SSO サポートのフローが似ています。詳細については、次を参照してください。

1. [タブでのシングル サインオン (SSO) 認証](../tabs/how-to/authentication/tab-sso-overview.md)
2. [Bots でのシングル サインオン (SSO) 認証](../bots/how-to/authentication/auth-aad-sso-bots.md)

### <a name="simplified-sso-with-teamsfx"></a>TeamsFx を使用した SSO の簡略化

TeamsFx は、SSO を使用し、構成がゼロの 1 行のステートメントにクラウド リソースにアクセスすることで、開発者タスクを減らすのに役立ちます。

TeamsFx SDK を使用すると、資格情報を使用して簡単な方法でユーザー認証コードを記述できます。

1. ブラウザー環境のユーザー ID: `TeamsUserCredential` Teams の現在のユーザーの ID を表します。
2. Node.js環境のユーザー ID: `OnBehalfOfUserCredential` On-Behalf-Of フローと SSO トークンを使用します。
3. Node.js環境のアプリケーション ID: `AppCredential` アプリケーション ID を表します。

TeamsFx SDK の詳細については、次を参照してください。

* [TeamsFx SDK](TeamsFx-SDK.md) または [API リファレンス](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true)
* [Microsoft Teams Framework (TeamsFx) サンプル ギャラリー](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2)

## <a name="see-also"></a>関連項目

* [Teams アプリを作成するための前提条件](tools-prerequisites.md)
