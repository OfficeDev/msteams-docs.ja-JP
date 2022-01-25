---
title: タブの認証フロー
description: タブの認証フローについて説明し、OAuth Azure ADコード サンプルを提供します。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams 認証フロー タブ
ms.openlocfilehash: 64a31cd13f05211234bc30d22a89005eb2b91880
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212511"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Microsoft Teamsの認証フロー

> [!NOTE]
> モバイル クライアントでタブで認証を機能するには、JavaScript SDK の 1.4.1 以上のバージョンを使用Microsoft Teams必要があります。  
> Teams SDK は、認証フロー用に個別のウィンドウを起動します。 属性を `SameSite` **Lax に設定します**。 Teamsクライアントまたは以前のバージョンの Chrome または Safari は `SameSite` サポートされていません =None。

OAuth 2.0 は、ユーザーや他の多くの ID プロバイダーが使用する認証と承認Azure Active Directory標準です。 OAuth 2.0 の基本的な理解は、認証を使用する場合の前提条件Teams。 詳細については、「正式な仕様よりも簡単に実行できる [OAuth 2](https://aaronparecki.com/oauth-2-simplified/) 簡略化」 [を参照してください](https://oauth.net/2/)。 タブとボットの認証フローは異なります。タブは Web サイトに似ているため、OAuth 2.0 を直接使用できます。 ボットの動作はいくつかの方法が異なりますが、コア概念は同じです。

たとえば、Node と [OAuth 2.0](https://oauth.net/2/grant-types/implicit/)暗黙的な付与の種類を使用するタブとボットの認証フローについては、「タブの認証フローを開始する」 [を参照してください](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow)。

> [!NOTE]
> ユーザーにログイン ボタン **を** 表示し、ボタンの選択に応じて API を呼び出す前に、SDK の初期化が完了するのを `microsoftTeams.authentication.authenticate` 待つ必要があります。 初期化が完了すると呼び `microsoftTeams.initialize` 出される API にコールバックを渡します。

![タブ認証シーケンス図](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. ユーザーは、タブ構成またはコンテンツ ページのコンテンツ (通常は [サインイン] または [ログイン] ボタン)**を操作** します。
2. タブは、認証開始ページの URL を作成します。 必要に応じて、URL プレースホルダーからの情報を使用するか、クライアント SDK Teams呼び出しを使用して、ユーザーの認証エクスペリエンス `microsoftTeams.getContext()` を合理化します。 たとえば、Azure AD を使用して認証する場合、パラメーターがユーザーの電子メール アドレスに設定されている場合、ユーザーが最近ログインした場合、ユーザーはサインインする `login_hint` 必要が生じないので、ユーザーはサインインする必要があります。 これは、ユーザー Azure ADキャッシュされた資格情報を使用する必要があるためです。 ポップアップ ウィンドウが簡単に表示され、表示されなくなります。
3. 次に、タブは `microsoftTeams.authentication.authenticate()` メソッドを呼び出し、`successCallback` 関数と `failureCallback` 関数を登録します。
4. Teamsポップアップ ウィンドウで iframe でスタート ページを開きます。 スタート ページはランダム なデータを生成し、将来の検証のために保存し、ID プロバイダーのエンドポイント (たとえば、id プロバイダーのエンドポイントにリダイレクト `state` `/authorize` `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` Azure AD。 `<tenant id>`context.tid である独自のテナント ID に置き換える。
Teams の他のアプリケーション認証フローと同様に、スタート ページはリスト内のドメイン上に、およびポスト サインイン リダイレクト ページと同じドメイン上にある `validDomains` 必要があります。

    > [!NOTE]
    > OAuth 2.0 暗黙的な付与フローでは、認証要求内のパラメーターが呼び出されます。これは、クロスサイト要求フォージェリ攻撃を防ぐための一意のセッション データを `state` [含む。](https://en.wikipedia.org/wiki/Cross-site_request_forgery) この例では、データにランダムに生成された GUID を使用 `state` します。

5. プロバイダーのサイトで、ユーザーはサインインし、タブへのアクセスを許可します。
6. プロバイダーは、ユーザーをアクセス トークンを使用してタブの OAuth 2.0 リダイレクト ページに移動します。
7. タブは、返された値が以前に保存された値と一致することを確認し、手順 3 で登録された関数を呼び出 `state` `microsoftTeams.authentication.notifySuccess()` `successCallback` します。
8. Teamsウィンドウを閉じます。
9. タブは、ユーザーの開始場所に応じて、構成 UI を表示するか、タブの内容を更新または再読み込みします。

## <a name="treat-tab-context-as-hints"></a>タブ コンテキストをヒントとして扱う

タブ コンテキストはユーザーに関する有用な情報を提供しますが、この情報を使用してユーザーを認証することはできません。 タブ コンテンツの URL に URL パラメーターとして情報を取得した場合や、クライアント SDK で関数を呼び出Microsoft Teams `microsoftTeams.getContext()` してください。 悪意のあるアクターは、独自のパラメーターを使用してタブ コンテンツ URL を呼び出す可能性があります。 アクターは、web ページの偽装を呼びMicrosoft Teamsして、タブ コンテンツ URL を iframe に読み込み、独自のデータを関数に返 `getContext()` します。 使用する前に、タブ コンテキスト内の ID 関連情報をヒントとして扱い、検証する必要があります。 ポップアップ ページから認証 [ページに移動するノートを参照してください](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page)。

## <a name="code-sample"></a>コード サンプル

タブ認証プロセスを示すサンプル コード:

| **サンプルの名前** | **説明** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Teamsタブ認証 | タブを使用したタブの認証Azure AD。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="see-also"></a>関連項目

ユーザー設定を使用したタブ認証の詳細な実装Azure ADを参照してください。

* [[ユーザーの認証] タブでTeamsする](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [サイレント認証](~/tabs/how-to/authentication/auth-silent-AAD.md)
