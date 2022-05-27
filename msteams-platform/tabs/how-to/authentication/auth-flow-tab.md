---
title: タブの認証フロー
description: タブでの認証フロー、Azure AD ごとの OAuth について説明し、コード サンプルを提供します
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams 認証フロー タブ
ms.openlocfilehash: a40a09b025949b36491534a4e8bdda9f523b24df
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756493"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>タブの Microsoft Teams 認証フロー

> [!NOTE]
> モバイル クライアントのタブで認証を機能させるには、少なくとも 1.4.1 バージョンの Microsoft Teams JavaScript SDK を使用していることを確認する必要があります。  
> Teams SDK は、認証フロー用に別のウィンドウを起動します。 `SameSite` 属性を **Lax** に設定します。 Teams デスクトップ クライアントまたは以前のバージョンの Chrome または Safari は、`SameSite`=None をサポートしていません。

OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。 OAuth 2.0 の基本的な解釈は、Teams で認証を操作するための前提条件です。 詳細については、[正式な仕様](https://oauth.net/2/)よりもわかりやすい [簡略化された OAuth2](https://aaronparecki.com/oauth-2-simplified/) を参照してください。 タブとボットの認証フローは異なります。タブは Web サイトに似ているため、OAuth 2.0 を直接使用できます。 ボットではいくつかの操作が異なりますが、コア概念は同じです。

たとえば、Node と [OAuth 2.0 暗黙的な許可の種類](https://oauth.net/2/grant-types/implicit/)を使用するタブとボットの認証フローについては、「[タブの認証フローを開始する](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow)」を参照してください。

> [!NOTE]
> ユーザーに **ログイン** ボタンを表示し、ボタンの `microsoftTeams.authentication.authenticate` 選択に応答して API を呼び出す前に、SDK の初期化が完了するのを待つ必要があります。 初期化が完了したときに呼び出される `microsoftTeams.initialize` API にコールバックを渡すことができます。

![タブ認証シーケンス図](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. ユーザーは、タブ構成またはコンテンツ ページのコンテンツ (通常は **[サインイン]** または **[ログイン]** ボタン) で操作します。
2. このタブは、認証の開始ページの URL を作成します。 オプションで、UR Lプレースホルダーからの情報を使用するか、`microsoftTeams.getContext()` Teams クライアント SDK メソッドを呼び出して、ユーザーの認証エクスペリエンスを合理化します。 たとえば、A Azure AD を使用して認証する場合、パラメーターがユーザーの電子メール アドレスに設定されている場合 `login_hint` 、ユーザーが最近サインインした場合、ユーザーはサインインする必要はありません。 これは、Azure AD がユーザーのキャッシュされた資格情報を使用するためです。 ポップアップ ウィンドウが短い時間表示され、消えます。
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
