---
title: ボットの認証フロー
description: ボットの認証フローについて説明します。
keywords: teams 認証フローボット
ms.date: 03/01/2018
ms.openlocfilehash: 5230a94b23f9042d9d7753b52467fba5b2fec89e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675119"
---
# <a name="microsoft-teams-authentication-flow-for-bots"></a>ボットの Microsoft Teams 認証フロー

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

OAuth 2.0 は、Azure AD とその他の多くの id プロバイダーによって使用される認証と承認のためのオープン標準です。 OAuth 2.0 に関する基本的な理解は、Teams で認証を使用するための前提条件です。[正式な仕様](https://oauth.net/2/)よりも簡単に理解できる[概要を](https://aaronparecki.com/oauth-2-simplified/)次に示します。 タブと bot の認証フローは、タブが web サイトに非常によく似ているため、OAuth 2.0 を直接使用することができますが、bot は異なる操作を実行する必要はありませんが、その中心概念は同じです。

[OAuth 2.0 認証コード許可タイプ](https://oauth.net/2/grant-types/authorization-code/)を使用してノードを使用するボットの認証フローを示す例については、「GitHub リポジトリの[Microsoft Teams 認証サンプル](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)」を参照してください。

![Bot 認証シーケンス図](~/assets/images/authentication/bot_auth_sequence_diagram.png)

1. ユーザーが bot にメッセージを送信します。
2. Bot は、ユーザーがサインインする必要があるかどうかを判断します。
    * この例では、bot はユーザーデータストアにアクセストークンを格納します。 選択した id プロバイダーのトークンが検証されていない場合は、ログインするようにユーザーに要求します。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. Bot は、認証フローの開始ページの URL を構築し、 `signin`アクションを使用してユーザーにカードを送信します。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))
    * Teams での他のアプリケーション認証フローと同様に、開始ページは、 `validDomains`リスト内のドメイン、およびログイン後リダイレクトページと同じドメインにある必要があります。
    * **重要**: OAuth 2.0 認証コードは、 `state` [クロスサイト要求偽造攻撃](https://en.wikipedia.org/wiki/Cross-site_request_forgery)を防止するための一意のセッショントークンを含む、認証要求のパラメーターに対して、要求フローの呼び出しを許可します。 この例では、ランダムに生成された GUID を使用します。
4. ユーザーが [*サインイン*] ボタンをクリックすると、Teams はポップアップウィンドウを開き、開始ページに移動します。
5. スタートページは、ユーザーを id プロバイダーの`authorize`エンドポイントにリダイレクトします。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. プロバイダーのサイトで、ユーザーはサインインして bot へのアクセスを許可します。
7. プロバイダーは、ユーザーを bot の OAuth リダイレクトページに、認証コードを使用して受け取ります。
8. Bot は、アクセストークンの認証コードを引き換えし、**条件付き**は、サインインフローを開始したユーザーにトークンを関連付けます。 次に、これを*暫定トークン*と呼びます。
    * この例では、bot は、サインインプロセスを`state`開始したユーザーの id をパラメーターの値と関連付け、後で id プロバイダーによって返される`state`値と一致させることができます。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
    * **重要**: bot は、id プロバイダーから受け取ったトークンを格納し、それを特定のユーザーに関連付けていますが、"保留中の検証" としてマークされています。 暫定トークンはまだ使用できません。さらに検証する必要があります。 
      1. **Id プロバイダーから受け取ったものを検証します。** `state`パラメーターの値は、前に保存されたものに対して確認する必要があります。 
      1. **Teams からの受信を確認します。** Id プロバイダーでボットを承認したユーザーが bot とチャットしているユーザーと同じユーザーであることを確認するために、 [2 段階の認証](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)検証が行われます。 これにより[、man-in-the-middle](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)および[フィッシング](https://en.wikipedia.org/wiki/Phishing)攻撃を防ぐことができます。 Bot は、検証コードを生成し、ユーザーに関連付けて保存します。 確認コードは、手順9および10で説明するように、Teams によって自動的に送信されます。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. OAuth コールバックは、を呼び出し`notifySuccess("<verification code>")`たページをレンダリングします。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams はポップアップを閉じ、送信`<verification code>`され`notifySuccess()`たを bot に送り返します。 Bot は、 `name = signin/verifyState`で[呼び出し](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke)メッセージを受信します。
11. Bot は、ユーザーの暫定トークンに格納されている検証コードに対して、受信確認コードをチェックします。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. 一致した場合、ボットはトークンを検証済みとして使用できることを示します。 それ以外の場合、認証フローは失敗し、bot が暫定トークンを削除します。

> [!Note]
> Mobile での認証に関する問題が発生した場合は、Javascript SDK がバージョン1.4.1 以降に更新されていることを確認してください。

## <a name="samples"></a>サンプル

Bot 認証プロセスを示すサンプルコードについては、以下を参照してください。

* [Microsoft Teams bot 認証のサンプル (ノード)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>詳細情報

Azure Active Directory を対象とする bot 認証の実装に関する詳細なチュートリアルについては、以下を参照してください。

* [Microsoft Teams bot でユーザーを認証する](~/resources/bot-v3/bot-authentication/auth-bot-AAD.md)
