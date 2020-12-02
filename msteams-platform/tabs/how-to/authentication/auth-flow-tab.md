---
title: タブの認証フロー
description: タブ内の認証フローについて説明します。
keywords: teams の認証フロータブ
ms.openlocfilehash: 5ecd4d7d3a2658d17a8c6dea5d73cbd98eb2dfde
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552543"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>タブの Microsoft Teams 認証フロー

> [!Note]
> モバイルクライアントのタブで認証が機能するには、少なくとも、Teams バージョンの Teams SDK を使用していることを確認する必要があります。
> Teams SDK が認証フローに対して個別のウィンドウを起動するため、samesite 属性を ' 甘い ' に設定できます。 現時点では、SameSite = None は Teams デスクトップクライアントまたは以前のバージョンの Chrome または Safari ではサポートされていません。

OAuth 2.0 は、Azure AD とその他の多くの id プロバイダーによって使用される認証と承認のためのオープン標準です。 OAuth 2.0 に関する基本的な理解は、Teams で認証を使用するための前提条件です。[正式な仕様](https://oauth.net/2/)よりも簡単に理解できる[概要を](https://aaronparecki.com/oauth-2-simplified/)次に示します。 タブと bot の認証フローは、タブが web サイトと非常によく似ており、OAuth 2.0 を直接使用できるため、少し異なります。bot は、いくつかの操作を行う必要はありませんが、中心となる概念は同じです。

ノードおよび [OAuth 2.0 の暗黙的な許可の種類](https://oauth.net/2/grant-types/implicit/)を使用したタブとボットの認証フローの例については、「[タブの認証フローを開始](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow)する」を参照して *ください*。

![タブ認証シーケンスの図](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. ユーザーは、タブの構成またはコンテンツページのコンテンツを操作します。通常は、"サインイン" または "ログイン" というラベルが付いたボタンです。
2. タブは、認証の開始ページの URL を構築します。オプションで URL プレースホルダーの情報を使用するか、Teams のクライアント SDK メソッドを呼び出して、 `microsoftTeams.getContext()` ユーザーの認証手順を合理化します。 たとえば、Azure AD を使用して認証する場合、ユーザー `login_hint` の電子メールアドレスにパラメーターが設定されていると、ユーザーは、必要に応じてユーザーのキャッシュされた資格情報を使用することになるため、後でサインインする必要がない場合があります。ポップアップは短時間で点滅して消えます。
3. 次に、タブは `microsoftTeams.authentication.authenticate()` メソッドを呼び出し、`successCallback` 関数と `failureCallback` 関数を登録します。
4. Teams は、ポップアップウィンドウ内の iframe で開始ページを開きます。 開始ページはランダムな `state` データを生成し、それを今後の検証のために保存し、 `/authorize` Azure AD などの id プロバイダーのエンドポイントにリダイレクトし `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` ます。 `<tenant id>`を独自のテナント id (コンテキスト tid) に置き換えます。
    * Teams での他のアプリケーション認証フローと同様に、開始ページは、そのリスト内のドメイン、 `validDomains` およびログイン後リダイレクトページと同じドメインにある必要があります。
    * **重要**: OAuth 2.0 の暗黙的な付与フローは、 `state` [クロスサイト要求偽造攻撃](https://en.wikipedia.org/wiki/Cross-site_request_forgery)を防止するための一意のセッションデータを含む、認証要求のパラメーターに対して呼び出しを行います。 次の例では、ランダムに生成された GUID をデータに使用し `state` ます。
5. プロバイダーのサイトで、ユーザーはサインインし、タブへのアクセスを許可します。
6. プロバイダーは、タブの OAuth 2.0 リダイレクトページにアクセストークンを使用してユーザーを取得します。
7. タブは、返された `state` 値が前に保存された内容と一致することを確認し、呼び出し `microsoftTeams.authentication.notifySuccess()` は、 `successCallback` 手順3で登録されている関数を呼び出します。
8. Teams によってポップアップウィンドウが閉じられます。
9. タブには、構成 UI が表示されるか、またはユーザーが開始した場所に応じて、タブの内容が更新または再読み込みされます。

## <a name="treat-tab-context-as-hints"></a>Tab コンテキストをヒントとして扱う

Tab コンテキストはユーザーに関して有用な情報を提供しますが、この情報を使用してユーザーがタブのコンテンツ URL への URL パラメーターとして取得するか、 `microsoftTeams.getContext()` Microsoft Teams クライアント SDK の関数を呼び出すかを認証しません。 悪意のあるアクターは、独自のパラメーターを使用してタブコンテンツ URL を呼び出すことができ、Microsoft Teams を偽装している web ページは、タブコンテンツ URL を iframe に読み込み、そのデータを関数に返すことができました `getContext()` 。 Tab コンテキストの id 関連情報は単にヒントとして扱い、使用する前に検証する必要があります。 [ポップアップページから [認証] ページに移動する](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)には、「注」を参照してください。

## <a name="samples"></a>サンプル

タブ認証プロセスを示すサンプルコードについては、以下を参照してください。

* [Microsoft Teams タブ認証のサンプル (ノード)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Microsoft Teams タブ認証のサンプル (C#)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

## <a name="more-details"></a>詳細情報

Azure Active Directory を対象とするタブ認証の実装に関する詳細なチュートリアルについては、以下を参照してください。

* [Microsoft Teams タブでユーザーを認証する](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [サイレント認証](~/tabs/how-to/authentication/auth-silent-AAD.md)
