---
title: ボットの Microsoft Teams 認証フロー
description: コード サンプルを使用して、サード パーティの OAuth プロバイダーを使用して Microsoft Teams ボット アプリの認証を有効にします。
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 67668f11fafcc8eff878d82913f002ed8c2f96bc
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2022
ms.locfileid: "67587016"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Microsoft Teams でのボットの認証フロー

OAuth 2.0 は、Azure Active Directory や他の多くの ID プロバイダーで使用される認証と承認のオープン 標準です。 OAuth 2.0 の基本的な理解は、Teams で認証を操作するための前提条件です。[ここでは、正式な仕様](https://oauth.net/2/)よりも従いやすい[優れた概要を示](https://aaronparecki.com/oauth-2-simplified/)します。 タブとボットの認証フローは少し異なります。タブは Web サイトに似ているため、OAuth 2.0 を直接使用できますが、ボットは異なる方法で行う必要はありませんが、コア概念は同じです。

Node.jsと [OAuth 2.0 承認コード付与の種類](https://oauth.net/2/grant-types/authorization-code/)を使用したボットの認証フローを示す例については、[GitHub リポジトリの Microsoft Teams 認証サンプル](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs)を参照してください。

![ボット認証シーケンス図](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. ユーザーはボットにメッセージを送信します。
2. ボットは、ユーザーがサインインする必要があるかどうかを決定します。
   この例では、ボットはアクセス トークンをユーザー データ ストアに格納します。 選択した ID プロバイダーの検証済みトークンがない場合は、サインインするようにユーザーに求めます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. ボットは、認証フローの開始ページへの URL を作成し、アクションを使用してユーザーにカードを `signin` 送信します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))</br>
    Teams の他のアプリケーション認証フローと同様に、スタート ページは、一覧にある `validDomains` ドメインと、ログイン後のリダイレクト ページと同じドメインにある必要があります。
    > [!IMPORTANT]
    > OAuth 2.0 承認コード許可フローは、クロス[サイト要求フォージェリ攻撃](https://en.wikipedia.org/wiki/Cross-site_request_forgery)を防ぐための一意のセッション トークンを含む認証要求のパラメーターを呼び出`state`します。 この例では、ランダムに生成された GUID を使用します。
4. ユーザーが *サインイン* ボタンを選択すると、Teams によってポップアップ ウィンドウが開き、スタート ページに移動します。
   > [!NOTE]
   > ポップアップ ウィンドウのサイズは、URL の幅と高さのクエリ文字列パラメーターを使用して制御できます。 たとえば、width=600 と height=600 を追加すると、ポップアップ ウィンドウのサイズは 600 x 600 ピクセルになります。 ポップアップ ウィンドウの実際のサイズは、Teams のメイン ウィンドウ サイズの割合として上限が設定されます。 Teams ウィンドウが小さい場合、ポップアップ ウィンドウは指定したディメンションより小さくなります。

5. スタート ページでは、ID プロバイダーのエンドポイントにユーザーが `authorize` リダイレクトされます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. プロバイダーのサイトで、ユーザーはサインインし、ボットへのアクセスを許可します。
7. プロバイダーは、承認コードを使用して、ユーザーをボットの OAuth リダイレクト ページに移動します。
8. ボットは、アクセス トークンの承認コードを引き換え、サインイン フローを開始したユーザーと **トークンを暫定的に** 関連付けます。 以下では、これを *仮トークン* と呼びます。
    * この例では、ボットはパラメーターの値を `state` サインイン プロセスを開始したユーザーの ID に関連付け、後で ID プロバイダーから返された値と `state` 照合できるようにします。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
      > [!IMPORTANT]
      > ボットは、ID プロバイダーから受け取ったトークンを格納し、特定のユーザーに関連付けますが、"保留中の検証" としてマークされます。
    * 仮トークンは、それ以上の検証なしでは使用できません。
      1. **ID プロバイダーから受け取った内容を検証します。** パラメーターの値は、 `state` 前に保存されたものに対して確認する必要があります。
      1. **Teams から受け取った内容を検証します。** ID プロバイダーでボットを承認したユーザーが、ボットとチャットしているユーザーと同じであることを確認するために、 [2 段階認証](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) 検証が実行されます。 これにより、 [中間者](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) 攻撃や [フィッシング攻撃から](https://en.wikipedia.org/wiki/Phishing) 保護されます。 ボットは検証コードを生成し、ユーザーに関連付けられた検証コードを格納します。 確認コードは、以下で説明するように Teams によって自動的に送信されます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. OAuth コールバックは、を呼び出 `notifySuccess("<verification code>")`すページをレンダリングします。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams によってポップアップ ウィンドウが閉じられ、送信されたメッセージ`notifySuccess()`が`<verification code>`ボットに送信されます。 ボットは、 .[](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) `name = signin/verifyState`
11. ボットは、受信確認コードを、ユーザーの仮トークンと共に格納された検証コードと照合します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. 一致する場合、ボットはトークンを検証済みとしてマークし、使用する準備が整います。 それ以外の場合、認証フローは失敗し、ボットは仮トークンを削除します。

    > [!NOTE]
    > モバイルでの認証に関する問題が発生した場合は、JavaScript SDK がバージョン 1.4.1 以降に更新されていることを確認してください。

## <a name="code-sample"></a>コード サンプル

ボット認証プロセスを示すサンプル コード:

| **サンプルの名前** | **説明** | **Node.js** | **.NET** | **Python** |
|-----------------|----------------|--------------|----------|-----------|
| Teams 認証 | このサンプルでは、Microsoft Teams アプリでの認証を示します。 | [表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) | | |
| ボット認証 | このサンプルでは、Microsoft Teams で実行されているボットの認証を使用する方法を示します | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth) | [表示](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth)

## <a name="see-also"></a>関連項目

[Teams ボットに認証を追加する](add-authentication.md)
