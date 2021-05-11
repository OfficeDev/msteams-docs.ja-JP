---
title: パートナー センターの開発者アカウントを作成する
description: アプリをアプリ ストアに発行Microsoft Teamsパートナー センターの開発者アカウントが必要です。
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 768a711bc60c11c17c7016f9ec63a8a09915a6e5
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101894"
---
# <a name="create-a-partner-center-developer-account"></a>パートナー センターの開発者アカウントを作成する

アプリをパートナー ストアに発行Microsoft Teams、パートナー センターの開発者アカウント[を設定する必要があります](https://docs.microsoft.com/office/dev/store/open-a-developer-account)。 シナリオによっては、既存のアカウントを使用できる場合があります。

## <a name="faq"></a>よくあるご質問 (FAQ)

パートナー センター アカウントの管理に関する一般的な質問に対する回答を取得します。

<br>

<details>

<summary><b>パートナー センター アカウントを作成する方法</b></summary>

パートナー センター アカウントは、次のいずれかの方法で作成できます。

* パートナー センターを使い、Microsoft ネットワーク アカウントを持ってない場合は、[パートナー センターの登録] ページ [を使用してアカウントを作成します](/office/dev/store/open-a-developer-account#create-an-account-using-the-partner-center-enrollment-page)。
* 既に Microsoft パートナー ネットワークに登録している場合は、既存の Microsoft パートナー センターの登録を使用して、パートナー センターから直接アカウント [を作成します](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)。

<br>

</details>

<details>

<summary><b>パートナー センターで自分のアカウントが見つからなかった場合は、</b></summary>

パートナー センターの [サポート チケットを開き、](https://partner.microsoft.com/support/v2/?stage=1) 次の項目を選択します。

| メニュー | オプション |
| -------   | -------  |
|カテゴリ| 商用マーケットプレース|
| トピック | 一般的な Marketplace のヘルプと使い方に関する質問 |
| サブトピック| Office アドイン |

<br>

</details>

<details>

<summary><b>パートナー センター アカウントの問題のサポートはどこで受け取れるのですか?</b></summary>

発行元 [のサポート ページにアクセスして](https://aka.ms/marketplacepublishersupport) 、問題を検索します。 ガイダンスが役に立たなかった場合は、パートナー センターの [サポート チケットを作成します](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)。

<br>

</details>

<details>

<summary><b>パートナー センターで自分の Office ストア アカウントを管理する方法</b></summary>

詳細については [、「パートナー センターを通じてアカウントを管理する」](/office/dev/store/manage-account-settings-and-profile) を参照してください。

<br>

</details>

<details>

<summary><b>電話番号にエリア コードが含めないので、プロファイルに電話番号を追加する方法を確認します。</b></summary>

電話番号には、国コード、地域コード、電話番号の 3 つの部分があります。 電話番号にエリア コードが含されていない場合は、2 番目のボックスを空のままにして、3 番目のボックスに入力します。

<br>

</details>

<details>

<summary><b>パートナー センターでアカウント設定とパートナー プロファイルを管理する方法</b></summary>

詳細については [、「アカウント設定とプロファイル情報の管理」](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) を参照してください。

<br>

</details>

<details>

<summary><b>アプリを提出しようとするときに、「このアカウントは発行対象ではありません」というメッセージが表示される理由</b></summary>

アカウント検証の状態が保留中のため、この [エラー メッセージを](/partner-center/verification-responses) 受け取った。 パートナー センター ダッシュボードで状態を確認 [します](https://partner.microsoft.com/dashboard)。 [アカウント]**設定** アイコンを選択し、[開発者設定] >**アカウント>選択します**。

![パートナー センターの検証状態](~/assets/images/partner-center-verification-status.png)

<br>

</details>

<details>

<summary><b>パートナー センター のアカウント検証プロセスで確認される情報</b></summary>

検証領域は、電子メールの所有権 **、雇用、** およびビジネスの **3****つがあります**。 詳細については、「確認済み [」と「応答方法」を参照してください](/partner-center/verification-responses#what-is-verified-and-how-to-respond)。

プライマリ連絡先、グローバル管理者、またはアカウント管理者の場合は、確認の状態を監視し、プロファイル ページの進行状況を追跡できます。

検証プロセスが完了すると、プロファイル ページの登録の状態が保留中から *承認済みに**変わります*。 プライマリ連絡先は、数営業日以内に Microsoft から電子メールを受信します。

<br>

</details>

<details>

<summary><b>アカウントの確認の状態がメールの所有権を超えて進めなかった。どのように進める必要がありますか?</b></summary>

電子メール **所有権の検証** プロセス中に、確認メールがプライマリ連絡先に送信されます。 メインの連絡先の受信トレイで、[必要な maccount@microsoft.com] という件名のメールを確認します **。Microsoft** でメール アカウントを確認し、電子メールの検証プロセスを完了します。 確認メールは、パートナー センター のアカウント設定に記載されているアドレスに送信されます。

電子メールの検証プロセスについては、次の情報を覚えておいてください。

* 電子メール検証リンクは 7 日間のみ有効です。
* パートナー プロファイル ページにアクセスし、[確認メールの再送信] リンクを選択すると、電子メールの再送信 **を要求** できます。
* メールを確実に受信するには、安全なドメイン microsoft.com **リストを** 作成し、迷惑メール フォルダーを確認します。

<br>

</details>

<details>

<summary><b>アカウント関連の問題に対するサポートを受け取る方法</b></summary>

詳細 [については、「パートナー センターの商用マーケットプレース プログラムのサポート」を](/azure/marketplace/partner-center-portal/support) 参照してください。

<br>

</details>

<details>

<summary><b>メール フォルダーを確認し、確認メールを受信していない。次に何をする必要がありますか?</b></summary>

以下の操作を試してください。

* 迷惑メールフォルダーまたはスパム フォルダーを確認します。
* ブラウザー キャッシュをクリアし、パートナー センター アカウント ダッシュボードに移動し、[検証メールの再送信 **] を選択します**。
* 別のブラウザーから **[再送信確認メール** ] リンクにアクセスしてみてください。
* IT 部門と一緒に作業して、確認メールが電子メール サーバーによってブロックされていないことを確認します。
* サーバーのスパム フィルターを調整して、サーバーからのすべてのメールを許可または **maccount@microsoft.com。**

<br>

</details>

<details>

<summary><b>通常、雇用確認プロセスにはどのくらいの時間が必要ですか?</b></summary>

提出された詳細が正しい場合、雇用確認プロセスの完了には約 2 時間かかります。

<br>

</details>

<details>

<summary><b>ビジネス検証プロセスには通常どれくらいの時間が必要ですか?</b></summary>

必要なすべてのドキュメントが提出された場合、ビジネス検証の完了には 1 日から 2 営業日かかります。

<br>

</details>

<details>

<summary><b>サポート チームに連絡を取った場合、チケットは迅速に行いますか?</b></summary>

サポート チケットは 1 週間で解決されます。 サポート チケットの作成時に指定したメールに送信された更新プログラムを確認します。

<br>

</details>

<details>

<summary><b>サポート チケットを作成しましたが、7 営業日以内に更新プログラムを受け取っていない。ヘルプはどこで受け取れるのですか?</b></summary>

次の詳細を含む <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a> メールを送信します。

* **件名 :** パートナー センター アカウントの問題 *<your app name>*
* **メール本文**:
    * サポート チケット番号
    * 販売者 ID
    * 問題のスクリーンショット (可能な場合)

<br>

</details>

<details>

<summary><b>パートナー センターのヘルプについては、他にどこに移動できますか?</b></summary>

次のリソースも支援できます。

* [Microsoft 365申請に関する FAQ](/office/dev/store/appsource-submission-faq)
* [商用マーケットプレースのドキュメント](/azure/marketplace/)

<br>

</details>

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ストア送信を準備する](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
