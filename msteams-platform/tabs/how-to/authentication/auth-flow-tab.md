---
title: サード パーティの OAuth プロバイダーを使用して認証を有効にする
description: この記事では、タブ、サード パーティの OAuth プロバイダー、Azure AD による OAuth、および認証コード サンプルの Teams 認証フローについて説明します。
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 2edd52d80428e47a8586ec27de4b1595d872df8c
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144251"
---
# <a name="enable-authentication-using-third-party-oauth-provider"></a>サード パーティの OAuth プロバイダーを使用して認証を有効にする

サード パーティの OAuth ID プロバイダー (IdP) を使用して、タブ アプリで認証を有効にすることができます。 このメソッドでは、アプリ ユーザー ID が検証され、Azure AD、Google、Facebook、GitHub、その他のプロバイダーなどの OAuth IdP によってアクセスが許可されました。 IdP との信頼関係を構成する必要があり、またアプリ ユーザーもそれに登録する必要があります。

> [!NOTE]
> モバイル クライアントのタブで認証を機能させるには、少なくとも 1.4.1 バージョンの Microsoft Teams JavaScript SDK を使用していることを確認する必要があります。  
> Teams SDK は、認証フロー用に別のウィンドウを起動します。 `SameSite` 属性を **Lax** に設定します。 Teams デスクトップ クライアントまたは以前のバージョンの Chrome または Safari は、`SameSite`=None をサポートしていません。

## <a name="use-oauth-idp-to-enable-authentication"></a>OAuth IdP を使用して認証を有効にする

OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。 OAuth 2.0 の基本的な解釈は、Teams で認証を操作するための前提条件です。 詳細については、[正式な仕様](https://oauth.net/2/)よりもわかりやすい [簡略化された OAuth2](https://aaronparecki.com/oauth-2-simplified/) を参照してください。 タブとボットの認証フローは異なります。タブは Web サイトに似ているため、OAuth 2.0 を直接使用できます。 ボットではいくつかの操作が異なりますが、コア概念は同じです。

たとえば、Node と [OAuth 2.0 暗黙的な許可の種類](https://oauth.net/2/grant-types/implicit/)を使用するタブとボットの認証フローについては、「[タブの認証フローを開始する](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow)」を参照してください。

このセクションでは、タブ アプリで認証を有効にするためのサード パーティの OAuth プロバイダーの例として Azure AD を使用します。

> [!NOTE]
> ユーザーに **ログイン** ボタンを表示し、ボタンの `microsoftTeams.authentication.authenticate` 選択に応答して API を呼び出す前に、SDK の初期化が完了するのを待つ必要があります。 初期化が完了したときに呼び出される `microsoftTeams.initialize` API にコールバックを渡すことができます。

![タブ認証シーケンス図](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. ユーザーは、タブ構成またはコンテンツ ページのコンテンツ (通常は **[サインイン]** または **[ログイン]** ボタン) で操作します。
2. このタブは、認証の開始ページの URL を作成します。 オプションで、UR Lプレースホルダーからの情報を使用するか、`microsoftTeams.getContext()` Teams クライアント SDK メソッドを呼び出して、ユーザーの認証エクスペリエンスを合理化します。 たとえば、Azure AD で認証するときに、`login_hint` パラメーターがユーザーの電子メール アドレスに設定されている場合、ユーザーが最近サインインしたことがあれば、サインインする必要がありません。 これは、Azure AD がユーザーのキャッシュされた資格情報を使用するためです。 ポップアップ ウィンドウが短い時間表示され、消えます。
3. 次に、タブは `microsoftTeams.authentication.authenticate()` メソッドを呼び出し、`successCallback` 関数と `failureCallback` 関数を登録します。
4. Teams は、ポップアップ ウィンドウの iframe で開始ページを開きます。 スタート ページはランダムな `state` データを生成し、将来の検証のために保存し、AzureAD の `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` などの ID プロバイダーの `/authorize` エンドポイントにリダイレクトします。 `<tenant id>` を context.tid である独自のテナント ID に置き換えます。
Teams 内の他のアプリケーション認証フローと同様に、開始ページは、その `validDomains` リストにあるドメイン上にあり、ログイン後のリダイレクト ページと同じドメイン上にある必要があります。

    > [!NOTE]
    > OAuth 2.0 の暗黙的な許可フローでは、認証リクエストに `state` パラメータが必要です。このパラメータには、[クロス サイト リクエスト フォージェリ攻撃](https://en.wikipedia.org/wiki/Cross-site_request_forgery)を防ぐための一意のセッションデータが含まれています。 例では、`state` データに対してランダムに生成された GUID を使用しています。

5. プロバイダーのサイトで、ユーザーはサインインし、タブへのアクセスを許可します。
6. ID プロバイダーは、アクセス トークンを使用してユーザーをタブの OAuth 2.0 リダイレクト ページにリダイレクトします。
7. タブは、返された `state` 値が以前に保存された値と一致することを確認し、`microsoftTeams.authentication.notifySuccess()` を呼び出します。次に、手順 3 で登録された `successCallback` 関数を呼び出します。
8. Microsoft Teams は、ポップアップ ウィンドウを終了します。
9. タブは、ユーザーが開始した場所に基づいて、構成 UI を表示するか、タブのコンテンツを更新または再読み込みします。

> [!NOTE]
> アプリケーションが SAML SSO をサポートしている場合、タブ SSO で生成された JWT トークンはサポートされていないため使用できません。

## <a name="treat-tab-context-as-hints"></a>タブ コンテキストをヒントとして扱う

タブ コンテキストはユーザーに関する有用な情報を提供しますが、この情報を使用してユーザーを認証しないでください。 タブ コンテンツ URL の URL パラメーターとして情報を取得したり、Microsoft Teams クライアント SDK で `microsoftTeams.getContext()` 関数を呼び出したりしても、ユーザーを認証してください。 悪意のあるアクターは、独自のパラメーターを使用してタブ コンテンツ URL を呼び出すことができます。 アクターは、偽装 Microsoft Teams Web ページを呼び出して、タブ コンテンツ URL を iframe に読み込み、独自のデータを `getContext()` 関数に返すこともできます。 使用する前に、タブ コンテキスト内の ID 関連情報をヒントとして扱い、検証する必要があります。 [ポップアップページから認証ページに移動する](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page)際の注意事項を参照してください。

## <a name="code-sample"></a>コード サンプル

タブ認証プロセスを示すサンプル コード:

| **サンプルの名前** | **説明** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Teams タブ認証 | Azure AD を使用したタブの認証プロセス。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="see-also"></a>関連項目

Azure AD を使用したタブ認証の詳細な実装については、次を参照してください。

* [Teams タブでユーザーを認証する](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [サイレント認証](~/tabs/how-to/authentication/auth-silent-AAD.md)
