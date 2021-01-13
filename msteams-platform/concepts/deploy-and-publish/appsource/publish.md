---
title: Microsoft Teams アプリ承認申請プロセスガイダンス
description: Microsoft Teams アプリ ストアにアプリを公開する申請の承認プロセスについて説明します。
keywords: teams publish store office publishing publish AppSource partner center account verification apps account not publish eligible
ms.openlocfilehash: 6268d408cc4c44633b9b3629c902044815639176
ms.sourcegitcommit: db19fee033b41152267bb524d67aee5b7f64b04a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797483"
---
# <a name="submit-your-app-to-appsource"></a>AppSource にアプリを提出する

## <a name="teams-app-submission"></a>Teams アプリの申請

[AppSource](https://appsource.microsoft.com)にアプリを発行すると、Teams アプリ カタログと Web でアプリを利用できます。 大きなレベルでは、AppSource にアプリを提出するプロセスは次の手順で行います。

1. 設計ガイドラインに従ってアプリ [を開発します](~/concepts/design/understand-use-cases.md)。 タブは、デスクトップと Web、モバイルの両方のタブ設計ガイドライン [に従う](~/tabs/design/tabs.md) 必要 [があります](~/tabs/design/tabs-mobile.md)。 ボットは、ボットの設計 [ガイドラインに従う必要があります](~/bots/design/bots.md)。
1. アプリが Microsoft Teams のアプリ [検証ポリシーを満た](/legal/marketplace/certification-policies) している必要があります。 
1. マニフェスト検証ツールを使って [アプリを自己テストします](prepare/submission-checklist.md#teams-app-validation-tool) 。
1. [パートナー センターで開発者アカウント](/office/dev/store/open-a-developer-account) を [セットアップします](https://support.microsoft.com/help/4499930/partner-center-overview)。 *下記の* [FAQ セクションでパートナー センター](#how-do-i-create-a-partner-center-account) アカウントを作成する方法も参照してください。
1. 提出チェックリストに従って、申請用にアプリ [を準備します](prepare/submission-checklist.md)。
1. 最も [失敗したテスト ケースを確認して、アプリ品質の承認を迅速に行います](prepare/frequently-failed-cases.md)。
1. パートナー センターから [AppSource にパッケージを提出します](/office/dev/store/use-partner-center-to-submit-to-appsource)。
1. パートナー センター ダッシュボードで承認プロセスを追跡します。 *「パートナー* [センターの概要」を参照してください](https://support.microsoft.com/help/4499930/partner-center-overview)。
1. 申請後 — 公開されたアプリの保守とサポートに [関するガイダンスを確認します](post-publish/overview.md)。

>[!NOTE]
>
>- Teams アプリは、モバイル対応である必要があります[](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment)。また、モバイル OS (iOS および Android) ではアップセルの要件に準拠する必要はありません。 
>- Teams アプリにボットが含まれている場合は、Bot Developer Framework [の実施基準に準拠する必要があります](https://aka.ms/bf-conduct)。
>- アプリに Office 365 コネクタが含まれている場合は、追加の用語が適用される場合があります。 *「コネクタ*[開発者ダッシュボードと](https://aka.ms/connectorsdashboard)アプリ開発者契約 [」を参照してください](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)。
>- GCC ユーザーがアプリを利用し、ストア内のアプリ登録情報が重複しないようにするには、認証プロセス/フローでユーザーを識別し、GCC ユーザーの指定または予想されるコンテンツ URL にユーザーをルーティングする必要があります。

## <a name="faqs--teams-apps-and-partner-account-verification-process-in-partner-center"></a>FAQ - パートナー センターでの Teams アプリとパートナー アカウント検証プロセス

## <a name="how-do-i-create-a-partner-center-account"></a>パートナー センター アカウントを作成する方法

パートナー センター アカウントを作成するには、次の 2 つの方法があります。

- パートナー センターを使い、Microsoft ネットワーク内にアカウントを持たなかった場合は、パートナー センターの登録ページを使用して [アカウントを作成します](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)。
- 既にパートナー ネットワークに登録している場合は、既存の登録を使用してパートナー センターに直接 [アカウントを作成します](/office/dev/store/)。

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a>パートナー センターで自分のストア アカウントOffice見つからでは?

パートナー センターの [サポート チケットを開](https://partner.microsoft.com/support/v2/?stage=1) き、ドロップダウン メニューから次を選択してください。

| メニュー | オプション |
| -------   | -------  |
|カテゴリ| Commercial Marketplace|
| トピック | 一般的なマーケットプレースのヘルプと使い方に関する質問 |
| サブトピック| Office アドイン |

## <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a>パートナー センター アカウントの問題に対するサポートはどこで受け取できますか?

問題のトピック [を検索し、ガイダンス](https://aka.ms/marketplacepublishersupport) を見つけるには、発行元のサポート ページにアクセスしてください。 提供されたガイダンスが役に立たない場合は、 [パートナー センターのサポート チケットを開きます](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)。

## <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a>パートナー センターでストア アカウントOffice管理する方法

パートナー センターで  [ストア アカウントOffice](/office/dev/store/manage-account-settings-and-profile) 管理する方法については、パートナー センターで Office ストア アカウントの管理にアクセスしてください。

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a>パートナー プロファイルの連絡先セクションに電話番号を追加する方法

電話番号には、国コード、エリア コード、電話番号の 3 つの部分があります。 電話番号にエリア コードが含まれる場合は、2 番目のボックスを空のままにして、3 番目のボックスに入力します。

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a>パートナー センターでアカウント設定とパートナー プロファイルを管理する方法

パートナー センターのアカウント [設定の管理に](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) 関するガイダンスについては、アカウント設定とプロファイル情報の管理ページをご覧ください。

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>パートナー センターからアドインを提出しようとするときに、「このアカウントは発行の対象ではありません」というメッセージが表示される理由は何ですか。

アカウントの確認状態が保留中の場合、上記のエラー [メッセージが](/partner-center/verification-responses) 表示されます。 パートナー センター ダッシュボードでアカウントの確認状態を確認するには、ページヘッダー シェルの右上隅にある [設定] オプション (歯車アイコン) を選択し、[開発者向け設定] の [アカウント アカウント設定] を選択します[](https://partner.microsoft.com/dashboard)  =>     =>  。

![パートナー センター のアカウント設定ページ](../../../assets/images/partner-center-accts-page.png)

![パートナー センターの確認状態](../../../assets/images/partner-center-verification-status.png)

アカウント検証プロセス中に、必要な各手順 (電子メールの所有権、雇用の確認、およびビジネスの確認) の状態が表示されます。 確認プロセスが正常に完了すると、プロファイル ページでの登録の確認状態が "保留中" から "承認済み" に変わります。プロセス手順は表示されなくなりました。

![パートナー センターの確認エラー](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="what-is-verified-in-partner-center-account-verification-process-and-how-to-respond"></a>パートナー センター のアカウント検証プロセスで確認される情報と対応方法
電子メールの所有権、雇用、ビジネスの 3 つの検証領域があります。 確認された内容と対応[](/partner-center/verification-responses#what-is-verified-and-how-to-respond)方法の詳細を参照してください。プライマリ連絡先 (グローバル管理者またはアカウント管理者) である場合は、パートナー プロファイルに移動して、確認状態を監視し、進捗状況を追跡することをお勧めします。

確認プロセスが完了すると、プロファイル ページの登録の確認状態が承認待ちから承認に変わります。そのページに状態が表示されたプロセス手順は表示されなくなります。 プライマリ連絡先は、検証が完了した数営業日以内に Microsoft からメールを受信します。

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-in-partner-center-how-should-i-proceed"></a>自分のアカウントの確認状態が、パートナー センターのメールの所有権を超えては進んだ状態ではありません。 どのように進めるべきですか?

電子メール **の所有権の** 検証プロセス中に、確認メールがプライマリ連絡先のメール アドレスに送信されます。 Please check your primary contact inbox for an email from **maccount@<span>microsoft</span>.com** with the subject line *Action needed: Verify your email account with Microsoft,* requesting that you complete the email verification process. 確認メールは、パートナー センターのアカウント設定ページに表示されるメール アドレスに送信されます。

> [!NOTE]
 >メール検証リンクは 7 日間のみ有効です。 パートナー プロファイル ページにアクセスし、[確認メールの再送信] リンクを選択すると、メールの再送信を **要求** できます。 電子メールを確実に受信するには、セキュリティで保護されたドメインとしてmicrosoft.comメールを受信し、迷惑メール フォルダーを確認します。

## <a name="how-i-do-get-further-support-for-my-account-related-issues"></a>アカウント関連の問題に対してさらにサポートを受け取る方法

サポート チケットの [作成に関](/azure/marketplace/partner-center-portal/support) するガイダンスと手順については、パートナー センターのページで商用マーケットプレース プログラムのサポートにアクセスしてください。

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what--should-i-do-next"></a>メール フォルダーを確認し、確認メールを受信していない。 次に何をする必要がありますか?

次の手順を実行してください。

1. 迷惑メール/スパム フォルダーを確認します。
1. ブラウザー のキャッシュをクリアし、パートナー センター アカウント のダッシュボードに移動し、[確認メールの再送信] リンクを選択して、確認メールをメール アドレスに再送信します。
1. 別のブラウザーから  **[検証メールの** 再送信] リンクにアクセスしてみてください。
1. IT 部門と連絡を取り、確認メールが電子メール サーバーによってブロックされていないことを確認します。
1. サーバーのスパム フィルターを調整して、サーバーからのすべてのメールを許可 **/セーフリストmaccount@microsoft。 <span></span>com**.

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>通常、雇用確認プロセスにはどのくらいの時間が必要ですか?

提出された詳細すべてが正しい場合、雇用の確認は 1 ~ 2 時間で完了します。

## <a name="how-long-does-the-business-verification-process-usually-take"></a>通常、"ビジネス検証" プロセスにはどのくらいの時間が必要ですか?

必要なすべてのドキュメントが提出されている場合、業務の検証には 1 ~ 2 営業日かかります。

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a>サポート チームに連絡すると、チケットは迅速に提供されますか?

サポート チケットは 1 週間以内に解決されます。 サポート チケットの発生時に提供されるメールに送信される更新プログラムを探してください。

## <a name="my-issue-is-not-listed-here--are-there-other-pages-i-can-reference-for-partner-center-issues"></a>問題はここに記載されません。  パートナー センターの問題に関して参照できる他のページはありますか?

詳細については、商用マーケット [プレースのドキュメント](/azure/marketplace/) を参照してください。

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>サポート チケットを作成し、7 営業日以内で、更新プログラムを受信していない。 その他のヘルプはどこで利用できますか?

Please send an email to **<teamsubm@microsoft.com>** with the following details:

1. **件名行**。 *パートナー センター アカウントの問題<App_Name>* (アプリの名前を指定します)。
1. **電子メールの本文:**
    * サポート チケット番号:
    * 販売者 ID:
    * 問題のスクリーン ショット (可能な場合):
    
## <a name="app-category-mapping"></a>アプリ カテゴリのマッピング

| Teams カテゴリ       | PC カテゴリ  |
|:---------------------|:---------------|
| 分析と BI | 分析、データ可視化、BI |
| 開発者と IT | 開発者ツール、IT 管理者 |
| 教育 | 教育 |
| 人事管理 | 人事および採用 |
| 生産性 | コンテンツ管理、ファイルとドキュメント、生産性、トレーニングとチュートリアル、ユーティリティ |
| プロジェクト管理 | コミュニケーション、プロジェクト管理、ワークフローおよびビジネス管理 |
| 販売とサポート | 顧客および連絡先の管理、カスタマー サポート、財務管理、販売とマーケティング |
| ソーシャルで楽しい | 画像とビデオ ギャラリー、ライフ スタイル、ニュースと天気予報、ソーシャル、旅行、ナビゲーション |

>
> [!div class="nextstepaction"]
> [Microsoft Teams のアプリ検証ポリシーの詳細](/legal/marketplace/certification-policies)
