---
title: Microsoft Teams アプリ承認申請プロセスガイダンス
description: Microsoft Teams アプリ ストアにアプリを公開する承認申請プロセスについて説明します。
ms.topic: conceptual
keywords: teams publish store office publishing publish AppSource partner center account verification apps account not publish eligible app submission
ms.openlocfilehash: 3dac91e8591edec597f6435fdc2bab989820661a
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886752"
---
# <a name="submit-your-app-to-appsource"></a>AppSource にアプリを提出する

## <a name="teams-app-submission"></a>Teams アプリの申請

AppSource に発行して、Microsoft Teams アプリ カタログと Web でアプリを [利用できます](https://appsource.microsoft.com)。 大きなレベルでは、AppSource にアプリを提出するプロセスは次のとおりです。

1. 設計ガイドラインに従ってアプリ [を開発します](~/concepts/design/understand-use-cases.md)。 タブは、デスクトップと Web、モバイルの両方のタブ設計ガイドライン [に従う](~/tabs/design/tabs.md) 必要 [があります](~/tabs/design/tabs-mobile.md)。 ボットは、ボットの設計 [ガイドラインに従う必要があります](~/bots/design/bots.md)。
1. アプリが Microsoft Teams のアプリ [検証ポリシーを満た](/legal/marketplace/certification-policies) している必要があります。 
1. マニフェスト検証ツールを使 [ってアプリをテストします](prepare/submission-checklist.md#teams-app-validation-tool)。
1. パートナー センターで [開発者アカウント](/office/dev/store/open-a-developer-account) を [セットアップします](https://support.microsoft.com/help/4499930/partner-center-overview)。 *「FAQ」*[セクションでパートナー センター アカウントを作成する](#how-do-i-create-a-partner-center-account)方法も参照してください。
1. 申請のチェックリストに従って、申請用に [アプリを準備します](prepare/submission-checklist.md)。
1. 最も [失敗したテスト ケースを確認して、アプリ品質の承認を迅速に行います](prepare/frequently-failed-cases.md)。
1. パートナー センターから [AppSource にパッケージを提出します](/office/dev/store/use-partner-center-to-submit-to-appsource)。
1. パートナー センター ダッシュボードで承認プロセスを追跡します。 *「パートナー* [センターの概要」を参照してください](https://support.microsoft.com/help/4499930/partner-center-overview)。
1. 提出後、公開されたアプリの [保守とサポートに関するガイダンスを確認します](post-publish/overview.md)。

>[!NOTE]
>
>- Teams アプリはモバイル対応である必要があります。また[](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment)、モバイル OS (iOS および Android) ではアップセルの要件に準拠する必要はありません。 
>- Teams アプリにボットが含まれている場合は、Bot Developer Framework [の実施基準に準拠する必要があります](https://aka.ms/bf-conduct)。
>- アプリに Office 365 コネクタが含まれている場合は、追加の用語が適用される場合があります。 「 [コネクタ開発者ダッシュボードと](https://aka.ms/connectorsdashboard) アプリ開発者契約 [」を参照してください](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)。
>- アプリを Government Community Cloud (GCC) ユーザーが利用し、ストア内のアプリ登録情報が重複しないようにするには、認証プロセスまたはフローでユーザーを識別し、GCC ユーザーの指定または予想されるコンテンツ URL にユーザーをルーティングする必要があります。

## <a name="faqs--teams-apps-and-partner-account-verification-process-in-partner-center"></a>FAQ - パートナー センターでの Teams アプリとパートナー アカウント検証プロセス

## <a name="how-do-i-create-a-partner-center-account"></a>パートナー センター アカウントを作成する方法

パートナー センター アカウントを作成するには、次の 2 つの方法があります。

- パートナー センターを使い、Microsoft ネットワークにアカウントを持ってない場合は、パートナー センターの登録ページを使用 [してアカウントを作成します](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)。
- 既にパートナー ネットワークに登録している場合は、既存の登録ページを使用して、パートナー センターで直接 [ アカウントを作成します](/office/dev/store/)。

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a>パートナー センターで自分のストア アカウントOffice見つからでは?

パートナー センター [のサポート チケットを開](https://partner.microsoft.com/support/v2/?stage=1) き、ドロップダウン メニューから次を選択します。

| メニュー | オプション |
| -------   | -------  |
|カテゴリ| Commercial Marketplace|
| トピック | 一般的なマーケットプレースのヘルプと使い方に関する質問 |
| サブトピック| Office アドイン |

## <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a>パートナー センター アカウントの問題に対するサポートはどこで受け取できますか?

発行元 [のサポート ページで問題](https://aka.ms/marketplacepublishersupport) のトピックを検索し、ガイダンスを見つける。 提供されたガイダンスが役に立たない場合は、パートナー センター [のサポート チケットを購入します](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)。

## <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a>パートナー センターでストア アカウントOffice管理する方法

ガイダンスについては [、パートナー センター Officeストアアカウントの管理に](/office/dev/store/manage-account-settings-and-profile) アクセスしてください。

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a>パートナー プロファイルの連絡先セクションに電話番号を追加する方法

電話番号には、国コード、エリア コード、電話番号の 3 つの部分があります。 電話番号にエリア コードが含まれる場合は、2 番目のボックスを空のままにして、3 番目のボックスに入力します。

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a>パートナー センターでアカウント設定とパートナー プロファイルを管理する方法

パートナー センター [のアカウント設定の管理に関する](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) ガイダンスについては、「アカウント設定とプロファイル情報の管理」ページを参照してください。

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>パートナー センターからアドインを提出しようとするときに、「このアカウントは発行の対象ではありません」というメッセージが表示される理由は何ですか。

アカウントの確認状態が保留中のときに、上記の [エラー メッセージ](/partner-center/verification-responses) が表示されます。 パートナー センター ダッシュボードでアカウントの確認状態を確認  [します](https://partner.microsoft.com/dashboard)。 [ **設定]** を選択すると、ページ ヘッダー シェルの右上隅にある歯車アイコンが表示されます。 Choose **Developer settings**  =>  **Account** Account   =>  **settings**.

![パートナー センター のアカウント設定ページ](../../../assets/images/partner-center-accts-page.png)

![パートナー センターの確認状態](../../../assets/images/partner-center-verification-status.png)

アカウント検証プロセスには、電子メールの所有権、雇用の確認、ビジネスの確認など、必要な各手順の状態が表示されます。  確認プロセスが完了すると、プロファイル ページの登録の確認状態が承認待ちから承認済みに *変わります*。 プロセス手順は表示されなくなりました。

![パートナー センターの確認エラー](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="what-is-verified-in-the-partner-center-account-verification-process-and-how-to-respond"></a>パートナー センター アカウントの確認プロセスで確認される情報と対応方法
確認領域には、電子メールの所有権 **、雇用**、 **ビジネスの** 3 **つがあります**。 検証プロセスの詳細については、「確認された機能と対応 [方法」を参照してください](/partner-center/verification-responses#what-is-verified-and-how-to-respond)。
プライマリ連絡先、グローバル管理者、またはアカウント管理者である場合は、パートナー プロファイルに移動して確認状態を監視し、進行状況を追跡します。

確認プロセスが完了すると、プロファイル ページの登録の確認状態が承認待ちから承認済みに *変わります*。 承認後、プロセスの手順とその状態はページで使用できなくなりました。 プライマリ連絡先は、確認が完了した数営業日以内に Microsoft からメールを受信します。

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-in-the-partner-center-how-should-i-proceed"></a>自分のアカウントの確認ステータスが、パートナー センターのメールの所有権を超えては進んだ状態ではありません。 どのように進めるべきですか?

電子メール **の所有権の** 検証プロセス中に、確認メールがプライマリ連絡先のメール アドレスに送信されます。 プライマリ連絡先の受信トレイで、maccount@ **<span>microsoft</span>.com** からのメールを確認し、件名行の操作が必要です。Microsoft でメール アカウントを *確認します*。 電子メールの検証プロセスを完了します。 確認メールは、パートナー センターのアカウント設定ページに表示されるメール アドレスに送信されます。

> [!NOTE]
> * メール検証リンクは 7 日間のみ有効です。 
> * パートナー プロファイル ページにアクセスし、[確認メールの再送信] リンクを選択すると、メールの再送信を **要求** できます。
> * 電子メールを確実に受信するには、セキュリティで保護されたドメインとしてmicrosoft.comメールを安全に一覧表示し、迷惑メール フォルダーを確認します。

## <a name="how-do-i-get-further-support-for-my-account-related-issues"></a>アカウント関連の問題に対するサポートを受け取る方法

サポート チケット [を作成するためのガイダンスと手順](/azure/marketplace/partner-center-portal/support) については、パートナー センターの [商用マーケットプレース のサポート] ページを参照してください。

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what-must-i-do-next"></a>メール フォルダーを確認し、確認メールを受信していない。 次に何をする必要がありますか?

以下の操作を試してください。
* 迷惑メールフォルダーまたはスパム フォルダーを確認します。
* ブラウザー のキャッシュをクリアし、パートナー センター アカウント のダッシュボードに移動し、[確認メールの再送信] リンクを選択して、確認メールをメール アドレスに再送信します。
* 別のブラウザーから **[検証メールの** 再送信] リンクにアクセスしてみてください。
* IT 部門と連絡を取り、確認メールが電子メール サーバーによってブロックされていないことを確認します。
* サーバーのスパム フィルターを調整して、サーバーからのすべてのメールを許可またはセーフ **リストmaccount@microsoft。 <span></span>com**.

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>通常、雇用確認プロセスにはどのくらいの時間が必要ですか?

提出された詳細すべてが正しい場合、雇用確認プロセスが完了するのに約 2 時間かかります。

## <a name="how-long-does-the-business-verification-process-usually-take"></a>ビジネス検証プロセスには通常どのくらいの時間が必要ですか?

すべての必要なドキュメントが送信された場合、業務の検証が完了するのに 1 から 2 営業日かかります。

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a>サポート チームに連絡すると、チケットは迅速に提供されますか?

サポート チケットは 1 週間後に解決されます。 サポート チケットを引き上げる際に提供された電子メール ID に送信された更新プログラムを確認します。

## <a name="my-issue-is-not-listed-here-are-there-other-pages-i-can-reference-for-partner-center-issues"></a>問題はここに記載されません。 パートナー センターの問題に関して参照できる他のページはありますか?

詳細については、 [商用マーケットプレースのドキュメント](/azure/marketplace/) を参照してください。

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>サポート チケットを作成し、7 営業日以内で、更新プログラムを受信していない。 その他のヘルプはどこで利用できますか?

次の詳細情報を **<teamsubm@microsoft.com>** 含むメールを送信します。

* **件名:** パートナー センター アカウントの問題<App_Name> (アプリの名前を指定します)。
* **電子メールの本文**:
    * サポート チケット番号
    * 販売者 ID
    * 問題のスクリーンショット (可能な場合)
    
## <a name="app-category-mapping"></a>アプリ カテゴリのマッピング

| Teams カテゴリ       | PC カテゴリ  |
|:---------------------|:---------------|
| 分析と BI | 分析、データ可視化、BI |
| 開発者と IT | 開発者ツール、IT 管理者 |
| 教育 | 教育 |
| 人事管理 | 人事および採用 |
| 生産性 | コンテンツ管理、ファイルとドキュメント、生産性、トレーニングとチュートリアル、ユーティリティ |
| プロジェクト管理 | コミュニケーション、プロジェクト管理、ワークフロー、およびビジネス管理 |
| 販売とサポート | 顧客および連絡先の管理、カスタマー サポート、財務管理、販売とマーケティング |
| ソーシャルで楽しい | 画像とビデオ ギャラリー、ライフ スタイル、ニュースと天気予報、ソーシャル、旅行、ナビゲーション |

>
> [!div class="nextstepaction"]
> [Microsoft Teams のアプリ検証ポリシーの詳細](/legal/marketplace/certification-policies)
