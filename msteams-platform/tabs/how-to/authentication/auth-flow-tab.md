---
title: タブの認証フロー
description: タブの認証フローについて説明する
ms.topic: conceptual
localization_priority: Normal
keywords: teams 認証フロー タブ
ms.openlocfilehash: 1282c149beba0ff5b424585f566a703f48234fa2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566692"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Microsoft Teamsの認証フロー

> [!NOTE]
> モバイル クライアントでタブで認証を機能するには、JavaScript SDK の 1.4.1 以上のバージョンを使用Microsoft Teams必要があります。
> TeamsSDK は、認証フロー用に個別のウィンドウを起動します。 属性を `SameSite` **Lax に設定します**。 Teamsクライアントまたは以前のバージョンの Chrome または Safari は `SameSite` サポートされていません =None。

OAuth 2.0 は、Azure Active Directory (AAD) および他の多くの ID プロバイダーによって使用される認証と承認のオープン標準です。 OAuth 2.0 の基本的な理解は、認証を使用する場合の前提条件Teams。 詳細については、「正式な仕様よりも簡単に実行できる [OAuth 2](https://aaronparecki.com/oauth-2-simplified/) 簡略化」 [を参照してください](https://oauth.net/2/)。 タブとボットの認証フローは異なります。タブは Web サイトに似ているため、OAuth 2.0 を直接使用できます。 ボットの動作はいくつかの方法が異なりますが、コア概念は同じです。

Node と [OAuth 2.0](https://oauth.net/2/grant-types/implicit/)暗黙的付与の種類を使用するタブとボットの認証フローの例については、「タブの認証フローを開始する」 [を参照してください](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow)。

> [!NOTE]
> ユーザーにログイン ボタン **を** 表示し、ボタンの選択に応じて API を呼び出す前に、SDK の初期化が完了するのを `microsoftTeams.authentication.authenticate` 待つ必要があります。 初期化が完了すると呼び `microsoftTeams.initialize` 出される API にコールバックを渡します。

![タブ認証シーケンス図](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. ユーザーは、タブ構成またはコンテンツ ページのコンテンツ (通常は [サインイン] または [ログイン] ボタン)**を操作** します。
2. タブは、認証開始ページの URL を作成します。 必要に応じて、URL プレースホルダーからの情報を使用するか、クライアント SDK Teams呼び出しを使用して、ユーザーの認証エクスペリエンス `microsoftTeams.getContext()` を合理化します。 たとえば、AAD を使用して認証する場合、パラメーターがユーザーの電子メール アドレスに設定されている場合、ユーザーが最近サインインした場合、ユーザーはサインイン `login_hint` する必要が生じなきます。 これは、AAD がユーザーのキャッシュされた資格情報を使用する理由です。 ポップアップ ウィンドウが簡単に表示され、表示されなくなります。
3. 次に、タブは `microsoftTeams.authentication.authenticate()` メソッドを呼び出し、`successCallback` 関数と `failureCallback` 関数を登録します。
4. Teamsポップアップ ウィンドウで iframe でスタート ページを開きます。 スタート ページは、ランダム なデータを生成し、将来の検証のために保存し、Azure プロバイダーのエンドポイントなどの ID プロバイダーのエンドポイント `state` `/authorize` `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` にリダイレクトAD。 `<tenant id>`context.tid である独自のテナント ID に置き換える。
Teams の他のアプリケーション認証フローと同様に、スタート ページはリスト内のドメイン上に、およびポスト サインイン リダイレクト ページと同じドメイン上にある `validDomains` 必要があります。

    > [!NOTE]
    > OAuth 2.0 暗黙的な付与フローでは、認証要求内のパラメーターが呼び出されます。これは、クロスサイト要求フォージェリ攻撃を防ぐための一意のセッション データを `state` [含む。](https://en.wikipedia.org/wiki/Cross-site_request_forgery) この例では、データにランダムに生成された GUID を使用 `state` します。

5. プロバイダーのサイトで、ユーザーはサインインし、タブへのアクセスを許可します。
6. プロバイダーは、ユーザーをアクセス トークンを使用してタブの OAuth 2.0 リダイレクト ページに移動します。
7. タブは、返された値が以前に保存された値と一致することを確認し、手順 3 で登録された関数を呼び出 `state` `microsoftTeams.authentication.notifySuccess()` `successCallback` します。
8. Teamsウィンドウを閉じます。
9. タブは、ユーザーの開始場所に応じて、構成 UI を表示するか、タブの内容を更新または再読み込みします。

## <a name="treat-tab-context-as-hints"></a>タブ コンテキストをヒントとして扱う

タブ コンテキストはユーザーに関する有用な情報を提供しますが、この情報を使用してユーザーを認証することはできません。 タブ コンテンツの URL に URL パラメーターとして情報を取得した場合や、クライアント SDK で関数を呼び出Microsoft Teams `microsoftTeams.getContext()` してください。 悪意のあるアクターは、独自のパラメーターを使用してタブ コンテンツ URL を呼び出す可能性があります。 アクターは、web ページの偽装を呼びMicrosoft Teamsして、タブ コンテンツ URL を iframe に読み込み、独自のデータを関数に返 `getContext()` します。 使用する前に、タブ コンテキスト内の ID 関連情報をヒントとして扱い、検証する必要があります。 ポップアップ ページから認証 [ページに移動するノートを参照してください](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)。

## <a name="code-sample"></a>コード サンプル

タブ認証プロセスを示すサンプル コード:

| **サンプル名** | **説明** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Teamsタブ認証 | AAD を使用したタブの認証プロセス。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="more-details"></a>詳細情報

AAD を使用したタブ認証の詳細な実装については、以下を参照してください。

* [[ユーザーの認証] タブでTeamsする](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [サイレント認証](~/tabs/how-to/authentication/auth-silent-AAD.md)
