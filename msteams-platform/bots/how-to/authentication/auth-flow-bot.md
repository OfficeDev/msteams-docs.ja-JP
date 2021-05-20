---
title: Microsoft Teamsボットの認証フロー
description: ボットのMicrosoft Teams認証フローについて説明します。
keywords: チーム認証フロー ボット
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: f3bf73c105dc38e1cea515bfa7bb7d5324b02ce4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565905"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Microsoft Teamsのボットの認証フロー

OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。 OAuth 2.0 の基本知識は、Teamsで認証を操作するための前提条件です。正式な[仕様](https://oauth.net/2/)よりも簡単に従う[良い概要を次に示](https://aaronparecki.com/oauth-2-simplified/)します。 タブとボットの認証フローは少し異なります — タブはウェブサイトと非常によく似ているので、OAuth 2.0 を直接使用できますが、ボットは異なる方法で実行する必要はありませんが、コア概念は同じです。

Node.js と[OAuth 2.0 承認コード許可タイプ](https://oauth.net/2/grant-types/authorization-code/)を使用するボットの認証フローを示す例については、「GitHubレポ[Microsoft Teams認証サンプル](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs)」を参照してください。

![ボット認証シーケンス図](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. ユーザーがボットにメッセージを送信します。
2. ボットは、ユーザーがサインインする必要があるかどうかを判断します。
   この例では、ボットはアクセス トークンをユーザー データ ストアに格納します。 選択した ID プロバイダーの検証済みトークンがない場合は、サインインするようにユーザーに要求します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. ボットは、認証フローの開始ページへの URL を構築し、アクションを持つカードをユーザーに送信 `signin` します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))</br>
    Teamsの他のアプリケーション認証フローと同様に、スタート ページは、リスト上のドメイン `validDomains` と、ログイン後のリダイレクト ページと同じドメインに存在する必要があります。
    > [!IMPORTANT] 
    > OAuth 2.0 承認コード許可フローは、 `state` [クロスサイトリクエストフォージェリ攻撃](https://en.wikipedia.org/wiki/Cross-site_request_forgery)を防ぐために一意のセッショントークンを含む認証リクエストのパラメータを呼び出します。 この例では、ランダムに生成された GUID を使用します。
4. ユーザーが *サインイン* ボタンを選択すると、ポップアップ ウィンドウTeams開き、スタート ページに移動します。
   > [!NOTE]
   > ポップアップ ウィンドウのサイズは、URL の幅と高さのクエリ文字列パラメーターを使用して制御できます。 たとえば、width=500 と height=500 を追加すると、ポップアップ ウィンドウのサイズは 500 x 500 ピクセルになります。 Teams、指定されたピクセル サイズのポップアップ ウィンドウが、メイン ウィンドウのサイズに対するパーセンテージの最大値まで表示されます。

5. 開始ページは、ユーザーを ID プロバイダーのエンドポイントにリダイレクト `authorize` します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. プロバイダーのサイトで、ユーザーはサインインし、ボットへのアクセスを許可します。
7. プロバイダーは、承認コードを使用して、ボットの OAuth リダイレクト ページにユーザーを移動します。
8. ボットはアクセス トークンの認証コードを使用し、サインイン フローを開始したユーザーに **トークンを暫定的に** 関連付けます。 以下では、これを *暫定トークン* と呼びます。
    * この例では、ボットは `state` 、パラメーターの値をサインイン プロセスを開始したユーザーの ID と関連付け、後で `state` ID プロバイダーが返す値と一致できるようにします。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
      > [!IMPORTANT] 
      > ボットは、ID プロバイダーから受け取ったトークンを格納し、特定のユーザーに関連付けますが、"保留中の検証" としてマークされます。 
    * 暫定トークンは、さらに検証しないと使用できません。
      1. **ID プロバイダーから受け取った内容を検証します。** パラメータの値は `state` 、以前に保存された値と照合して確認する必要があります。 
      1. **Teamsから受け取った内容を検証します。** ID プロバイダーでボットを承認したユーザーが、ボットとチャットしているユーザーと同じであることを確認するために [、2 段階の認証](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) 検証が実行されます。 これは [、中間者](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) と [フィッシング](https://en.wikipedia.org/wiki/Phishing) 攻撃から保護します。 ボットは検証コードを生成し、ユーザーに関連付けられたコードを保存します。 確認コードは、以下のTeamsによって自動的に送信されます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. OAuth コールバックは、 を呼び出すページをレンダリング `notifySuccess("<verification code>")` します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teamsポップアップ ウィンドウを閉じ、 `<verification code>` 送信したメッセージを `notifySuccess()` ボットに送信します。 ボットは、 と共に [呼び出し](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) メッセージを受信 `name = signin/verifyState` します。
11. ボットは、ユーザーの仮トークンに保存されている確認コードに対して受信確認コードをチェックします。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. 一致する場合、ボットはトークンを検証済みで使用できる状態としてマークします。 それ以外の場合、認証フローは失敗し、ボットは暫定トークンを削除します。

    > [!NOTE]
    > モバイルでの認証に関する問題が発生した場合は、JavaScript SDK がバージョン 1.4.1 以降に更新されていることを確認してください。

## <a name="code-sample"></a>コード サンプル

ボット認証プロセスを示すサンプル コード:

| **サンプル名** | **説明** | **Node.js** | **.NET** | **Python** |
|-----------------|----------------|--------------|----------|-----------|
| Teams認証 | このサンプルでは、Microsoft Teams アプリでの認証を示します。 | [View](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) | | |
| ボット認証 | このサンプルでは、Microsoft Teamsで実行するボットに認証を使用する方法を実証します。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth)

## <a name="see-also"></a>関連項目

[Teamsボットに認証を追加する](add-authentication.md)
