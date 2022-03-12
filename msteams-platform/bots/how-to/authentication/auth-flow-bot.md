---
title: Microsoft Teamsの認証フロー
description: コード サンプルMicrosoft Teamsボットの認証フローを説明します。
keywords: teams 認証フロー ボット
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 30e7817ba72dbca50852b91b4c5791f8ece1a36a
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453027"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>サーバー内のボットの認証フロー Microsoft Teams

OAuth 2.0 は、ユーザーや他の多くの ID プロバイダーが使用する認証と承認Azure Active Directory標準です。 OAuth 2.0 の基本的な理解は、認証を使用する場合の前提条件Teams。[ここでは、正式な仕様よりも](https://aaronparecki.com/oauth-2-simplified/)簡単にフォローできる優れた概要[を示します](https://oauth.net/2/)。 タブとボットの認証フローは少し異なります。タブは Web サイトと非常に似ているので、OAuth 2.0 を直接使用できますが、ボットはそうではなく、いくつかの異なる方法で行う必要がありますが、コア概念は同じです。

Node.js および [OAuth 2.0](https://oauth.net/2/grant-types/authorization-code/) 認証[](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs)コード付与の種類を使用するボットの認証フローを示す例については、「GitHub Microsoft Teams 認証サンプル」を参照してください。

![ボット認証シーケンス図](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. ユーザーはボットにメッセージを送信します。
2. ボットは、ユーザーがサインインする必要があるかどうかを判断します。
   この例では、ボットはアクセス トークンをユーザー データ ストアに格納します。 選択した ID プロバイダーの検証済みトークンが存在しない場合は、ユーザーにサインインを求めるメッセージが表示されます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. ボットは、認証フローの開始ページへの URL を作成し、アクションを使用してユーザーにカードを送信 `signin` します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))</br>
    Teams `validDomains` の他のアプリケーション認証フローと同様に、スタート ページは、リスト上のドメインと、ログイン後のリダイレクト ページと同じドメインに含める必要があります。
    > [!IMPORTANT]
    > OAuth 2.0 `state` 承認コード付与フローは、クロスサイト要求フォージェリ攻撃を防止するために一意のセッション トークンを含む認証要求のパラメーターを呼び出 [します](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。 この例では、ランダムに生成された GUID を使用します。
4. ユーザーがサインイン *ボタンを選択* するとTeamsポップアップ ウィンドウが開き、スタート ページに移動します。
   > [!NOTE]
   > ポップアップ ウィンドウのサイズは、URL の幅と高さのクエリ文字列パラメーターを使用して制御できます。 たとえば、width=600 と height=600 を追加すると、ポップアップ ウィンドウのサイズは 600x600 ピクセルになります。 ポップアップ ウィンドウの実際のサイズは、メイン ウィンドウ のサイズに対する割合Teams制限されます。 ウィンドウのTeams小さい場合、ポップアップ ウィンドウは指定したサイズより小さくて小さになります。

5. スタート ページは、ユーザーを ID プロバイダーのエンドポイントにリダイレクト `authorize` します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. プロバイダーのサイトで、ユーザーはサインインし、ボットへのアクセスを許可します。
7. プロバイダーは、承認コードを使用してボットの OAuth リダイレクト ページにユーザーを移動します。
8. ボットはアクセス トークンの承認コードを引き換え、サインイン フローを開始したユーザーとトークンを暫定的に関連付ける。 以下では、これを暫定 *トークンと呼ぶ*。
    * この例では `state` 、ボットはパラメーターの値をサインイン プロセスを開始したユーザーの ID `state` に関連付け、後で ID プロバイダーによって返される値と一致することができます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
      > [!IMPORTANT]
      > ボットは ID プロバイダーから受け取ったトークンを格納し、それを特定のユーザーに関連付けしますが、"保留中の検証" としてマークされます。
    * 暫定トークンは、それ以上の検証なしでは使用できません。
      1. **ID プロバイダーから受け取った情報を検証します。** パラメーターの値は、 `state` 以前に保存した値に対して確認する必要があります。
      1. **アプリから受け取った情報をTeams。** ID [プロバイダーを使用して](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) ボットを承認したユーザーが、ボットとチャットしているユーザーと同じことを確認するために、2 段階認証の検証が実行されます。 これにより、中間 [者や](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) フィッシング攻撃 [から保護](https://en.wikipedia.org/wiki/Phishing) されます。 ボットは検証コードを生成し、ユーザーに関連付けられたコードを格納します。 検証コードは、以下に示すTeamsによって自動的に送信されます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. OAuth コールバックは、 を呼び出すページをレンダリングします `notifySuccess("<verification code>")`。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teamsウィンドウを閉じ、送信されたウィンドウを`<verification code>`ボット`notifySuccess()`に送信します。 ボットは、 を指定して [呼び出し](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) メッセージを受信します `name = signin/verifyState`。
11. ボットは、受信検証コードを、ユーザーの暫定トークンに格納されている検証コードと照合します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. 一致する場合、ボットはトークンを検証済みとしてマークし、すぐに使用できます。 それ以外の場合、認証フローは失敗し、ボットは暫定トークンを削除します。

    > [!NOTE]
    > モバイルでの認証に問題が発生した場合は、JavaScript SDK がバージョン 1.4.1 以降に更新されている必要があります。

## <a name="code-sample"></a>コード サンプル

ボット認証プロセスを示すサンプル コード:

| **サンプルの名前** | **説明** | **Node.js** | **.NET** | **Python** |
|-----------------|----------------|--------------|----------|-----------|
| Teams認証 | このサンプルでは、アプリでの認証Microsoft Teams示します。 | [表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) | | |
| ボット認証 | このサンプルでは、アプリで実行されているボットに認証を使用する方法をMicrosoft Teams | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth)

## <a name="see-also"></a>関連項目

[Teams ボットに認証を追加する](add-authentication.md)
