---
title: Teams で SSO を使用したタブの認証のトラブルシューティング
description: Teams でのシングル サインオン (SSO) 認証の問題と、タブ アプリでシングル サインオン (SSO) を使用する方法のトラブルシューティングを行います。
ms.topic: how-to
ms.localizationpriority: high
keywords: Teams 認証タブ Microsoft Azure Active Directory (Azure AD) SSO エラーに関する質問
ms.openlocfilehash: 8396b42c217ea58a0a4709e1dbd8580da32da991
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586897"
---
# <a name="troubleshoot-sso-authentication-in-teams"></a>Teams での SSO 認証のトラブルシューティング

SSO に関する問題と質問の一覧と、それらを修正する方法です。
<br>

## <a name="support-for-microsoft-graph"></a>Microsoft Graph のサポート

<br>
<details>
<summary>1. Graph API は Postman で機能しますか?</summary>
<br>
Microsoft Graph API は Microsoft Graph Postman のコレクションで使用できます。

詳細については、「[Microsoft Graph API で Postman を使用する](/graph/use-postman)」をご覧ください。
</details>
<br>
<details>
<summary>2. Graph API は Microsoft Graph エクスプローラーで機能しますか?</summary>
<br>
はい、Graph API は Microsoft Graph エクスプローラーで機能します。

詳細については、「[Graph エクスプローラー](https://developer.microsoft.com/graph/graph-explorer)」を参照してください。

</details>
<br>

## <a name="error-messages-and-how-to-handle-them"></a>エラー メッセージとその処理方法

<br>
<details>
<summary>1. エラー: 同意がありません。</summary>
<br>
Azure AD は、Microsoft Graph のリソースへのアクセス要求を受信すると、ユーザー (またはテナント管理者) がこのリソースに対する同意があるかどうかを確認します。 ユーザーまたは管理者からの同意の記録がない場合、Azure AD は Web サービスにエラー メッセージを送信します。

コードでは、エラーを処理する方法 (たとえば、403 Forbidden 応答の本文にて) をクライアントに指示する必要があります:

- タブ アプリに管理者のみが同意できる Microsoft Graph スコープが必要な場合は、コードでエラーを生成する必要があります。
- 唯一必要なスコープに対して同意できるのがユーザーである場合は、コードはユーザー認証の代替システムにフォールバックする必要があります。

</details>
<br>
<details>
<summary>2. エラー: スコープ (アクセス許可) がありません。</summary>
<br>
このエラーは、開発中にのみ発生します。

このエラーを処理するには、サーバー側のコードからクライアントに 403 Forbidden 応答を送信する必要があります。 そのエラーをコンソールに記録するか、ログに記録する必要があります。
</details>
<br>
<details>
<summary>3. エラー: Microsoft Graph のアクセス トークンの対象ユーザーが無効です。</summary>
<br>
サーバー側のコードは、クライアントに 403 Forbidden 応答を送信して、ユーザーにメッセージを表示する必要があります。 また、エラーをコンソールに記録するか、ログに記録することをお勧めします。
</details>
<br>
<details>
<summary>4. エラー: ホスト名は、既に所有されているドメインに基づいていてはなりません。</summary>
<br>
このエラーは、次の 2 つのシナリオのいずれかで発生します:

1. カスタム ドメインは Azure AD に追加されていません。 カスタム ドメインを Azure AD に追加して登録するには、 [Azure AD にカスタム ドメイン名を追加する](/azure/active-directory/fundamentals/add-custom-domain) の手順に従い、その後手順通りに [アクセス トークンのスコープを](tab-sso-register-aad.md#configure-scope-for-access-token) をもう一度構成します。
1. Microsoft 365 テナントで管理者資格情報を使用してサインインしていません。 管理者として Microsoft 365 にサインインします。

</details>
<br>
<details>
<summary>5. エラー: 返されたアクセス トークンでユーザー プリンシパル名 (UPN) が受信されていません。</summary>
<br>
AZURE AD では、オプションの要求として UPN を追加できます。

詳細については、「[アプリにオプションの要求を提供する](/azure/active-directory/develop/active-directory-optional-claims)」と「[アクセス トークン](/azure/active-directory/develop/access-tokens)」を参照してください。
</details>
<br>
<details>
<summary>6. エラー: Teams SDK エラー: resourceDisabled。</summary>
<br>
このエラーを回避するには、アプリケーション ID URI が Azure AD アプリの登録と Teams クライエントで正しく構成されていることを確認してください。

アプリケーション ID URI の詳細については、「[API を公開するには](tab-sso-register-aad.md#to-expose-an-api)」を参照してください。

</details>
<br>

<details>
<summary>7. エラー: タブ アプリを実行するときの一般的なエラー。</summary>
<br>
Azure AD で行われたアプリ構成の中、 1 つ以上が正しくない場合、一般的なエラーが表示されることがあります。 このエラーを解決するには、コードで構成されたアプリの詳細と Teams マニフェストが Azure AD の値と一致するかどうかを確認します。

次の図は、Azure AD で構成されたアプリの詳細の例を示しています。

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/azure-app-details.png" alt-text="Azure AD のアプリ構成値":::

Azure AD、クライアント側コード、Teams アプリ マニフェストの間で、次の値が一致しているかを確認します:

- **アプリ ID**: Azure AD で生成したアプリ ID は、コードと Teams マニフェスト ファイルで同じである必要があります。 Teams マニフェストのアプリ ID が Azure AD の **アプリケーション (クライアント) ID** と一致するかどうかを確認します。

- **アプリ シークレット**: アプリのバックエンドで構成されたアプリ シークレットは、Azure AD の **クライアント資格情報** と一致する必要があります。
    クライアント シークレットの有効期限が切れているかどうかも確認する必要があります。

- **アプリケーション ID URI**: コードと Teams アプリ マニフェスト ファイル内のアプリ ID URI は、Azure AD の **アプリケーション ID URI** と一致する必要があります。

- **アプリのアクセス許可**: スコープで定義したアクセス許可がアプリの要件に従っているかどうかを確認します。 そうである場合は、アクセス トークンでユーザーに付与されたかどうかを確認します。

- **管理者の同意**: スコープに管理者の同意が必要な場合は、特定のスコープに対してユーザーに同意が付与されているかどうかを確認します。

さらに、タブ アプリに送信されたアクセス トークンを調べて、次の値が正しいかどうかを確認します:

- **対象ユーザー (aud)**: トークン内のアプリ ID が Azure AD で指定されている正しいものかどうかを確認します。
- **テナント ID (tid)**: トークンに記載されているテナントが正しいかどうかを確認します。
- **ユーザー ID (preferred_username)**: ユーザー ID が、現在のユーザーがアクセスしようとするスコープのアクセス トークン要求のユーザー名と一致するかどうかを確認します。
- **スコープ (scp)**: アクセス トークンが要求されるスコープが正しく、Azure AD で定義されているかどうかを確認します。
- **Azure AD バージョン 1.0 または 2.0 (ver)**: Azure AD のバージョンが正しいかどうかを確認します。

[JWT](https://jwt.ms) を使用してトークンを検査できます。

</details>
