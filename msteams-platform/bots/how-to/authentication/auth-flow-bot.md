---
title: ボットの Microsoft Teams 認証フロー
description: Bot の Microsoft Teams 認証フローについて説明します。
keywords: teams 認証フローボット
ms.topic: overview
ms.openlocfilehash: b9e72a0e1064779d9a2e49deda24e5e2eaed5962
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409086"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Microsoft Teams でのボットの認証フロー

OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。 OAuth 2.0 に関する基本的な理解は、Teams で認証を使用するための前提条件です。[正式な仕様](https://oauth.net/2/)よりも簡単に理解できる[概要を](https://aaronparecki.com/oauth-2-simplified/)次に示します。 タブとボットの認証フローは少し異なります。タブは、OAuth 2.0 を直接使用できるようにするために、web サイトと非常によく似ていますが、ボットはまったく異なるものにする必要はありませんが、コア概念は同じです。

Node.js および[OAuth 2.0 認証コード許可タイプ](https://oauth.net/2/grant-types/authorization-code/)を使用したボットの認証フローを示す例については、「GitHub リポジトリの[Microsoft Teams 認証サンプル](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)」を参照してください。

![Bot 認証シーケンス図](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. ユーザーが bot にメッセージを送信します。
2. Bot は、ユーザーがサインインする必要があるかどうかを判断します。
    * この例では、bot はユーザーデータストアにアクセストークンを格納します。 選択した id プロバイダーの検証済みトークンがない場合は、ユーザーにサインインを求めるメッセージが表示されます。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. Bot は、認証フローの開始ページの URL を構築し、アクションを使用してユーザーにカードを送信し `signin` ます。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))
    * Teams での他のアプリケーション認証フローと同様に、開始ページは、リスト上のドメイン内にあり、 `validDomains` ログイン後リダイレクトページと同じドメイン内にある必要があります。
    * **重要**: OAuth 2.0 認証コードは、 `state` [クロスサイト要求偽造攻撃](https://en.wikipedia.org/wiki/Cross-site_request_forgery)を防止するための一意のセッショントークンを含む、認証要求のパラメーターに対して、要求フローの呼び出しを許可します。 この例では、ランダムに生成された GUID を使用します。
4. ユーザーが [ *サインイン* ] ボタンを選択すると、Teams はポップアップウィンドウを開き、開始ページに移動します。
> [!NOTE]
> ポップアップウィンドウのサイズは、URL の幅と高さのクエリ文字列パラメーターを使用して制御できます。 たとえば、幅を500に、高さに500を追加すると、500x500 ピクセルのポップアップが表示されます。 Teams では、指定したピクセルサイズのポップアップウィンドウが表示されます。最大値は、メインウィンドウのサイズに対する割合です。
5. スタートページは、ユーザーを id プロバイダーのエンドポイントにリダイレクトし `authorize` ます。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. プロバイダーのサイトで、ユーザーはサインインして bot へのアクセスを許可します。
7. プロバイダーは、ユーザーを bot の OAuth リダイレクトページに認証コードで受け取ります。
8. Bot は、アクセストークンの認証コードを引き換えし、 **条件付き** は、サインインフローを開始したユーザーにトークンを関連付けます。 次に、これを *暫定トークン* と呼びます。
    * この例では、bot は、 `state` サインインプロセスを開始したユーザーの ID をパラメーターの値と関連付け、後で `state` id プロバイダーによって返される値と一致させることができます。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
    * **重要**: bot は、id プロバイダーから受け取ったトークンを格納し、それを特定のユーザーに関連付けていますが、"保留中の検証" としてマークされています。 暫定トークンはまだ使用できません。さらに検証する必要があります。
      1. **Id プロバイダーから受け取ったものを検証します。** パラメーターの値は、 `state` 前に保存されたものに対して確認する必要があります。 
      1. **Teams からの受信を確認します。** Id プロバイダーでボットを承認したユーザーが bot とチャットしているユーザーと同じユーザーであることを確認するために、 [2 段階の認証](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) 検証が行われます。 これにより [、man-in-the-middle](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) および [フィッシング](https://en.wikipedia.org/wiki/Phishing) 攻撃を防ぐことができます。 Bot は、検証コードを生成し、ユーザーに関連付けて保存します。 確認コードは、以下に示すように Teams によって自動的に送信されます。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. OAuth コールバックは、を呼び出したページをレンダリング `notifySuccess("<verification code>")` します。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams はポップアップウィンドウを閉じ、 `<verification code>` 送信されたを `notifySuccess()` bot に送り返します。 Bot は、で [呼び出し](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) メッセージを受信し `name = signin/verifyState` ます。
11. Bot は、ユーザーの暫定トークンに格納されている検証コードに対して、受信確認コードをチェックします。 ([ビューコード](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. 一致した場合、ボットはトークンを検証済みとして使用できることを示します。 それ以外の場合、認証フローは失敗し、bot が暫定トークンを削除します。

> [!NOTE]
> Mobile での認証に関する問題が発生した場合は、JavaScript SDK がバージョン1.4.1 以降に更新されていることを確認してください。

## <a name="samples"></a>サンプル

Bot 認証プロセスを示すサンプルコードについては、以下を参照してください。

* [Microsoft Teams bot 認証のサンプル (Node.js)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>詳細情報

Azure AD を対象とする bot 認証の実装に関する詳細なチュートリアルについては、以下を参照してください。

* [Teams の bot に認証を追加する](add-authentication.md)
