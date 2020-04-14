---
title: Microsoft Teams アプリ承認プロセスガイダンス
description: Microsoft Teams アプリストアに公開されたアプリを取得するための承認プロセスについて説明します。
keywords: teams 発行ストア office 発行アプリソース
ms.openlocfilehash: 761cb69ddebac28af5ffc39401eefa9e1b424bc3
ms.sourcegitcommit: 27789fd2e6f522f33f2135c66b0153949d9b0d64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "43285938"
---
# <a name="submit-your-app-to-appsource"></a>アプリを AppSource に提出する

## <a name="teams-app-submission"></a>Teams アプリの提出

アプリを[Appsource](https://appsource.microsoft.com)に発行すると、Teams アプリカタログと web 上で使用できるようになります。 高レベルでは、アプリを AppSource に提出するプロセスは次のようになります。

1. [デザインガイドライン](~/concepts/design/understand-use-cases.md)に従ってアプリを開発します。 タブは、[タブデザインガイドライン](~/tabs/design/tabs.md)に準拠している必要があります。 Bot は[bot 設計ガイドライン](~/bots/design/bots.md)に従う必要があります。
1. [パートナーセンター](https://support.microsoft.com/help/4499930/partner-center-overview)で[開発者アカウントをセットアップ](/office/dev/store/open-a-developer-account)します。
1. [提出のチェックリスト](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)に従って、アプリを提出する準備をします。
1. [アプリの送信を成功させるためのヒントを](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)確認します。
1. [パートナーセンターを使用して、Appsource](/office/dev/store/use-partner-center-to-submit-to-appsource)にパッケージを提出します。
1. パートナーセンターダッシュボードで承認プロセスを追跡します。 *「* [Partner Center の概要](https://support.microsoft.com/help/4499930/partner-center-overview)」を参照してください。
1. 投稿後: 公開された[アプリの管理とサポート](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)に関するガイダンスを確認してください。

>[!NOTE]
>
> * Teams アプリに bot が含まれている場合は、ボット開発者フレームワーク[の倫理](https://aka.ms/bf-conduct)規定に準拠する必要があります。
> * アプリに Office 365 コネクタが含まれている場合は、追加の用語が適用されることがあります。 *「* [コネクタ開発者ダッシュボード](https://aka.ms/connectorsdashboard)と[アプリ開発者アグリーメント](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)」を参照してください。

## <a name="faqs--teams-apps-and-partner-accounts"></a>**Faq-Teams アプリとパートナーアカウント**

## <a name="how-do-i-create-a-partner-center-account"></a>パートナーセンターアカウントを作成するにはどうすればよいですか?

パートナーセンターアカウントを作成するには、次の2つの方法があります。

* パートナーセンターを初めて使用していて、Microsoft ネットワーク内にアカウントがない場合は、[パートナーセンターの登録ページを使用してアカウントを作成](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)します。
* パートナーネットワークに既に登録されている場合は、[既存の登録を使用してパートナーセンターで直接アカウントを作成](/office/dev/store/)します。

## <a name="how-do-i-add-my-phone-number-to-the-contact-info-section"></a>[連絡先情報] セクションに電話番号を追加するにはどうすればよいですか?

電話番号には、国番号、市外局番、電話番号の3つのパーツがあります。 いずれかのセクションが該当しない場合は、 `0`番号を入力してください。

## <a name="why-do-i-get-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>パートナーセンターからアドインを送信しようとすると、"このアカウントは公開されません" というメッセージが表示されるのはなぜですか?

[アカウントの確認状態](/partner-center/verification-responses)が保留中の場合、上記のエラーメッセージが表示されます。 パートナーセンターの[ダッシュボード](https://partner.microsoft.com/dashboard)で [**設定**] オプション (歯車アイコン) を選択し、[**開発者設定** => ] [**アカウント**  => **アカウント設定**] を選択することによって、アカウントの確認状態を確認できます。 アカウント検証プロセスの間に、各必要な手順の状態 (電子メールの所有権、雇用の確認、およびビジネスの確認) が表示されます。 検証プロセスが正常に完了すると、プロファイルページの登録の検証状態が "保留" から "承認済み" に変わり、プロセスの手順は表示されなくなります。 考えられる検証の問題を解決するには、*以下を参照してください*。

## <a name="how-i-do-get-further-support-for-my-account-related-issues"></a>自分のアカウント関連の問題について、さらにサポートを受けるにはどうすればよいですか?

パートナーの[ヘルプとサポートページ](https://aka.ms/marketplacepublishersupport)にアクセスして、問題に関連するドキュメントに役立つソリューションを検索します。 提供されている自己提供ソリューションまたはドキュメントが問題解決に役に立たない場合は、[**次の手順**] セクションの下にある [問題の**詳細の入力**] を選択して、サポートチケットを提出してください。 検索ボックスで問題のトピックを検索するか、検索ボックスの下にある [**トピックの参照**] を選択して、さらにドリルダウンすることができます。

> [!TIP]
> **アカウント検証**の問題についてのヘルプを探している場合は、次のようにします。
>
>1. **検索ボックス**の下にある [**トピックの参照**] を選択します。
>1. [**カテゴリ**] ドロップダウンメニューから [**すべてのプログラム**] を選択します。
> 1. [**トピック**] ドロップダウンメニューから、[**アカウント]、[オンボード]、[アクセス**] を選択します。
>1. [サブ**トピック**] ドロップダウンメニューから**オプションを選択し**ます。
>1. を参照してください。 [**次の手順**] セクションの下にある [問題の**詳細を入力**] を選択します。
>

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what--should-i-do-next"></a>メールフォルダーをチェックしていて、確認の電子メールを受信していません。 次の手順を実行します。

次のことを試してください。

1. 迷惑メールフォルダーを確認してください。
1. ブラウザーのキャッシュをクリアし、パートナーセンターのアカウントダッシュボードに移動し、[**再送信確認**] 電子メールリンクを選択して、確認の電子メールを電子メールアドレスに送信します。
1. 別のブラウザーから [**再送信の確認の電子メール**へのアクセスを試行してください。
1. IT 部門と協力して、電子メールサーバーによって検証メールがブロックされないようにします。
1. サーバーのスパムフィルターを調整して、maccount@microsoft からのすべての電子メールを許可またはホワイトリストに**します。<span> </span>com**。

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>雇用確認プロセスには、通常どのくらいの時間がかかりますか?

すべての詳細が正しく提供されている場合、雇用の確認は 1 ~ 2 時間で完了します。

## <a name="ive-already-reached-out-to-support-is-there-a-way-to-expedite-my-case"></a>サポートが終了したら、ケースを早める方法はありますか?

サポートチケットは、週の時間内に解決されます。 サポートチケットの発生時に提供されたメールに送信される更新プログラムを探してください。

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>サポートチケットを作成したが、それは7営業日でしたが、更新を受信していません。 追加のヘルプはどこで入手できますか?

次の情報を使用**<teamsubm@microsoft.com>** して、にメールを送信してください。

1. **件名行** *<App_Name>のパートナーセンターのアカウントの問題*(アプリの名前を指定してください)。
2. **メール本文:**
    * サポートチケット番号:
    * 販売者 ID:
    * この問題のスクリーンショット。

> [!div class="nextstepaction"]
> [Microsoft Teams のアプリの検証ポリシーの詳細情報](/office/dev/store/validation-policies#14-microsoft-teams-apps)
