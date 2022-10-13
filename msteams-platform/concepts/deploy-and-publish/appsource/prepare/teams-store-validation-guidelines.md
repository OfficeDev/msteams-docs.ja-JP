---
title: Microsoft Teams ストア検証ガイドライン
description: アプリが Microsoft Teams ストアの申請プロセスに合格する可能性を高める方法について説明します。 必須の修正プログラムと推奨される修正プログラムについて理解します。 検証ガイドラインを確認します。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: 0a0151c72820baf1b6bd39ee00539cacbd3fa38b
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2022
ms.locfileid: "68561212"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams ストア検証ガイドライン

これらのガイドラインに従うことで、アプリが Microsoft Teams ストアの審査プロセスに合格する可能性が高まります。 Teams 固有のガイドラインは、Microsoft [コマーシャル マーケットプレース認定ポリシー](/legal/marketplace/certification-policies#1140-teams)を補完するものであり、新機能やユーザー フィードバック、ビジネス ルールの変更を反映して頻繁に更新されています。

> [!NOTE]
>
> * 一部のガイドラインは、アプリに適用できない場合があります。 たとえば、アプリにボットが含まれていない場合は、ボット関連のガイドラインを無視することができます。
> * これらのガイドラインを Microsoft の商用認定ポリシーに相互参照し、検証プロセスで発生した合格または不合格のシナリオの例を示す「やるべきこと」と「やってはいけないこと」を追加しました。
> * 特定のガイドラインは、*必須の修正* としてマークされます。 アプリの申請がこれらの必須のガイドラインを満たしていない場合は、Microsoft から改善のための手順を示すエラー レポートが送信されます。  アプリの申請は、問題を修正した場合にのみ Microsoft Teams ストアの検証に合格します。
> * Other guidelines are marked as *Suggested Fix*. For an ideal user experience, we suggest that you fix the issues, however, your app submission will not be blocked from publishing on the Teams store, if you choose not to fix the issues.

:::row:::
   :::column:::
      :::image type="icon" source="../../../../assets/icons/value-proposition.png" link="#value-proposition" border="false":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../../assets/icons/security.png" link="#security" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/function.png" link="#general-functionality-and-performance" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/package.png" link="#app-package-and-store-listing" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/saas-offer.PNG" link="#apps-linked-to-saas-offer" border="false":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/tab.png" link="#tabs" border="false":::
   :::column-end:::
   :::column:::
      :::image type="icon" source="../../../../assets/icons/bot.png" link="#bots-1" border="false":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../../assets/icons/messaging-extension.png" link="#message-extensions" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/task-module.png" link="#task-modules" border="false":::
   :::column-end:::
     :::column span="":::
      :::image type="icon" source="../../../../assets/icons/meeting.png" link="#meeting-extensions" border="false":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/notifications.png" link="#notifications" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/microsoft-365.png" link="#microsoft-365-app-compliance-program" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/advertising.png" link="#advertising" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/crypto-currency-based-apps-icon.png" link="#cryptocurrency-based-apps" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/app-functionality-icon.png" link="#app-functionality" border="false":::
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/mobile-experience-icon.png" link="#mobile-experience" border="false":::
   :::column-end:::
:::row-end:::

## <a name="value-proposition"></a>価値提案

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用認定ポリシー番号 1140.1](/legal/marketplace/certification-policies#11401-value-proposition-and-offer-requirements) に沿ったものであり、そのオファーの価値提案に関して、Microsoft Teams アプリの開発者に追加のガイダンスを提供します。

### <a name="app-name"></a>アプリ名

[*必須の修正プログラム*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、Microsoft [商用認定ポリシー番号 1140.1.1](/legal/marketplace/certification-policies#114011-app-name) に沿ったものであり、それらのアプリの名前の指定に関して、開発者に追加のガイダンスを提供します。
<br></br>
<details><summary>詳細を知るために展開する</summary>

アプリの名前は、ユーザーがストアでアプリを見つける際に重要な役割を果たします。 次のガイドラインを使用してアプリの名前を指定します。

* 名前には、ユーザーに関連する用語を含める必要があります。
* 開発者の名前を普通名詞の接頭辞または接尾辞として含める。 たとえば、**タスク** ではなく **Contoso タスク** がこれにあたります。
* 共同ブランド化または共同販売を誤って示す可能性がある **Teams** またはその他の Microsoft 製品名 (Excel、PowerPoint、Word、OneDrive、SharePoint、OneNote、Azure、Surface、Xbox など) を使用しないでください。 Microsoft ソフトウェア、製品、およびサービスの参照に関する詳細については、「[Microsoft の商標およびブランドに関するガイドライン](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general)」を参照してください。
* ストアに登録済みのアプリや、コマーシャル マーケットプレース上のその他のオファーと同じ名前を使用してはいけません。
* 卑猥な言葉や軽蔑的な言葉を含んではいけません。 名前には、人種や文化に配慮しない言葉が含まれてはいけません。
* 一意である必要があります。 アプリ (Contoso) が Microsoft Teams ストアと Microsoft AppSource に一覧表示され、Contoso メキシコなどの地域に固有の別のアプリを一覧表示する場合は、申請が次の条件を満たしている必要があります。
  * タイトル、メタデータ、最初の応答アプリ エクスペリエンス、ヘルプ セクションでアプリの地域固有の機能を呼び出します。 たとえば、タイトルは「Contoso Mexico」でなければなりません。 アプリのタイトルは、エンド ユーザーの混乱を避けるために、既存のアプリと同じ開発者を明確に区別する必要があります。
  * パートナー センターでアプリ パッケージをアップロードする場合は、**[可用性]** セクションでアプリを利用できる適切な **マーケット** を選択します。

* アプリ名は、チャット、連絡先、予定表、通話、ファイル、アクティビティ、Teams、アプリ、ヘルプなどの Teams の主要な機能を使用しないでください。 アプリ名は、チャット、連絡先、予定表、通話、ファイル、アクティビティ、Teams、アプリ、左側のナビゲーションへのインストールに関するヘルプのいずれかに短縮できます。

* If your app is part of an official partnership with Microsoft, the name of your app must come first. For example, **Contoso Connector for Microsoft Teams**.

* アプリ名には、Microsoft または Microsoft 製品への参照を含めることはできません。 アプリが Microsoft と正式に提携している場合を除き、アプリ **名で** **Teams**、**Microsoft**、または App を使用しないでください。 このようなインスタンスでは、Microsoft への参照の前にアプリ名を最初に指定する必要があります。 たとえば、 **Microsoft Teams 用の Contoso コネクタなどです**。

* 名前付けにかっこを使用して Microsoft 製品を含めないでください。

* 開発者名は、マニフェストと AppSource で同じである必要があります。

* 送信されるアプリ マニフェストは、運用マニフェストである必要があります。 したがって、アプリ名は、アプリが運用前のアプリであることを示す必要はありません。 たとえば、アプリ名に Beta、Dev、Preview、UAT などの単語を含めることはできません。

 > [!TIP]
 > アプリ名、開発者名、アプリ アイコン、AppSource のスクリーンショット、ビデオ、簡単な説明、Web サイトを含む Microsoft Teams ストアと AppSource でのアプリのブランド化は、アプリが Microsoft 1P の公式サービスでない限り、公式の Microsoft オファリングを偽装しないでください。

</details>

### <a name="suitable-for-workplace-consumption"></a>職場での消費に適していること

[*必須の修正*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、Microsoft 商用認定ポリシー番号 [1140.1.2](/legal/marketplace/certification-policies#114012-workplace-appropriateness)、[100.8](/legal/marketplace/certification-policies#1008-significant-value)、[100.10](/legal/marketplace/certification-policies#10010-inappropriate-content) に沿ったものであり、開発者に職場に適したアプリを構築するための追加のガイダンスを提供します。
<br></br>
<details><summary>詳細を知るために展開する</summary>

アプリ コンテンツは、職場での一般的な消費に適したものであり、コマーシャル マーケットプレースの認証ポリシーに一覧表示されたすべての制限事項に従う必要があります。 宗教、政治、ギャンブル、長時間の娯楽などに関するコンテンツは禁止されています。

アプリは、グループのコラボレーションを可能にするもの、個人の生産性を向上させるもの、またはその両方である必要があります。 チームの結束や交流を目的としたアプリでは、コラボレーションが促進され、複数の参加者が利用できるように設計されている必要があります。 アプリは、1 回のセッションに 60 分を超える時間を必要としたり、生産性に影響を与えるものであってはいけません。

</details>

### <a name="similar-platforms-and-services"></a>類似したプラットフォームやサービス

[*必須の修正プログラム*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用認定ポリシー番号 1140.1.3](/legal/marketplace/certification-policies#114013-other-platforms-and-services) に沿ったものです。

アプリ内では、Teams のエクスペリエンスが占有的である必要があります。アプリ コンテンツやアプリのメタデータには、他の同様のチャットベースのコラボレーション プラットフォームやサービスから取られた、名前、アイコン、またはイメージを含めてはいけません。ただし、アプリが特定の相互運用性を提供している場合はその限りではありません。

### <a name="feature-names"></a>機能名

ボタンやその他の UI テキストのアプリ機能名は、Teams やその他の Microsoft 製品用に予約された用語を使用しないでください。 たとえば、 **会議の開始**、 **通話の発信**、または **スタート チャット** は、Microsoft Teams で Microsoft によって使用されている機能名です。 必要に応じて、 **Contoso 会議の開始** など、区別を明確にするためにアプリ名を含めます。

### <a name="authentication"></a>認証

[*必須の修正プログラム*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用認定ポリシー番号 1140.1.4](/legal/marketplace/certification-policies#114014-access-to-services) に沿ったものであり、外部サービスを使用したそれらのアプリの認証に関して、開発者にガイダンスを提供します。

アプリ認証を実装する方法の詳細については、「[Teams での認証](~/concepts/authentication/authentication.md)」を参照してください。
<br></br>
<details><summary>詳細を知るために展開する</summary>

#### <a name="authenticating-with-external-services"></a>外部サービスを使用した認証

アプリが外部サービスを使用してユーザーを認証する場合は、以下のガイドラインに従ってください。

* **サインイン、サインアウト、サインアップのエクスペリエンス**:
  * 外部アカウントまたはサービスに依存するアプリでは、シンプルでわかりやすいサインイン、サインアウト、およびサインアップ エクスペリエンスを提供する必要があります。
  * ユーザーがサインアウトする場合は、アプリからのみサインアウトし、Teams にはサインインしたままにする必要があります。
  * 外部アカウントやサービスに依存するアプリは、新しいユーザーがサインアップしたり、アプリ発行元に連絡してサービスの詳細を確認したり、サービスにアクセスしたりするための方法を提供する必要があります。
  それらの方法は、アプリのマニフェスト、AppSource の詳細な説明、およびアプリの初回実行時エクスペリエンス (ボットのようこそメッセージ、タブのセットアップないしは構成ページ) から利用できる必要があります。
  * テナント管理者によるワンタイム セットアップが必要であるアプリでは、(他のテナント ユーザーがアプリをインストールして使用する前に) テナント管理者に対する依存関係を記述してそれが適用される形にアプリを構成しておく必要があります。
  依存関係は、アプリのマニフェスト、AppSource の「詳細な説明」、初回実行時エクスペリエンスのすべてのタッチポイント (すなわち、ボットのようこそメッセージ、タブのセットアップないしは構成ページ)、ボットの応答や拡張機能や静的タブのコンテンツページのヘルプ テキスト (必須とされている) に記述されている必要があります。
  
* **コンテンツ共有エクスペリエンス**: Teams チャネルでコンテンツを共有するために外部サービスを使用した認証を必要とするアプリは、外部サービスでその機能がサポートされている場合、コンテンツを切断または共有解除する方法をヘルプ ドキュメント (または同様のリソース) で明示する必要があります。 これは、コンテンツの共有を解除する機能が、Teams アプリに存在する必要があるということではありません。

</details>

## <a name="security"></a>セキュリティ

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用認定ポリシー番号 1140.3](/legal/marketplace/certification-policies#11403-security) と一致します。

### <a name="financial-information"></a>財務情報

[*必須の修正プログラム*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは [、Microsoft 商用認定ポリシー番号 1140.3.1](/legal/marketplace/certification-policies#114031-financial-transactions) とインラインであり、Teams インターフェイス内での財務情報の送信に関するガイダンスを提供し、Teams アプリのモバイル (Android および iOS) バージョンでの制限付き支払いシナリオについて開発者に通知します。
<br></br>
<details><summary>詳細を知るために展開する</summary>

アプリは、ユーザーに対して、Teams インターフェイス内で支払いを求めたり、ボットを介してユーザーに財務情報を送信してはいけません。

:::image type="content" source="../../../../assets/images/submission/validation-financial-information-1.png" alt-text="validation-financial-info":::

ユーザーがアプリの使用に同意する前に、使用条件、プライバシー ポリシー、プロファイル ページ、Web サイトなどで開示を行った場合に限り、安全な外部決済サービスにリンクすることができます。

[一般ポリシー番号 100.10 の不適切なコンテンツ](/legal/marketplace/certification-policies#10010-inappropriate-content)で禁止されている商品やサービスについて、アプリを介して購入できるようにしてはいけません。

iOS 版または Android 版 Teams で実行するアプリは、以下のガイドラインを遵守する必要があります。

* アプリは、アプリ内購入、試用版の提供、有料版へのアップセルを目的とする UI、またはユーザーが他のコンテンツ、アプリ、アドインを購入するオンライン ストアを含めてはいけません。

    :::image type="content" source="../../../../assets/images/submission/validation-financial-information-in-app-purchase.png" alt-text="validation-financial-info-in-app-purchase":::

    :::image type="content" source="../../../../assets/images/submission/validation-financial-information-online-stores.png" alt-text="validation-online-store":::

* アプリでアカウントが必要な場合、ユーザーは無料でアカウントにサインアップできます。 **無料版** または **無料アカウント** という用語の使用は禁止されています。
* You can determine whether an account is active indefinitely or for a limited time. When the account expires the app must not show UI, text, or links indicating the need to pay.
* アプリのプライバシー ポリシーと使用条件には、商取引に関係した UIやリンクが含まれていてはいけません。

</details>

### <a name="bots"></a>ボット

[*必須の修正プログラム*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.3.2](/legal/marketplace/certification-policies#114032-bots-and-messaging-extension) に沿ったものです。
<br></br>
<details><summary>詳細を知るために展開する</summary>

Microsoft Azure Bot Service を使用するアプリ (ボットやメッセージ拡張機能など) の場合、Microsoft [オンライン サービスの使用条件](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)で定義されているすべての要件に従う必要があります。

ボットを介してファイルをアップロードする場合は、必ずボットからユーザーに許可を求め、確認メッセージを表示しなければなりません。

:::image type="content" source="../../../../assets/images/submission/validation-bot-confirmation-message.png" alt-text="validation-bot-confirmation":::

</details>

### <a name="external-domains"></a>外部ドメイン

[*必須の修正*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー番号 1140.3.3](/legal/marketplace/certification-policies#114033-external-domains) に沿ったもので、`validDomains` マニフェスト プロパティでの制限付きドメインの使用に関する開発者向けのガイダンスを提供します。
<br></br>
<details><summary>詳細を知るために展開する</summary>

Don't include domains outside of your organization's control (including wildcards) and tunneling services in your app's domain configurations. The following exceptions include:

* アプリ内で Azure Bot Service の OAuthCard が使用されている場合、有効なドメイン (validDomains) に `token.botframework.com` を含める必要があります。そうしない場合は、**[サインイン]** ボタンが機能しません。
* アプリが SharePoint に依存している場合は、`{teamSiteDomain}` コンテキスト プロパティを使用して、関連するルート SharePoint サイトを有効なドメインとして含めることができます。
* **.com**、**.in**、**.org** などの最上位ドメインを有効なドメインとして使用しないでください。 [*必須の修正プログラム*]

* **.onmicrosoft.com または** **onmicrosoft** が制御下にない有効なドメインとして使用しないでください。 ただし、 **ドメイン** に **ワイルドカードが含** まれている場合でも、サイトが制御下にある有効なドメインとして yoursite.com を使用できます。 [*必須の修正*]

* アプリが Microsoft Power Platform 上に構築された PowerApp の場合は、アプリが Teams 内でアクセス可能で機能できるようにするには、有効なドメインとして *apps.powerapps.com* を含める必要があります。

</details>

### <a name="sensitive-content"></a>機密コンテンツ

[*必須の修正プログラム*]

アプリは、クレジット カード、金融機関の支払い明細、健康情報、連絡先の追跡などの個人情報、およびその他の機密データを、それらの情報の表示を意図していないユーザーに向けて投稿してはいけません。

ユーザーのマシンや環境にファイルや実行ファイル (.exe) をダウンロードする場合は、その前にユーザーに警告しなければなりません。

## <a name="general-functionality-and-performance"></a>一般的な機能とパフォーマンス

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4](/legal/marketplace/certification-policies#11404-functionality) に沿ったものです。

* 管理者と既存のユーザーの両方に対しては、転送方法に関するガイダンスが必須です。 ハイパーリンクとして転送ガイダンスを追加して、サインアップ、開始、お問い合わせ、ヘルプ リンク、電子メールの送信を行うことができます。
* アプリ機能の下でアカウントの依存関係や制限を呼び出すことは必要ありませんが、マニフェストの長い説明と AppSource アプリの一覧の両方に追加する必要があります。
* 新しいユーザーのテナント管理者に対する依存関係を呼び出す必要があります。 依存関係がない場合は、サインアップ、お問い合わせ、リンクの開始、または電子メールの提供が必須です。

### <a name="launching-external-functionality"></a>外部機能の起動

[*必須の修正*]

アプリの主要なユーザー シナリオにおいて、ユーザーがTeams から離れることがあってはなりません。  アプリ内のコンテンツの表示やユーザーとのやり取りは、ボット、アダプティブ カード、タブ、タスク モジュールなど、Teams の機能の範囲内で実行される必要があります。
<br>
</br>

<details><summary>詳細を知るために展開する</summary>

* ユーザーがTeams の範囲内に留まり、外部のサイトやアプリにリンクを介して移動しないようにします。 外部の機能を利用する必要があるシナリオの場合は、その機能の利用を開始する許可をユーザーから明示的に得る必要があります。

* 外部の機能を開始するボタンの名前は、その操作によりユーザーが Teams から離れることが明確にわかるようなものである必要があります。 たとえば、「**Contoso.com への移動はこちら**」や「**Contoso.com で表示**」といった例が考えられます。

* ユーザーが Teams の外部に移動していることをユーザーに知らせる **ポップアップ** アイコンを追加します。 リンクの右側にあるポップアップ アイコン :::image type="icon" source="../../../../assets/icons/pop-out-icon.png" ::: を使用できます。

* **ポップアップ** アイコンを追加できない場合は、次のいずれかのオプションを実装して、Teams の外部に移動していることをユーザーに知らせることができます。
  * アダプティブ カードにメモを追加します。これは、ユーザーがこの **アプリを使用してヘルプを表示** するを選択すると、Teams の外部でユーザーを受け取ることを示します。
  * インタースティシャルダイアログを追加します。

</details>

### <a name="compatibility"></a>互換性

[*必須の修正プログラム*]

アプリは、以下のオペレーティング システムやブラウザーの最新バージョンで完全に機能する必要があります。

* Microsoft Windows
* macOS
* Microsoft Edge
* Google Chrome
* iOS
* Android

アプリは、サポートされていないブラウザーやオペレーティング システムに関しては、穏当な表現でエラー メッセージを表示する必要があります。

### <a name="response-time"></a>応答時間

[*必須の修正プログラム*]

Teams アプリは、合理的な時間内に応答するか、読み込み中や入力中のインジケーター、メッセージ、または警告を表示する必要があります。

* タブは、2 秒以内に反応するか、読み込みメッセージや警告を表示する必要があります。
* ボットは、ユーザーのコマンドに対して 2 秒以内に応答するか、入力インジケーターを表示する必要があります。
* メッセージ拡張機能は、ユーザーのコマンドに対して 2 秒以内に応答する必要があります。
* 通知は、ユーザーのアクションから 2 秒以内に表示される必要があります。

## <a name="app-package-and-store-listing"></a>アプリ パッケージと Store 登録情報

[*必須の修正*]

アプリケーション パッケージは、正しく書式設定され、すべての必要な情報とコンポーネントが含まれている必要があります。

> [!TIP]
>
> * 提供されたテスト アカウントまたはテスト環境が永続的に有効であることを確認する必要があります。これは、アプリが商用マーケットプレースに公開されるまでです。
> * 公開されたアプリを検証するために、次のようなテスト手順が明記されている必要があります。
>
>   * アプリが外部アカウントに依存する認証を使用している場合は、 **テスト アカウントを構成する手順** を明記する。
>   * Teams 内で実行されるコア ワークフローにおける **期待されるアプリの動作** について概略を記述する。
>   * アプリの詳細な説明や関連資料に記載されている機能、特徴、成果物に関する制限、条件、例外について **明確に説明する**。
>   * アプリを検証するテスターが考慮すべき **あらゆる考慮事項を強調する**。
>   * テストを支援するために、**テスト アカウントにダミー データを事前に設定する**。
>   * テスト アカウントを指定する場合は、サード パーティの統合を有効にしていることを確認します。 また、2 要素認証または多要素認証を無効にします。

### <a name="app-manifest"></a>アプリ マニフェスト

[*必須の修正*]

Teams アプリ マニフェストは、アプリの構成を定義します。

* マニフェストは、一般公開されたマニフェスト スキーマに適合している必要があります。 詳細については、「[マニフェストのリファレンス](~/resources/schema/manifest-schema.md)」を参照してください。 マニフェストのプレビュー バージョンを使用してアプリを申請しないでください。
* アプリにボットやメッセージ拡張機能が含まれている場合、アプリ マニフェストの詳細は、ボット名、ロゴ、プライバシー ポリシーのリンク、サービス使用条件のリンクなど、Bot Framework のメタデータと一致している必要があります。
* アプリが Azure Active Directory を認証に使用する場合は、マニフェストに Microsoft Azure Active Directory (Azure AD) アプリケーション (クライアント) ID を含めます。 詳細については、「[マニフェストのリファレンス](~/resources/schema/manifest-schema.md#webapplicationinfo)」を参照してください。

### <a name="uses-of-latest-manifest-schema"></a>最新のマニフェスト スキーマの使用

* アプリでシングル サインオン (SSO) を使用している場合は、ユーザー認証のためにマニフェストでMicrosoft Azure Active Directory (Azure AD) ID を宣言する必要があります。 [*必須の修正*]

* パブリックにリリースされたマニフェスト スキーマを使用する必要があります。 マニフェスト スキーマ 1.10 以降のパブリック バージョンを使用するようにアプリ パッケージを更新できます。 [*必須の修正プログラム*]

* アプリの更新プログラムを送信するときは、アプリのバージョン番号のみを増やします。 更新されたアプリのアプリ ID は、発行されたアプリのアプリ ID と一致している必要があります。 [*必須の修正*]

* アプリ パッケージ内に追加のファイルが存在することは許容されません。 [*必須の修正プログラム*]

* バージョン番号は、マニフェスト ファイル スキーマと追加言語マニフェスト スキーマで同じである必要があります。 [*必須の修正*]

* アプリをローカライズするには、Teams マニフェスト スキーマ バージョン 1.5 以降を使用する必要があります。 manifest.json ファイルでアプリ スキーマ バージョン 1.5 以降を使用するには、属性を `$schema` 1.5 以降に更新します。 プロパティ`$schema`を`manifestVersion`バージョン (この場合は 1.5) に更新します。 [*必須の修正プログラム*]

* 既存の機能の追加、更新、または削除、マニフェストまたはパートナー センターのメタデータの追加または削除を行うときは、アプリのバージョン番号を増やし、検証のためにパートナー センター アカウントに新しいアプリ マニフェストを送信する必要があります。

* バージョン文字列は、セマンティック バージョン管理仕様 (SemVer) 標準 (MAJOR) に従う必要があります。マイナー。PATCH)。 [*必須の修正*]

* アプリで管理者がアクセス許可を確認し、Teams 管理センターで同意を付与する必要がある場合は、マニフェストで宣言 `webapplicationinfo` する必要があります。 マニフェストで宣言されていない場合 `webapplicationinfo` は、Teams 管理センターのアプリの **[アクセス許可]** ページが **...** として表示されます。[*必須の修正*]

* Teams アプリ認定の一環として、アプリ マニフェストの運用バージョンを送信する必要があります。 [*必須の修正プログラム*]

* マニフェストで Microsoft Partner Network (MPN) ID を宣言することをお勧めします。 MPN ID は、アプリをビルドするパートナー組織を識別するのに役立ちます。 [*修正の提案*]

### <a name="app-icons"></a>アプリのアイコン

[*必須の修正プログラム*]

アイコンは、ユーザーが Teams ストアを閲覧する際に目にする主要な要素の 1 つです。
<br></br>
<details><summary>詳細を知るために展開する</summary>

アイコンは、アプリのブランドや目的を伝えるとともに、以下の要件を満たす必要があります。

* アプリ パッケージには、カラー アイコンおよびアウトライン アイコンという、2 つのアプリ アイコンの PNG ファイルを含める必要があります。
* カラー アイコンの解像度は 192x192 ピクセルである必要があります。  アイコン記号の配色は自由ですが、無地または完全に透明な正方形の背景に配置する必要があります。
* アイコンのアウトライン バージョンは、次のシナリオで表示されます。
  * アプリが使用中で、Teams の左側のアプリ バーに **ホストされて** いるとき。
  * ユーザーがアプリのメッセージ拡張をピン留めするとき。

* アウトライン アイコンの解像度は 32x32 ピクセルです。透明な背景、または白地に透明な背景が使用できます。 アウトライン アイコン内の記号の周りには、余分なパディングがあってはいけません。

* ご使用のアプリ パッケージには、適切なサイズと書式設定されたアイコンが含まれる必要があります。 アイコンは、Store 登録情報のメタデータの情報と一致している必要があります。

詳細については、「[アイコンのガイドライン](~/concepts/build-and-test/apps-package.md#app-icons)」を参照してください。

</details>

### <a name="app-descriptions"></a>アプリの説明

アプリの短い説明と長い説明が必要です。 アプリ構成とパートナー センターの説明は同じである必要があります。

:::image type="content" source="../../../../assets/images/submission/validation-app-description-adequete-information.png" alt-text="図は、Teams アプリでの適切なアプリの説明の例を示しています。":::

:::image type="content" source="../../../../assets/images/submission/validation-app-description-inadequete.png" alt-text="図は、不適切なアプリの説明に失敗したシナリオを示しています。":::

<br></br>
<details><summary>詳細を知るために展開する</summary>

アプリについての説明は、直接的にも間接的にも、他のブランド (Microsoft が所有するブランドか否かにかかわらず) を傷つけるものであってはいけません。  説明に、実証できない要求が含まれていないことを確認します。 たとえば、「**効率が 200% 向上することを保証します**」という記述は不適切です。

* アプリの説明に比較マーケティング情報を含めることはできません。 たとえば、競合するオファーやマーケットプレースを参照するタグやその他のメタデータを含む、オファーリストで競合他社のロゴや商標を使用しないでください。 [*必須の修正*]

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-comparitive-marketing-fail.png" alt-text="図は、アプリの説明に比較マーケティング情報の例を示しています。":::

* ハイパーリンクの連絡先の詳細、作業の開始、ヘルプ、またはアプリの説明へのサインアップ。

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-contact-deatils-hyperlinked.png" alt-text="図は、アプリの説明にハイパーリンクされた連絡先の詳細の例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-contact-deatils-not-hyperlinked.png" alt-text="図は、アプリの説明にハイパーリンクされていない連絡先の詳細の例を示しています。":::

* アプリの説明には、目的の対象ユーザーを識別し、その一意で明確な価値を簡単かつ明確に説明し、サポートされている Microsoft 製品やその他のソフトウェアを特定し、その使用に関する前提条件または要件を含める必要があります。 顧客がオファーを取得する前に、リストおよび関連資料に記載されているように、機能、機能、成果物に対する制限事項、条件、または例外を明確に記述する必要があります。 宣言する機能は、オファーのコア関数と説明に関連している必要があります。 [*必須の修正プログラム*]

* アプリ名を更新する場合は、マニフェスト、AppSource、および該当する場所のオファー メタデータで、古いアプリ名を新しいアプリ名に置き換えます。 [*必須の修正*]

* 制限事項とアカウントの依存関係は、マニフェストアプリの説明、AppSource、およびパートナー センターで呼び出す必要があります。 以下に例を示します。
  * エンタープライズ アカウント
  * 有料サブスクリプション
  * 別のライセンスまたはアカウント
  * 言語
  * 公衆交換電話網 (PSTN) ダイヤル
  * 地域の依存関係
  * 翻訳ツールまたはライブ エージェントの予約のリード タイム
  * ロール ベースの機能
  * ネイティブ アプリへの依存関係

  :::image type="content" source="../../../../assets/images/submission/validation-app-description-limitations-calledout-pass.png" alt-text="図は、アプリの説明で呼び出される制限事項の例を示しています。":::
  
  :::image type="content" source="../../../../assets/images/submission/validation-app-description-limitations-not-calledout-fail.png" alt-text="図は、アプリの説明で呼び出されない制限事項の例を示しています。":::

* アプリが特定のリージョンまたは地理的な場所でサポートされている場合は、そのオファーのマニフェスト、パートナー センター、AppSource のアプリの説明でその特定のリージョンの依存関係を呼び出す必要があります。

* Teams を参照する必要がある場合は、Microsoft Teams としてアプリの一覧に最初の参照を記述します。 後の参照は、Teams と短縮することができます。

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-teams-reference-pass.png" alt-text="図は、アプリの説明で Teams への正しい参照の例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-teams-reference-fail.png" alt-text="図は、アプリの説明で Teams への不適切な参照の例を示しています。":::

#### <a name="short-description"></a>簡潔な説明

簡潔な説明とは、アプリの価値提案を強調した、ターゲットとなるユーザーに向けて書かれた短い説明です。

**すべきこと**:

* 簡潔な説明を、 1 文で表現する。
* 最も重要な情報を最初に説明する。
* 顧客が検索すると考えられるキーワードを含める。
* 使用可能な文字制限を効率的に使用する。 たとえば、アプリ名を繰り返さない。

**してはいけないこと**

[*修正の提案*]

簡潔な説明の中に **アプリ** という言葉を使用する。

#### <a name="long-description"></a>詳しい説明

詳しい説明では、アプリの価値提案、主要な対象ユーザー、対象の業界を強調する魅力的なストーリーを提供できます。 この説明は 4,000 文字にもなりますが、ほとんどのユーザーは 300 から 500 文字程度しか読みません。

**すべきこと**:

* [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) を使用して説明を書式設定する。

* ユーザーに対して、積極的かつ直接的な表現を使用する (たとえば、「**... が可能です**」)。

* 機能を箇条書きにする (一読で理解できるようになる)。

* 一覧や関連資料には、ユーザーがアプリをインストールする前に確認できるように、制限事項、特徴、機能に関する条件ないしは例外、成果物の内訳を明確に記載する。 一覧に記載されるコアの機能は、Teams の機能に関連していなければならない。

* アプリの説明が Teams アプリ内で使用可能な機能と一致していることを確認します。 Teams アプリ外でのワークフローについての言及は限定的なものに留められ、かつ記述される場合も Teams アプリの機能と明確に区別して記述されている必要がある。

* ヘルプやサポートへのリンクを含める。

* **Office 365** ではなく **Microsoft 365** と表記する。

* アプリが Teams (または Microsoft 365) と連携する方法について説明する際には、次のような表現を使用する。
  * **... は Microsoft Teams と連携します。**
  * **... が Microsoft Teams と連携しています。**
  * **... が Microsoft Teams 内で〇〇しています。**
  * **... が Microsoft Teams に対して〇〇しています。**
  * **... が Microsoft Teams に組み込まれています。**
  * **... が ... 向けにビルド**
  * **... が ... 向けに開発**
  * **... が ... 向けに設計**

**してはいけないこと**:

[*必須の修正*]

* 500 文字を超える。
* **Microsoft** の省略形として **MS** や **MSFT** を使用する。

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-microsoft-abbreviated.png" alt-text="図は、Microsoft を MS または MSFT として初めて省略する例をアプリの説明に示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-microsoft-not-abbreviated.png" alt-text="図は、アプリの説明で初めて Microsoft を MS または MSFT として省略しない例を示しています。":::

* アプリが Microsoft の提供物であるかのように記述する。たとえば、Microsoft のスローガンやタグラインを使用する。

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-offering-from-microsoft.png" alt-text="図は、アプリの説明で Microsoft オファリングを示さない方法の例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-no-offering-indication-from-microsoft.png" alt-text="Microsoft のスローガンとタグラインを使用せずにアプリの説明を記述する方法の例を示すグラフィック。":::

* Microsoft の認定パートナーでないにもかかわらず、以下のような表現を使用する。
  * **... は ... の認定〇〇です**
  * **... は ... を装備しています**
* 入力ミス、文法エラーが含まれている。
* 必要性がない場合にもかかわらず、マニフェストや AppSource の「詳細な説明」の全体、またはアプリのコンテンツの全体をキャピタライズする (英語の場合)。

   :::image type="content" source="../../../../assets/images/submission/validation-long-description-typos-pass.png" alt-text="図は、エラーのないアプリの長い説明の例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-long-description-typos-fail.png" alt-text="図は、入力ミスとエラーを含むアプリの長い説明の例を示しています。":::

* AppSource へのリンクを含める。

  :::image type="content" source="../../../../assets/images/submission/validation-app-description-link-to-appsource.png" alt-text="図は、アプリの長い説明で AppSource へのリンクを含む失敗シナリオの例を示しています。":::

* 検証されていない主張を事実として記述する。 たとえば、「ベストです」、「トップです」、「〇〇にランク付けされています」といった表現を使用する (ただし、根拠ある事実である場合は、その限りではない)。
* マーケットプレース上の他のオファーと比較する。

</details>

### <a name="screenshots"></a>スクリーンショット

スクリーンショットは、アプリ名、アイコン、説明を補完するために、アプリの視覚的なプレビューを提供します。
<br></br>
<details><summary>詳細を知るために展開する</summary>

次のことを覚えておいてください。

* スクリーンショットは、1 つの一覧につき 5 枚まで設定できます。
* サポートされているファイルの種類は、PNG、JPEG、GIF です。
* 解像度は 1366x768 ピクセルである必要があります。
* 最大サイズは 1,024KB です。

**すべきこと**:

* Focus on your app's capabilities. For example, how people can communicate with your bot.
* アプリを正確に表現するコンテンツを含めます。
* 賢明な表現を使用する。
* スクリーンショットには、ブランドを反映する色で縁取りを加え、マーケティング コンテンツを含める。
* 鮮明で読みやすいテキストを含む高解像度のスクリーンショットを使用します。 [*必須の修正プログラム*]
* エンド ユーザーのためにアプリの実際の UI を正確に表すモックアップを使用します。 [*必須の修正プログラム*]
* アプリのマーケットプレースの一覧に少なくとも 3 つのスクリーンショットを入力します。
* Teams アプリが他の Microsoft 365 ハブに拡張可能な場合、提供されるスクリーンショットは、他の Microsoft 365 ハブのアプリ機能を示している必要があります。
* 少なくとも 1 つのスクリーンショットに、モバイル デバイス上のアプリの機能を示す必要があります。
* ユーザーがアプリの機能を明確に理解できるように、スクリーンショットにキャプションを入力することをお勧めします。

**してはいけないこと**:

* アプリが Teams の外部で使用されていることを示すなど、アプリの実際の UI を不正確に反映するモックアップを含めます。

> [!TIP]
>
> * アプリを使用する理由を伝えるには、ビデオが最も効果的です。 ビデオは、ユーザーがリストで最初に見るものでもあります。
> * アプリの一覧でビデオを提供することを選択した場合は、パートナー センターでビデオ リンクを送信する前に、YouTube または Vimeo の設定で広告をオフにする必要があります。 アプリの一覧で提供されるビデオは、期間が 90 秒を超えてはなりません。また、Microsoft Teams とのアプリの機能と統合のみを示す必要があります。 詳細については、「[ストアのリスト広告向けビデオを作成する](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)」を参照してください。

</details>

### <a name="privacy-policy"></a>プライバシー ポリシー

[*必須の修正プログラム*]

Teams アプリに特化した特定のポリシーも、すべてのサービスを対象とした全体的なポリシーも、プライバシー ポリシーとして指定できます。

* 汎用のプライバシー ポリシー テンプレートを使用する場合は、**サービス**、**アプリケーション**、または **プライバシー ポリシーの範囲内のプラットフォーム** への参照を追加する必要があります。 **サービス**、**アプリケーション**、**プラットフォーム** への参照が含まれている場合は、範囲内に Teams アプリを指定する必要はありません。 アプリの検証プロセスでは、これらの参照が解析され、Teams アプリがその他のサービスや Web サイトとともに検証されます。
* ユーザー データ ストレージ、保持、および削除の処理方法を含める必要があります。 データ保護のためのセキュリティ制御について説明する必要があります。
* 連絡先情報を含める必要があります。
* 壊れている URL や、ベータ版やステージング用の URL を含んではいけません。
* AppSource へのリンクを含めてはいけません。
* プライバシー ポリシーには、認証を必要とせずにアクセスできなければなりません。
* コマース UI またはストア リンクを含めてはいけません。

### <a name="terms-of-use"></a>使用条件

[*必須の修正プログラム*]

次のガイドラインに沿って使用条件を記述します。

* 提供するサービスに適用できる具体的なものである必要があります。
* 独自のドメインでホストされている必要があります。
* セキュリティで保護された (HTTPS) リンクが必要です。
* 使用条件へのアクセスは、認証が必要なものであってはいけません。

### <a name="support-links"></a>サポート リンク

[*必須の修正*]

アプリのサポート URL は、認証が必要なものであってはいけません。 たとえば、ユーザーが問い合わせるためにログインするものであってはいけません。
<br></br>
<details><summary>詳細を知るために展開する</summary>

サポート URL には、連絡先の詳細や、ユーザーがサポート チケットを発行するための方法を含める必要があります。 たとえば、サポート URL が GitHub でホストされている場合、GitHub ページは所有権下になければならず、ユーザーがサポート チケットを発行するには、連絡先の詳細や転送方法を含める必要があります。

:::image type="content" source="../../../../assets/images/submission/validation-supportlinks-authentication.png" alt-text="validation-support-links-auth":::

</details>

### <a name="localization"></a>ローカリゼーション

[*必須の修正*]

* アプリがローカリゼーションを提供する場合、アプリ パッケージには、Teams の言語設定に基づいて表示される言語の翻訳ファイルを含める必要があります。 ファイルは、Teams のローカリゼーション スキーマに準拠している必要があります。 詳細については、「[Teams のローカリゼーション スキーマ](~/concepts/build-and-test/apps-localization.md)」を参照してください。

* アプリ メタデータコンテンツは、他のローカライズ言語と同じである `en-us` 必要があります。 [*必須の修正*]

* AppSource アプリの説明には、サポートされている言語を表示する必要があります。 たとえば、このアプリは X (X= ローカライズされた言語) で使用できます。 [*必須の修正プログラム*]

* ユーザーのクライアント設定が追加の言語と一致しない場合は、既定の言語が最終フォールバック言語として使用されます。 アプリケーションがサポートする `localizationInfo` 正しい既定の言語でプロパティを更新します。 [*必須の修正*]

* アプリケーションが `localizationInfo` サポートする適切な既定の言語でプロパティを更新するか、マニフェストとパートナー センターの長い説明と短い説明にローカライズされたコンテンツを追加します。 [*必須の修正プログラム*]

## <a name="apps-linked-to-saas-offer"></a>SaaS オファーに関連付けられたアプリ

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.5](/legal/marketplace/certification-policies?branch=pr-en-us-5673) に沿ったものです。 SaaS オファーにリンクされた Teams アプリを構築する場合は、これらのガイドラインに準拠していることを確認してください。
<br></br>
<details><summary>全般</summary>

* ISV は、同じテナント内の複数のユーザー (サブスクライバー) が自身のサブスクリプションを管理し、テナント内のユーザーにライセンスを割り当てる機能をサポートする必要があります。
* このプランは、SaaS プランに関連付けられた [Teams アプリの技術的要件](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/include-saas-offer)をすべて満たす必要があります。
* SaaS プランに関連付けられた Teams アプリは、[サービスとしての 1000 個のソフトウェア (SaaS)](/legal/marketplace/certification-policies#1000-software-as-a-service-saas)で定義されたすべての要件を満たす必要があります。
* マニフェスト ファイル中の `subscriptionOffer` 要素で定義された詳細が正しくなければなりません。 アプリ マニフェストで、値 `publisherId.offerId` を使用してノード `subscriptionOffer` を追加または更新します。 たとえば、発行元 ID が `contoso1234` で、オファー ID が `offer01` である場合、アプリ マニフェストで指定する値は `contoso1234.offer01` である必要があります。
* Teams アプリに関連付けられた SaaS プランは AppSource に存在する必要があり、プレビュー プランはストア承認には承諾されません。

</details>

</br>
<details><summary>オファーのメタデータ</summary>

* オファーのメタデータは、Teams のマニフェスト、AppSource における Teams アプリ登録の内容、および AppSource における SaaS オファーと一致していなければなりません。
* Teams アプリと SaaS プランは、同じ発行元または開発者によるものでなければなりません。 アプリ マニフェストで参照される SaaS プランは、Teams アプリがコマーシャル マーケットプレースに申請される場合と同じ発行元に属している必要があります。
* 申請したオファーが SaaS オファーにリンクされた Teams アプリである場合は、プラン一覧のパートナー センター製品セットアップ セクションで **[追加購入]** に対して **[はい。製品には、サービスの購入や追加のアプリ内購入の提供が必要です]** を選択する必要があります。
* プランの説明と価格の詳細は、ユーザーがプラン一覧を明確に理解するために十分な情報を提供する必要があります。
* 追加のサービスへの制限事項、依存関係や、提供される機能の例外は、プランの説明で正確に呼び出す必要があります。
* SaaS プランにリンクされた Teams アプリは、ユーザーごとに割り当てられたライセンスをサポートするように設計されています。 状況によっては、SaaSオファーが他の方法で構築される場合や、専用の購入フローが用意されている場合もあります。 それぞれの方法や購入フローに関しては、アプリのメタデータおよびサブスクリプション プランの詳細の中で、明確に説明されている必要があります。
* SaaS オファーでは、購入フローのすべての該当する状態にあるすべてのユーザーに向けて、メッセージとガイダンスが提供される必要があります。

</details>
</br>

<details><summary>SaaS プランのホーム ページとライセンス管理</summary>

* サブスクライバーに製品の使用方法を紹介します。
* サブスクライバーへのライセンスの割り当てを許可します。
* FAQ、サポート情報、メールなど、さまざまな方法で問題のサポートに取り組みます。
* ユーザーを検証して、他のユーザー経由でライセンスが割り当てられていないか確認します。
* ライセンスの割り当て後にユーザーに通知します。
* Teams にアプリを追加し、Teams チャット ボットまたは電子メールを使用して作業を開始する方法についてユーザーに説明します。

</details>
</br>

<details><summary>ユーザビリティと機能の内容</summary>

* ライセンスの購入と割り当てが正常に行われたら、次の情報が提供される必要があります。
  * ユーザーがサブスクライブしたプランの機能にアクセスする方法
  * ユーザーに対して提供される、サブスクリプション プランの付加価値と主要なメリット
  * Teams アプリから、SaaS アプリケーションのホーム ページへのリンクを提供し、サブスクライバーが将来にわたってライセンスを管理できるようにします。

</details>
</br>

<details><summary>SaaS アプリケーションの構成とテスト</summary>

テスト目的でアプリのセットアップが複雑な場合は、エンド ツー エンドの機能ドキュメント、リンクされた SaaS オファーの構成手順、ライセンスとユーザー管理に関する手順を *Notes for Certification* の一部として提供します。

> [!TIP]
> アプリやライセンス管理の仕組みを説明したビデオを追加して、チームのテストをサポートすることができます。

</details>

## <a name="tabs"></a>タブ

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.2](/legal/marketplace/certification-policies#114042-tabs) に沿ったものです。
アプリにタブが含まれている場合は、これらのガイドラインに準拠していることを確認します。
> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams タブ デザインのガイドライン](~/tabs/design/tabs.md)」を参照してください。

</br>
<details><summary>セットアップ</summary>

* タブのセットアップでは、新規ユーザーを **待たせてはいけません**。 アクションやワークフローを完了するためのメッセージを提供します。 [*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-new-user.png" alt-text="図は、セットアップ時に行き止まりが設定された Tab の例を示しています。":::

* ユーザーは、Teams の外部でコンテンツを作成し、Teams に戻ってピン留めするために、Teams 内でタブ構成エクスペリエンスを残してはなりません。 タブ構成画面の範囲内で、構成の値と方法が説明される必要があります。 [*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-profile-name.png" alt-text="validation-tabs-set-up-profile-name":::

* Tab configuration screen must not embed an entire website. Keep your configuration experience focused. For example, if you're building a project management app that lets users configure a project in a channel, keep the tab configuration screen focused on allowing the user to select a project from your app to configure in the channel. [*Mandatory Fix*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-experience.png" alt-text="validation-tabs-setup-configuration-exp":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-screen.png" alt-text="validation-tabs-set-up-configuration-screen":::

* タブの構成中にユーザーに URL の入力を要求するアプリは、次の手順を実行する必要があります。
  * ユーザーが URL を取得または生成するための適切な方法の転送ガイダンスを提供します。 [*必須の修正*]
  * アプリの説明に従って、アプリの機能に関連する URL または適切な URL を確認します。 [*必須の修正プログラム*]

    :::image type="content" source="../../../../assets/images/submission/validation-tab-configuration-way-forward-url-pass.png" alt-text="スクリーンショットは、ユーザーが URL を生成する方法を示すタブ構成の例を示しています。":::
  
    :::image type="content" source="../../../../assets/images/submission/validation-tab-configuration-way-forward-url-fail.png" alt-text="スクリーンショットは、ユーザーが URL を生成する方法がないタブ構成の例を示しています。":::

* ユーザーがサポート要件についてお問い合わせできるように、プレーンテキストではなく、構成画面の連絡先情報をハイパーリンクします。 [*必須の修正*]

* シームレスな初回実行ユーザー エクスペリエンスを実現するには、構成画面でサポート URL または電子メールをハイパーリンクすることをお勧めします。 [*修正の提案*]

</details>
</br>

<details><summary>ビュー</summary>

* The sign in screen area must not use large logos. [*Mandatory Fix*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-applogin.png" alt-text="validation-views-app-login":::

* 複数のタブに分割して表示することで、コンテンツはシンプルになります。

    :::image type="content" source="../../../../assets/images/submission/validation-views-multiple-tabs.png" alt-text="val-views-multiple-tabs":::

* タブでは、ヘッダーが重複しないようにする必要があります。 タブ フレームワークにはアプリのアイコンと名前が既に表示されているため、I フレームから重複するロゴを削除します。 [*修正の提案*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-no-duplicate-header-logo.png" alt-text="図は、重複するヘッダーとロゴのないタブの例を示しています。":::

    :::image type="content" source="../../../../assets/images/submission/validation-views-duplicate-header-logo.png" alt-text="図は、重複するヘッダーとロゴを含むタブの例を示しています。":::

</details>
</br>

<details><summary>ナビゲーション</summary>

ナビゲーションに関するガイドラインは次のとおりです。

* タブは、Teams の主要なナビゲーションと競合するようなナビゲーションを設定してはなりません。 タブに左ナビゲーションを指定する場合は、アイコンのみやテキストが上下に並べて表示されたアイコンを含めてはいけません。 これは、テキストが上下に並べて表示されたアイコン (Teams のナビゲーション バーを模倣したもの) を表示するオプションを持つ折りたたみ可能なレールであってはいけません。 インライン テキストやテキストのみを持つアイコンを含めるか、タブ左レールの代わりにハンバーガー メニューを使用します。 [*必須の修正プログラム*]

Fluent UI コンポーネントの [Basic](~/concepts/design/design-teams-app-basic-ui-components.md) と [Advanced](~\concepts\design\design-teams-app-advanced-ui-components.md) を使用してアプリをデザインしてください。

:::image type="content" source="../../../../assets/images/submission/validation-navigation-static-tab.png" alt-text="図は、プライマリ Teams ナビゲーションと競合しないタブ内のナビゲーションの例を示しています。":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-left-navigation.png" alt-text="図は、プライマリ Teams ナビゲーションと競合する左側のナビゲーション レールの例を示しています。":::

* 左レールにツールバーがあるタブは、Teams の左ナビゲーションから 20px の間隔を空ける必要があります。 [*必須の修正プログラム*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-spacing-between-toolbar.png" alt-text="validation-nav-spacing-between-toolbar":::

* タブの 2 番目と 3 番目のページは、階層リンクまたは左ナビゲーションを介して移動されるメイン タブ領域のレベル 2 (L2) ビューとレベル 3 (L3) ビューで開く必要があります。 次のコンポーネントを使用して、タブ内のナビゲーションを支援することもできます。
  * 戻るボタン
  * ページ ヘッダー
  * ハンバーガー メニュー

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-improper-navigation-leveles.png" alt-text="複数のナビゲーション レベルを持つ会議内ダイアログの例を示すスクリーンショット。":::

* タブ内のディープ リンクは、外部 Web ページではなく、Teams 内にリンクさせる必要があります。 たとえば、タスク モジュールやその他のタブなどです。 [*必須の修正プログラム*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-view-button-not-linked-static-tab.png" alt-text="validation-nav-view-button-not-linked-static-tab":::

* アプリのコア エクスペリエンスに対しては、タブから Teams 外部に移動することが可能であってはいけません。 一方、コア エクスペリエンス以外のワークフローに対しては、タブから Teams の外部にリダイレクトさせることができます。 たとえば、サポート チケットを発生する場合などです。 [*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-within-configuration.png" alt-text="validation-nav-core-workflow-within-configuration":::

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-redirects-outside.png" alt-text="validation-nav-core-workflow-redirects-outside":::

* 会議中タブに水平スクロールを表示しないでください。[*必須の修正*]

* アプリで使用される会議中のダイアログでは、水平方向のスクロールを許可しないでください。 会議中のダイアログは控えめに使用し、軽くタスク指向のシナリオに使用します。 サポートされているサイズ範囲内で会議中ダイアログの I フレームの幅を指定して、さまざまなシナリオを考慮できます。 [*必須の修正プログラム*]
* アプリで使用されるタスク モジュールでは、水平方向のスクロールを許可しないでください。 タスク モジュールを使用すると、水平方向のスクロールを必要とせずに、さまざまなサイズを選択してコンテンツを応答性を高めます。 必要に応じて、ステージ ビュー (全画面表示 UI コンポーネントを使用して Web コンテンツを表示) を使用して、水平スクロールなしでワークフローを完了できます。 [*必須の修正*]

* タブが固定 UI 要素を持つ無限キャンバスを使用しない限り、タブ キャンバス全体がスクロール可能な場合、任意のスコープの個人用チャット、チャネル、会議内の詳細タブのタブに存在する水平スクロールは許可されません。 [*必須の修正プログラム*]

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-allowed-scenarios.png" alt-text="図は、水平スクロールが許可されているモバイルのすべてのシナリオの例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-allowed-kanban.png" alt-text="図は、かんばんボードの水平スクロールの例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-list-view-components.png" alt-text="グラフィックは、多くのコンポーネントを含むリスト ビューの例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-fixed-board.png" alt-text="グラフィックは、無限キャンバスと固定ボードを含むホワイトボードの水平スクロールの例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-in-list-view.png" alt-text="図は、リスト ビューでの水平スクロールの例を示しています。":::

* アダプティブ カードの水平スクロールは、Teams に存在してはなりません。 [*必須の修正プログラム*]

* タブのナビゲーションに使用される下部レールは、Teams ネイティブ モバイル アプリのナビゲーションと競合しないようにする必要があります。 [*必須の修正プログラム*]

  :::image type="content" source="../../../../assets/images/submission/validation-tab-bottom-rail-conflicts-with-teams-mobile.png" alt-text="図は、Teams ネイティブ モバイル アプリのナビゲーションと競合するタブの例を示しています。":::

</details>
</br>

<details><summary>ユーザビリティ</summary>

* タブは、既存の Web サイトをホストする以上の価値を提供するものである必要があります。 [*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-provides-workflows.png" alt-text="グラフィックは、チーム内のチャネル メンバーにとって価値のあるワークフローを持つアプリの例を示しています。":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-website-i-framed.png" alt-text="グラフィックは、戻るオプションがない I フレーム内の Web サイト全体を含むアプリの例を示しています。":::

* タブ内でコンテンツを切り捨てたり、オーバーラップしたりしてはいけません。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-content-truncation.png" alt-text="validation-usability-content-truncations":::

* ユーザーがタブで最後に行った操作を取り消すことができるようにする必要があります。

* 個人用コンテキストのタブには、アプリの共有インスタンスからのコンテンツを集約して表示させる場合があります。 たとえば、かんばんカードを使用してプロジェクトにコメントを付加する機能を提供する、構成可能タブを含んだ「プロジェクト管理アプリ」の場合、集約されたコンテンツを個人用アプリに表示させる必要があります。 [*修正の提案*]

* タブは Teams テーマに対応するものである必要があります。 ユーザーがテーマを変更すると、アプリのテーマにもその選択が反映される必要があります。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-responsive-tabs.png" alt-text="図は、Teams のテーマに対応するタブの例を示しています。":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-unresponsive-tabs.png" alt-text="図は、Teams のテーマに応答しないタブの例を示しています。":::

* タブでは、Teams フォント、タイプ ランプ、カラー パレット、グリッド システム、モーション、音声のトーンなど、Teams スタイルのコンポーネントを可能な限り使用する必要があります。 詳細については、「[タブ デザイン ガイドライン](/microsoftteams/platform/tabs/design/tabs)」を参照してください。 [*修正の提案*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-uses-diff-font.png" alt-text="スクリーンショットは、ネイティブ Teams フォントではなく calibri フォントを含むタブの例を示しています。":::

* 設定を変更する必要があるアプリの機能が存在する場合は、**[設定]** タブを用意します。[*おすすめの修正プログラム*]
* タブは、ページ内ナビゲーション、ダイアログの位置と使用、情報階層など、Teams の対話設計に従う必要があります。 詳細については、 [Microsoft Teams Fluent UI キットに関するページを](~/concepts/design/design-teams-app-basic-ui-components.md)参照してください。

* タブ エクスペリエンスは、モバイル (Android と iOS) で完全にレスポンシブでなければなりません。

   > [!TIP]
   >
   > * 個人用タブと一緒に個人用ボットを設定します。
   > * ユーザーが自分の個人用タブからコンテンツを共有できるようにします。

* タブには、タブ内のワークフローを完全に妨げる要素や妨げる要素を含めることはできません。たとえば、最小化できないタブ内のボットなどです。

   :::image type="content" source="../../../../assets/images/submission/validation-tab-elements-impede-workflow.png" alt-text="図は、タブ内のワークフローを妨げる要素を含むタブの例を示しています。":::

* Tab には機能が壊れてはなりません。 オファーは使用可能なソフトウェア ソリューションである必要があり、リストやその他の関連資料に記載されている機能、機能、成果物を提供する必要があります。 [*必須の修正プログラム*]

* タブにフッターが含まれている場合は、アプリの機能に関係のないリンクをすべてフッターから削除してください。

</details>
</br>

<details><summary>スコープの選択</summary>

* 構成可能なタブのランディング ページ内のコンテンツは、個人の使用を対象にしてはならず、**マイ タスク** や **マイ ダッシュボード** などの個人用コンテンツを含んではいけません。

   :::image type="content" source="../../../../assets/images/submission/validation-configurable-tab-content-personal-scope.png" alt-text="図は、[マイ タスク] や [マイ ダッシュボード] などの個人用スコープを持つ構成可能なタブのコンテンツの例を示しています。":::

* 構成エクスペリエンスの後、ランディング ページにチーム全体の共同作業ビューが表示される必要があります。

* 作業効率や職場の生産性向上のために、アプリ内で個人スコープのビューを提供するには、個人向けアプリへのディープ リンクを使用して表示を絞り込むか、または構成可能タブ内の L2 ないしは L3 のビューに移動します。その際、ランディング ページはコンテキストごとに、すべてのユーザーに対して同じ状態に保ちます。

* 構成可能タブのランディング ページのコンテンツは、コンテキストごとに、すべてのチャネル メンバーに対して同じでなければいけません。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-tab-personal-info.png" alt-text="図は、構成可能なタブのランディング ページのコンテンツの例を、すべてのメンバーで状況に応じて異なって示しています。":::

* 構成可能タブの機能は、十分に絞り込まれたものでなければなりません。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-nested-tabs.png" alt-text="validation-usability-configurable-nested-tab":::

</details>
<br/>

## <a name="bots"></a>ボット

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.3](/legal/marketplace/certification-policies#114043-bots) に沿ったものです。

アプリにボットが含まれている場合は、これらのガイドラインに準拠していることを確認します。

> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams ボット デザインのガイドライン](~/bots/design/bots.md)」を参照してください。

</br>
<details><summary>ボット デザイン ガイドライン</summary>

* Teams アプリは、 [Teams ボットの設計ガイドライン](../../../../bots/design/bots.md)に従う必要があります。

* ワークフローに繰り返しタスクを実行するユーザーが含まれる場合に、複数ターンボットの応答を回避するためにタスク モジュールを実装する必要があります。 たとえば、タスク モジュールを使用して、複数ターンの会話を使用する代わりに、名前、dob、場所、および指定を繰り返しキャプチャします。 [*必須の修正*]

* アプリ内の壊れたリンク、応答、またはワークフローはすべて修正する必要があります。 [*必須の修正プログラム*]

</details>

</br>
<details><summary>ボット コマンド</summary>

Analyzing user input and predicting user intent is difficult. Bot commands provide users a set of words or phrases for your bot to understand.

* アプリ マニフェストのセクションに、サポートされているボット コマンドを少なくとも 1 つ一覧表示する `{commandList}` 必要があります。 これらのコマンドは、ユーザーがボットにメッセージを送信しようとする際に、作成ボックスに表示されます。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-listed.png" alt-text="図は、アプリ マニフェストに一覧表示されているボット コマンドの例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-not-listed.png" alt-text="図は、アプリ マニフェストに一覧表示されていないボット コマンドの例を示しています。":::

* **Hi**、**Hello**、**Help** などの汎用的なコマンドを含め、ボットがサポートするすべてのコマンドが正しく動作する必要があります。
  
  :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-generic-response-pass.png" alt-text="グラフィックは、汎用コマンドに応答するボットの例を示しています。":::

  :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-generic-no-response.png" alt-text="グラフィックは、汎用コマンドに応答しないボットの例を示しています。":::

* ボット コマンドは、ユーザーのワークフローを妨げるものではなく、常に前に進める方法を提供するものでなければいけません。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-deadend.png" alt-text="validation-bot-commands-dead-end":::

* マニフェストのセクションに少なくとも 1 つの有効なボット コマンドを `items.commands.title` 一覧表示し、ボット コマンドとその使用方法をユーザーにわかりやすくするための適切な説明を追加する必要があります。 マニフェスト 画面のセクションに `commandLists` 、ボット コマンド メニューに事前設定されたコマンドとして一覧表示されるボット コマンドを使用すると、新しいユーザーがボットと対話できるようになります。 [*必須の修正*]

* ボットの応答には、Microsoft の公式製品イメージやアバターを含めることはできません。 アプリで独自のアセットを使用します。 アプリでの Microsoft 製品イメージの使用は許可されていません。 お客様は、End-Userライセンス契約 (EULA)、コンテンツに付随するライセンス条項、または [Microsoft の商標およびブランドガイドライン](https://www.microsoft.com/legal/intellectualproperty/trademarks)に明示的なアクセス許可が付与されている場合にのみ、Microsoft 著作権で保護された製品イメージをコピー、変更、配布、表示、ライセンス、または販売することができます。 [*必須の修正プログラム*]

* ボットは、継続的読み込みインジケーターを表示せずにユーザー コマンドに応答する必要があります。 [*必須の修正*]

* ボット ヘルプ コマンド応答は、Teams の外部でユーザーをリダイレクトしないでください。 ボット ヘルプ コマンド応答は、ユーザーを Teams アプリ内のキャンバスにリダイレクトしたり、アダプティブ カードで応答を転送する方法を提供したりできます。 [*必須の修正プログラム*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-redirects-user-outside-teams.png" alt-text="図は、Teams の外部でユーザーをリダイレクトするボット応答の例を示しています。":::

* ボットは、入力が無関係または不適切な場合でも、常にユーザー入力に対して有効な応答を提供する必要があります。 [*必須の修正*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-valid-improper-input.png" alt-text="不適切なボット コマンドに対する有効な応答の例を図に示します。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-improper-response-invalid-command.png" alt-text="不適切なボット コマンドに対する無効な応答の例を図に示します。":::

* スラッシュ (**/**) などの特殊文字は、ボット コマンドの先頭に付けてはなりません。 [*必須の修正プログラム*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-special-characters.png" alt-text="図は、失敗したシナリオの例を示しています。このシナリオでは、特殊文字の先頭にボット コマンドが付けられます。":::

* ボットは、無効なユーザー コマンドに対して有効な応答を提供する必要があります。 ボットは、ユーザーが無効なボット コマンドを送信した場合に、ユーザーを行き止めしたり、エラーを表示したりしないでください。 [*必須の修正*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-way-forward-for-invalid-command.png" alt-text="図は、無効なコマンドの転送方法を提供するボットの例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-bot-dead-end-invalid-command.png" alt-text="図は、ボットが有効で無効なコマンドに対して同じ応答を送信する失敗したシナリオの例を示しています。":::

* ボットの機能は、ボットがインストールされているスコープに関連する必要があり、ボットはインストールされたスコープに値を提供する必要があります。 [*必須の修正プログラム*]

* ボットに重複するコマンドを含めることはできません。 [*必須の修正*]

* ボットは、ユーザー コマンドに応答した後に入力インジケーターを表示することはできませんが、ユーザー コマンドに応答するときに入力インジケーターを表示できます。 [*必須の修正プログラム*]

* ボットは、小文字または大文字で入力された **ヘルプ** コマンドに対して有効な応答を提供する必要があります。これにより、ユーザーは転送方法を提供したり、ボットの使用状況に関連するヘルプ コンテンツにユーザーがアクセスしたりできます。 ボットは、ユーザーがアプリにログオンしていない場合でも、有効な応答を提供する必要があります。 [*必須の修正プログラム*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-valid-response-lowercase.png" alt-text="図は、ボットがコマンドに対して有効な応答を小文字または大文字で提供していない例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-valid-response-logged-app.png" alt-text="図は、ユーザーがアプリにログオンしていない場合に有効な応答がないボットの例を示しています。":::

* ボットは、 **ヘルプ** コマンドに対して有効な応答を提供する必要があります。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-help-command.png" alt-text="図は、ヘルプ コマンドに対して有効な応答を送信するボットの例を示しています。":::

* モバイル上のボットの応答は、エンド ユーザーのボットの使用が目的のワークフローを完了することを妨げるデータ切り捨てなしで応答性を持つ必要があります。 [*必須の修正プログラム*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-no-truncate-mobile.png" alt-text="グラフィックは、モバイルで切り捨てずにボット メッセージの例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-truncate-mobile.png" alt-text="図は、モバイルでのボット メッセージの切り捨ての例を示しています。":::

* ボット応答アダプティブ カード内のすべてのリンクは、応答性が高い必要があります。 Teams プラットフォームの外部でユーザーを受け取るリンクには、[表示] などの明確なリダイレクト テキストが必要です **。** または **、ボット** の応答アクション ボタンのポップアップ アイコン。またはボット応答メッセージ本文に適切なリダイレクト テキストがあります。 [*必須の修正プログラム*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-action-button-redirect-warning.png" alt-text="図は、リダイレクトを含むボット応答アクション ボタンの例を示しています。":::

* 設計上、ボットがユーザー コマンドに応答したりサポートしたりせず、ユーザーに通知のみを目的とした一方向のボットである場合。 マニフェストでは true に設定 `isNotificationOnly` する必要があります。 [*必須の修正プログラム*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-command-isnotification-only-true.png" alt-text="図は、アプリ マニフェストで通知のみのプロパティが true に設定されている例を示しています。":::

  :::image type="content" source="../../../../assets/images/submission/validation-bot-command-isnotification-only-not-true.png" alt-text="図は、ボットのみがユーザーのメッセージに応答しない通知の例を示しています。":::

* ボットのユーザー エクスペリエンスがモバイル プラットフォームで壊れてはなりません。 ボットは、モバイルで完全に応答性が高い必要があります。 [*必須の修正*]

> [!TIP]
> 個人用ボットの場合は、**[ヘルプ]** タブを設けて、ボットにより可能となる機能について詳しく説明します。

</details>
</br>

<details><summary>ボットのウェルカム メッセージ</summary>

* アプリの構成フローが複雑である場合 (エンタープライズ ライセンスが必須である、直感的なサインアップ フローが提供されていない、などの場合)、アプリのボットは初回実行時に必ず、ウェルカム メッセージを送信する必要があります。

  最適なエクスペリエンスを得るには、チャネルにボットをインストールしたユーザー、ボットを構成する方法、およびサポートされているすべてのボット コマンドを簡単に説明する、ボットによって提供される値をウェルカム メッセージに含める必要があります。 ボタン付きのアダプティブ カードを使用してウェルカム メッセージを表示すると、より使いやすくなります。 詳細については、「[ボットのウェルカム メッセージをトリガーする方法](~/bots/how-to/conversations/send-proactive-messages.md)」を参照してください。 アプリの構成フローが複雑でない場合、ボットの初回実行時にウェルカム メッセージを表示させることは選択になります。 ただし、ウェルカム メッセージを表示させる場合は、ウェルカム メッセージのガイドラインに従う必要があります。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message.png" alt-text="図は、ボットが複雑な構成ワークフローを持っているときにウェルカム メッセージを送信するボットの例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-no-welcome-message.png" alt-text="図は、ボットが複雑な構成ワークフローを持っているときにウェルカム メッセージを送信しないボットの例を示しています。":::

* チャネルやチャットでのボットのウェルカム メッセージは、初回実行時には省略可能であり、特にボットが個人用に利用でき、同様のアクションを実行する場合は省略できます。 ボットはユーザーに個別にウェルカム メッセージを送信してはいけません ([スパム](#botmessagespamming)と見なされます)。 メッセージには、ボットを追加したユーザーもメンションしなければなりません。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-not-triggered.png" alt-text="validation-bot-welcome-message-not-trigger":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-triggered.png" alt-text="validation-bot-wel-message-trigger":::

* 通知のみのボットは、ボットが通知のみのボットであり、ユーザーがボットと対話できないことを明確にするウェルカム メッセージを送信する必要があります。 [*必須の修正*]

   :::image type="content" source="../../../../assets/images/submission/validation-notification-only-welcome-message-pass.png" alt-text="図は、ボットがウェルカム メッセージを送信する例を示しています。これは、通知のみのボットです。":::

* ウェルカム メッセージは、ユーザーを配信停止にしないでください。 ウェルカム メッセージには、チャネルにボットをインストールしたユーザーに対してボットによって提供される値、ボットを構成する方法、およびサポートされているすべてのボット コマンドを簡単に説明する必要があります。 ボタン付きのアダプティブ カードを使用してウェルカム メッセージを表示すると、より使いやすくなります。 [*必須の修正*]

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-no-way-forward.png" alt-text="図は、ボットがウェルカム メッセージでユーザーを転送する方法がない失敗したシナリオの例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-clear-way-forward.png" alt-text="図は、ユーザーがタスクを完了するための明確な方法を備えたボットウェルカム メッセージの例を示しています。":::

* チャネルまたはグループ チャット スコープにインストールされたボットは、1:1 チャットですべてのチーム メンバーにプロアクティブなウェルカム メッセージを送信しないでください。 [*必須の修正プログラム*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-send-proactive-message-to-all-members.png" alt-text="図は、ボットがすべてのチーム メンバーにプロアクティブなウェルカム メッセージを送信する例を示しています。":::

* 通知のみのボットは、メッセージにボットの構成を完了するための重要な情報が含まれている場合、または通知がトリガーされたときにシナリオを明確にする場合にのみ、チャネルでプロアクティブウェルカム メッセージを送信できます。 [*必須の修正プログラム*]

* チャネルまたはグループ チャット スコープにインストールされたボットは、チャネルまたはグループ チャット内のすべてのユーザーとは無関係なプロアクティブ メッセージ (ウェルカム メッセージだけでなく) を送信しないでください。代わりに、1:1 チャットを介してプロアクティブ メッセージをユーザーに送信する必要があります。 [*必須の修正プログラム*]

* チャネルまたはグループ チャット スコープにインストールされたボットは、ユーザーが個々のワークフローを開始できないようにする必要があります。 ボットは、ユーザーとの 1 対 1 チャットで個々のワークフローを完了する必要があります。 [*必須の修正*]

* ボットウェルカム メッセージは、インストールされているスコープでのボットの使用に関連する制限を明確に呼び出す必要があります。 [*必須の修正プログラム*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-messahe-with-app-limitation.png" alt-text="図は、ボットウェルカム メッセージのアプリ制限の例を示しています。":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-messahe-without-app-limitation.png" alt-text="ウェルカム メッセージにアプリの制限のないボットの例を示す図。":::

* ウェルカム メッセージは、個人用スコープでのアプリのインストール時に自動トリガーする必要があります。 ボットが個人用スコープでウェルカム メッセージを送信しない場合、ユーザーは行き止まりになります。 アプリに複雑な構成ワークフローが含まれていない場合は、開発者がチャネルまたはグループ チャット スコープでウェルカム メッセージをトリガーすることは省略可能です。 [*必須の修正*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-no-welcome-message-in-personal-scope.png" alt-text="図は、個人用スコープでウェルカム メッセージを自動的に送信しないボットの例を示しています。":::

* ウェルカム メッセージは、ボットのインストール時に 1 回だけトリガーする必要があります。 ウェルカム メッセージは、ユーザーがヘルプ コマンドを呼び出すたびにトリガーすることはできません。 ユーザーがボットに関連するヘルプにアクセスする方法を含めるには、ヘルプ コマンドの応答に重点を置く必要があります。 [*必須の修正プログラム*]

* ウェルカム メッセージは、すべてのボット コマンドでトリガーすることはできません。 これはスパムと見なされます。 [*必須の修正*]

  :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-trigger-for-any-command.png" alt-text="図は、任意のコマンドのウェルカム メッセージをトリガーするボットの例を示しています。":::

* ウェルカム メッセージのコンテンツは、アプリの長い説明とインストール スコープで説明されているボット ワークフローに関連している必要があります。 ウェルカム メッセージには、チャネルにボットをインストールしたユーザーに対してボットによって提供される値、ボットを構成する方法、およびサポートされているすべてのボット コマンドを簡単に説明する必要があります。 [*必須の修正プログラム*]

* アプリのインストール時にトリガーされた場合、ボットは複数のウェルカム メッセージを送信しないでください。 [*必須の修正*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-multiple-message-trigger-install.png" alt-text="図は、アプリのインストール時に複数のウェルカム メッセージをトリガーするボットの例を示しています。":::

* ウェルカム メッセージのアプリ名は、マニフェスト内のアプリ名と一致している必要があります。 [*必須の修正プログラム*]

  :::image type="content" source="../../../../assets/images/submission/validation-app-name-mismatch-manifeast-and-welcome-message.png" alt-text="ウェルカム メッセージのアプリ名の例を示す図は、アプリ マニフェストのアプリ名と一致しません。":::

* アプリが特定の相互運用性を提供しない限り、ウェルカム メッセージに競合他社のチャット ベースのコラボレーション プラットフォーム名を表示しないでください。

* ウェルカム メッセージは、ユーザーを別の Teams アプリにリダイレクトしないでください。代わりに、ウェルカム メッセージでユーザーが最初のタスクを完了し、アプリでサポートされているすべてのボット コマンドを簡単に説明する必要があります。 [*必須の修正*]

* ウェルカム メッセージには、AppSource を含むアプリ マーケットプレースへのリンクを含めることはできません。 [*必須の修正プログラム*]

* アプリに管理者主導のインストールが必要な複雑な構成ワークフローがある場合、直感的ですぐに利用できるサインアップ フローがない場合、またはユーザーが Teams エクスペリエンスの外部で構成手順を完了し、戻る必要がある場合、ボットはインストール後にチームまたはグループ チャットスコープでプロアクティブなウェルカム メッセージを送信する必要があります。 [*必須の修正*]

* ボットがチャネルでウェルカム メッセージを送信する場合は、それをユーザーに個別に送信しないでください (スパムと見なされます)。 ウェルカム メッセージには、ボットを追加したユーザーについても言及する必要があります。 [*修正の提案*]

> [!TIP]
> 個別のユーザーへのウェルカム メッセージでは、カルーセル ツアーを使用してボットやその他のアプリ機能の概要を効果的に伝えることにより、ユーザーにボット コマンドを試すように促すことができます。 たとえば、「**タスクを作成する**」などです。

</details>
</br>

<details><summary><a id="botmessagespamming">ボット メッセージのスパム</a></summary>

ボットは、短期間に複数のメッセージを連続して送信するようなスパム行為をしてはいけません。

* **チャネルやチャットでのボットメッセージ**: 複数の投稿を同時に行うことはスパム行為となるので避けてください。 1 つの記事を作成し、同じスレッドに返信してください。

    :::image type="content" source="../../../../assets/images/submission/validation-bot-message-spamming-one-message.png" alt-text="validation-bot-message-spam-one-message":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-message-spamming-multiple-messages.png" alt-text="validation-bot-message-spam-multiple-message":::

* **個人用アプリでのボット メッセージ**:
  * 複数のメッセージを連続して送信しないでください。

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-multiple-message-quick-succession.png" alt-text="図は、ボットが複数のメッセージを連続して送信する例を示しています。":::

  * 情報が完結した 1 件のメッセージを送信してください。
  * 単一のワークフローの反復を複数の会話にまたがって実行することは避けてください。
  * フォーム (またはタスク モジュール) を使用して、ユーザーのすべての入力を一度に収集します。
  * 自然言語処理 (NLP) ベースの会話型チャットボットを利用すれば、マルチターンの会話により話し合いの進行が促進され、ワークフローを完了させることができます。

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-task-module.png" alt-text="validation-bot-message-using-task-module":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-mutliple-conversation.png" alt-text="図は、複数ターン メッセージを使用して 1 つの会話を完了するボットの例を示しています。":::

* **ウェルカム メッセージ**: 一定の間隔で同じウェルカム メッセージを繰り返してはいけません。 たとえば、チームに新しいメンバーが加わったとき、他のメンバーにウェルカム メッセージを送ることは、スパム行為とみなされます。 新しいメンバーへのメッセージは個人的に送信してください。

   :::image type="icon" source="../../../../assets/images/submission/validation-bot-send-proactive-message-to-all-members.png" alt-text="図は、同じウェルカム メッセージでユーザーをスパムするボットの例を示しています。":::

</details>
</br>

<details><summary>ボット通知</summary>

ボット通知には、ボットに定義された範囲 (チーム、チャット、個人用) に関連するコンテンツを含める必要があります。

:::image type="content" source="../../../../assets/images/submission/validation-bot-notifications-relevant.png" alt-text="validation-bot-notification-relevant":::

:::image type="content" source="../../../../assets/images/submission/validation-bot-notifications-not-relevant.png" alt-text="validation-bot-notification-not-relevant":::

</details>
</br>
<details><summary>ボットとアダプティブ カード</summary>

アダプティブ カードは、ボット メッセージを表示するのに最適な方法です。 カードは簡素なものに限定してください。アクションは最大 6 つまでとします。 より多くのコンテンツを表示するには、タスク モジュールやタブの使用を検討してください。

カードの詳細については、以下を参照してください。

* [アダプティブ カードをデザインする](~/task-modules-and-cards/cards/design-effective-cards.md)
* [カード リファレンス](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

ボット エクスペリエンスは、モバイル上でレスポンシブ対応でなければなりません。 ボットの応答では、可能な限り、ワークフローを前に進める方法が提供されている必要があります。 ボットはレスポンシブ対応であり、かつ失敗時には適切なエラー メッセージが表示されなければなりません。 コラボレーション中のトリガーに基づいて、個人スコープからユーザーに対して送信されるボット メッセージからは、(メッセージの発信元を含む) コンテキスト情報が提供される必要があります。

</details>
</br>

<details><summary>通知専用ボット</summary>

通知専用ボットによって構成されたアプリでは、コア アプリまたはバックエンドの特定のトリガーまたはイベントによってユーザーへの通知がトリガーされ、それによりユーザーに価値が提供されます。 たとえば、営業チームに対して、新しい潜在顧客や見込み客がフォローアップのために通知されてリストに追加される場合などがその例となります。 高品質の通知専用ボットは、ワークフローの完了やアラートなど、特定のイベント完了時にユーザーに定期的に通知します。

通知は、次のような場合に Teams での価値を提供します。

1. 投稿されたカードやテキストにより十分な情報が提供されており、ユーザーが追加で操作する必要がない。
1. 投稿されたカードやテキストが、ユーザーがアクションを起こすべきか、あるいはTeams 外部のリンクを開いて詳細を確認すべきかを判断するのに十分なプレビュー情報が提供されている。

コンテンツを含む通知のみを提供するアプリ。 **新しい通知が表示** され、 **クリックして Teams** の外部に移動する必要があります。それ以外の場合は、Teams 内で大きな価値が得られません。

   :::image type="content" source="../../../../assets/images/submission/validation-bot-notification-only-inadequete-info.png" alt-text="スクリーンショットは、プレビューで不十分な情報を含む通知のみのビットの例を示しています。":::

> [!TIP]
> 情報をプレビューし、投稿されたカードに基本的なインライン ユーザー アクションを提供して、ユーザーが (複雑さにかかわらず) すべてのアクションに対して Teams の外部に移動する必要がないようにします。

</details>
<br/>

<details><summary>ボットメタデータ情報</summary>

* アプリ マニフェスト内のボット情報 (ボット名、ロゴ、プライバシー リンク、サービス利用規約リンク) は、Bot Framework メタデータと一致している必要があります。 [*必須の修正*]

* ボット ID は、アプリ マニフェストと Bot Framework メタデータで一致する必要があります。 [*必須の修正プログラム*]

* アプリ マニフェストのボット ID が、アプリの最後のストア発行バージョンのボット ID と一致していることを確認します。 アプリの更新でボット ID を変更すると、アプリの既存のユーザーに対してボットとのすべてのユーザー操作履歴が永続的に失われ、新しいボット ID を使用して新しい会話チェーンが開始されます。 [*必須の修正*]

* アプリ名、メタデータ、ボットウェルカム メッセージ、またはボットの応答に対する変更は、新しい名前で更新する必要があります。 [*必須の修正プログラム*]

* ボットウェルカム メッセージまたはボット応答のアプリ名は、マニフェスト内のアプリ名と一致している必要があります。 [*必須の修正*]

</details>
<br/>

<details><summary>共同作業スコープ内のボット</summary>

* チャネルまたはグループ チャット スコープにボットをインストールし、チーム固有のトリガーに対して 1 対 1 のチャットとしてユーザーにプロアクティブな通知を送信するためのチーム名簿を取得することはできません。 たとえば、会議のためにユーザーをペアリングするアプリなどです。 [*必須の修正プログラム*]

* チャネルチャットまたはグループ チャットのボットは、1 対 1 のチャットが許可されていないため、ユーザーに対してプロアクティブな通知を送信するためのチャネルまたはグループ チャットのメッセージまたは投稿を取得するためにのみ使用されます。 [*必須の修正*]

* コラボレーション スコープにインストールされたボットは、コラボレーション スコープ内のユーザー値を提供する必要があります。 [*必須の修正プログラム*]

</details>

## <a name="message-extensions"></a>メッセージの拡張機能

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.4](/legal/marketplace/certification-policies#114044-messaging-extensions) に沿ったものです。

アプリにメッセージ拡張機能が含まれている場合は、これらのガイドラインに準拠していることを確認します。

> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams メッセージ拡張機能デザインのガイドライン](~/messaging-extensions/design/messaging-extension-design.md)」を参照してください。

<br/>

<details><summary>メッセージング拡張機能のデザインのガイドライン</summary>

* Teams アプリがメッセージング拡張機能機能を使用している場合、アプリは [メッセージング拡張機能の設計ガイドライン](../../../../messaging-extensions/design/messaging-extension-design.md)に従う必要があります。

   :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-design-guidelines-fail.png" alt-text="図は、拡張機能のガイドラインを満たしていないアプリの例を示しています。":::

* メッセージング拡張機能は、会話から離れることなく、アプリのコンテンツを挿入したり、メッセージに対して操作したりするためのショートカットです。 メッセージング拡張機能をシンプルにし、アクションを効果的に完了するために必要なコンポーネントのみを表示します。 完全な Web サイトは、メッセージング拡張機能内で I フレーム化しないでください [*必須の修正*]

* メッセージング拡張機能のアダプティブ カードのプレビュー イメージは、適切に読み込む必要があります。 [*必須の修正プログラム*]

  :::image type="content" source="../../../../assets/images/submission/validation-preview-image-adaptive-card-loading.png" alt-text="グラフィックは、アダプティブ カードでのプレビュー イメージの読み込みの例を示しています。":::

  :::image type="content" source="../../../../assets/images/submission/validation-preview-image-adaptive-card-not-loading.png" alt-text="グラフィックは、アダプティブ カードに読み込まれないプレビュー イメージの例を示しています。":::

* メッセージング拡張機能の応答カードには、エンド ユーザーの混乱を防ぐためにアプリ アイコンを含める必要があります。 [*必須の修正プログラム*]

* アプリの機能が壊れてはなりません。 アプリは、ユーザーがメッセージング拡張機能のワークフローを完了するのを停止したりブロックしたりしないでください。 [*必須の修正*]

* メッセージング拡張機能は、グループ チャットとチャネルスコープで、意図したとおりに応答または動作する必要があります。 [*必須の修正プログラム*]

* ユーザーがメッセージング拡張機能にサインインまたはサインアウトする方法を含める必要があります。 [*必須の修正*]

</details>
</br>

<details><summary>アクション ベースのメッセージ拡張機能のアクション コマンド</summary>

操作ベースのメッセージ拡張機能では、以下のことを行う必要があります。

* ユーザーがサインインなどの中間的な手順を行うことなく、メッセージに対するアクションを起こせるようにする。

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-no-intermediate-step.png" alt-text="validation-messaging-extension-no-intermediate-steps":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-intermediate-step-available.png" alt-text="validation-messaging-extension-intermediate-steps-available":::

* メッセージ コンテキストを次の作業状態に渡す。 [*必須の修正プログラム*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-passes-message.png" alt-text="validation-messaging-extension-app-passes-messages":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-doesnot-pass-message.png" alt-text="validation-messaging-extension-app-doesnot-pass-messages":::

* アプリ内のチャット メッセージ、チャネルへの投稿、アクションの呼び出しによってトリガーされるアクション コマンドの名前には、一般動詞による表記だけではなく、ホスト アプリの名前も含めます。 たとえば、**Skype 会議を開始して会議を****開始** し、**ファイルを DocuSign にアップロード****してファイルをアップロードします**。 [*修正の提案*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-host-name.png" alt-text="図は、アクション コマンドのホスト アプリ名の例を示しています。":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-verb.png" alt-text="図は、アクション コマンドの汎用動詞の例を示しています。":::

* メッセージ アクションを呼び出すと、ユーザーはワークフローを完了できる必要があります。 意図したとおりにメッセージ アクションを機能させるエラー、空白の応答、または継続的読み込みインジケーターは存在してはなりません。 [*必須の修正プログラム*]

   :::image type="content" source="../../../../assets/images/submission/validation-continous-loading-indicator-action-command.png" alt-text="図は、ボットがアクション コマンドを呼び出したときの継続的読み込みインジケーターの例を示しています。":::

* 重複するアクション コマンドは存在しない必要があります。 [*必須の修正プログラム*]

* メッセージ アクションでは、ユーザーが無効な応答なしで意図したとおりにワークフローを完了できるようにする必要があります。 [*必須の修正プログラム*]

* アクション ベースのメッセージング拡張機能のみを持つアプリは、次の終了状態である必要があります。

  * メッセージ拡張機能が呼び出されるコンテキストまたはユーザー シナリオに基づく 1 対 1 のボット チャットで、関連するアクションを通知として投稿します。 [*必須の修正プログラム*]

  * 実行されたアクションに基づいて、ユーザーが他のユーザーとカードを共有できるようにします。 これは、アプリがサイレント アクションを実行しないようにするためです。 たとえば、チケットはチャネル内のメッセージに基づいて作成されますが、アプリは通知を送信しないか、チケットの作成後にチケットの詳細を共有するようにユーザーに要求する方法を提供しません。 [*必須の修正*]

</details>
</br>

<details><summary>プレビュー リンク (リンク展開)</summary>

[*必須の修正*]

メッセージ拡張機能では、認識されたリンクが Teams の作成ボックスでプレビューされます。  制御外のドメイン (絶対 URL、ワイルドカードのいずれについても) を追加してはいけません。  たとえば、`yourapp.onmicrosoft.com` は有効ですが、`*.onmicrosoft.com` は無効です。 トップレベルの ドメインも禁止です。 たとえば、`*.com` および `*.org` が禁止となります。 [*必須の修正プログラム*]

</details>
</br>

<details><summary>検索コマンド</summary>

* 検索ベースのメッセージ拡張機能では、ユーザーが効果的に検索できるようなテキストが用意されている必要があります。 [*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-search-commands-text-available.png" alt-text="図は、ユーザーが効果的に検索するためのヘルプ テキストを含むメッセージ拡張機能の例を示しています。":::

    :::image type="content" source="../../../../assets/images/submission/validation-search-commands-text-not-available.png" alt-text="図は、ユーザーが効果的に検索するためのヘルプ テキストのないメッセージ拡張機能の例を示しています。":::

* @メンション実行可能ファイルは、明確で、理解しやすく、読みやすいものである必要があります。

    :::image type="content" source="../../../../assets/images/submission/validation-search-command-unclear-executable.png" alt-text="validation-search-commands-unclear-executable":::

</details>
</br>

<details><summary>検索ベースのメッセージ拡張機能のアクション コマンド</summary>

[*必須の修正*]

検索ベースのメッセージ拡張機能により構成されるアプリは、コンテキストの切り替えなしでコンテキストに沿った会話が可能なカードを共有することで、ユーザーに価値を提供します。

検索ベースのメッセージ拡張機能のみのアプリの検証を渡すには、ユーザー エクスペリエンスが壊れていないことを確認するために、ベースラインとして次のものが必要です。 メッセージ拡張機能を介して共有されるカードは、次の場合に Teams に価値を提供します。

1. 投稿されたカードにより十分な情報が提供され、ユーザーが追加で操作する必要がない。
1. 投稿されたカードが、ユーザーがアクションを起こしたり、Teams 外部のリンクを開いて詳細を表示ことを決定するのに十分なプレビュー情報を提供している。

    :::image type="content" source="../../../../assets/images/submission/validation-search-based-messaging-ext-adequete-info.png" alt-text="validation-search-base-messaging-ext-adequete-info":::

    :::image type="content" source="../../../../assets/images/submission/validation-search-based-messaging-ext-inadequete-info.png" alt-text="validation-search-base-messaging-ext-inadequete-info":::

リンク展開のみが提供されるアプリでは、Teams 内で十分な価値が提供されません。  アプリがリンク展開のみを提供し、他の機能が提供されない場合は、アプリ内に追加のワークフローを構築することを検討してください。

</details>

## <a name="task-modules"></a>タスク モジュール

[*必須の修正*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.5](/legal/marketplace/certification-policies#114045-task-modules) に沿ったものです。
<br></br>
<details><summary>詳細を知るために展開する</summary>

タスク モジュールには、アイコンと関連付けられたアプリの短い名前を含める必要があります。 タスク モジュールは、アプリ全体を埋め込んだり、特定の操作を完了するために必要なコンポーネントのみを表示するものであってはいけません。

詳細については、「[Teams タスク モジュールのデザイン ガイドライン](~\task-modules-and-cards\task-modules\design-teams-task-modules.md)」を参照してください。

:::image type="content" source="../../../../assets/images/submission/validation-task-module-displays-components.png" alt-text="validation-task-module-displays-component":::

:::image type="content" source="../../../../assets/images/submission/validation-task-module-embeds-app.png" alt-text="validation-task-module-embed-app":::

> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams タスク モジュール デザインのガイドライン](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)」を参照してください。

</details>

## <a name="meeting-extensions"></a>ミーディング拡張機能

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.6](/legal/marketplace/certification-policies#114046-meeting-extensions) に沿ったものです。
> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams ミーティング拡張機能デザインのガイドライン](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)」を参照してください。

</br>
<details><summary>会議拡張機能の設計ガイドライン</summary>

* Teams アプリは [、会議拡張機能の設計ガイドライン](../../../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)に従う必要があります。

* 会議内アプリエクスペリエンスを使用すると、会議内のタブ、ダイアログ ボックス、会議内共有を使用して会議中に参加者を参加させることができます。 アプリで Teams 会議拡張機能がサポートされている場合は、Teams 会議エクスペリエンスに合わせて応答性の高い会議内エクスペリエンスを提供する必要があります。 [*必須の修正プログラム*]

* 会議前のエクスペリエンスにおいてユーザーは、検索して見つかった会議アプリを追加できます。 ユーザーは、会議の参加者を調査するための投票の開発など、会議前のタスクを実行することもできます。 会議前エクスペリエンスを提供するアプリは、会議のワークフローに関連し、ユーザーに価値を提供する必要があります。 [*必須の修正プログラム*]

* 会議後のアプリ エクスペリエンスでは、ユーザーは会議の結果 (アンケート結果やフィードバック、その他のアプリ コンテンツなど) を表示できます。 会議後エクスペリエンスを提供するアプリは、会議のワークフローに関連し、ユーザーに価値を提供する必要があります。 [*必須の修正プログラム*]

* 会議中のアプリ エクスペリエンスでは、会議中に会議参加者を積極的に関与させ、すべての出席者の会議エクスペリエンスを強化できます。 アプリのコア ユーザー ワークフローを完了するために、Teams 会議の外部に出席者を連れて行く必要はありません。 [*必須の修正*]

   :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-outside-teams-core-workflows.png" alt-text="図は、コア アプリ機能を完了するために Teams の外部でユーザーをリダイレクトする会議内エクスペリエンスの例を示しています。":::

* アプリは、Teams でカスタムの Together Mode シーンのみを提供する以外の価値を提供する必要があります。 [*必須の修正プログラム*]

* Teams モバイルでの会議にアプリを有効にするには、マニフェストのスコープの下`configurableTabs`と`meetingDetailsTab``meetingChatTab``meetingSidePanel`コンテキスト プロパティとして宣言`groupChat`する必要があります。 [*必須の修正*]

* 会議キャンバスは、会議の出席者を行き止めしてはなりません。 会議キャンバスでは、リージョン固有の依存関係などのアプリの制限に対して正常なエラー メッセージを表示する必要があります。 [*必須の修正プログラム*]

* 会議の出席者を混乱しないように、会議キャンバスのヘッダーに正しいアプリ名を表示する必要があります。 [*必須の修正*]

* ユーザーが会議拡張機能からサインアウトまたはログアウトするためのオプションを含める必要があります。 [*必須の修正プログラム*]

* モバイル プラットフォームの会議タブには、関連するワークフローを含める必要があります。 空のページを会議タブに表示しないでください。[*必須の修正*]

* 会議ステージは、集中的で直感的で共同作業に参加するキャンバスです。 会議ステージでは、完全な Web サイト エクスペリエンスを埋め込む必要はありません。 [*必須の修正プログラム*]

* アプリは、ユーザーを行き詰めたり、会議のシナリオでワークフローの完了をブロックしたりする継続的な読み込み画面、エラー、または壊れた機能を表示しないでください。 [*必須の修正*]

   :::image type="content" source="../../../../assets/images/submission/validation-app-shows-continous-loading-screen.png" alt-text="グラフィックは、アプリ内の連続読み込み画面の例を示しています。":::

* アプリは、会議の開始時に新しい Teams インスタンスを開く必要があります。 会議キャンバスは、リアルタイムのコラボレーションを促進する Teams 機能の拡張機能であり、新しい会議は現在アクティブな Teams インスタンス内で常に開く必要があります。 [*必須の修正プログラム*]

* 会議アプリは、競合他社のチャット ベースのプラットフォームにリダイレクトすることなく、Microsoft Teams プラットフォーム内でワークフローを完了する必要があります。 [*必須の修正*]

   :::image type="content" source="../../../../assets/images/submission/validation-apps-redirecting-competitor-chat-platform.png" alt-text="グラフィックは、競合他社のチャット ベースのプラットフォームにリダイレクトするアプリの例を示しています。":::

* アプリがロール ベースのビューをサポートしており、特定のワークフローがすべての参加者に利用できない場合は、タブとサイド パネルで参加者に適切なメッセージングを実装することをお勧めします。アプリは現在開催者のビュー用であり、出席者が会議ノート、アクション アイテム、および予定を更新する方法の詳細を提供します。 [*必須の修正プログラム*]

   :::image type="content" source="../../../../assets/images/submission/validation-way-forward-not-available-for-role-based-views.png" alt-text="図は、ロール ベースのビューの参加者に進む方法がないアプリの例を示しています。":::

</details>
<br/>

<details><summary>全般</summary>

ミーティング拡張機能には、次のガイドラインを使用します。

* 会議機能拡張アプリは、Teams 会議エクスペリエンスに合わせて、応答性の高い会議内エクスペリエンスを提供する必要があります。 会議内エクスペリエンスは、会議の拡張性をサポートする Teams アプリでは必須ですが、会議前と会議後のエクスペリエンスは必須ではありません。

  * 会議前のエクスペリエンスにおいてユーザーは、検索して見つかった会議アプリを追加できます。 ユーザーは、会議の参加者を調査するための投票の開発などの会議前タスクを実行することもできます。 アプリが会議前のエクスペリエンスを提供する場合は、会議のワークフローに関連するものでなければなりません。

  * 会議後のアプリ エクスペリエンスを使用すると、ユーザーは会議の結果 (アンケート結果やフィードバック、その他のアプリ コンテンツなど) を表示できます。 アプリが会議後のエクスペリエンスを提供する場合は、会議のワークフローに関連するものでなければなりません。

  * 会議中のアプリ エクスペリエンスでは、会議中に会議参加者を積極的に関与させ、すべての出席者の会議エクスペリエンスを強化できます。 アプリのコア ユーザー ワークフローを完了するために、Teams 会議の外部に出席者を連れて行く必要はありません。

* アプリによって、Teams のカスタムの Together Mode シーン以上の価値が提供されなければなりません。

* Shared meeting stage 機能は、Teams のデスクトップ アプリからのみ起動できます。  ただし、Shared meeting stage の使用エクスペリエンスは、モバイル デバイスで表示する場合にも問題なく使用可能である必要があります。

> [!TIP]
> Teams モバイルでの会議にアプリを有効にするには、マニフェストのスコープの下`configurableTabs`と`meetingDetailsTab``meetingChatTab``meetingSidePanel`コンテキスト プロパティとして宣言`groupChat`する必要があります。

</details>
</br>

<details><summary>会議前後のエクスペリエンス</summary>

* 会議前後の画面は、一般的なタブ デザイン ガイドラインに準拠している必要があります。 詳細については、「[Teams デザイン ガイドライン](~/tabs/design/tabs.md)」を参照してください。
* 複数の項目を表示する場合に、タブのレイアウトが整理されている必要があります。 たとえば、10 件を超える投票またはアンケートについては、「[レイアウトの例](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting)」を参照してください。
* アプリでアンケートや投票の結果がエクスポートされた場合に、「**結果が正常にダウンロードされました**」と表示してユーザーに通知する必要があります。

   :::image type="content" source="../../../../assets/images/submission/validation-meeting-experience-tab-design-guidelines-fail.png" alt-text="図は、タブデザインガイドラインに従っていないタブの例を示しています。":::

</details>

</br>
<details><summary>会議中のエクスペリエンス</summary>

* アプリは、会議中のみダーク テーマを使用する必要があります。 詳細については、「[Teams デザイン ガイドライン](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming)」を参照してください。
* 会議中にアプリ アイコンにカーソルを合わせると、ツールヒントにアプリ名が表示される必要があります。

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-display-app-name.png" alt-text="validation-in-meeting-exp-display-app-names":::

* メッセージ拡張機能は、会議中も会議以外のときと同じように機能する必要があります。

</details>

</br>
<details><summary>会議中のタブ</summary>

* レスポンシブ対応である必要があります。
* パディングとコンポーネントのサイズを一定に保つ必要があります。
* 複数のレベルのナビゲーションがある場合は、戻るボタンが必要です。

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button.png" alt-text="戻るボタンの表示の例を示す図。":::

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button-absent.png" alt-text="戻るボタンが表示されない例を図に示します。":::

* 閉じるボタンが複数あってはいけません。 タブを閉じるためのヘッダー ボタンがすでに埋め込まれているため、ユーザーを混乱させるかもしれません。
* 水平スクロールを使用しないでください。

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-tab-vertical-scroll.png" alt-text="グラフィックは、垂直スクロールを含む会議内タブの例を示しています。":::

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-tab-horizontal-scroll.png" alt-text="図は、横スクロールを含む会議内タブの例を示しています。":::

</details>

</br>
<details><summary>会議中のダイアログ</summary>

* 頻繁に使用してはなければなりません。簡素でかつタスク指向性のあるシナリオに対してのみ使用してください。
* コンテンツは 1 列に表示されていなければなりません。また、複数のナビゲーション レベルがあってはなりません。

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-single-column-layout.png" alt-text="図は、会議中ダイアログの単一列レイアウトの例を示しています。":::

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-multiple-column-layout.png" alt-text="図は、会議内ダイアログの複数の列レイアウトの例を示しています。":::

* タスク モジュールを使用してはいけません。
* 会議ステージの中心に位置合わせする必要があります。

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-dialog-not-aligned.png" alt-text="図は、会議中のダイアログが会議ステージの中心と一致しない例を示しています。":::

* ユーザーがボタンを選択したり、アクションを実行したりした後に閉じる必要があります。

* **Together モード**: 以下のベスト プラクティスを検討して、シーン構築を行ってください。
  * 画像はすべて PNG 形式で作成します。
  * すべてのイメージをまとめたパッケージの解像度は、1920x1080 を超えないようにしてください。 解像度は偶数です。 この解像度は、シーンを正常に表示するための必要条件です。
  * シーンの最大サイズは 10 MB です。
  * 各画像の最大サイズは 5 MB です。 シーンは、複数の画像のコレクションです。 制限は、個々の画像に対するものです。
  * 必要に応じて **[透明]** を選択します。 このチェック ボックスは、画像が選択されている場合に右パネルで使用できます。 シーン内で重なり合っている画像には、画像が重なっていることを示すために、「Transparent」とマークする必要があります。

</details>

## <a name="notifications"></a>通知

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.7](/legal/marketplace/certification-policies#114047-notification-apis) に沿ったものです。

アプリが [Microsoft Graph によって提供されるアクティビティ フィード API を](/graph/teams-send-activityfeednotifications)使用している場合は、次のガイドラインに従っていることを確認します。

> [!TIP]
> アプリで、1 日または 1 か月後など、長い間隔で通知がトリガーされる通知シナリオがサポートされている場合。 確認のために送信する前に、このような通知をバックグラウンドでトリガーして通知をテストしてください。

<br></br>

<details><summary>通知の設計ガイドライン</summary>

* Teams アプリは [、アクティビティ フィード通知の設計ガイドライン](/graph/teams-send-activityfeednotifications)に従う必要があります。

* 無関係、不適切、応答しない、または壊れたワークフローは、ユーザーが Teams アクティビティ フィードで通知を選択した後に存在してはなりません。 ユーザーがアクティビティ フィード通知を選択した後、ワークフローの完了をブロックすることはできません。 [*必須の修正*]

* エンド ユーザーが混乱することなく通知のソースまたはトリガーを理解できるように、アクティビティ フィード通知にアプリの名前を含めます。 [*必須の修正プログラム*]

* アプリは、アプリの長い説明、アプリの最初の実行エクスペリエンス、マニフェストで宣言 `activityTypes` されているシナリオで説明されているすべての通知シナリオに対して通知をトリガーする必要があります。 [*必須の修正プログラム*]

* 通知は、ユーザーのアクションから 5 秒以内に表示される必要があります。 [*必須の修正*]

* アプリの長い説明またはアプリの最初の実行エクスペリエンスで、通知の制限 (存在する場合) を呼び出す必要があります。 [*必須の修正プログラム*]

</details>
<br/>

<details><summary>全般</summary>

* アプリ構成で指定されたすべての通知トリガーが動作する必要があります。
* 通知は、アプリにおいて構成されているすべての言語についてローカライズされていなければなりません。
* 通知は、ユーザーのアクションから 5 秒以内に表示される必要があります。
* 通知は、アプリが互換性のあるすべてのプラットフォームでサポートされている言語に従ってローカライズする必要があります。 [*必須の修正*]

</details>
</br>

<details><summary>アバター</summary>

* 通知のアバターは、アプリのカラー アイコンと一致している必要があります。
* ユーザーによってトリガーされた通知には、そのユーザーのアバターが表示されなければなりません。

</details>
</br>
<details><summary>スパム</summary>

* アプリは、1 分間に 10 件以上の通知をユーザーに送信してはいけません。
* ボットとアクティビティ フィードは、同じ通知を重複してトリガーしてはいけません。
* 通知は、ユーザーに何らかの価値を提供するものである必要があります。些細なイベントや無関係なイベントに使用してはいけません。

</details>
</br>
<details><summary>ナビゲーションとレイアウト</summary>

* 通知は、Teams アクティビティ フィードのレイアウトとエクスペリエンスに関するガイドラインに準拠する必要があります。
* 通知を選択したユーザーは、Teams 内の関連コンテンツに誘導されなければなりません。

</details>

## <a name="microsoft-365-app-compliance-program"></a>Microsoft 365 アプリ コンプライアンス プログラム

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.6](/legal/marketplace/certification-policies#11406-publisher-attestation) に沿ったものです。
<br></br>
<details><summary>詳細を知るために展開する</summary>

Microsoft 365 アプリ コンプライアンス プログラムは、アプリに関するセキュリティおよびコンプライアンス情報を評価することにより、組織がリスクを評価し管理することを目的としています。 Teams ストアにアプリを公開する場合は、以下のプロセスを完了する必要があります。

* **発行元の検証**: 管理者とエンド ユーザーが、Microsoft ID プラットフォームを利用するアプリの開発者の信頼性について理解する上で役立ちます。  検証が完了すると、Azure Active Directory (Azure AD) 同意ダイアログやその他の画面に青い「**確認済み**」バッジが表示されます。 詳細については、「[アプリを発行元確認済みとしてマークする](/azure/active-directory/develop/mark-app-as-publisher-verified)」を参照してください。

    :::image type="content" source="../../../../assets/images/submission/validation-365-compliance-publisher-verification.png" alt-text="図は、Azure Active Directory の同意ダイアログで青い検証済みバッジの例を示しています。":::

* **発行元の構成証明**: 潜在的な顧客がアプリの使用を適切な情報に基づいて判断できるように、一般的な情報、データの取り扱い、セキュリティとコンプライアンスに関する情報を共有するプロセス。

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: 過去に登録済みのアプリを提出する場合、そのアプリが Teams ストアに登録されるまでは、正式に発行元の構成証明を完了することができません。 登録されたことのあるアプリを更新する場合は、アプリの最新バージョンを提出する前に発行元の構成証明を完了してください。

</details>

## <a name="advertising"></a>広告

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.7](/legal/marketplace/certification-policies#11407-advertising) に沿ったものです。

アプリは、動的な広告、バナー広告、メッセージ内広告などの広告を表示してはいけません。

:::image type="content" source="../../../../assets/images/submission/validation-advertising-banners.png" alt-text="図は、Teams での広告の失敗したシナリオの例を示しています。":::

## <a name="cryptocurrency-based-apps"></a>暗号化ベースのアプリ

アプリが配布されているすべての法律に準拠していることを示す必要があります (アプリの場合)。

* アプリ内での暗号化トランザクションまたは送信を容易にします。

* 暗号化関連のコンテンツを宣伝します。

* ユーザーが格納されている仮想通貨を格納またはアクセスできるようにします。

* ユーザーが Teams プラットフォームの外部で暗号化ベースのトランザクションまたは送信を完了することを推奨または有効にします。

* 暗号化トークンのマイニングを奨励または促進します。

* 初期コイン オファリングへのユーザーの参加を促進します。

* タスクを完了するための暗号化トークンを使用して、ユーザーに報酬を与えたり、インセンティブを与えたりします。

Microsoft の内部レビューの後、コンプライアンスのデモンストレーションが満足できる場合、Microsoft はアプリのさらなる認定を続行できます。 コンプライアンスのデモンストレーションが不十分な場合、Microsoft はアプリの認定を続行しないという決定について通知を受け取ります。

## <a name="app-functionality"></a>アプリの機能

* アプリ内のワークフローまたはコンテンツは、スコープに関連している必要があります。 [*必須の修正プログラム*]
* すべてのアプリ機能は機能している必要があり、AppSource またはマニフェストの長い説明に従って適切に動作する必要があります。 [*必須の修正*]
* アプリは、ユーザーの環境でファイルまたは実行可能ファイルをダウンロードする前に、常にユーザーを親しませておく必要があります。 アクションの呼び出し (CTA) は、テキストベースかそれ以外の方法で行われます。これにより、ファイルまたは実行可能ファイルがユーザー アクションでダウンロードされていることがアプリで許可されます。 [*必須の修正プログラム*]

## <a name="mobile-experience"></a>モバイル エクスペリエンス

* モバイル アドインは無料である必要があります。 アップセル、オンライン ストア、またはその他の支払い要求を促進するアプリ内コンテンツやリンクを含めることはできません。 アプリに必要なアカウントには、使用料を含めず、時間に制限がある場合は、支払う必要があることを示すコンテンツを含めてはなりません。

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-add-in-charges.png" alt-text="グラフィックは、支払いを求めるモバイル アドインの例を示しています。":::

* **FREE**、**無料試用版**、**または TRY FREE** という単語の使用は、デスクトップまたは Web アプリのエクスペリエンスで制限や考慮事項なしで許可されます。

* 試用版またはアプリのアップグレードのコンテキストでプレーンテキストとして **FREE** という単語を使用することは、モバイルで許可されます。

* 支払い情報や価格情報のないランディング ページにつながるリンクを含む試用版またはアプリのアップグレードのコンテキストでの **FREE** という言葉の使用は、モバイルで許可されます。 アプリが **有料** であることを通知するプレーンテキストは、モバイルで許可されます。

* 試用版またはアプリのアップグレードのコンテキストで **プレーンテキストとして FREE** という単語を使用することは、モバイルでは許可されません。

* 試用版またはアプリのアップグレードのコンテキストで **FREE** という単語を使用し、モバイルでの価格情報や支払いの詳細を含むランディング ページにつながるリンクに関連付けることはできません。

* 画像、テキスト、リンクなど、あらゆる形式のモバイルの価格の詳細は許可されません。 モバイルでの **ビュー プラン** などの CTA は許可されていません。 価格の詳細がないプランに関する情報は、モバイル上の連絡先リンクまたは電子メールでは許可されません。 有料アップグレードにリンクまたは言及している連絡先の詳細を含むテキストは、モバイルでは許可されません。 物理的な商品の支払は、モバイルで許可されます。 たとえば、アプリで支払いを許可してタクシーを予約できます。

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-exp-pricing-details-on-mobile-fail.png" alt-text="グラフィックは、モバイルでの価格の詳細の例を示しています。":::

* アプリ内のデジタル商品の支払は、モバイルでは許可されません。 [*必須の修正*]

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-exp-payments-digital-goods.png" alt-text="グラフィックは、モバイルでのデジタル商品の支払いの例を示しています。":::

* Teams アプリは、適切なクロスデバイス モバイル エクスペリエンスを提供する必要があります。 [*必須の修正プログラム*]

* モバイルでサポートされていない機能は、ユーザーを配信不能にすることはできず、該当する場合は正常なエラー メッセージを提供する必要があります。 [*必須の修正*]

## <a name="next-step"></a>次の手順

> [!div class=*nextstepaction*]
> [パートナー センター アカウントを作成する](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)

## <a name="see-also"></a>関連項目

* [アプリを配布する](~/concepts/deploy-and-publish/apps-publish-overview.md)
* [ストア送信を準備する](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [アプリのテストおよびデバッグ](~/concepts/build-and-test/debug.md)
* [パートナー センターの開発者アカウントを作成する](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
