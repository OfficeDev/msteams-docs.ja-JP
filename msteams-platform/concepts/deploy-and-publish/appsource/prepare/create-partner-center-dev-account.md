---
title: パートナー センターの開発者アカウントを作成する
description: アプリを Microsoft Teams ストアに公開するためにパートナー センター開発者アカウントを作成するときの FAQ。
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: aa2d0b7f30f049c800b31705900ddc81ea1d91cc
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232191"
---
# <a name="create-a-partner-center-developer-account"></a>パートナー センターの開発者アカウントを作成する

アプリを Microsoft Teams ストアに公開するには、[パートナー センター開発者アカウントを設定する](/office/dev/store/open-a-developer-account)必要があります。 シナリオによっては、既存のアカウントを使用できる場合があります。

## <a name="faq"></a>よくあるご質問 (FAQ)

パートナー センター アカウントの管理に関する一般的な質問への回答を入手してください。

<br>

<details>

<summary><b>パートナー センター アカウントを作成するにはどうすればよいですか?</b></summary>

パートナー センター アカウントは、次のいずれかの方法で作成できます。

* パートナー センターを初めて使用し、Microsoft ネットワーク アカウントをお持ちでない場合は、[パートナー センターの登録ページを使用してアカウントを作成します](/office/dev/store/open-a-developer-account#create-an-account-using-the-partner-center-enrollment-page)。
* 既に Microsoft パートナー ネットワークに登録している場合は、[既存の Microsoft パートナー センターの登録を使用して、パートナー センターから直接アカウントを作成します](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)。

<br>

</details>

<details>

<summary><b>パートナー センターで自分のアカウントが見つからない場合はどうなりますか?</b></summary>

[パートナー センターのサポート チケット](https://partner.microsoft.com/support/v2/?stage=1)を開き、次を選択します。

| メニュー | オプション |
| -------   | -------  |
|カテゴリ| 商用マーケットプレース|
| トピック | 一般的なマーケットプレイスのヘルプと使い方の質問 |
| サブトピック| Office アドイン |

<br>

</details>

<details>

<summary><b>パートナー センター アカウントの問題のサポートはどこで受けられますか?</b></summary>

[発行元のサポート ページ](https://aka.ms/marketplacepublishersupport)にアクセスして、問題を検索してください。 ガイダンスが役に立たない場合は、[パートナー センターのサポート チケット](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)を作成します。

<br>

</details>

<details>

<summary><b>パートナー センターで Office ストア アカウントを管理するにはどうすればよいですか?</b></summary>

詳細については、「[パートナー センターを通じたアカウントの管理](/office/dev/store/manage-account-settings-and-profile)」を参照してください。

<br>

</details>

<details>

<summary><b>電話番号に市外局番がないので、プロファイルに追加するにはどうすればよいですか?</b></summary>

電話番号には、国番号、市外局番、電話番号の 3 つの部分があります。 電話番号に市外局番が含まれていない場合は、2 番目のボックスを空のままにして、3 番目のボックスに入力します。

<br>

</details>

<details>

<summary><b>パートナー センターでアカウント設定とパートナー プロファイルを管理するにはどうすればよいですか?</b></summary>

詳細については、「[アカウント設定とプロファイル情報の管理](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info)」を参照してください。

<br>

</details>

<details>

<summary><b>アプリを送信しようとすると、「このアカウントは公開対象ではありません」というメッセージが表示されるのはなぜですか?</b></summary>

[アカウント認証状態](/partner-center/verification-responses)が保留中であるため、このエラー メッセージが表示されました。 パートナー センターの[ダッシュボード](https://partner.microsoft.com/dashboard)で状態を確認してください。 **[設定]** 歯車アイコンを選択し、**[開発者設定] > [アカウント] > [アカウント設定]** を選択します。

![パートナー センターの検証状態](~/assets/images/partner-center-verification-status.png)

<br>

</details>

<details>

<summary><b>パートナー センターのアカウント検証プロセスで何が検証されますか?</b></summary>

検証領域には、**メールの所有権**、**雇用**、**ビジネス** の 3 つがあります。 詳細については、「[検証内容と対応方法](/partner-center/verification-responses#what-is-verified-and-how-to-respond)」を参照してください。

主な連絡先、グローバル管理者、またはアカウント管理者の場合は、プロフィール ページで検証状態を監視し、進行状況を追跡できます。

検証プロセスが完了すると、プロフィール ページの登録状態が *保留中* から *承認済み* に変わります。 その後、主な連絡先は、数営業日以内に Microsoft からメールを受信します。

<br>

</details>

<details>

<summary><b>アカウント検証状態は、メールの所有権を超えて進んでいません。どうすればいいですか?</b></summary>

**メールの所有権** の検証プロセス中に、確認メールが主な連絡先に送信されます。 主な連絡先の受信トレイで、件名 "**必要なアクション: Microsoft でメール アカウントを確認し**、メールの検証プロセスを完了してください" の **maccount@microsoft.com** からのメールを確認してください。 確認メールは、パートナー センターのアカウント設定に記載されているアドレスに送信されます。

メールの検証プロセスについては、次の点に注意してください。

* メール検証リンクは 7 日間のみ有効です。
* パートナーのプロフィール ページにアクセスし、**[確認メールの再送信]** リンクを選択すると、メールの再送信を要求できます。
* メールを確実に受信するには、安全なドメインとして **microsoft.com** を安全にリストし、迷惑メール フォルダーを確認します。

<br>

</details>

<details>

<summary><b>メール フォルダーを確認しましたが、確認メールが届きません。次に何をしなければなりませんか?</b></summary>

以下の操作を試してください。

* 迷惑メール フォルダーを確認してください。
* ブラウザーのキャッシュをクリアし、パートナー センター アカウントのダッシュボードに移動して、**[確認メールを再送信]** を選択します。
* 別のブラウザーから **[確認メールの再送信]** リンクにアクセスしてみてください。
* IT 部門と協力して、確認メールがメール サーバーによってブロックされていないことを確認します。
* サーバーのスパム フィルターを調整して、**maccount@microsoft.com** からのすべてのメールを許可または安全にリストします。

<br>

</details>

<details>

<summary><b>雇用検証プロセスには通常どのくらい時間がかかりますか?</b></summary>

提出されたすべての詳細が正しければ、雇用検証プロセスは完了するのに約 2 時間かかります。

<br>

</details>

<details>

<summary><b>ビジネス検証プロセスには通常どのくらい時間がかかりますか?</b></summary>

必要な書類がすべて提出された場合、ビジネスの検証が完了するまでに 1 - 2 営業日かかります。

<br>

</details>

<details>

<summary><b>サポート チームに連絡した場合、チケットは迅速に処理されますか?</b></summary>

サポート チケットは 1 週間で解決されます。 サポート チケットの作成時に提供したメール アドレスに送信された更新を確認します。

<br>

</details>

<details>

<summary><b>サポート チケットを作成しましたが、7 営業日経っても更新が届きません。どこでサポートを受けることができますか?</b></summary>

次の詳細を記載したメールを <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a> に送信します。

* **件名**: *アプリ名* のパートナー センター アカウントの問題。
* **メール本文**:
  * サポート チケット番号。
  * 販売者 ID。
  * 問題のスクリーンショット (可能な場合)。

<br>

</details>

<details>

<summary><b>パートナー センターのサポートは他にどこにありますか?</b></summary>

次のリソースも役立ちます。

* [Microsoft 365 アプリの提出に関する FAQ](/office/dev/store/appsource-submission-faq)。
* [商用マーケットプレースのドキュメント](/azure/marketplace/)。

<br>

</details>

## <a name="update-apple-app-store-connect-team-id-on-partner-center"></a>パートナー センターで Apple App Store Connect Team ID を更新する

エンドユーザーが Teams iOS プラットフォームにアプリをインストールできるようにするには、Microsoft パートナー センターで Apple App Store Connect Team ID を更新します。 Apple App Store Connect Team ID は Apple と共有されます。 Apple App Store Connect Team ID を更新するには、次の手順に従います。

1. 全体管理者の資格情報を使用して、[Microsoft パートナー センター](https://partner.microsoft.com/dashboard/home) にログインします。
1. ページの右上隅にある設定アイコンを選択します。
1. 左側のウィンドウから、**「組織プロファイル］** の下にある **［法務情報］** セクションに移動します。
1. **［開発者］** タブを選択します。
1. Apple App Store Connect Team ID を入力します。
1. オファー ページに移動し、Teams アプリを再発行します。
  
Apple App Store Connect Team ID が更新され、ユーザーは Teams iOS プラットフォームにアプリをインストールできるようになりました。

Apple Developer ポータルから Apple App Store Connect Team ID を取得するには、次の手順に従います。

1. [Apple Developer Center](https://developer.apple.com/) にログインします。
1. **[アカウント]** を選択し、**[メンバーシップ]** に移動します。
1. **[メンバーシップ]** で、**Apple App Store Connect Team ID にアクセスします**。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [ストア送信を準備する](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
