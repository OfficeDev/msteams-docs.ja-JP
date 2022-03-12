---
title: ボットの認証フロー
description: ボットの認証フローについて説明します。
keywords: teams 認証フロー ボット
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: c29275933ada0d286ef1bfecf19fef787df9592c
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453188"
---
# <a name="microsoft-teams-authentication-flow-for-bots"></a>Microsoft Teamsの認証フロー

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

OAuth 2.0 は、ユーザーや他の多くの ID プロバイダーが使用する認証と承認Azure AD標準です。 OAuth 2.0 の基本的な理解は、認証を使用する場合の前提条件Teams。[ここでは、正式な仕様よりも](https://aaronparecki.com/oauth-2-simplified/)簡単にフォローできる優れた概要[を示します](https://oauth.net/2/)。 タブとボットの認証フローは、タブが Web サイトと非常に似ているため、OAuth 2.0 を直接使用できるので、少し異なります。また、ボットは異なる方法でいくつかの操作を行う必要がありますが、コア概念は同じです。

[OAuth 2.0](https://oauth.net/2/grant-types/authorization-code/) 承認コード付与[の種類を使用](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)して Node を使用するボットの認証フローを示す例については、「GitHub Microsoft Teams 認証サンプル」を参照してください。

![ボット認証シーケンス図](~/assets/images/authentication/bot_auth_sequence_diagram.png)

1. ユーザーはボットにメッセージを送信します。
2. ボットは、ユーザーがサインインする必要があるかどうかを判断します。
    * この例では、ボットはアクセス トークンをユーザー データ ストアに格納します。 選択した ID プロバイダーの検証済みトークンが存在しない場合は、ユーザーにログインを求めるメッセージが表示されます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. ボットは、認証フローの開始ページへの URL を作成し、アクションを使用してユーザーにカードを送信 `signin` します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))
    * Teams の他`validDomains`のアプリケーション認証フローと同様に、スタート ページは、リスト内のドメインと、ログイン後のリダイレクト ページと同じドメイン上にある必要があります。
    * **重要**: OAuth 2.0 `state` 承認コード付与フローは、一意のセッション トークンを含む認証要求内のパラメーターを呼び出して、クロスサイト要求フォージェリ攻撃を防止 [します。](https://en.wikipedia.org/wiki/Cross-site_request_forgery) この例では、ランダムに生成された GUID を使用します。
4. ユーザーがサインイン ボタンをクリックするとTeamsポップアップ ウィンドウが開き、開始ページに移動します。
5. スタート ページは、ユーザーを ID プロバイダーのエンドポイントにリダイレクト `authorize` します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. プロバイダーのサイトで、ユーザーはサインインし、ボットへのアクセスを許可します。
7. プロバイダーは、認証コードを使用して、ユーザーをボットの OAuth リダイレクト ページに移動します。
8. ボットはアクセス トークンの承認コードを引き換え、サインイン フローを開始したユーザーとトークンを暫定的に関連付ける。 以下では、これを暫定 *トークンと呼ぶ*。
    * この例では `state` 、ボットはパラメーターの値を、サインイン プロセスを開始したユーザーの ID `state` に関連付け、後で ID プロバイダーによって返される値と一致することができます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
    * **重要**: ボットは ID プロバイダーから受け取ったトークンを格納し、それを特定のユーザーに関連付けしますが、"保留中の検証" としてマークされます。 暫定トークンはまだ使用できません。さらに検証する必要があります。
      1. **ID プロバイダーから受け取った情報を検証します。** パラメーターの値は、 `state` 以前に保存した値に対して確認する必要があります。
      1. **アプリから受け取った情報をTeams。** ID [プロバイダーを使用して](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) ボットを承認したユーザーが、ボットとチャットしているユーザーと同じことを確認するために、2 段階認証の検証が実行されます。 これにより、中間 [者や](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) フィッシング攻撃 [から保護](https://en.wikipedia.org/wiki/Phishing) されます。 ボットは検証コードを生成し、ユーザーに関連付けられたコードを格納します。 検証コードは、手順 9 と 10 でTeams手順に従って自動的に送信されます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. OAuth コールバックは、 を呼び出すページをレンダリングします `notifySuccess("<verification code>")`。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teamsを閉じて、送信されたメッセージ`<verification code>`をボット`notifySuccess()`に送信します。 ボットは、 を指定して [呼び出し](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) メッセージを受信します `name = signin/verifyState`。
11. ボットは、受信検証コードを、ユーザーの暫定トークンに格納されている検証コードと照合します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. 一致する場合、ボットはトークンを検証済みとしてマークし、すぐに使用できます。 それ以外の場合、認証フローは失敗し、ボットは暫定トークンを削除します。

> [!Note]
> モバイルでの認証に問題が発生した場合は、Javascript SDK がバージョン 1.4.1 以降に更新されている必要があります。

## <a name="samples"></a>サンプル

ボット認証プロセスを示すサンプル コードについては、以下を参照してください。

* [Microsoft Teamsボット認証サンプル (Node)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>詳細情報

ボット認証のターゲット設定の詳細な実装のチュートリアルについてはAzure Active Directory参照してください。

* [ボットでユーザーをMicrosoft Teamsする](~/resources/bot-v3/bot-authentication/auth-bot-AAD.md)
