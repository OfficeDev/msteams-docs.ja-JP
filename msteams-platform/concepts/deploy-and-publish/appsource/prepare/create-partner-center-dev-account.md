---
title: パートナー センターの開発者アカウントを作成する
description: アプリをMicrosoft Teams ストアに公開するには、パートナー センターの開発者アカウントが必要です。
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: ac31ff3d46a87814edfe2b7ec789d183e9c02e2f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566041"
---
# <a name="create-a-partner-center-developer-account"></a>パートナー センターの開発者アカウントを作成する

アプリを Microsoft Teams ストアに公開するには、[パートナー センターの開発者アカウント を設定する](/office/dev/store/open-a-developer-account)必要があります。 シナリオによっては、既存のアカウントを使用できる場合があります。

## <a name="faq"></a>FAQ

パートナー センター アカウントの管理に関してよく寄せられる質問に対する回答を得ます。

<br>

<details>

<summary><b>パートナー センター アカウントを作成する方法</b></summary>

パートナー センター アカウントは、次のいずれかの方法で作成できます。

* パートナー センターを使用する際に Microsoft ネットワーク アカウントを持っていない場合は、 [パートナー センターの登録ページ を使用してアカウントを作成](/office/dev/store/open-a-developer-account#create-an-account-using-the-partner-center-enrollment-page)します。
* 既に Microsoft パートナー ネットワークに登録している場合は、 [既存の Microsoft パートナー センターの登録を使用して、パートナー センターから直接アカウントを作成](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)します。

<br>

</details>

<details>

<summary><b>パートナー センターでアカウントが見つからない場合はどうしたらいいですか?</b></summary>

パートナー [センターのサポート チケット](https://partner.microsoft.com/support/v2/?stage=1) を開き、次の項目を選択します。

| メニュー | オプション |
| -------   | -------  |
|カテゴリ| 商業市場|
| トピック | 一般的なマーケットプレースヘルプとハウツーの質問 |
| サブトピック| Office アドイン |

<br>

</details>

<details>

<summary><b>パートナー センター アカウントの問題のサポートはどこで受けられますか?</b></summary>

問題を検索するには [、パブリッシャーのサポート ページ](https://aka.ms/marketplacepublishersupport) にアクセスします。 ガイダンスが役に立たない場合は、 [パートナー センター のサポート チケット](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)を作成します。

<br>

</details>

<details>

<summary><b>パートナー センターでOffice ストア アカウントを管理するにはどうすればよいですか。</b></summary>

詳細については、 [パートナー センターを通じてアカウントを管理する](/office/dev/store/manage-account-settings-and-profile) を参照してください。

<br>

</details>

<details>

<summary><b>電話番号に市外局番が付いていないので、プロフィールに追加するにはどうすればよいですか?</b></summary>

電話番号には、国番号、市外局番、電話番号の 3 つの部分があります。 電話番号に市外局番が含まれていない場合は、2 番目のボックスを空のままにして、3 番目のボックスに入力します。

<br>

</details>

<details>

<summary><b>パートナー センターでアカウント設定とパートナー プロフィールを管理するにはどうすればよいですか。</b></summary>

詳細については、「 [アカウント設定とプロファイル情報の管理](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) 」をご覧ください。

<br>

</details>

<details>

<summary><b>アプリを送信しようとすると、「このアカウントは公開対象外です」というメッセージが表示されるのはなぜですか?</b></summary>

[アカウントの確認ステータス](/partner-center/verification-responses)が保留中であるため、このエラー メッセージが表示されました。 パートナー センター [ダッシュボード](https://partner.microsoft.com/dashboard)で状態を確認します。 **設定** 歯車アイコンを選択し、[**アカウント>アカウント設定] > [開発者設定]** を選択します。

![パートナー センターの確認状態](~/assets/images/partner-center-verification-status.png)

<br>

</details>

<details>

<summary><b>パートナー センターのアカウント確認プロセスで確認される内容</b></summary>

**電子メールの所有権**、**雇用**、および **ビジネス** の 3 つの検証領域があります。 詳細については、 の [検証内容と応答方法を](/partner-center/verification-responses#what-is-verified-and-how-to-respond)参照してください。

メインの連絡先、グローバル管理者、またはアカウント管理者の場合は、プロフィールページで確認ステータスを監視し、進捗状況を追跡できます。

検証プロセスが完了すると、プロファイル ページでの登録の状態が *[保留中]* から *[承認済* み] に変わります。 その後、主な連絡先は、数営業日以内に Microsoft から電子メールを受信します。

<br>

</details>

<details>

<summary><b>アカウントの確認ステータスが電子メールの所有権を超えて進んでいない。どのように進めるか?</b></summary>

E **メール所有権** の確認プロセス中に、確認メールが取引先責任者に送信されます。 件名が必要な [アクション] が含 **まれる maccount@microsoft.com** からの電子メールをメインの連絡先の受信トレイで確認してください: Microsoft **で電子メール アカウントを確認** し、電子メールの確認プロセスを完了します。 確認メールは、パートナー センターアカウント設定に記載されているアドレスに送信されます。

電子メールの確認プロセスについて、次の点に注意してください。

* 電子メールの確認リンクは、7 日間のみ有効です。
* パートナープロフィールページにアクセスし、[確認メールの再送信] リンクを選択して、 **メールの再送信** をリクエストできます。
* 電子メールを確実に受信するには、安全な **リスト microsoft.com** 安全なドメインとして、迷惑メールフォルダーを確認してください。

<br>

</details>

<details>

<summary><b>アカウント関連の問題に対するサポートを追加するにはどうすればよいですか。</b></summary>

詳細については [、パートナー センターのコマーシャル マーケットプレース プログラムのサポート](/azure/marketplace/partner-center-portal/support) を参照してください。

<br>

</details>

<details>

<summary><b>メールフォルダを確認し、確認メールを受信していません。次に何をしなければなりませんか?</b></summary>

以下の操作を試してください。

* 迷惑メールまたはスパムフォルダを確認します。
* ブラウザのキャッシュをクリアし、パートナー センター アカウント ダッシュボードに移動して、[ **確認メールを再送信**] を選択します。
* 別のブラウザから **確認メールを再送信** するリンクにアクセスしてみてください。
* IT 部門と協力して、確認メールが電子メール サーバーによってブロックされないようにします。
* サーバーのスパムフィルタを調整して **、maccount@microsoft.com** からのメールをすべて許可または安全にリストします。

<br>

</details>

<details>

<summary><b>雇用確認プロセスは通常どのくらいの時間がかかりますか?</b></summary>

提出された詳細がすべて正しければ、雇用確認プロセスが完了するまでに約2時間かかります。

<br>

</details>

<details>

<summary><b>ビジネス検証プロセスは通常どのくらいの時間がかかりますか?</b></summary>

必要な書類がすべて提出された場合、業務の確認には1~2営業日かかります。

<br>

</details>

<details>

<summary><b>サポートチームに連絡を取った場合、航空券は迅速に発行されますか?</b></summary>

サポートチケットは1週間後に解決されます。 サポートチケットの作成時に指定したメールに送信された更新を確認します。

<br>

</details>

<details>

<summary><b>サポート チケットを作成しましたが、7 営業日で更新を受け取っていません。どこで助けを得るのですか?</b></summary>

次の詳細を <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a> に電子メールを送信します。

* **件名 :** パートナー センター アカウントの問題 *<your app name>* です。
* **電子メールの本文**:
    * サポートチケット番号。
    * あなたの売り手ID。
    * 問題のスクリーンショット (可能な場合)。

<br>

</details>

<details>

<summary><b>パートナー センターのヘルプは、他にどこに行くことができますか?</b></summary>

次のリソースも役立ちます。

* [アプリの提出に関するFAQをMicrosoft 365。](/office/dev/store/appsource-submission-faq)
* [商用市場のドキュメント](/azure/marketplace/)

<br>

</details>

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ストア送信を準備する](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
