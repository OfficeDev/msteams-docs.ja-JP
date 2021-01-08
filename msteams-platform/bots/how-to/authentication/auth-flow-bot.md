---
title: ボットの Microsoft Teams 認証フロー
description: ボットでの Microsoft Teams 認証フローについて説明します
keywords: teams 認証フロー ボット
ms.topic: overview
ms.openlocfilehash: 3d1d0055984de07b50a45015e062e6725279d1aa
ms.sourcegitcommit: b9771f8f4be9ac1ff8c85c2d7bd8d5c5408bc653
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/06/2021
ms.locfileid: "49768082"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Microsoft Teams のボットの認証フロー

OAuth 2.0 は、Azure Active Directory (Azure AD) および他の多くの ID プロバイダーが使用する認証および承認のオープン スタンダードです。 OAuth 2.0 の基本的な理解は、Teams で認証を操作する場合の前提条件です。 [ここでは、正式な仕様よりも](https://aaronparecki.com/oauth-2-simplified/) 簡単に従える優れた概要を [示します](https://oauth.net/2/)。 タブとボットの認証フローは少し異なります。タブは Web サイトに非常に似ているので、OAuth 2.0 を直接使用できますが、ボットはいくつかの操作を異なる方法で行う必要はありません。ただし、中心概念は同じです。

Node.js と[OAuth 2.0](https://oauth.net/2/grant-types/authorization-code/)認証コード付与の種類を使用したボットの認証フローを示す例については、GitHub リポジトリ[の Microsoft Teams](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)認証サンプルを参照してください。

![ボット認証シーケンス図](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. ユーザーがボットにメッセージを送信します。
2. ボットは、ユーザーがサインインする必要があるかどうかを判断します。
   この例では、ボットはアクセス トークンをユーザー データ ストアに格納します。 選択した ID プロバイダーの検証済みトークンが存在しない場合は、ユーザーにサインインを求めるメッセージが表示されます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. ボットは認証フローの開始ページへの URL を作成し、アクションを使用してユーザーにカードを送信 `signin` します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))</br>
    Teams の他のアプリケーション認証フローと同様に、スタート ページは、リスト上のドメインと、ログイン後のリダイレクト ページと同じドメインに含める `validDomains` 必要があります。
    > [!IMPORTANT] 
    > OAuth 2.0 認証コード付与フローは、クロスサイト要求フォージェリ攻撃を防ぐために、一意のセッション トークンを含む認証要求のパラメーターを呼び出 `state` [します](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。 この例では、ランダムに生成された GUID を使用します。
4. ユーザーがサインイン ボタンを選択 *すると* 、Teams がポップアップ ウィンドウを開き、スタート ページに移動します。
   > [!NOTE]
   > ポップアップ ウィンドウのサイズは、URL の幅と高さのクエリ文字列パラメーターを使用して制御できます。 たとえば、幅 = 500、高さ = 500 を追加した場合、ポップアップ ウィンドウのサイズは 500x500 ピクセルになります。 Teams は、指定されたピクセル サイズのポップアップ ウィンドウを表示します。最大サイズは、メイン ウィンドウのサイズに対する割合です。

5. 開始ページは、ユーザーを ID プロバイダーのエンドポイントにリダイレクト `authorize` します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. プロバイダーのサイトで、ユーザーはサインインし、ボットへのアクセスを許可します。
7. プロバイダーは、認証コードを使用してユーザーをボットの OAuth リダイレクト ページに移動します。
8. ボットは認証コードをアクセス トークンに引き換え、サインイン フローを開始したユーザーにトークンを暫定で関連付ける。 以下では、これを暫定 *トークンと呼ぶ必要があります*。
    * この例では、ボットはパラメーターの値をサインイン プロセスを開始したユーザーの ID に関連付け、後で ID プロバイダーから返された値と一致できます `state` `state` 。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
      > [!IMPORTANT] 
      > ボットは ID プロバイダーから受け取ったトークンを格納し、それを特定のユーザーに関連付け、"保留中の検証" としてマークされます。 
    * 暫定トークンは、それ以上の検証を行わずに使用できません。
      1. **ID プロバイダーから受信した情報を検証します。** パラメーターの値は `state` 、以前に保存された値に対して確認する必要があります。 
      1. **Teams から受け取った情報を検証します。** ID [プロバイダーでボット](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) を承認したユーザーが、ボットとチャットしているユーザーと同じユーザーである必要がある場合は、2 段階認証検証が実行されます。 これにより[、man-in-the-middle 攻撃や](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)[フィッシング攻撃から](https://en.wikipedia.org/wiki/Phishing)保護されます。 ボットは検証コードを生成し、ユーザーに関連付けられたコードを保存します。 確認コードは、次に示すとおり、Teams によって自動的に送信されます。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. OAuth コールバックは、呼び出すページをレンダリングします `notifySuccess("<verification code>")` 。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams はポップアップ ウィンドウを閉じ、送信されたメッセージ `<verification code>` `notifySuccess()` をボットに送り返します。 ボットが次の呼び出し [メッセージを](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) 受信します `name = signin/verifyState` 。
11. ボットは、受信検証コードを、ユーザーの暫定トークンと一緒に格納されている検証コードと照合します。 ([コードの表示](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. 一致する場合、ボットはトークンを検証済みで使用できる状態としてマークします。 それ以外の場合、認証フローは失敗し、ボットは暫定トークンを削除します。

    > [!NOTE]
    > モバイルでの認証に問題が発生した場合は、JavaScript SDK がバージョン 1.4.1 以降に更新されている必要があります。

## <a name="samples"></a>サンプル

ボット認証プロセスを示すサンプル コードについては、以下を参照してください。

[Microsoft Teams ボット認証のサンプル (Node.js)](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)

## <a name="more-details"></a>詳細情報

Azure 認証をターゲットとするボット認証の詳細な実装チュートリアルについてはAD参照してください。

[Teams ボットに認証を追加する](add-authentication.md)
