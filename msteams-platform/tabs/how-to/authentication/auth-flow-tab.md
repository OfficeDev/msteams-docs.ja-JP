---
title: タブの認証フロー
description: タブでの認証フローについて説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: チーム認証フロー タブ
ms.openlocfilehash: 1282c149beba0ff5b424585f566a703f48234fa2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566692"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>タブの認証フローのMicrosoft Teams

> [!NOTE]
> モバイル クライアントでタブで認証を使用するには、少なくとも 1.4.1 バージョンの Microsoft Teams JavaScript SDK を使用していることを確認する必要があります。
> TeamsSDK は、認証フロー用に別のウィンドウを起動します。 属性を `SameSite` **[緩み]** に設定します。 デスクトップ クライアントまたは以前のバージョンの Chrome または Safari では、Teams =None はサポートされません `SameSite` 。

OAuth 2.0 は、Azure Active Directory (AAD) およびその他の多くの ID プロバイダーが使用する認証および承認のオープン標準です。 OAuth 2.0 の基本知識は、Teamsで認証を操作するための前提条件です。 詳細については、[正式仕様](https://oauth.net/2/)よりも簡単に従う[OAuth 2 の簡略化](https://aaronparecki.com/oauth-2-simplified/)を参照してください。 タブとボットの認証フローは、タブが Web サイトに似ているため、OAuth 2.0 を直接使用できるため、異なります。 ボットはいくつかの方法で異なりますが、コア概念は同じです。

Node および [OAuth 2.0 の暗黙的な許可タイプ](https://oauth.net/2/grant-types/implicit/)を使用するタブおよびボットの認証フローの例については、「 [タブの認証フローの開始](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow)」を参照してください。

> [!NOTE]
> ユーザーに **ログイン** ボタンを表示し、ボタンの `microsoftTeams.authentication.authenticate` 選択に応答して API を呼び出す前に、SDK の初期化が完了するまで待つ必要があります。 `microsoftTeams.initialize`初期化が完了したときに呼び出される API にコールバックを渡すことができます。

![タブ認証シーケンス図](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. ユーザーはタブ構成またはコンテンツ ページのコンテンツ (通常は **[サインイン** ] または [ログイン] ボタン) **と** 対話します。
2. タブは、認証開始ページの URL を構成します。 オプションで、URL プレースホルダーからの情報またはクライアント SDK メソッドTeams呼び出 `microsoftTeams.getContext()` しを使用して、ユーザーの認証エクスペリエンスを合理化します。 たとえば、AAD を使用して認証を行う場合、 `login_hint` パラメーターがユーザーの電子メール アドレスに設定されている場合、ユーザーはサインインする必要はありません。 これは、AAD がユーザーのキャッシュされた資格情報を使用するためです。 ポップアップ ウィンドウが短時間表示され、表示されなくなります。
3. 次に、タブは `microsoftTeams.authentication.authenticate()` メソッドを呼び出し、`successCallback` 関数と `failureCallback` 関数を登録します。
4. Teamsポップアップ ウィンドウの iframe で開始ページを開きます。 開始ページは、ランダム `state` なデータを生成し、将来の検証のために保存し `/authorize` 、Azure AD など、ID プロバイダーのエンドポイントにリダイレクト `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` します。 `<tenant id>`context.tid である独自のテナント ID で置き換えます。
Teamsの他のアプリケーション認証フローと同様に、スタート ページは、そのリスト内のドメイン `validDomains` 上にあり、ポスト サインイン のリダイレクト ページと同じドメインになければなりません。

    > [!NOTE]
    > OAuth 2.0 の暗黙的な許可フローは `state` 、 [クロスサイトリクエストフォージェリ攻撃](https://en.wikipedia.org/wiki/Cross-site_request_forgery)を防ぐために一意のセッションデータを含む認証要求のパラメータを呼び出します。 この例では、ランダムに生成された GUID をデータに使用 `state` しています。

5. プロバイダーのサイトで、ユーザーはサインインし、タブへのアクセスを許可します。
6. プロバイダーは、アクセス トークンを使用して、タブの OAuth 2.0 リダイレクト ページにユーザーを移動します。
7. タブは、戻り `state` 値が以前に保存されたものと一致することを確認し、次 `microsoftTeams.authentication.notifySuccess()` に手順 3 で登録された関数を呼び出すを呼び出します `successCallback` 。
8. Teamsポップアップ ウィンドウを閉じます。
9. このタブには、ユーザーがどこから開始したかによって、構成 UI の表示、更新、またはタブの内容の再読み込みが行われます。

## <a name="treat-tab-context-as-hints"></a>タブコンテキストをヒントとして扱う

タブ コンテキストはユーザーに関する有用な情報を提供しますが、この情報を使用してユーザーを認証しないでください。 ユーザーの情報をタブ コンテンツ URL の URL パラメータとして取得する場合や `microsoftTeams.getContext()` 、Microsoft Teams クライアント SDK で関数を呼び出して、ユーザーを認証してください。 悪意のあるアクターは、独自のパラメータを使用してタブ コンテンツ URL を呼び出すことができます。 アクターは、Microsoft Teams偽装する Web ページを呼び出して、タブ コンテンツ URL を iframe に読み込み、独自のデータを関数に返 `getContext()` すこともできます。 タブコンテキストの ID 関連情報は、単にヒントとして扱い、使用する前に検証する必要があります。 [ポップアップページから認証ページに移動するのメモを](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)参照してください。

## <a name="code-sample"></a>コード サンプル

タブ認証プロセスを示すサンプル コード:

| **サンプル名** | **説明** | **C#** | **Node.js** |
|-----------------|-----------------|-------------|------------|
| Teamsタブ認証 | AAD を使用したタブの認証プロセス。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-sample/nodejs) |

## <a name="more-details"></a>詳細情報

AAD を使用したタブ認証の詳細な実装については、以下を参照してください。

* [Teams タブでユーザーを認証する](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [サイレント認証](~/tabs/how-to/authentication/auth-silent-AAD.md)
