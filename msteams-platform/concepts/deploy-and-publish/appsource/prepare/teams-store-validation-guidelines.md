---
title: Microsoft Teams ストア検証ガイドライン
description: この記事では、Teams ストア (AppSource) に送信されたすべてのアプリが従う必要があるガイドラインを示します。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: 65d6a8683249c7b076705087675029eb91f6eb24
ms.sourcegitcommit: d3b7b4a12c757b97cf0e996bedd22335a9a70afc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2022
ms.locfileid: "67417651"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams ストア検証ガイドライン

これらのガイドラインに従うことで、アプリが Microsoft Teams ストアの審査プロセスに合格する可能性が高まります。 Teams 固有のガイドラインは、Microsoft [コマーシャル マーケットプレース認定ポリシー](/legal/marketplace/certification-policies#1140-teams)を補完するものであり、新機能やユーザー フィードバック、ビジネス ルールの変更を反映して頻繁に更新されています。

> [!NOTE]
>
> * 一部のガイドラインは、アプリに適用できない場合があります。 たとえば、アプリにボットが含まれていない場合は、ボット関連のガイドラインを無視することができます。
> * これらのガイドラインを Microsoft の商用認定ポリシーに相互参照し、検証プロセスで発生した合格または不合格のシナリオの例を示す「やるべきこと」と「やってはいけないこと」を追加しました。
> * 特定のガイドラインは、*必須の修正* としてマークされます。 アプリの申請がこれらの必須のガイドラインを満たしていない場合は、Microsoft から改善のための手順を示すエラー レポートが送信されます。  アプリの申請は、問題を修正した場合にのみ Microsoft Teams ストアの検証に合格します。
> * その他のガイドラインは、*修正の提案* としてマークされます。理想的なユーザー エクスペリエンスを得るためには、問題を修正することをお勧めします。ただし、問題を修正しない場合でも、アプリの申請が Teams ストアでの公開をブロックされることはありません。

:::row:::
   :::column:::
      :::image type="content" source="../../../../assets/icons/value-proposition.png" alt-text="value-proposition-teams" link="#value-proposition":::
   :::column-end:::
   :::column span="":::
     :::image type="content" source="../../../../assets/icons/security.png" alt-text="security-store" link="#security":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/function.png" alt-text="機能" link="#general-functionality-and-performance":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/package.png" alt-text="app-package" link="#app-package-and-store-listing":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/saas-offer.PNG" alt-text="SaaS" link="#apps-linked-to-saas-offer":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/tab.png" alt-text="tab-teams" link="#tabs":::
   :::column-end:::
   :::column:::
      :::image type="content" source="../../../../assets/icons/bot.png" alt-text="bot-teams" link="#bots-1":::
   :::column-end:::
   :::column span="":::
     :::image type="content" source="../../../../assets/icons/messaging-extension.png" alt-text="メッセージング" link="#message-extensions":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/task-module.png" alt-text="task-module-teams" link="#task-modules":::
   :::column-end:::
     :::column span="":::
      :::image type="content" source="../../../../assets/icons/meeting.png" alt-text="meeting-extension" link="#meeting-extensions":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/empty.png" alt-text="empty-2":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/notifications.png" alt-text="teams-notification" link="#notifications":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/microsoft-365.png" alt-text="microsoft" link="#microsoft-365-app-compliance-program":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/advertising.png" alt-text="advertising-teams" link="#advertising":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/empty.png" alt-text="empty-1":::
   :::column-end:::
:::row-end:::

## <a name="value-proposition"></a>価値提案

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用認定ポリシー番号 1140.1](/legal/marketplace/certification-policies#11401-value-proposition-and-offer-requirements) に沿ったものであり、そのオファーの価値提案に関して、Microsoft Teams アプリの開発者に追加のガイダンスを提供します。

### <a name="app-name"></a>アプリ名

[*必須の修正*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、Microsoft [商用認定ポリシー番号 1140.1.1](/legal/marketplace/certification-policies#114011-app-name) に沿ったものであり、それらのアプリの名前の指定に関して、開発者に追加のガイダンスを提供します。
<br></br>
<details><summary>詳細を知るために展開する</summary>

アプリの名前は、ユーザーがストアでアプリを見つける際に重要な役割を果たします。 次のガイドラインを使用してアプリの名前を指定します。

* 名前には、ユーザーに関連する用語を含める必要があります。
* 次のような Teams のコア機能の名前は、アプリ名に含めてはいけません。  
  * **チャット**
  * **連絡先**
  * **Calendar**
  * **通話**
  * **ファイル**
  * **アクティビティ**
  * **アプリ**
  * **ヘルプ**
* 開発者の名前を普通名詞の接頭辞または接尾辞として含める。 たとえば、**タスク** ではなく **Contoso タスク** がこれにあたります。
* ブランド提携や共同販売を誤って示す可能性のある、**Teams** やその他の Microsoft 製品の名前 (Excel、PowerPoint、Word、OneDrive、SharePoint、OneNote、Azure、Surface、Xbox など) を使用することはできません。 Microsoft ソフトウェア、製品、およびサービスの参照に関する詳細については、「[Microsoft の商標およびブランドに関するガイドライン](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general)」を参照してください。
* アプリが Microsoft との公式パートナーシップのメンバーである場合、アプリの名前が最初に来る必要があります。たとえば、**Contoso Connector for Microsoft Teams** がこれにあたります。
* ストアに登録済みのアプリや、コマーシャル マーケットプレース上のその他のオファーと同じ名前を使用してはいけません。
* 卑猥な言葉や軽蔑的な言葉を含んではいけません。 名前には、人種や文化に配慮しない言葉が含まれてはいけません。
* 一意である必要があります。ご使用のアプリ (Contoso) が Microsoft Teams ストアと Microsoft AppSource に一覧表示されていて、Contoso Mexico のように地域に特化した別のアプリを一覧表示する場合、申請が次の条件を満たす必要があります。
  * タイトル、メタデータ、最初の応答アプリ エクスペリエンス、ヘルプ セクションでアプリの地域固有の機能を呼び出します。 たとえば、タイトルは「Contoso Mexico」でなければなりません。 アプリのタイトルは、エンド ユーザーの混乱を避けるために、既存のアプリと同じ開発者を明確に区別する必要があります。
  * パートナー センターでアプリ パッケージをアップロードする場合は、**[可用性]** セクションでアプリを利用できる適切な **マーケット** を選択します。

 > [!TIP]  
 > Microsoft Teams ストアおよび Microsoft AppSource上に公開するアプリのブランド要素 (アプリ名、開発者名、アプリ アイコン、Microsoft AppSource スクリーンショット、ビデオ、短い説明、Web サイトなど) は、Microsoft の公式の提供物として表示してはいけません。ただし、アプリが公式の Microsoft 1P ライセンスを取得済みである場合はその限りではありません。

</details>

### <a name="suitable-for-workplace-consumption"></a>職場での消費に適していること

[*必須の修正プログラム*]

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

ボタンやその他の UI テキストに含まれるアプリの機能名は、Teams やその他の Microsoft 製品で使用されている用語と重複してはいけません。 たとえば、**会議を開始**、**通話する**、**チャットを開始** などです。 必要に応じて、アプリ名を挿入してください (たとえば、**[Contoso 会議の開始]** としてください)。

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

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは [Microsoft 商用認定ポリシー番号 1140.3.1](/legal/marketplace/certification-policies#114031-financial-transactions) に沿ったもので、Teams インターフェイス内の財務情報の送信に関するガイダンスを提供し、Teams アプリのモバイル (Android および iOS) バージョンでの制限付き支払いのシナリオを開発者に対して示します。
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
* アカウントを無期限にアクティブにするか、期間限定にするかを決めることができます。 アカウントの有効期限が切れたとき、アプリ内に、支払いを求めるUI、テキスト、またはリンクを表示してはいけません。
* アプリのプライバシー ポリシーと使用条件には、商取引に関係した UIやリンクが含まれていてはいけません。

</details>

### <a name="bots"></a>ボット

[*必須の修正*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.3.2](/legal/marketplace/certification-policies#114032-bots-and-messaging-extension) に沿ったものです。
<br></br>
<details><summary>詳細を知るために展開する</summary>

Microsoft Azure Bot Service を使用するアプリ (ボットやメッセージ拡張機能など) の場合、Microsoft [オンライン サービスの使用条件](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)で定義されているすべての要件に従う必要があります。

ボットを介してファイルをアップロードする場合は、必ずボットからユーザーに許可を求め、確認メッセージを表示しなければなりません。

:::image type="content" source="../../../../assets/images/submission/validation-bot-confirmation-message.png" alt-text="validation-bot-confirmation":::

</details>

### <a name="external-domains"></a>外部ドメイン

[*必須の修正プログラム*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー番号 1140.3.3](/legal/marketplace/certification-policies#114033-external-domains) に沿ったもので、`validDomains` マニフェスト プロパティでの制限付きドメインの使用に関する開発者向けのガイダンスを提供します。
<br></br>
<details><summary>詳細を知るために展開する</summary>

組織の制御外のドメイン (ワイルドカードなど) やトンネリング サービスをアプリのドメイン構成に含めてはいけません。以下の例外があります。

* アプリ内で Azure Bot Service の OAuthCard が使用されている場合、有効なドメイン (validDomains) に `token.botframework.com` を含める必要があります。そうしない場合は、**[サインイン]** ボタンが機能しません。
* アプリが SharePoint に依存している場合は、`{teamSiteDomain}` コンテキスト プロパティを使用して、関連するルート SharePoint サイトを有効なドメインとして含めることができます。

#### <a name="government-community-cloud-listings"></a>Government Community Cloud の一覧表示

Government Community Cloud (GCC) ユーザーにアプリを配布するには、Teams ストアに重複して表示しないようにする一方で、認証プロセスでユーザーを特定し、GCC 固有の URL または予想される URL にルーティングする必要があります。

</details>

### <a name="sensitive-content"></a>機密コンテンツ

[*必須の修正プログラム*]

アプリは、クレジット カード、金融機関の支払い明細、健康情報、連絡先の追跡などの個人情報、およびその他の機密データを、それらの情報の表示を意図していないユーザーに向けて投稿してはいけません。

ユーザーのマシンや環境にファイルや実行ファイル (.exe) をダウンロードする場合は、その前にユーザーに警告しなければなりません。

## <a name="general-functionality-and-performance"></a>一般的な機能とパフォーマンス

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4](/legal/marketplace/certification-policies#11404-functionality) に沿ったものです。

### <a name="launching-external-functionality"></a>外部機能の起動

[*必須の修正プログラム*]

アプリの主要なユーザー シナリオにおいて、ユーザーがTeams から離れることがあってはなりません。  アプリ内のコンテンツの表示やユーザーとのやり取りは、ボット、アダプティブ カード、タブ、タスク モジュールなど、Teams の機能の範囲内で実行される必要があります。
<br></br>
<details><summary>詳細を知るために展開する</summary>

ユーザーがTeams の範囲内に留まり、外部のサイトやアプリにリンクを介して移動しないようにします。 外部の機能を利用する必要があるシナリオの場合は、その機能の利用を開始する許可をユーザーから明示的に得る必要があります。

外部の機能を開始するボタンの名前は、その操作によりユーザーが Teams から離れることが明確にわかるようなものである必要があります。 たとえば、「**Contoso.com への移動はこちら**」や「**Contoso.com で表示**」といった例が考えられます。

</details>

### <a name="compatibility"></a>互換性

[*必須の修正*]

アプリは、以下のオペレーティング システムやブラウザーの最新バージョンで完全に機能する必要があります。

* Microsoft Windows
* macOS
* Microsoft&nbsp;Edge
* Google Chrome
* iOS
* Android

アプリは、サポートされていないブラウザーやオペレーティング システムに関しては、穏当な表現でエラー メッセージを表示する必要があります。

### <a name="response-time"></a>応答時間

[*必須の修正*]

Teams アプリは、合理的な時間内に応答するか、読み込み中や入力中のインジケーター、メッセージ、または警告を表示する必要があります。

* タブは、2 秒以内に反応するか、読み込みメッセージや警告を表示する必要があります。
* ボットは、ユーザーのコマンドに対して 2 秒以内に応答するか、入力インジケーターを表示する必要があります。
* メッセージ拡張機能は、ユーザーのコマンドに対して 2 秒以内に応答する必要があります。
* 通知は、ユーザーのアクションから 2 秒以内に表示される必要があります。

## <a name="app-package-and-store-listing"></a>アプリ パッケージと Store 登録情報

[*必須の修正プログラム*]

アプリケーション パッケージは、正しく書式設定され、すべての必要な情報とコンポーネントが含まれている必要があります。

> [!TIP]  
> 公開されたアプリを検証するために、次のようなテスト手順が明記されている必要があります。
>
> * アプリが外部アカウントに依存する認証を使用している場合は、 **テスト アカウントを構成する手順** を明記する。
> * Teams 内で実行されるコア ワークフローにおける **期待されるアプリの動作** について概略を記述する。
> * アプリの詳細な説明や関連資料に記載されている機能、特徴、成果物に関する制限、条件、例外について **明確に説明する**。
> * アプリを検証するテスターが考慮すべき **あらゆる考慮事項を強調する**。  
> * テストを支援するために、**テスト アカウントにダミー データを事前に設定する**。

### <a name="app-manifest"></a>アプリ マニフェスト

[*必須の修正*]

Teams アプリ マニフェストは、アプリの構成を定義します。

* マニフェストは、一般公開されたマニフェスト スキーマに適合している必要があります。 詳細については、「[マニフェストのリファレンス](~/resources/schema/manifest-schema.md)」を参照してください。 マニフェストのプレビュー バージョンを使用してアプリを申請しないでください。
* アプリにボットやメッセージ拡張機能が含まれている場合、アプリ マニフェストの詳細は、ボット名、ロゴ、プライバシー ポリシーのリンク、サービス使用条件のリンクなど、Bot Framework のメタデータと一致している必要があります。
* アプリが Azure Active Directory を認証に使用する場合は、マニフェストに Microsoft Azure Active Directory (Azure AD) アプリケーション (クライアント) ID を含めます。 詳細については、「[マニフェストのリファレンス](~/resources/schema/manifest-schema.md#webapplicationinfo)」を参照してください。

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

アプリの簡潔な説明と詳しい説明が備わっている必要があります。 アプリ構成とパートナー センターでの説明が同じである必要があります。
<br></br>
<details><summary>詳細を知るために展開する</summary>

アプリについての説明は、直接的にも間接的にも、他のブランド (Microsoft が所有するブランドか否かにかかわらず) を傷つけるものであってはいけません。  説明に根拠のない主張が含まれていないことを確認してください。 たとえば、「**効率が 200% 向上することを保証します**」という記述は不適切です。

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
* 説明が、Teams アプリ内で利用可能な機能と一致している。 Teams アプリ外でのワークフローについての言及は限定的なものに留められ、かつ記述される場合も Teams アプリの機能と明確に区別して記述されている必要がある。
* ヘルプやサポートへのリンクを含める。
* **Office 365** ではなく **Microsoft 365** と表記する。
* **Teams** を表記する場合は、初出の表記を **Microsoft Teams** とし、その後の表記をTeams という短縮表記とすることができる。 後の参照は、**Teams** と短縮することができます。
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
* アプリが Microsoft の提供物であるかのように記述する。たとえば、Microsoft のスローガンやタグラインを使用する。
* 自分が所有していない著作権で保護されたブランド名を使用する。
* Microsoft の認定パートナーでないにもかかわらず、以下のような表現を使用する。
  * **... は ... の認定〇〇です**
  * **... は ... を装備しています**
* 入力ミス、文法エラーが含まれている。
* 必要性がない場合にもかかわらず、マニフェストや AppSource の「詳細な説明」の全体、またはアプリのコンテンツの全体をキャピタライズする (英語の場合)。
* AppSource へのリンクを含める。
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

* アプリの機能 (ユーザーとボットのコミュニケーションの内容など) に重点を置く。
* アプリを正確に表現するコンテンツを含めます。
* 賢明な表現を使用する。
* スクリーンショットには、ブランドを反映する色で縁取りを加え、マーケティング コンテンツを含める。

**してはいけないこと**:

[*修正の提案*]

* スマートフォンやノート PC など、特定のデバイスを表示する。
* Teams やブラウザの UI をキャプチャしたものをスクリーンショットの一部として含める。
* Teams 外でアプリが使用されている場面など、アプリの実際の UI を正確に反映していないモックアップを含める。

> [!TIP]  
> アプリを使用する理由を伝えるには、ビデオが最も効果的です。 ビデオは、ユーザーがリストで最初に見るものでもあります。 詳細については、「[ストアのリスト広告向けビデオを作成する](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)」を参照してください。

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

[*必須の修正*]

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

アプリがローカリゼーションを提供する場合、アプリ パッケージには、Teams の言語設定に基づいて表示される言語の翻訳ファイルを含める必要があります。 ファイルは、Teams のローカリゼーション スキーマに準拠している必要があります。 詳細については、「[Teams のローカリゼーション スキーマ](~/concepts/build-and-test/apps-localization.md)」を参照してください。

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
* FAQ、ナレッジベース、電子メール アドレスなど、さまざまな方法で問題のサポートに取り組む方法を提供します。
* ユーザーを検証して、他のユーザー経由でライセンスが割り当てられていないか確認します。
* ライセンスの割り当て後にユーザーに通知します。
* アプリを Teams に追加して使い始める方法を、Teams チャット ボットやメール経由でユーザーに案内します。

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

テスト目的でのアプリのセットアップが複雑な場合は、エンドツーエンドの機能ドキュメント、関連付けられた SaaS の構成手順、ライセンスとユーザー管理の手順を「構成用メモ」の一部として提供します。

> [!TIP]  
> アプリやライセンス管理の仕組みを説明したビデオを追加して、チームのテストをサポートすることができます。

</details>

## <a name="tabs"></a>タブ

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.2](/legal/marketplace/certification-policies#114042-tabs) に沿ったものです。
アプリにタブが含まれている場合は、以下のガイドラインに従っていることを確認してください。
> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams タブ デザインのガイドライン](~/tabs/design/tabs.md)」を参照してください。

</br>
<details><summary>セットアップ</summary>

* タブのセットアップでは、新規ユーザーを **待たせてはいけません**。 アクションやワークフローを完了するためのメッセージを提供します。 [*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-create-new-account.png" alt-text="validation-tabs-setup-create-new-acc":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-missing-forward-guidance.png" alt-text="validation-tabs-missing-fwd-guidance":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-new-user.png" alt-text="validation-tabs-set-up-new-user":::

* 最初の実行エクスペリエンスを最適なものにするには、タブの設定後ではなくセットアップ中に、ユーザーの認証を行う必要があります。 認証は、タブ構成ウィンドウの外側で行うことができます。 [*修正の提案*]

* ユーザーは、Teams 内のタブ構成機能を離れて Teams の外でコンテンツを作成してから、Teams に戻ってピン留めしてはいけません。 タブ構成画面の範囲内で、構成の値と方法が説明される必要があります。 [*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-profile-name.png" alt-text="validation-tabs-set-up-profile-name":::

* Web サイトの全体が埋め込まれたようなタブ構成画面は禁止です。 タブ構成のエクスペリエンスは、十分に焦点が絞られたものでなければなりません。たとえば、ユーザーがプロジェクトをチャネル内で構成できる「プロジェクト管理アプリ」の場合、タブ構成画面では、ユーザーがアプリからプロジェクトを選択し、そのプロジェクトをチャネル内で構成していくプロセスに焦点が絞られなければなりません。[*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-experience.png" alt-text="validation-tabs-setup-configuration-exp":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-screen.png" alt-text="validation-tabs-set-up-configuration-screen":::

* タブ構成画面では、ユーザーに URL の埋め込みを依頼してはいけません。 タブ構成のタイミングで、タブ構成画面からいったん離れてURL を取得し、もう一度戻って URL を入力することをユーザーに求める UX は、好ましいものではありません。 Teamsには、チャネル内に Web サイトへのリンクをピン留めする同様の機能がすでに存在しています。 したがって、タブ構成のタイミングでユーザーに Web サイトの URL を埋め込むよう求め、チャネル タブには Web サイトの全体が表示されるだけという限定的な使用方法が採用されている場合、アプリはユーザーに十分な価値を提供しているとは言えません。 [*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configured-url.png" alt-text="validation-tabs-set-up-configured-url":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configured-url-two.png" alt-text="validation-tabs-set-up-configured-url-two":::

</details>
</br>

<details><summary>ビュー</summary>

* サインイン画面領域では、大きなロゴを使用してはいけません。[*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-applogin.png" alt-text="validation-views-app-login":::

* 複数のタブに分割して表示することで、コンテンツはシンプルになります。 [*修正の提案*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-multiple-tabs.png" alt-text="val-views-multiple-tabs":::

* タブのヘッダーに重複がないようにしてください。タブのフレームワークにはアプリ アイコンとアプリ名が表示されるため、IFRAME​​ から重複するロゴを削除する必要があります。[*修正の提案*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-duplicate-header-logo.png" alt-text="validation-views-duplicate-head-logo":::

</details>
</br>

<details><summary>ナビゲーション</summary>

ナビゲーションに関するガイドラインは次のとおりです。

* タブは、Teams の主要なナビゲーションと競合するようなナビゲーションを設定してはなりません。 タブに左ナビゲーションを指定する場合は、アイコンのみやテキストが上下に並べて表示されたアイコンを含めてはいけません。 これは、テキストが上下に並べて表示されたアイコン (Teams のナビゲーション バーを模倣したもの) を表示するオプションを持つ折りたたみ可能なレールであってはいけません。 インライン テキストやテキストのみを持つアイコンを含めるか、タブ左レールの代わりにハンバーガー メニューを使用します。 [*必須の修正プログラム*]

Fluent UI コンポーネントの [Basic](~/concepts/design/design-teams-app-basic-ui-components.md) と [Advanced](~\concepts\design\design-teams-app-advanced-ui-components.md) を使用してアプリをデザインしてください。

:::image type="content" source="../../../../assets/images/submission/validation-navigation-static-tab.png" alt-text="validation-nav-static-tab":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-horizontal-rail.png" alt-text="validation-nav-horizontal-rail":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-left-navigation.png" alt-text="validation-navigation-left-nav":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-icon-text.png" alt-text="validation-nav-icon-text":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-collapsable-left-rail.png" alt-text="validation-nav-collapsable-left-rail":::

* 左レールにツールバーがあるタブは、Teams の左ナビゲーションから 20px の間隔を空ける必要があります。 [*必須の修正プログラム*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-spacing-between-toolbar.png" alt-text="validation-nav-spacing-between-toolbar":::

* パンくずや左ナビゲーションを辿ることにより、メインのタブ領域のレベル 2 (L2)、レベル 3 (L3) のビューに、第2、第3のタブが表示される必要があります。また、タブ ナビゲーションをサポートするために、以下のコンポーネントを含めることができます: [*必須の修正*]
  * 戻るボタン
  * ページ ヘッダー
  * ハンバーガー メニュー
* タブの横スクロールは禁止です。ただし、 ホワイトボード アプリなど、ユーザーがアプリの操作感を損なうことなく共同作業を行うために大きなキャンバスを必要とするアプリでは、ビジネス上の必要性に応じて横スクロールを使用できます。[*修正の提案*]

* タブ内のディープ リンクは、外部の Web ページではなく、Teams 内の機能 (タスク モジュール、他のタブなど) にリンクされている必要があります。[*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-view-button-not-linked-static-tab.png" alt-text="validation-nav-view-button-not-linked-static-tab":::

* アプリのコア エクスペリエンスに対しては、タブから Teams 外部に移動することが可能であってはいけません。 一方、コア エクスペリエンス以外のワークフローに対しては、タブから Teams の外部にリダイレクトさせることができます。 たとえば、サポート チケットを発生する場合などです。 [*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-within-configuration.png" alt-text="validation-nav-core-workflow-within-configuration":::

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-redirects-outside.png" alt-text="validation-nav-core-workflow-redirects-outside":::

</details>
</br>

<details><summary>ユーザビリティ</summary>

* タブは、既存の Web サイトをホストする以上の価値を提供するものである必要があります。 [*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-provides-workflows.png" alt-text="validation-usability-app-provides-work-flow":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-website-i-framed.png" alt-text="validation-usability-website-i-frame":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-teams-app-identical-website.png" alt-text="validation-usability-teams-app-identical-websites":::

* タブ内でコンテンツを切り捨てたり、オーバーラップしたりしてはいけません。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-content-truncation.png" alt-text="validation-usability-content-truncations":::

* ユーザーがタブで最後に行った操作を取り消すことができるようにする必要があります。

* 個人用コンテキストのタブには、アプリの共有インスタンスからのコンテンツを集約して表示させる場合があります。 たとえば、かんばんカードを使用してプロジェクトにコメントを付加する機能を提供する、構成可能タブを含んだ「プロジェクト管理アプリ」の場合、集約されたコンテンツを個人用アプリに表示させる必要があります。 [*修正の提案*]

* タブは Teams テーマに対応するものである必要があります。 ユーザーがテーマを変更すると、アプリのテーマにもその選択が反映される必要があります。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-responsive-tabs.png" alt-text="validation-usability-responsive-tab":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-unresponsive-tabs.png" alt-text="validation-usability-unresponsive-tab":::

* タブには、Teams フォント、入力ランプ、カラー パレット、グリッド システム、モーション、声のトーンなど、Teams スタイルのコンポーネントを可能な限り使用する必要があります。詳細については、「[タブ デザイン ガイドライン](/microsoftteams/platform/tabs/design/tabs)」を参照してください。[*修正の提案*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-uses-diff-font.png" alt-text="validation-usability-app-uses-font":::

* 設定を変更する必要があるアプリの機能が存在する場合は、**[設定]** タブを用意します。[*おすすめの修正プログラム*]
* タブは、ページ内ナビゲーション、ダイアログの配置や使用方法、情報階層など、Teams の対話型デザインに沿ったものである必要があります。詳細については、「[Microsoft Teams Fluent UI キット](~/concepts/design/design-teams-app-basic-ui-components.md)」を参照してください。

* IFRAME 内のタブ コンテンツは、Teams のコア機能を模倣した機能を含んではなりません。 たとえば、ボット、メッセージの拡張機能、通話、会議などです。

* 構成可能タブのランディング ページのコンテンツは、コンテキストごとに、すべてのチャネル メンバーに対して同じでなければいけません。

* 構成可能なタブのランディング ページ内のコンテンツは、個人の使用を対象にしてはならず、**マイ タスク** や **マイ ダッシュボード** などの個人用コンテンツを含んではいけません。

* 作業効率や職場の生産性向上のために、アプリ内で個人スコープのビューを提供するには、個人向けアプリへのディープ リンクを使用して表示を絞り込むか、または構成可能タブ内の L2 ないしは L3 のビューに移動します。その際、ランディング ページはコンテキストごとに、すべてのユーザーに対して同じ状態に保ちます。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-tab-personal-info.png" alt-text="validation-usability-configurable-tab-pers-info":::

* 構成可能タブの機能は、十分に絞り込まれたものでなければなりません。

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-nested-tabs.png" alt-text="validation-usability-configurable-nested-tab":::

* タブ エクスペリエンスは、モバイル (Android と iOS) で完全にレスポンシブでなければなりません。

> [!TIP]
>
> * 個人用タブと一緒に個人用ボットを設定します。
> * ユーザーが自分の個人用タブからコンテンツを共有できるようにします。

</details>

## <a name="bots"></a>ボット

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.3](/legal/marketplace/certification-policies#114043-bots) に沿ったものです。

アプリにボットが含まれている場合は、以下のガイドラインに従っていることを確認してください。

> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams ボット デザインのガイドライン](~/bots/design/bots.md)」を参照してください。

</br>
<details><summary>ボット コマンド</summary>

ユーザーによる入力の分析からその意図を推定することは容易ではありません。 そのため、ボット コマンドでは、ボットが理解できる単語や語句の集合があらかじめユーザーに提供されます。

* サポートされているボット コマンドをアプリ構成に一覧表示することを強く推奨します。 これらのコマンドは、ユーザーがボットにメッセージを送信しようとする際に、作成ボックスに表示されます。

    :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-listed.png" alt-text="validation-bot-commands-list":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-not-listed.png" alt-text="validation-bot-commands-not-list":::

* **Hi**、**Hello**、**Help** などの汎用的なコマンドを含め、ボットがサポートするすべてのコマンドが正しく動作する必要があります。

    :::image type="content" source="../../../../assets/images/submission/validation-bot-help-command.png" alt-text="validation-bots-help-command":::

* ボット コマンドは、ユーザーのワークフローを妨げるものではなく、常に前に進める方法を提供するものでなければいけません。

    :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-deadend.png" alt-text="validation-bot-commands-dead-end":::

> [!TIP]
> 個人用ボットの場合は、**[ヘルプ]** タブを設けて、ボットにより可能となる機能について詳しく説明します。

</details>
</br>

<details><summary>ボットのウェルカム メッセージ</summary>

* アプリの構成フローが複雑である場合 (エンタープライズ ライセンスが必須である、直感的なサインアップ フローが提供されていない、などの場合)、アプリのボットは初回実行時に必ず、ウェルカム メッセージを送信する必要があります。

最適なエクスペリエンスを得るために、ウェルカム メッセージには、ボットがユーザーに提供する価値、チャネルにボットをインストールしたユーザー、ボットを構成する方法、およびサポートされているすべてのボット コマンドの簡単な説明が含まれる必要があります。 ボタン付きのアダプティブ カードを使用してウェルカム メッセージを表示すると、より使いやすくなります。 詳細については、「[ボットのウェルカム メッセージをトリガーする方法](~/bots/how-to/conversations/send-proactive-messages.md)」を参照してください。 アプリの構成フローが複雑でない場合、ボットの初回実行時にウェルカム メッセージを表示させることは選択になります。 ただし、ウェルカム メッセージを表示させる場合は、ウェルカム メッセージのガイドラインに従う必要があります。

:::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message.png" alt-text="validation-bot-welcom-message":::

:::image type="content" source="../../../../assets/images/submission/validation-bot-no-welcome-message.png" alt-text="validation-bot-no-wel-come-message":::

* チャネルやチャットでのボットのウェルカム メッセージは、初回実行時には省略可能であり、特にボットが個人用に利用でき、同様のアクションを実行する場合は省略できます。 ボットはユーザーに個別にウェルカム メッセージを送信してはいけません ([スパム](#botmessagespamming)と見なされます)。 メッセージには、ボットを追加したユーザーもメンションしなければなりません。

    :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-not-triggered.png" alt-text="validation-bot-welcome-message-not-trigger":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-triggered.png" alt-text="validation-bot-wel-message-trigger":::

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
  * 短時間のうちに複数のメッセージを送信しないでください。
  * 情報が完結した 1 件のメッセージを送信してください。
  * 単一のワークフローの反復を複数の会話にまたがって実行することは避けてください。
  * フォーム (またはタスク モジュール) を使用して、ユーザーのすべての入力を一度に収集します。
  * 自然言語処理 (NLP) ベースの会話型チャットボットを利用すれば、マルチターンの会話により話し合いの進行が促進され、ワークフローを完了させることができます。

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-task-module.png" alt-text="validation-bot-message-using-task-module":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-mutliple-conversation.png" alt-text="validation-bot-messages-using-mutliple-conversations":::

* **ウェルカム メッセージ**: 一定の間隔で同じウェルカム メッセージを繰り返してはいけません。 たとえば、チームに新しいメンバーが加わったとき、他のメンバーにウェルカム メッセージを送ることは、スパム行為とみなされます。 新しいメンバーへのメッセージは個人的に送信してください。

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

「**新しい通知があります。クリックして表示してください**」という通知が提供されるだけで、ユーザーが Teams から離れなければそれ以外の機能が利用できない場合、Teams アプリにより十分な価値が提供されているとは言えません。

:::image type="content" source="../../../../assets/images/submission/validation-navigation-static-tab.png" alt-text="validation-nav-static-tab":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-horizontal-rail.png" alt-text="validation-nav-horizontal-rail":::

:::image type="content" source="../../../../assets/images/submission/validation-bot-notification-only-inadequete-info.png" alt-text="validation-bot-notifications-only-inadequete-info":::

> [!TIP]
> 投稿されたカード内に表示される情報を見直し、ユーザーが選択できる基本的なアクションのすべてが、Teams から離れることなく利用できるような形で提供されていることを確認してください (適用される機能の複雑さに関わらず)。

</details>

## <a name="message-extensions"></a>メッセージの拡張機能

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.4](/legal/marketplace/certification-policies#114044-messaging-extensions) に沿ったものです。

アプリにメッセージ拡張機能が含まれている場合は、以下のガイドラインに従っていることを確認してください。

> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams メッセージ拡張機能デザインのガイドライン](~/messaging-extensions/design/messaging-extension-design.md)」を参照してください。

</br>
<details><summary>操作コマンド</summary>

操作ベースのメッセージ拡張機能では、以下のことを行う必要があります。

* ユーザーがサインインなどの中間的な手順を行うことなく、メッセージに対するアクションを起こせるようにする。

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-no-intermediate-step.png" alt-text="validation-messaging-extension-no-intermediate-steps":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-intermediate-step-available.png" alt-text="validation-messaging-extension-intermediate-steps-available":::

* メッセージ コンテキストを次の作業状態に渡す。 [*必須の修正プログラム*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-passes-message.png" alt-text="validation-messaging-extension-app-passes-messages":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-doesnot-pass-message.png" alt-text="validation-messaging-extension-app-doesnot-pass-messages":::

* アプリ内のチャット メッセージ、チャネルへの投稿、アクションの呼び出しによってトリガーされるアクション コマンドの名前には、一般動詞による表記だけではなく、ホスト アプリの名前も含めます。 たとえば、**[会議を開始]** ではなく **[Skype 会議を開始]**、**[ファイルをアップロード]** ではなく **[DocuSign にファイルをアップロード]** とします。 [*修正の提案*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-host-name.png" alt-text="validation-messaging-extension-action-command-host-names":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-verb.png" alt-text="validation-messaging-extension-action-commands-verb":::

</details>
</br>

<details><summary>プレビュー リンク (リンク展開)</summary>

[*必須の修正*]

メッセージ拡張機能では、認識されたリンクが Teams の作成ボックスでプレビューされます。  制御外のドメイン (絶対 URL、ワイルドカードのいずれについても) を追加してはいけません。  たとえば、`yourapp.onmicrosoft.com` は有効ですが、`*.onmicrosoft.com` は無効です。 トップレベルの ドメインも禁止です。 たとえば、`*.com` および `*.org` が禁止となります。 [*必須の修正*]

</details>
</br>

<details><summary>検索コマンド</summary>

* 検索ベースのメッセージ拡張機能では、ユーザーが効果的に検索できるようなテキストが用意されている必要があります。 [*必須の修正*]

    :::image type="content" source="../../../../assets/images/submission/validation-search-commands-text-available.png" alt-text="validation-search-command-text-available":::

* @メンション実行可能ファイルは、明確で、理解しやすく、読みやすいものである必要があります。

    :::image type="content" source="../../../../assets/images/submission/validation-search-command-unclear-executable.png" alt-text="validation-search-commands-unclear-executable":::

</details>
</br>

<details><summary>操作コマンド</summary>検索ベースのメッセージ拡張機能専用アプリ

[*必須の修正*]

検索ベースのメッセージ拡張機能により構成されるアプリは、コンテキストの切り替えなしでコンテキストに沿った会話が可能なカードを共有することで、ユーザーに価値を提供します。

検索ベースのメッセージ拡張機能専用アプリの検証に合格するには、ユーザー エクスペリエンスが壊れないようにするためのベースラインとして、以下の項目が必要です。 メッセージ拡張機能を介して共有されるカードは、次の場合に Teams に価値を提供します。

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
<details><summary>全般</summary>

ミーティング拡張機能には、次のガイドラインを使用します。

* ミーティング拡張アプリは、レスポンシブ対応の会議中エクスペリエンスを提供し、かつ Teams の会議エクスペリエンスと連携して動作する必要があります。 会議中エクスペリエンスは必須ですが、会議前および会議後エクスペリエンスは必須ではありません。

  * 会議前のエクスペリエンスにおいてユーザーは、検索して見つかった会議アプリを追加できます。 またユーザーは、会議前のタスク (会議の参加者に対してアンケートを実施する機能など) を利用することもできます。 アプリが会議前のエクスペリエンスを提供する場合は、会議のワークフローに関連するものでなければなりません。

  * 会議後のアプリ エクスペリエンスでは、ユーザーは、投票されたアンケート結果、フィードバック、その他のアプリ コンテンツなど、会議の結果を表示できます。 アプリが会議後のエクスペリエンスを提供する場合は、会議のワークフローに関連するものでなければなりません。

  * 会議中のアプリ エクスペリエンスでは、会議中に会議参加者を積極的に関与させ、すべての出席者の会議エクスペリエンスを強化できます。 アプリのコア ユーザー ワークフローを完了させるために、出席者が Teams 会議の外部に移動するようにしてはいけません。

* アプリによって、Teams のカスタムの Together Mode シーン以上の価値が提供されなければなりません。

* Shared meeting stage 機能は、Teams のデスクトップ アプリからのみ起動できます。  ただし、Shared meeting stage の使用エクスペリエンスは、モバイル デバイスで表示する場合にも問題なく使用可能である必要があります。

> [!TIP]
> Teams モバイルで会議用アプリを有効にするには、マニフェストにおいて、`groupchat` を `configurableTabs` と `meetingDetailsTab` のスコープとして宣言するか、`meetingChatTab` と `meetingSidePanel` をコンテキスト プロパティとして宣言する必要があります。

</details>

</br>
<details><summary>会議前後のエクスペリエンス</summary>

* 会議前後の画面は、一般的なタブ デザイン ガイドラインに準拠している必要があります。 詳細については、「[Teams デザイン ガイドライン](~/tabs/design/tabs.md)」を参照してください。
* タブは横スクロールしてはいけません。
* 複数の項目を表示する場合に、タブのレイアウトが整理されている必要があります。 たとえば、10 件を超える投票またはアンケートについては、「[レイアウトの例](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting)」を参照してください。
* アプリでアンケートや投票の結果がエクスポートされた場合に、「**結果が正常にダウンロードされました**」と表示してユーザーに通知する必要があります。

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

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button.png" alt-text="validation-in-meeting-exp-back-buttons":::

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button-absent.png" alt-text="validation-in-meeting-exp-back-buttons-absent":::

* 閉じるボタンが複数あってはいけません。 タブを閉じるためのヘッダー ボタンがすでに埋め込まれているため、ユーザーを混乱させるかもしれません。
* 横スクロールさせてはいけません。

</details>

</br>
<details><summary>会議中のダイアログ</summary>

* 頻繁に使用してはなければなりません。簡素でかつタスク指向性のあるシナリオに対してのみ使用してください。
* コンテンツは 1 列に表示されていなければなりません。また、複数のナビゲーション レベルがあってはなりません。
* タスク モジュールを使用してはいけません。
* 会議ステージの中心に位置合わせする必要があります。

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-dialog-not-aligned.png" alt-text="validation-in-meeting-dialog-not-align":::

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

アプリで [Microsoft Graph が提供するアクティビティ フィード API](/graph/teams-send-activityfeednotifications) を使用する場合は、以下のガイドラインを遵守してください。
<br></br>
<details><summary>全般</summary>

* アプリ構成で指定されたすべての通知トリガーが動作する必要があります。
* 通知は、アプリにおいて構成されているすべての言語についてローカライズされていなければなりません。
* 通知は、ユーザーのアクションから 5 秒以内に表示される必要があります。

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

    :::image type="content" source="../../../../assets/images/submission/validation-365-compliance-publisher-verification.png" alt-text="validation-365-compliance-publisher-verifications":::

* **発行元の構成証明**: 潜在的な顧客がアプリの使用を適切な情報に基づいて判断できるように、一般的な情報、データの取り扱い、セキュリティとコンプライアンスに関する情報を共有するプロセス。

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: 過去に登録済みのアプリを提出する場合、そのアプリが Teams ストアに登録されるまでは、正式に発行元の構成証明を完了することができません。 登録されたことのあるアプリを更新する場合は、アプリの最新バージョンを提出する前に発行元の構成証明を完了してください。

</details>

## <a name="advertising"></a>広告

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.7](/legal/marketplace/certification-policies#11407-advertising) に沿ったものです。

アプリは、動的な広告、バナー広告、メッセージ内広告などの広告を表示してはいけません。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [パートナー センター アカウントを作成する](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)

## <a name="see-also"></a>関連項目

* [アプリを配布する](~/concepts/deploy-and-publish/apps-publish-overview.md)
* [ストア送信を準備する](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [アプリのテストおよびデバッグ](~/concepts/build-and-test/debug.md)
* [パートナー センターの開発者アカウントを作成する](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
