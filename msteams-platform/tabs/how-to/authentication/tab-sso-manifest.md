---
title: タブの SSO を有効にするためのマニフェストを更新する
description: タブの SSO を有効にするためのマニフェストの更新について説明します
ms.topic: how-to
ms.localizationpriority: high
keywords: Teams 認証タブ Microsoft Azure Active Directory (Azure AD) Graph API
ms.openlocfilehash: c4e558debe5aff41ad8d6ce76ba952b6d607cd24
ms.sourcegitcommit: 07f41abbeb1572a306a789485953c5588d65051e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2022
ms.locfileid: "66658964"
---
# <a name="update-manifest-for-sso-and-preview-app"></a>SSO 用のマニフェストを更新しアプリをプレビューする

Teams アプリ マニフェストを更新する前に、タブ アプリで SSO を有効にするコードを構成していることを確認してください。

> [!div class="nextstepaction"]
> [コードを構成する](tab-sso-code.md)

Azure AD にタブ アプリを登録し、アプリ ID を取得しました。 また、アクセス トークンを呼び出して `getAuthToken()` 処理するようにコードを構成しました。 ここで、Teams アプリ マニフェストを更新して、タブ アプリの SSO を有効にする必要があります。 Teams アプリ マニフェストは、アプリがどのように Teams に統合されるかを説明します。

## <a name="webapplicationinfo-property"></a>webApplicationInfo プロパティ

Teams アプリ マニフェスト ファイルで `webApplicationInfo` プロパティを構成します。 このプロパティがアプリの SSO を有効にして、アプリ ユーザーがタブ アプリにシームレスにアクセスできるようになります。

&nbsp;&nbsp;:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-manifest.png" alt-text="Teams アプリ マニフェストの構成":::

`webApplicationInfo` には 2 つの要素があります、`id` および `resource`。

| 要素 | 説明 |
| --- | --- |
| id | Azure AD で作成したアプリ ID (GUID) を入力します。 |
| resource | スコープの作成時に Azure AD で作成したアプリのサブドメイン URI とアプリケーション ID URI を入力します。 これを **Azure AD** > **[API の公開]** セクションからコピーできます。 |

> [!NOTE]
> `webApplicationInfo` プロパティを実装するには、マニフェスト バージョン 1.5 以上を使用します。

Azure AD に登録したアプリケーション ID URI は、公開した API のスコープで構成されます。 `getAuthToken()` を使用した認証要求が Teams アプリ マニフェストで指定されたドメインからのものであることを確認するために、アプリのサブドメイン URI `resource` を構成します。

詳細については、「[webApplicationInfo](../../../resources/schema/manifest-schema.md#webapplicationinfo)」を参照してください。

## <a name="to-configure-teams-app-manifest"></a>Teams アプリ マニフェストを構成するには

1. タブ アプリ プロジェクトを開きます。
2. マニフェスト フォルダーを開きます。

  > [!NOTE]
  >
  > - マニフェスト フォルダーは、プロジェクトのルートにある必要があります。 詳細については、「[Microsoft Teams アプリ パッケージを作成する](../../../concepts/build-and-test/apps-package.md)」を参照してください。
  > - manifest.json を作成する方法の詳細については、「[参照: Microsoft Teams のマニフェスト スキーマ](../../../resources/schema/manifest-schema.md)」を参照してください。

1. manifest.json ファイルを開く
1. 次のコード スニペットをマニフェスト ファイルに追加して、新しいプロパティを追加します:

    ```json
    "webApplicationInfo": {
    "id": "{Azure AD AppId}",
    "resource": "api://{Subdomain}.example.com/{Azure AD AppId}"
    }
    ```

    ここで、
    - {Azure AD AppId} は、Azure AD にアプリを登録したときに作成したアプリ ID です。 これは GUID です。
    - {{Subdomain}.app ID URI} は、Azure AD でスコープを作成するときに登録したアプリケーション ID URI です。

4. **id** プロパティで Azure AD からのアプリ ID を更新します。
5. 次のプロパティでサブドメイン URL を更新します:
   1. `contentUrl`
   2. `configurationUrl`
   3. `validDomains`
6. Teams アプリ マニフェスト ファイルを保存します。

<br>
<details>
<summary>更新後のアプリ マニフェストの例です。</summary>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
  "manifestVersion": "1.11",
  "version": "1.0.0",
  "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
  "packageName": "com.contoso.teamsauthsso",
  "developer": {
    "name": "Microsoft",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com/privacy",
    "termsOfUseUrl": "https://www.microsoft.com/termsofuse"
  },
  "name": {
    "short": "Teams Auth SSO",
    "full": "Teams Auth SSO"
  },
  "description": {
    "short": "Teams Auth SSO app",
    "full": "The Teams Auth SSO app"
  },
  "icons": {
    "outline": "outline.png",
    "color": "color.png"
  },
  "accentColor": "#60A18E",
  "staticTabs": [
    {
      "entityId": "auth",
      "name": "Auth",
      "contentUrl": "https://contoso.com/Home/Index",
      "scopes": [ "personal" ]
    }
  ],
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/Home/Configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team"
      ]
    }
  ],
  "permissions": [ "identity", "messageTeamMembers" ],
  "validDomains": [
    "contoso.com"
  ],
  "webApplicationInfo": {
    "id": "bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c",
    "resource": "api://contoso.com/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c"
  }
}
```

</details>

> [!NOTE]
> デバッグ中に、ngrok を使用して Azure AD でアプリをテストできます。 その場合は、サブドメイン `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` を ngrok URL に置き換える必要があります。 ngrok サブドメインが変更されるたびに URL を更新する必要があります。たとえば、api://23c3-103-50-148-128.ngrok.io/bccfbe67-e08b-4ec1-a7fd-e0aaf41a097c。

## <a name="sideload-and-preview-in-teams"></a>Teams でのサイドロードとプレビュー

Azure AD、アプリ コード、Teams マニフェスト ファイルで SSO を有効にするようにタブ アプリを構成しました。 Teams でタブ アプリをサイドロードし、Teams 環境でプレビューできるようになりました。

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-flow.png" alt-text="SSO アプリ":::

Teams でタブ アプリをプレビューするには:

1. アプリ パッケージを作成します。

   アプリ パッケージは、アプリ マニフェストとアプリ アイコンを含む ZIP ファイルです。

1. Teams を開きます。

1. **[アプリ]** > **[アプリの管理]** > **[アプリのアップロード]** を選択します。

    アプリをアップロードするオプションが表示されます。

1. **[カスタム アプリのアップロード]** を選択して、タブ アプリを Teams にサイドロードします。

1. アプリ パッケージの ZIP ファイルを選択し、**[追加]** を選択します。

    タブ アプリがサイドロードされ、ダイアログが表示され、必要になる可能性がある追加のアクセス許可を通知します。

1. **[続行]** を選択します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-consent.png" alt-text="必要な追加のアクセス許可について通知する [Teams] のダイアログ ボックス":::

    Azure AD の同意ダイアログが表示されます。

1. Open-ID スコープに同意するには、**[承諾する]** を選択します。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/aad-sso-consent.png" alt-text="Azure AD の同意ダイアログのスクリーンショット":::

    Teams によってタブ アプリが開き、それを使用できます。

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/teams-sso-app.png" alt-text="SSO が有効になっている Teams タブ アプリの例":::

    おめでとうございます! タブ アプリの SSO を有効にしました。

## <a name="see-also"></a>関連項目

- [Microsoft Teams のマニフェスト スキーマ](../../../resources/schema/manifest-schema.md)
- [マニフェスト スキーマの形式](https://developer.microsoft.com/json-schemas/teams/v1.12/MicrosoftTeams.schema.json)
- [Microsoft Teams アプリ パッケージを作成する](../../../concepts/build-and-test/apps-package.md)
