---
title: Teams ストアの申請プロセスについて
description: Microsoft Teams アプリ ストアにアプリを発行する承認申請プロセスについて説明します。
ms.topic: overview
localization_priority: Normal
keywords: teams publish store office publishing publish AppSource パートナー センター アカウント検証アプリ アカウントが対象アプリの申請を発行しない
ms.openlocfilehash: 79584ae1eb0be24b4a66e2421f23dd694f8d610f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019896"
---
# <a name="submit-your-app-to-appsource"></a>アプリを AppSource に送信する

## <a name="teams-app-submission"></a>Teams アプリの申請

アプリを AppSource に発行して、Microsoft Teams アプリ カタログと Web 上でアプリを [利用できます](https://appsource.microsoft.com)。 高レベルでは、AppSource にアプリを送信するプロセスは次のとおりです。

1. 設計ガイドラインに従ってアプリ [を開発します](~/concepts/design/understand-use-cases.md)。 タブは、デスクトップと Web、モバイルの両方のタブ [設計ガイドラインに従う](~/tabs/design/tabs.md) 必要 [があります](~/tabs/design/tabs-mobile.md)。 ボットは、ボットの設計 [ガイドラインに従う必要があります](~/bots/design/bots.md)。
1. アプリが Microsoft Teams のアプリ [検証ポリシーを満た](/legal/marketplace/certification-policies) している必要があります。 
1. マニフェスト検証ツールを使用 [してアプリをテストします](prepare/submission-checklist.md#teams-app-validation-tool)。
1. パートナー センターで[開発者アカウント](/office/dev/store/open-a-developer-account)[を設定します](https://support.microsoft.com/help/4499930/partner-center-overview)。 *「FAQ」*[セクションの「パートナー センター アカウントを作成する](#how-do-i-create-a-partner-center-account)方法」も参照してください。
1. 申請チェックリストに従って、アプリを申請 [用に準備します](prepare/submission-checklist.md)。
1. 最も [失敗したテスト ケースを確認して、アプリ品質の承認を迅速に行います](prepare/frequently-failed-cases.md)。
1. パートナー センターを通じて [AppSource にパッケージを送信します](/office/dev/store/use-partner-center-to-submit-to-appsource)。
1. パートナー センター ダッシュボードで承認プロセスを追跡します。 *「パートナー* [センターの概要」を参照してください](https://support.microsoft.com/help/4499930/partner-center-overview)。
1. 申請後、発行済みアプリの保守と [サポートに関するガイダンスを確認します](post-publish/overview.md)。

>[!NOTE]
>
>- Teams アプリはモバイル対応で、モバイル OS [](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment) (iOS と Android) ではアップセルの要件に準拠している必要があります。 
>- Teams アプリにボットが含まれている場合は、Bot Developer Framework Code of [Conduct に準拠する必要があります](https://aka.ms/bf-conduct)。
>- アプリに 365 Connector Office場合は、追加の用語が適用される場合があります。 [「Connectors Developer Dashboard and App](https://aka.ms/connectorsdashboard) Developer [Agreement」を参照してください](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)。
>- アプリを Government Community Cloud (GCC) ユーザーが利用し、ストア内のアプリの登録情報が重複しないようにするには、認証プロセスまたはフローでユーザーを特定し、GCC ユーザーの指定または予想されるコンテンツ URL にルーティングする必要があります。

## <a name="faqs--teams-apps-and-partner-account-verification-process-in-partner-center"></a>FAQ - パートナー センターの Teams アプリとパートナー アカウントの確認プロセス

## <a name="how-do-i-create-a-partner-center-account"></a>パートナー センター アカウントを作成する方法

パートナー センター アカウントを作成するには、次の 2 つの方法があります。

- パートナー センターを利用し、Microsoft ネットワークにアカウントを持ってない場合は、[パートナー センターの登録] ページ [を使用してアカウントを作成します](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)。
- パートナー ネットワークに既に登録されている場合は、既存の登録ページを使用してパートナー センターに直接 [ アカウントを作成します](/office/dev/store/)。

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a>パートナー センターで自分のストア Officeが見つからな場合は、

パートナー センター [のサポート チケットを開](https://partner.microsoft.com/support/v2/?stage=1) き、ドロップダウン メニューから次の項目を選択します。

| メニュー | オプション |
| -------   | -------  |
|カテゴリ| 商用マーケットプレース|
| トピック | 一般的な Marketplace のヘルプと使い方に関する質問 |
| サブトピック| Office アドイン |

## <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a>パートナー センター アカウントの問題のサポートはどこで受け取れるのですか?

発行元 [のサポート ページにアクセスして](https://aka.ms/marketplacepublishersupport) 、問題のトピックを検索し、ガイダンスを見つける。 提供されたガイダンスが役に立たない場合は、パートナー センター [のサポート チケットを引き上げてください](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)。

## <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a>パートナー センターで自分のストア Officeを管理する方法

ガイダンスについては [、「パートナー センター Officeストアの管理」アカウントを](/office/dev/store/manage-account-settings-and-profile) 参照してください。

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a>パートナー プロファイル連絡先セクションに電話番号を追加する方法

電話番号には、国コード、地域コード、電話番号の 3 つの部分があります。 電話番号にエリア コードが含されていない場合は、2 番目のボックスを空のままにして、3 番目のボックスを完成します。

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a>パートナー センターでアカウント設定とパートナー プロファイルを管理する方法

パートナー センター の [アカウント設定の管理に関する](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) ガイダンスについては、「アカウント設定とプロファイル情報の管理」ページをご覧ください。

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>パートナー センターを通じてアドインを提出しようとするときに、「このアカウントは発行対象ではありません」というメッセージが表示される理由

アカウント検証の状態が保留中の場合、上記 [のエラー メッセージ](/partner-center/verification-responses) が表示されます。 パートナー センター ダッシュボードでアカウント検証の状態を確認  [します](https://partner.microsoft.com/dashboard)。 [ **設定]** を選択し、ページ ヘッダー シェルの右上隅にある歯車アイコンを選択します。 [開発者 **設定] [**  =>  **アカウント**   =>  **アカウントの設定] を選択します**。

![パートナー センター のアカウント設定ページ](../../../assets/images/partner-center-accts-page.png)

![パートナー センターの検証状態](../../../assets/images/partner-center-verification-status.png)

電子メールの所有権、雇用の検証、ビジネス検証など、必要な各手順の状態がアカウント検証プロセスに表示されます。  検証プロセスが完了すると、プロファイル ページの登録の確認状態が保留中から承認済み *に**変わります*。 プロセス手順は表示されなくなりました。

![パートナー センターの検証エラー](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="what-is-verified-in-the-partner-center-account-verification-process-and-how-to-respond"></a>パートナー センター のアカウント検証プロセスで確認される情報と対応方法
検証領域は、電子メールの所有権 **、雇用、** およびビジネスの **3****つがあります**。 検証プロセスの詳細については、「確認される処理と応答 [方法」を参照してください](/partner-center/verification-responses#what-is-verified-and-how-to-respond)。
プライマリ連絡先、グローバル管理者、またはアカウント管理者の場合は、パートナー プロファイルに移動して検証の状態を監視し、進行状況を追跡します。

検証プロセスが完了すると、プロファイル ページの登録の確認状態が保留中から承認済み *に**変わります*。 承認後、プロセスの手順とその状態はページで使用できなくなりました。 プライマリ連絡先は、検証が完了した数営業日以内に Microsoft から電子メールを受信します。

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-in-the-partner-center-how-should-i-proceed"></a>パートナー センターの [メールの所有権] を超えて、アカウントの検証の状態が進んだのではありません。 どのように進める必要がありますか?

電子メール **所有権の検証** プロセス中に、確認メールがプライマリ連絡先の電子メール アドレスに送信されます。 メインの連絡先の受信トレイで、microsoft **.com maccount@<span>の</span>** メールを確認します。件名の [アクションが必要です: Microsoft でメール アカウントを確認する] を *クリックします*。 電子メールの検証プロセスを完了します。 確認メールは、パートナー センターの [アカウント設定] ページに記載されているメール アドレスに送信されます。

> [!NOTE]
> * 電子メール検証リンクは 7 日間のみ有効です。 
> * パートナー プロファイル ページにアクセスし、[確認メールの再送信] リンクを選択すると、メールの再送信を **要求** できます。
> * メールを確実に受信するには、セキュリティで保護されたドメイン microsoft.com メールを安全に一覧表示し、迷惑メール フォルダーを確認します。

## <a name="how-do-i-get-further-support-for-my-account-related-issues"></a>アカウントに関連する問題のサポートを受け取る方法

サポート チケット [を作成するためのガイダンスと](/azure/marketplace/partner-center-portal/support) 手順については、「パートナー センターの商用マーケットプレース プログラムのサポート」ページをご覧ください。

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what-must-i-do-next"></a>メール フォルダーを確認し、確認メールを受信していない。 次に何をする必要がありますか?

以下の操作を試してください。
* 迷惑メールフォルダーまたはスパム フォルダーを確認します。
* ブラウザー キャッシュをクリアし、パートナー センター アカウント ダッシュボードに移動し、[確認メールの再送信] リンクを選択して、確認メールを電子メール アドレスに再送信します。
* 別のブラウザーから **[再送信確認メール** ] リンクにアクセスしてみてください。
* IT 部門と一緒に作業して、確認メールが電子メール サーバーによってブロックされていないことを確認します。
* サーバーのスパム フィルターを調整して、サーバーからのすべてのメールを許可または **maccount@microsoft。 <span></span>com**.

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>通常、雇用確認プロセスにはどのくらいの時間が必要ですか?

提出された詳細が正しい場合、雇用確認プロセスの完了には約 2 時間かかります。

## <a name="how-long-does-the-business-verification-process-usually-take"></a>ビジネス検証プロセスには通常どれくらいの時間が必要ですか?

必要なすべてのドキュメントが提出された場合、ビジネス検証の完了には 1 日から 2 営業日かかります。

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a>サポート チームに連絡を取った場合、チケットは迅速に行いますか?

サポート チケットは 1 週間で解決されます。 サポート チケットを引き上げる際に提供されたメール ID に送信される更新プログラムを確認します。

## <a name="my-issue-is-not-listed-here-are-there-other-pages-i-can-reference-for-partner-center-issues"></a>ここでは、問題は一覧に表示されません。 パートナー センターの問題に関して参照できるページは他にもありますか?

詳細については [、商用マーケットプレースのドキュメント](/azure/marketplace/) を参照してください。

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>サポート チケットを作成しました。7 営業日が過ごし、更新プログラムを受け取っていない。 追加のヘルプはどこで受け取れるのですか?

次の詳細を含 **<teamsubm@microsoft.com>** むメールを送信します。

* **件名 :** パートナー センター アカウントの問題 (<App_Name>名を指定します)。
* **メール本文**:
    * サポート チケット番号
    * 販売者 ID
    * 問題のスクリーンショット (可能な場合)
    
## <a name="app-category-mapping"></a>アプリ カテゴリのマッピング

| Teams カテゴリ       | PC カテゴリ  |
|:---------------------|:---------------|
| 分析と BI | 分析、データ可視化、BI |
| 開発者と IT | 開発者ツール、IT 管理者 |
| 教育 | 教育 |
| 人事管理 | 人事と採用 |
| 生産性 | コンテンツ管理、ファイルとドキュメント、生産性、トレーニングとチュートリアル、ユーティリティ |
| プロジェクト管理 | コミュニケーション、プロジェクト管理、ワークフロー、およびビジネス管理 |
| 販売とサポート | 顧客と連絡先の管理、カスタマー サポート、財務管理、営業およびマーケティング |
| ソーシャルで楽しい | 画像とビデオ ギャラリー、ライフスタイル、ニュースと天気予報、ソーシャル、旅行、ナビゲーション |

>
> [!div class="nextstepaction"]
> [Microsoft Teams のアプリ検証ポリシーの詳細](/legal/marketplace/certification-policies)
