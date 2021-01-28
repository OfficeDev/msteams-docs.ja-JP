---
title: タブの認証フロー
description: タブの認証フローについて説明します
ms.topic: conceptual
keywords: Teams の認証フロー タブ
ms.openlocfilehash: 9505419a6594529bcf8d19a90d029705e573c67b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014587"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>タブの Microsoft Teams 認証フロー

> [!Note]
> モバイル クライアントのタブで認証を機能するには、Teams JavaScript SDK の 1.4.1 バージョン以上を使用している必要があります。
> Teams SDK は認証フロー用に個別のウィンドウを起動するため、samesite 属性を 'Lax' に設定できます。 現在、SameSite=None は Teams デスクトップ クライアントまたは Chrome または Safari の以前のバージョンではサポートされていません。

OAuth 2.0 は、Azure AD および他の多くの ID プロバイダーで使用される認証と承認のオープン標準です。 OAuth 2.0 の基本的な理解は、Teams で認証を操作する場合の前提条件です。 [ここでは、正式な仕様よりも](https://aaronparecki.com/oauth-2-simplified/) 簡単に従える優れた概要 [を示します](https://oauth.net/2/)。 タブとボットの認証フローは少し異なります。タブは Web サイトに非常に似ているため、OAuth 2.0 を直接使用できます。bots are not and must do a few things differently, but the core concepts are identical.

*「Node*[と](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow) [OAuth 2.0](https://oauth.net/2/grant-types/implicit/)の暗黙的な許可の種類を使用して、タブとボットの認証フローの例については、タブの認証フローを開始する」を参照してください。

![タブ認証シーケンス図](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. ユーザーは、タブ構成またはコンテンツ ページのコンテンツを操作します。通常、"サインイン" または "ログイン" というラベルの付いたボタンです。
2. タブは、認証開始ページの URL を作成します。必要に応じて、URL プレースホルダーの情報を使用するか、Teams クライアント SDK メソッドを呼び出して、ユーザーの認証エクスペリエンスを `microsoftTeams.getContext()` 合理化します。 たとえば、Azure AD で認証を行う場合、パラメーターがユーザーの電子メール アドレスに設定されている場合、Azure AD はユーザーのキャッシュされた資格情報を可能な限り使用します。ポップアップが短時間点滅して消えるので、ユーザーが最近サインインした場合でも、ユーザーはサインインする必要がなくなる可能性があります。 `login_hint`
3. 次に、タブは `microsoftTeams.authentication.authenticate()` メソッドを呼び出し、`successCallback` 関数と `failureCallback` 関数を登録します。
4. Teams は、ポップアップ ウィンドウの iframe でスタート ページを開きます。 開始ページは、ランダムなデータを生成し、将来の検証のために保存し、Azure AD などの ID プロバイダーの `state` `/authorize` `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` エンドポイントにリダイレクトします。 独自 `<tenant id>` のテナント ID (context.tid) に置き換えてください。
    * Teams の他のアプリケーション認証フローと同様に、スタート ページは、そのリスト内のドメインと、ログイン後のリダイレクト ページと同じドメイン上にある `validDomains` 必要があります。
    * **重要**: OAuth 2.0 の暗黙的な許可フローは、クロスサイト要求フォージェリ攻撃を防ぐために、一意のセッション データを含む認証要求のパラメーターを呼び出 `state` [します](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。 次の例では、データにランダムに生成された GUID を使用 `state` します。
5. プロバイダーのサイトで、ユーザーはサインインし、タブへのアクセスを許可します。
6. プロバイダーは、アクセス トークンを使用してユーザーをタブの OAuth 2.0 リダイレクト ページに移動します。
7. タブは、戻り値が以前に保存された値と一致することを確認し、呼び出しは手順 3 で登録された関数を呼び出 `state` `microsoftTeams.authentication.notifySuccess()` `successCallback` します。
8. Teams がポップアップ ウィンドウを閉じます。
9. タブは、ユーザーの開始場所に応じて、構成 UI を表示するか、タブのコンテンツを更新または再読み込みします。

## <a name="treat-tab-context-as-hints"></a>タブ コンテキストをヒントとして扱う

タブ コンテキストはユーザーに関する有用な情報を提供しますが、タブ コンテンツの URL への URL パラメーターとして取得するか、Microsoft Teams クライアント SDK の関数を呼び出す場合でも、この情報を使用してユーザーを認証しません。 `microsoftTeams.getContext()` 悪意のあるアクターが独自のパラメーターを使用してタブ コンテンツの URL を呼び出す可能性があります。また、Microsoft Teams を偽装する Web ページが iframe にタブ コンテンツ URL を読み込み、独自のデータを関数に返す可能性があります。 `getContext()` タブ コンテキストでは、ID 関連の情報をヒントとして扱い、使用する前に検証する必要があります。 ポップアップ ページから承認ページに [移動するのメモを参照してください](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)。

## <a name="samples"></a>サンプル

タブ認証プロセスを示すサンプル コードについては、以下を参照してください。

* [Microsoft Teams タブ認証のサンプル (ノード)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Microsoft Teams タブ認証のサンプル (C#)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

## <a name="more-details"></a>詳細情報

Azure Active Directory をターゲットとするタブ認証の詳細な実装チュートリアルについては、以下を参照してください。

* [Microsoft Teams タブでユーザーを認証する](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [サイレント認証](~/tabs/how-to/authentication/auth-silent-AAD.md)
