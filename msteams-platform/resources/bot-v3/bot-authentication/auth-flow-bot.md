---
title: ボットの認証フロー
description: ボットでの認証フローについて説明します
keywords: teams 認証フロー ボット
localization_priority: Normal
ms.topic: conceptual
ms.date: 03/01/2018
ms.openlocfilehash: e3bc5395a6a95272901076ec8bf51dc2ad57dfd2
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035332"
---
# <a name="microsoft-teams-authentication-flow-for-bots"></a>ボットの Microsoft Teams 認証フロー

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

OAuth 2.0 は、Azure AD およびその他の多くの ID プロバイダーによって使用される認証と承認のためのオープンな標準です。 OAuth 2.0 の基本的な理解は、Teams で認証を操作するための前提条件です。[ここでは、正式な仕様](https://oauth.net/2/)よりも従いやすい[優れた概要を示](https://aaronparecki.com/oauth-2-simplified/)します。 タブとボットの認証フローは異なります。 タブは Web サイトに似ているため、OAuth 2.0 を直接使用できます。ボットは異なる方法で行う必要はなく、いくつかの操作を行う必要がありますが、コア概念は同じです。

[OAuth 2.0 承認コード付与の種類](https://oauth.net/2/grant-types/authorization-code/)を使用してノードを使用するボットの認証フローを示す例については、[GitHub リポジトリの Microsoft Teams 認証サンプル](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)を参照してください。

![ボット認証シーケンス図](~/assets/images/authentication/bot_auth_sequence_diagram.png)

1. ユーザーはボットにメッセージを送信します。
2. ボットは、ユーザーがサインインする必要があるかどうかを決定します。
    * この例では、ボットはアクセス トークンをユーザー データ ストアに格納します。 選択した ID プロバイダーの検証済みトークンがない場合は、ログインするようにユーザーに求めます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. ボットは、認証フローの開始ページへの URL を作成し、アクションを使用してユーザーにカードを `signin` 送信します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))
    * Teams の他のアプリケーション認証フローと同様に、スタート ページは、リスト内 `validDomains` のドメインと、ログイン後のリダイレクト ページと同じドメイン上にある必要があります。
    * **重要**: OAuth 2.0 承認コード許可フローは、`state`[クロスサイト要求フォージェリ攻撃](https://en.wikipedia.org/wiki/Cross-site_request_forgery)を防ぐために、一意のセッション トークンを含む認証要求のパラメーターを呼び出します。 この例では、ランダムに生成された GUID を使用します。
4. ユーザーが *サインイン* ボタンを選択すると、Teams によってポップアップ ウィンドウが開き、スタート ページに移動します。
5. スタート ページでは、ID プロバイダーのエンドポイントにユーザーが `authorize` リダイレクトされます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. プロバイダーのサイトで、ユーザーはサインインし、ボットへのアクセスを許可します。
7. プロバイダーは、承認コードを使用して、ユーザーをボットの OAuth リダイレクト ページに移動します。
8. ボットは、アクセス トークンの承認コードを引き換え、サインイン フローを開始したユーザーと **トークンを暫定的に** 関連付けます。 以下では、これを *仮トークン* と呼びます。
    * この例では、ボットはパラメーターの値を `state` サインイン プロセスを開始したユーザーの ID に関連付け、後で ID プロバイダーから返された値と `state` 照合できるようにします。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
    * **重要**: ボットは、ID プロバイダーから受け取ったトークンを格納し、それを特定のユーザーに関連付けますが、"保留中の検証" としてマークされます。 仮トークンはまだ使用できません。さらに検証する必要があります。
      1. **ID プロバイダーから受け取った内容を検証します。** パラメーターの値は、 `state` 前に保存されたものに対して確認する必要があります。
      1. **Teams から受け取った内容を検証します。** ID プロバイダーでボットを承認したユーザーが、ボットとチャットしているユーザーと同じであることを確認するために、 [2 段階認証](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) 検証が実行されます。 この検証は、 [中間者](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) 攻撃と [フィッシング攻撃を](https://en.wikipedia.org/wiki/Phishing) 防ぎます。 ボットは検証コードを生成し、ユーザーに関連付けられた検証コードを格納します。 確認コードは、手順 9 と手順 10 で説明するように Teams によって自動的に送信されます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. OAuth コールバックは、を呼び出 `notifySuccess("<verification code>")`すページをレンダリングします。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams によってポップアップが閉じられ、送信されたメッセージが `<verification code>` ボットに `notifySuccess()` 送信されます。 ボットは、 .[](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) `name = signin/verifyState`
11. ボットは、受信確認コードを、ユーザーの仮トークンと共に格納された検証コードと照合します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. 一致する場合、ボットはトークンを検証済みとしてマークし、使用する準備が整います。 それ以外の場合、認証フローは失敗し、ボットは仮トークンを削除します。

> [!Note]
> モバイルでの認証に関する問題が発生した場合は、Javascript SDK がバージョン 1.4.1 以降に更新されていることを確認してください。

## <a name="samples"></a>サンプル

ボット認証プロセスを示すサンプル コードについては、次を参照してください。

* [Microsoft Teams ボット認証サンプル (ノード)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>詳細情報

Azure Active Directory を対象とするボット認証の実装に関する詳細なチュートリアルについては、次を参照してください。

* [Microsoft Teams ボットでユーザーを認証する](~/resources/bot-v3/bot-authentication/auth-bot-AAD.md)
