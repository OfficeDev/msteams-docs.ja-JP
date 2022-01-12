---
title: Microsoft Teams ストア検証ガイドライン
description: Teams ストア (AppSource) に提出されるすべてのアプリが従う必要があるガイドラインについて説明します。
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: medium
ms.openlocfilehash: 23b3f67f5f949080dc9389e82dc459a33fbf029a
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768281"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams ストア検証ガイドライン

これらのガイドラインに従うことで、アプリが Microsoft Teams ストアの送信プロセスに合格する可能性が高まります。 Teams 固有のガイドラインは、Microsoft [コマーシャル マーケットプレース認定ポリシー](/legal/marketplace/certification-policies)を補完するものであり、新機能やユーザー フィードバック、ビジネス ルールの変更を反映して頻繁に更新されています。

> [!NOTE]
> * 一部のガイドラインは、アプリに適用できない場合があります。 たとえば、アプリにボットが含まれていない場合は、ボット関連のガイドラインを無視することができます。
> * これらのガイドラインを Microsoft の商用認定ポリシーに相互参照し、検証プロセスで発生した合格または不合格のシナリオの例を示す「やるべきこと」と「やってはいけないこと」を追加しました。
> * 特定のガイドラインは、*必須の修正プログラム* としてマークされます。 アプリの申請がこれらの必須のガイドラインを満たしていない場合は、Microsoft から軽減するための手順を示すエラー レポートが送信されます。 アプリの申請は、問題を修正した場合にのみ Microsoft Teams ストアの検証に合格します。 
> * その他のガイドラインは、*おすすめの修正プログラム* としてマークされます。 理想的なユーザー エクスペリエンスを得るためには、問題を修正することをお勧めします。ただし、問題を修正しない場合でも、アプリの申請が Teams ストアでの公開をブロックされることはありません。 


## <a name="value-proposition"></a>価値提供
> [!NOTE]  
> このセクションは、[Microsoft 商用認定ポリシー番号 1140.1](/legal/marketplace/certification-policies#11401-value-proposition-and-offer-requirements) に沿ったものであり、そのオファーの価値提供に関して、Microsoft Teams アプリの開発者に追加のガイダンスを提供します。

### <a name="app-name"></a>アプリ名

[*必須の修正プログラム*]

> [!NOTE]  
> このセクションは、Microsoft [商用認定ポリシー番号 1140.1.1](/legal/marketplace/certification-policies#114011-app-name) に沿ったものであり、それらのアプリの名前の指定に関して、開発者に追加のガイダンスを提供します。

アプリの名前は、ユーザーがストアでアプリを見つける際に重要な役割を果たします。 次のガイドラインを使用してアプリの名前を指定します。

* 名前には、ユーザーに関連する用語を含める必要があります。
* 次のような Teams のコア機能の名前は、アプリ名に含めてはいけません。  
  * **チャット**
  * **連絡先**
  * **Calendar**
  * **通話**
  * **Files**
  * **アクティビティ**
  * **アプリ**
  * **ヘルプ**
* 開発者の名前を含むプレフィックスまたはサフィックスの一般名詞。 たとえば、**タスク** ではなく **Contoso タスク** がこれにあたります。
* 共同ブランド化や共同販売を誤って示す可能性のある、**Teams** やその他の Microsoft 製品名 (Excel、PowerPoint、Word、OneDrive、SharePoint、OneNote、Azure、Surface、Xbox など) を使用してはいけません。 Microsoft ソフトウェア、製品、およびサービスの参照に関する詳細については、「[Microsoft の商標およびブランドに関するガイドライン](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general)」を参照してください。
* アプリが Microsoft との公式パートナーシップのメンバーである場合、アプリの名前が最初に来る必要があります。たとえば、**Contoso Connector for Microsoft Teams** がこれにあたります。
* ストアに一覧表示されているアプリの名前や、コマーシャル マーケットプレースでのその他のサービスをコピーしてはいけません。
* 卑猥な言葉や軽蔑的な言葉を含んではいけません。 名前には、人種や文化に配慮しない言葉が含まれてはいけません。
* 一意である必要があります。 ご使用のアプリ (Contoso) が Microsoft Teams ストアと Microsoft AppSource に一覧表示されていて、Contoso Mexico のように地域に特化した別のアプリを一覧表示する場合、申請が次の条件を満たす必要があります。
  * タイトル、メタデータ、最初の応答アプリ エクスペリエンス、ヘルプ セクションでアプリの地域固有の機能を呼び出します。 たとえば、タイトルは「Contoso Mexico」でなければなりません。 アプリのタイトルは、エンド ユーザーの混乱を避けるために、既存のアプリと同じ開発者を明確に区別する必要があります。
  * パートナー センターでアプリ パッケージをアップロードする場合は、**[可用性]** セクションでアプリを利用できる適切な **マーケット** を選択します。

 > [!TIP]  
 > Microsoft Teams ストアと Microsoft AppSource でのアプリのブランド化 (アプリ名、開発者名、アプリ アイコン、Microsoft AppSource スクリーンショット、ビデオ、短い説明、Web サイトなど) は、アプリが公式の Microsoft 1P 製品ではない限り、公式の Microsoft 製品を偽装してはいけません。

### <a name="suitable-for-workplace-consumption"></a>職場での消費に適していること

[*必須の修正プログラム*]

> [!NOTE]  
> このセクションは、Microsoft 商用認定ポリシー番号 [1140.1.2](/legal/marketplace/certification-policies#114012-workplace-appropriateness)、[100.8](/legal/marketplace/certification-policies#1008-significant-value)、[100.10](/legal/marketplace/certification-policies#10010-inappropriate-content) に沿ったものであり、開発者に職場に適したアプリを構築するための追加のガイダンスを提供します。

アプリ コンテンツは、職場での一般的な消費に適したものであり、コマーシャル マーケットプレースの認証ポリシーに一覧表示されたすべての制限事項に従う必要があります。 宗教、政治、ギャンブル、長時間の娯楽などに関するコンテンツは禁止されています。

アプリは、グループのコラボレーションを可能にするもの、個人の生産性を向上させるもの、またはその両方である必要があります。 チームの結束や交流を目的としたアプリは、協力的で複数の参加者向けに設計する必要があります。 アプリは、1 回のセッションに 60 分を超える時間を必要としたり、生産性に影響を与えるものであってはいけません。

### <a name="similar-platforms-and-services"></a>類似したプラットフォームやサービス

[*必須の修正プログラム*]

> [!NOTE]  
> このセクションは、[Microsoft 商用認定ポリシー番号 1140.1.3](/legal/marketplace/certification-policies#114013-other-platforms-and-services) に沿ったものです。

アプリは Teams のエクスペリエンスに重点を置く必要があります。アプリが特定の相互運用性を提供しない限り、アプリ コンテンツやアプリのメタデータに名前、アイコン、または他の同様のチャットベースのコラボレーション プラットフォームやサービスのイメージを含めてはいけません。

### <a name="feature-names"></a>機能名

ボタンやその他の UI テキストに含まれるアプリの機能名は、Teams やその他の Microsoft 製品で使用されている用語と重複してはいけません。 たとえば、**会議を開始**、**通話する**、**チャットを開始** などです。 必要に応じて、アプリ名 (**[Contoso 会議の開始]** など) を含める必要があります。

### <a name="authentication"></a>認証

[*必須の修正プログラム*]

> [!NOTE]  
> このセクションは、Microsoft [商用認定ポリシー番号 1140.1.4](/legal/marketplace/certification-policies#114014-access-to-services) に沿ったものであり、外部サービスを使用したそれらのアプリの認証に関して、開発者にガイダンスを提供します。

アプリ認証を実装する方法の詳細については、「[Teams での認証](~/concepts/authentication/authentication.md)」を参照してください。

#### <a name="authenticating-with-external-services"></a>外部サービスを使用した認証

 アプリが外部サービスを使用してユーザーを認証する場合は、以下のガイドラインに従ってください。

* **サインイン、サインアウト、サインアップのエクスペリエンス**:
  * 外部アカウントまたはサービスに依存するアプリでは、シンプルでわかりやすいサインイン、サインアウト、およびサインアップ エクスペリエンスを提供する必要があります。
  * ユーザーがサインアウトする場合は、アプリからのみサインアウトし、Teams にはサインインしたままにする必要があります。
  * 外部アカウントやサービスに依存するアプリは、新しいユーザーがサインアップしたり、アプリ発行元に連絡してサービスの詳細を確認したり、サービスにアクセスしたりするための方法を提供する必要があります。
  転送は、アプリのマニフェスト、AppSource の詳細な説明、およびアプリの最初の実行エクスペリエンス (ボットのようこそメッセージ、タブ セットアップ、構成ページ) で使用できる必要があります。
  * テナント管理者が 1 回のセットアップを完了する必要があるアプリは、(他のテナント ユーザーがアプリをインストールして使用する前に) テナント管理者への依存関係を呼び出してアプリを構成する必要があります。  
  依存関係は、アプリのマニフェスト、AppSource の詳細な説明、すべての最初の実行エクスペリエンス タッチポイント (ボットのようこそメッセージ、タブ セットアップ、構成ページ)、ボット応答、拡張機能の作成、静的なタブ コンテンツの一部として必要と見なされるヘルプ テキストで呼び出す必要があります。
  
* **コンテンツ共有エクスペリエンス**: Teams チャネルでコンテンツを共有するために外部サービスを使用した認証を必要とするアプリは、外部サービスでその機能がサポートされている場合、コンテンツを切断または共有解除する方法をヘルプ ドキュメント (または同様のリソース) で明示する必要があります。 これは、コンテンツの共有を解除する機能が、Teams アプリに存在する必要があるということではありません。

## <a name="security"></a>セキュリティ
> [!NOTE]  
> このセクションは、[Microsoft 商用認定ポリシー番号 1140.3](/legal/marketplace/certification-policies#11403-security) と一致します。

### <a name="financial-information"></a>財務情報

[*必須の修正プログラム*]

> [!NOTE]  
> このセクションは [Microsoft 商用認定ポリシー番号 1140.3.1](/legal/marketplace/certification-policies#114031-financial-transactions) に沿ったもので、Teams インターフェイス内の財務情報の送信に関するガイダンスを提供し、Teams アプリのモバイル (Android および iOS) バージョンでの制限付き支払いシナリオを開発者に通知します。

アプリは、ユーザーに対して、Teams インターフェイス内で支払いを求めたり、ボット インターフェイスを介してユーザーに財務情報を送信したりしてはいけません。  
   


:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![[アプリ内決済]](~/assets/images/submission/validation-financial-information-1.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

ユーザーがアプリの使用に同意する前に、使用条件、プライバシー ポリシー、プロファイル ページ、Web サイトなどで開示を行った場合に限り、安全な外部決済サービスにリンクすることができます。

[一般ポリシー番号 100.10 の不適切なコンテンツ](/legal/marketplace/certification-policies#10010-inappropriate-content)で禁止されている商品やサービスについて、アプリ経由での決済を促進しないでください。

iOS 版または Android 版 Teams で実行するアプリは、以下のガイドラインを遵守する必要があります。

* アプリは、アプリ内購入、試用版の提供、有料版へのアップセルを目的とする UI、またはユーザーが他のコンテンツ、アプリ、アドインを購入するオンライン ストアを含めてはいけません。   
    
:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![アプリ内購入](~/assets/images/submission/validation-financial-information-in-app-purchase.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![オンライン ストア](~/assets/images/submission/validation-financial-information-online-stores.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 

* アプリでアカウントが必要な場合、ユーザーは無料でアカウントにサインアップできます。 **無料版** または **無料アカウント** という用語の使用は禁止されています。
* アカウントを無期限にアクティブにするか、期間限定にするかを決めることができます。 アカウントの有効期限が切れると、アプリに支払いが必要であることを示す UI、テキスト、またはリンクを表示することはできません。
* アプリのプライバシー ポリシーと使用条件には、商用の UI またはストアへのリンクがないことが必要です。

### <a name="bots"></a>ボット

[*必須の修正プログラム*]

> [!NOTE]
> このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.3.2](/legal/marketplace/certification-policies#114032-bots-and-messaging-extension) に沿ったものです。

Microsoft Azure Bot Service を使用するアプリ (ボットやメッセージング拡張機能など) の場合、Microsoft [オンライン サービスの使用条件](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)で定義されているすべての要件に従う必要があります。

ボットは、ファイルをアップロードする場合に必ずアクセス許可を依頼し、確認メッセージを表示する必要があります。
    
:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![確認メッセージ](~/assets/images/submission/validation-bot-confirmation-message.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 


### <a name="external-domains"></a>外部ドメイン

[*必須の修正プログラム*]

> [!NOTE]
> このセクションは、[Microsoft 商用マーケットプレース ポリシー番号 1140.3.3](/legal/marketplace/certification-policies#114033-external-domains) に沿ったもので、`validDomains` マニフェスト プロパティでの制限付きドメインの使用に関する開発者向けのガイダンスを提供します。

組織の制御外のドメイン (ワイルドカードなど) やトンネリング サービスをアプリのドメイン構成に含めてはいけません。 例外は次のとおりです。

  * アプリが Azure Bot Service の OAuthCard を使用している場合、有効なドメインとして `token.botframework.com` を含める必要があり、そうしないと **[サインイン]** ボタンが機能しません。
  * アプリが SharePoint に依存している場合は、`{teamSiteDomain}` コンテキスト プロパティを使用して、関連するルート SharePoint サイトを有効なドメインとして含めることができます。

#### <a name="government-community-cloud-listings"></a>Government Community Cloud の一覧表示

Government Community Cloud (GCC) ユーザーにアプリを配布するには、Teams ストアに重複して表示しないようにする一方で、認証プロセスでユーザーを特定し、GCC 固有の URL または予想される URL にルーティングする必要があります。

### <a name="sensitive-content"></a>機密コンテンツ

[*必須の修正プログラム*]

ご使用のアプリは、クレジット カード、金融機関の支払い明細、健康状態、連絡先の追跡、その他個人を特定できる情報 (PII) などの機密データを、コンテンツの表示を意図していない対象ユーザーに投稿してはいけません。

ユーザーのマシンや環境にファイルや実行ファイル (.exe) をダウンロードする前に、ユーザーに警告しなければなりません。

## <a name="general-functionality-and-performance"></a>一般的な機能とパフォーマンス

> [!NOTE]
> このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4](/legal/marketplace/certification-policies#11404-functionality) に沿ったものです。

### <a name="launching-external-functionality"></a>外部機能の起動

[*必須の修正プログラム*]

アプリは、コアなユーザー シナリオのためにユーザーを Teams から除外するものであってはいけません。 アプリ コンテンツや対話型操作は、ボット、アダプティブ カード、タブ、タスク モジュールなど、Teams 機能の中で発生する必要があります。

ユーザーを外部のサイトやアプリではなく、Teams 内のユーザーにリンクさせます。 外部機能を必要とするシナリオでは、アプリはその機能を起動するための明示的なユーザー権限を得ることが必要です。

外部機能を起動するボタン UI テキストには、ユーザーが Teams インスタンスから外されることを示すコンテンツを含める必要があります。 たとえば、「**Contoso.com へのこの方法**」や「**Contoso.com での表示**」などのテキストを含めます。

### <a name="compatibility"></a>互換性

[*必須の修正プログラム*]

アプリは、以下のオペレーティング システムやブラウザーの最新バージョンで完全に機能する必要があります。

* Microsoft Windows
* macOS
* Microsoft Edge
* Google Chrome
* iOS
* Android

アプリは、サポートされていないブラウザーやオペレーティング システムで滑らかなエラー メッセージを表示する必要があります。

### <a name="response-time"></a>応答時間

[*必須の修正プログラム*]

Teams アプリは、合理的な時間内に応答するか、読み込み中や入力中のインジケーター、メッセージ、または警告を表示する必要があります。

* タブは、2 秒以内に反応するか、読み込みメッセージや警告を表示する必要があります。
* ボットは、ユーザーのコマンドに対して 2 秒以内に応答するか、入力インジケーターを表示する必要があります。
* メッセージング拡張機能は、ユーザーのコマンドに対して 2 秒以内に応答する必要があります。
* 通知は、ユーザーのアクションから 2 秒以内に表示される必要があります。

## <a name="app-package-and-store-listing"></a>アプリ パッケージと Store 登録情報

[*必須の修正プログラム*]

アプリケーション パッケージは、正しく書式設定され、すべての必要な情報とコンポーネントが含まれている必要があります。

> [!TIP]  
> アプリの申請を検証するには、次の詳細なテスト手順を含める必要があります。
> * アプリが認証用の外部アカウントに依存する場合に **アプリのテスト アカウントを構成する手順**。
> * Teams 内のコア ワークフローに **期待されるアプリの動作** の概要。
> * アプリの詳細な説明や関連資料に記載されている機能、特徴、成果物などに対する制限、条件、例外を **明確に説明する**。
> * アプリの申請を検証する際に、テスターに関する **考慮事項を強調します**。  
> * テストを支援するために、**テスト アカウントにダミー データを事前に設定します**。

### <a name="app-manifest"></a>アプリ マニフェスト

[*必須の修正プログラム*]

Teams アプリ マニフェストは、アプリの構成を定義します。

* マニフェストは、一般公開されたマニフェスト スキーマに適合している必要があります。 詳細については、「[マニフェストのリファレンス](~/resources/schema/manifest-schema.md)」を参照してください。 マニフェストのプレビュー バージョンを使用してアプリを申請しないでください。
* アプリにボットやメッセージング拡張機能が含まれている場合、アプリ マニフェストの詳細は、ボット名、ロゴ、プライバシー ポリシーのリンク、サービス使用条件のリンクなど、ボット フレームワーク メタデータと一致している必要があります。
* アプリが Azure Active Directory (Azure AD) を認証に使用する場合は、マニフェストに Azure AD Application (クライアント) ID を含めます。詳細については、「[マニフェストのリファレンス](~/resources/schema/manifest-schema.md#webapplicationinfo)」を参照してください。

### <a name="app-icons"></a>アプリのアイコン

[*必須の修正プログラム*]

アイコンは、ユーザーが Teams ストアを閲覧する際に目にする主要な要素の 1 つです。 アイコンは、アプリのブランドや目的を伝えるとともに、以下の要件を満たす必要があります。

* アプリ パッケージには、カラー アイコンとアウトライン アイコンの 2 つの PNG バージョンのアプリ アイコンを含める必要があります。
* アイコンのカラー バージョンは 192x192 ピクセルである必要があります。 アイコン記号の配色は自由ですが、無地または完全に透明な正方形の背景に配置する必要があります。
* アイコンのアウトライン バージョンは、次のシナリオで表示されます。
  * アプリが使用されていて、Teams の左側のアプリ バーで **ホストされている** 場合。
  * ユーザーがアプリのメッセージング拡張機能をピン留めする場合。

* アウトラインは 32x32 ピクセルで、透明な背景、または白地に透明な背景が使用できます。 アイコンは、記号の周りに余分なパディングがないことが必要です。

* ご使用のアプリ パッケージには、適切なサイズと書式設定されたアイコンが含まれる必要があります。 アイコンは、Store 登録情報のメタデータの情報と一致している必要があります。

詳細については、「[アイコンのガイドライン](~/concepts/build-and-test/apps-package.md#app-icons)」を参照してください。

### <a name="app-descriptions"></a>アプリの説明

アプリの簡潔な説明と詳しい説明が備わっている必要があります。 アプリ構成とパートナー センターでの説明が同じである必要があります。

説明は、(Microsoft が所有するかどうかにかかわらず) 直接的または間接的に他のブランドを中傷するものであってはいけません。 説明に根拠のない主張が含まれていないか確認してください。 たとえば、**効率が 200% 向上することを保証します**。

#### <a name="short-description"></a>簡潔な説明

簡潔な説明とは、アプリの価値提供を強調し、ターゲットとなる対象ユーザー向けの簡潔な説明です。

**すべきこと**:

* 簡潔な説明を 1 文にまとめる。
* 最も重要な情報を最初に説明する。
* 顧客が検索すると考えられるキーワードを含める。
* 使用可能な文字制限を効率的に使用する。 たとえば、アプリ名を繰り返さない。

**してはいけないこと**

[*修正の提案*]

簡潔な説明の中に **アプリ** という言葉を使用する。

#### <a name="long-description"></a>詳しい説明

詳しい説明では、アプリの価値提供、主要な対象ユーザー、対象の業界を強調する魅力的なストーリーを提供できます。 この説明は 4,000 文字にもなりますが、ほとんどのユーザーは 300 から 500 文字程度しか読みません。

**すべきこと**:

* [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) を使用して説明を書式設定する。
* 積極的な語り口で、ユーザーに直接語りかける。 たとえば、「**あなたは、... ができるようになります**」などです。
* 箇条書きで機能を一覧表示することで、説明に目を通しやすくなります。
* ユーザーがアプリをインストールする前に、一覧や関連資料に記載されている機能、成果物などに対する制限、機能、条件、例外を明確に説明する。 Teams 機能は、一覧に記載されているコア機能に関連するものである必要があります。
* アプリの説明が、Teams アプリ内で利用可能な機能と一致します。 Teams アプリ以外のワークフローへのいかなる参照も制限され、Teams アプリの機能から明確に呼び出される必要があります。
* ヘルプやサポートのリンクを入れる。
* **Office 365** の代わりに **Microsoft 365** を参照する。
* **Teams** を参照する必要がある場合は、最初の参照を **Microsoft Teams** と書きます。 後の参照は、**Teams** と短縮することができます。
* アプリが Teams (または Microsoft 365) との連携方法について説明する場合は、次のような言語を使用します。
  * **... は Microsoft Teams を操作します。**
  * **... は Microsoft Teams を操作しています。**
  * **... は Microsoft Teams 内です。**
  * **... は Microsoft Teams 向けです。**
  * **... は Microsoft Teams と統合されます。**
  * **... は ... 向けに構築**
  * **... は ... 向けに開発**
  * **... は ... 向けに設計**

**してはいけないこと**:

[*必須の修正プログラム*]

* 500 文字を超える。
* **Microsoft** を **MS** や **MSFT** などの省略形にする。
* Microsoft のスローガンやタグラインを使用するなど、Microsoft の提供するアプリであることを示す。
* 自分が所有していない著作権で保護されたブランド名を使用する。
* Microsoft の認定パートナーでない限り、以下の言語を使用してください。
  * **... は ... の認定済みです**
  * **... は ... が提供しています**
* 入力ミス、文法上のエラーを含める。
* マニフェストや AppSource の詳細な説明またはアプリ コンテンツを不必要に大文字にする。
* AppSource へのリンクを含める。
* 未確認の要求を作成する。 たとえば、要求のソースに付属しない場合、ベスト、トップ、ランク付けです。
* 自分のサービスを他のマーケットプレースのサービスと比較します。

### <a name="screenshots"></a>スクリーンショット

スクリーンショットは、アプリ名、アイコン、説明を補完するために、アプリの視覚的なプレビューを提供します。 次のことを覚えておいてください。

* スクリーンショットは、1 つの一覧につき 5 枚まで設定できます。
* サポートされているファイルの種類は、PNG、JPEG、GIF です。
* 寸法は 1366x768 ピクセルである必要があります。
* 最大サイズは 1,024KB です。

**すべきこと**:

* アプリの機能 (ユーザーがボットとどのようにコミュニケーションできるかなど) に重点を置きます。
* アプリを正確に表現するコンテンツを含めます。
* テキスト慎重に使用してください。
* ブランドを反映し、マーケティング コンテンツを含む色を使用してスクリーンショットを縁取ります。

**してはいけないこと**:

[*修正の提案*]

* スマートフォンやノート PC など、特定のデバイスを表示する。
* アプリにないクロムや UI を表示する。
* あらゆるチームやブラウザーの UI をスクリーンショットにキャプチャする。
* アプリが Teams 以外で使用されていることを示すなど、アプリの実際の UI を正確に反映していないモックアップを含める。

> [!TIP]  
> アプリを使用する理由を伝えるには、ビデオが最も効果的です。 ビデオは、ユーザーがリストで最初に見るものでもあります。 詳細については、「[ストアのリスト広告向けビデオを作成する](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)」を参照してください。

### <a name="privacy-policy"></a>プライバシー ポリシー

[*必須の修正プログラム*]

プライバシー ポリシーは、Teams アプリに特化したものにも、すべてのサービスを対象とした全体的なポリシーにもできます。

* 汎用のプライバシー ポリシー テンプレートを使用する場合は、**サービス**、**アプリケーション**、または **プライバシー ポリシーの範囲内のプラットフォーム** への参照を追加する必要があります。 **サービス**、**アプリケーション**、**プラットフォーム** への参照が含まれている場合は、範囲内に Teams アプリを指定する必要はありません。 アプリの検証プロセスでは、これらの参照を解釈して、Teams アプリを他のサービスや Web サイトと一緒に含めるようにします。
* ユーザー データ ストレージ、保持、および削除の処理方法を含める必要があります。 データ保護のためのセキュリティ制御について説明する必要があります。
* 連絡先情報を含める必要があります。
* 壊れている URL や、ベータ版やステージング用の URL を含んではいけません。
* AppSource へのリンクを含めてはいけません。
* プライバシー ポリシーへのアクセスに認証が必要なものであってはいけません。
* コマース UI またはストア リンクを含めてはいけません。

### <a name="terms-of-use"></a>使用条件

[*必須の修正プログラム*]

次のガイドラインを使用して使用条件を記述します。
 * 提供するサービスに適用できる具体的なものである必要があります。
 * 独自のドメインでホストされている必要があります。
 * セキュリティで保護された (HTTPS) リンクが必要です。
 * 使用条件へのアクセスは、認証が必要なものであってはいけません。

### <a name="support-links"></a>サポート リンク

アプリのサポート URL は、認証が必要なものであってはいけません。 たとえば、ユーザーが問い合わせるためにログインするものであってはいけません。 

サポート URL には、連絡先の詳細や、ユーザーがサポート チケットを発行するための方法を含める必要があります。 たとえば、サポート URL が GitHub でホストされている場合、GitHub ページは所有権下になければならず、ユーザーがサポート チケットを発行するには、連絡先の詳細や転送方法を含める必要があります。 [*必須の修正プログラム*]

  ![サポート URL](~/assets/images/submission/validation-supportlinks-authentication.png)  

### <a name="localization"></a>ローカリゼーション

[*必須の修正プログラム*]

アプリがローカリゼーションをサポートする場合、アプリ パッケージには、Teams 言語設定に基づいて表示される言語翻訳を備えたファイルを含める必要があります。 ファイルは、Teams のローカリゼーション スキーマに準拠している必要があります。 詳細については、「[Teams のローカリゼーション スキーマ](~/concepts/build-and-test/apps-localization.md)」を参照してください。

## <a name="apps-linked-to-saas-offer"></a>SaaS プランに関連付けられたアプリ

* ISV は、同じテナント内の複数のユーザー (サブスクライバー) が自身のサブスクリプションを管理し、テナント内のユーザーにライセンスを割り当てる機能をサポートする必要があります。 
* このプランは、SaaS プランに関連付けられた [Teams アプリの技術的要件](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/include-saas-offer?branch=pr-en-us-2759)をすべて満たす必要があります。 
* SaaS プランに関連付けられた Teams アプリは、[サービスとしての 1000 個のソフトウェア (SaaS)](/legal/marketplace/certification-policies#1000-software-as-a-service-saas)で定義されたすべての要件を満たす必要があります。 
* マニフェスト ファイルに記載されている `subscriptionOffer` 個の詳細が正しい必要があります。 アプリ マニフェストで、値 `publisherId.offerId` を使用してノード `subscriptionOffer` を追加または更新します。 たとえば、発行元 ID が `contoso1234` で、オファー ID が `offer01` である場合、アプリ マニフェストで指定する値は `contoso1234.offer01` である必要があります。          
* Teams アプリに関連付けられた SaaS プランは AppSource に存在する必要があり、プレビュー プランはストア承認には承諾されません。

### <a name="offer-metadata"></a>メタデータの提供 

* メタデータの提供は、Teams マニフェスト、AppSource での Teams アプリの一覧表示、および AppSource での SaaS プランと一致する必要があります。
* Teams アプリと SaaS プランは、同じ発行元または開発者によるものでなければなりません。 アプリ マニフェストで参照される SaaS プランは、Teams アプリがコマーシャル マーケットプレースに申請される場合と同じ発行元に属している必要があります。 
* 申請したプランが SaaS プランにリンクされた Teams アプリである場合は、プラン一覧のパートナー センター製品セットアップ セクションで **[追加購入]** を **[はい。製品には、サービスの購入や追加のアプリ内購入の提供が必要です]** を選択する必要があります。     
* プランの説明と価格の詳細は、ユーザーがプラン一覧を明確に理解するために十分な情報を提供する必要があります。   
* 追加のサービスへの制限事項、依存関係や、提供される機能の例外は、プランの説明で正確に呼び出す必要があります。     
* SaaS プランにリンクされた Teams アプリは、ユーザーごとに割り当てられたライセンスをサポートするように設計されています。 場合によっては、SaaS プランが他の方法で構築される場合や、専用の購入フローが用意されている場合があります。 アプリのメタデータとサブスクリプション プランの詳細に、メソッドと購入フローについて明確に説明する必要があります。
* SaaS プランは、購入フローの該当するすべての状態で、すべてのユーザーにメッセージとガイダンスを提供する必要があります。

### <a name="saas-offer-home-page-and-license-management"></a>SaaS プランのホーム ページとライセンス管理  

* サブスクライバーに製品の使用方法を紹介します。 
* サブスクライバーへのライセンスの割り当てを許可します。 
* FAQ、ナレッジベース、電子メール アドレスなど、さまざまな方法で問題のサポートに取り組む方法を提供します。          
* ユーザーを検証して、他のユーザー経由でライセンスが割り当てられていないか確認します。 
* ライセンスの割り当て後にユーザーに通知します。 
* アプリを Teams に追加して使い始める方法を、Teams チャット ボットやメール経由でユーザーに案内します。 

### <a name="usability-and-functionality"></a>使いやすさと機能  

* ライセンスの購入と割り当てが正常に行われたら、次の情報を入力する必要があります。
    * 登録したプランの機能へのユーザーへのアクセス。   
    * ユーザーへのサブスクリプション プランの価値の追加と大きなメリット。   
* Teams アプリから、SaaS アプリケーション ホーム ページへのリンクを提供し、サブスクライバーが将来的にライセンスを管理できるようにします。 

### <a name="configure-and-test-saas-application"></a>SaaS アプリケーションの構成とテスト

テスト目的でのアプリのセットアップが複雑な場合は、エンドツーエンドの機能ドキュメント、関連付けられた SaaS の構成手順、ライセンスとユーザー管理の手順を「構成用メモ」の一部として提供します。    

> [!TIP]  
> アプリやライセンス管理の仕組みを説明したビデオを追加して、チームのテストをサポートすることができます。 

## <a name="tabs"></a>タブ
> [!NOTE]  
> このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.2](/legal/marketplace/certification-policies#114042-tabs) に沿ったものです。
アプリにタブが含まれている場合は、以下のガイドラインに従っていることを確認してください。

> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams タブ デザインのガイドライン](~/tabs/design/tabs.md)」を参照してください。

### <a name="setup"></a>セットアップ

* タブのセットアップでは、新規ユーザーを **待たせてはいけません**。 アクションやワークフローを完了するためのメッセージを提供します。 [*必須の修正プログラム*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![新規アカウントを作成](~/assets/images/submission/validation-tabs-setup-create-new-account.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![フォワード ガイダンスが見つからない](~/assets/images/submission/validation-tabs-missing-forward-guidance.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::     

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![新規ユーザー登録](~/assets/images/submission/validation-tabs-setup-new-user.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::      

* 最初の実行エクスペリエンスを最適なものにするには、タブの設定ごではなくセットアップ中にユーザーの認証を行う必要があります。 認証は、タブ構成ウィンドウの外側で行うことができます。 [*修正の提案*]

* ユーザーは、Teams 内のタブ構成機能を離れて Teams の外でコンテンツを作成し、その後 Teams に戻ってピン留めしてはいけません。 タブ構成画面では、構成の値と構成方法を説明する必要があります。 [*必須の修正プログラム*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![プロファイル名の取得](~/assets/images/submission/validation-tabs-setup-profile-name.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::    
    

* タブ構成画面では、Web サイト全体を埋め込んではいけません。 構成エクスペリエンスに焦点を当て続けます。 たとえば、ユーザーがチャネルでプロジェクトを構成できるプロジェクト管理アプリを作成する場合は、タブ構成画面に焦点を当て、ユーザーがチャネルで構成するアプリからプロジェクトを選択できるようにします。 [*必須の修正プログラム*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![構成機能](~/assets/images/submission/validation-tabs-setup-configuration-experience.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![構成画面](~/assets/images/submission/validation-tabs-setup-configuration-screen.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
     

* タブ構成画面では、ユーザーに URL の埋め込みを依頼してはいけません。 タブ設定時に URL の構成を求めるのは、ユーザーにタブ設定画面を離れて URL を取得し、構成画面に戻って URL を入力させる、壊れた UX です。 既に以前から存在する Teams 機能を使用すると、ユーザーはチャネル内の Web サイト リンクをピン留めできます。 タブ構成時にユーザーに Web サイト URL を埋め込めるよう要求し、アプリがチャネル タブに Web サイトのコンテンツ全体を表示するように制限されている場合、アプリはユーザーに十分な価値を提供していません。 [*必須の修正プログラム*]
    
:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![構成済み URL](~/assets/images/submission/validation-tabs-setup-configured-url.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
    
:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![制限のある構成済み URL](~/assets/images/submission/validation-tabs-setup-configured-url-two.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::      

    

### <a name="views"></a>ビュー

* サインイン画面領域では、大きなロゴを使用してはいけません。 [*必須の修正プログラム*]
      
:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![大きなロゴを表示する](~\assets\images\submission\validation-views-applogin.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* 複数のタブに分割して表示することで、コンテンツはシンプルになります。 [*修正の提案*]

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![複数のタブ](~/assets/images/submission/validation-views-multiple-tabs.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* タブでは、ヘッダーが重複しないようにする必要があります。 タブ フレームワークではすでにアプリ アイコンとアプリ名が表示されているため、IFRAME​​ から重複するロゴを削除します。 [*修正の提案*]

 :::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![重複するヘッダー ロゴ](~/assets/images/submission/validation-views-duplicate-header-logo.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

### <a name="navigation"></a>ナビゲーション

ナビゲーション ガイドラインは次のとおりです。

* タブは、Teams の主要なナビゲーションと競合するようなナビゲーションを設定してはなりません。 タブに左ナビゲーションを指定する場合は、アイコンのみやテキストが上下に並べて表示されたアイコンを含めてはいけません。 これは、テキストが上下に並べて表示されたアイコン (Teams のナビゲーション バーを模倣したもの) を表示するオプションを持つ折りたたみ可能なレールであってはいけません。 インライン テキストやテキストのみを持つアイコンを含めるか、タブ左レールの代わりにハンバーガー メニューを使用します。 [*必須の修正プログラム*]

Fluent UI コンポーネントの[初級](~/concepts/design/design-teams-app-basic-ui-components.md)と[上級](~\concepts\design\design-teams-app-advanced-ui-components.md)を使用してアプリをデザインします。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![左ナビゲーション](~/assets/images/submission/validation-navigation-left-navigation.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  
  
    

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![アイコンとテキスト](~/assets/images/submission/validation-navigation-icon-text.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  
   
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![折りたたみ可能な左レール](~/assets/images/submission/validation-navigation-collapsable-left-rail.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::      

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![静的タブ](~/assets/images/submission/validation-navigation-static-tab.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::     

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![水平レール](~/assets/images/submission/validation-navigation-horizontal-rail.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::        

* 左レールにツールバーがあるタブは、Teams の左ナビゲーションから 20px の間隔を空ける必要があります。 [*必須の修正プログラム*]

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![ツールバー間の間隔](~/assets/images/submission/validation-navigation-spacing-between-toolbar.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  
    

* タブ内の二次ページ、三次ページは、パンくずや左ナビゲーションで移動するメインのタブ領域で、レベル 2 (L2)、レベル 3 (L3) のビューで開く必要があります。 また、タブ ナビゲーションをサポートするために、以下のコンポーネントを含めることができます: [*必須の修正プログラム*]
    * 戻るボタン
    * ページ ヘッダー
    * ハンバーガー メニュー
* タブは横スクロールしてはいけません。 ホワイトボード アプリなど、ユーザーがアプリの操作感を損なうことなく共同作業を行うために大きなキャンバスを必要とするアプリでは、ビジネス上の必要性に応じて横スクロールを使用することができます。 [*修正の提案*]

* タブ内のディープ リンクは、外部 Web ページではなく、Teams 内にリンクさせる必要があります。 たとえば、タスク モジュールやその他のタブなどです。 [*必須の修正プログラム*]

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![[表示] ボタンにリンクしていない](~/assets/images/submission/validation-navigation-view-button-not-linked-static-tab.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
    

* タブは、ユーザーがアプリのコア エクスペリエンスのために Teams 外部に移動することを許可するものであってはなりません。 タブは、コア以外のワークフロー用に Teams の外部にリダイレクトすることができます。 たとえば、サポート チケットを発生する場合などです。 [*必須の修正プログラム*]

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![[構成] タブ内のコア ワークフロー](~/assets/images/submission/validation-navigation-core-workflow-within-configuration.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::   
   
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![アプリ コア ワークフローで外部にリダイレクト](~/assets/images/submission/validation-navigation-core-workflow-redirects-outside.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::       

    

### <a name="usability"></a>ユーザビリティ

* タブは、既存の Web サイトをホストするだけに留まらず、価値も提供する必要があります。 [*必須の修正プログラム*]

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![ワークフローを指定するユーザービリティ アプリ](~/assets/images/submission/validation-usability-app-provides-workflows.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
      
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![使いやすい Web サイト I-Frame](~/assets/images/submission/validation-usability-website-i-framed.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
    
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![使いやすい Teams アプリの同一性](~/assets/images/submission/validation-usability-teams-app-identical-website.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::    

* タブ内でコンテンツを切り捨てたり、オーバーラップしたりしてはいけません。
      
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![使いやすいコンテンツの切り捨て](~/assets/images/submission/validation-usability-content-truncation.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::


* ユーザーがタブで最後に行った操作を取り消すことができるようにする必要があります。

* 個人用コンテキストのタブでは、アプリの共有インスタンスからコンテンツを集約することができます。 たとえば、チャネル メンバーがかんばんカードでプロジェクトにコメントできる構成可能なタブを持つプロジェクト管理アプリは、このコンテンツを集約し、個人用アプリに表示する必要があります。 [*修正の提案*]

* タブは Teams テーマに対応するものである必要があります。 ユーザーがテーマを変更すると、アプリのテーマにもその選択が反映される必要があります。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![使いやすさ 応答性の高いタブ](~/assets/images/submission/validation-usability-responsive-tabs.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
      
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![使いやすさ 応答しないタブ](~/assets/images/submission/validation-usability-unresponsive-tabs.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
   

* タブには、Teams フォント、入力ランプ、カラー パレット、グリッド システム、モーション、声のトーンなど、Teams スタイルのコンポーネントを可能な限り使用する必要があります。 詳細については、「[タブ デザイン ガイドライン](/microsoftteams/platform/tabs/design/tabs)」を参照してください。 [*修正の提案*]

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![使いやすさ 異なるフォント](~/assets/images/submission/validation-usability-app-uses-diff-font.png)   
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::   

* アプリの機能で設定を変更する必要がある場合は、**[設定]** タブを含めます。[*おすすめの修正プログラム*]
* タブは、ページ内ナビゲーション、ダイアログの配置や使用方法、情報階層など、Teams の対話型デザインに沿ったものである必要があります。 詳細については、「[Microsoft Teams Fluent UI キット](~/concepts/design/design-teams-app-basic-ui-components.md)」を参照してください。

* IFRAME 内のタブ コンテンツは、Teams のコア機能を模倣した機能を含んではなりません。 たとえば、ボット、メッセージングの拡張機能、通話、会議などです。

* 構成可能なタブのランディング ページのコンテンツは、チャネルのすべてのメンバー向けにコンテキストに応じて同じでなければいけません。

* 構成可能なタブのランディング ページ内のコンテンツは、個人の使用を対象にしてはならず、**マイ タスク** や **マイ ダッシュボード** などの個人用コンテンツを含んではいけません。

* 効率性や職場の生産性を高めるために、アプリで個人的な範囲のビューを提供する必要がある場合は、フィルター処理されたビュー、個人用アプリへのディープ リンクを使用するか、または構成可能なタブ内の L2 ビューまたは L3 ビューに移動し、すべてのユーザーに対してランディング ページをコンテキストに応じて同じ状態を維持します。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![使いやすさ 構成可能なタブ 個人情報](~/assets/images/submission/validation-usability-configurable-tab-personal-info.png)   
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  
     

* 構成可能なタブには、フォーカス機能が必要です。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![使いやすさ 構成可能な入れ子のタブ](~/assets/images/submission/validation-usability-configurable-nested-tabs.png)    
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
    

* タブ エクスペリエンスは、モバイル (Android と iOS) で完全に応答しなければなりません。

> [!TIP]
> * 個人用タブと一緒に個人用ボットを設定します。
> * ユーザーが自分の個人用タブからコンテンツを共有できるようにします。

## <a name="bots"></a>ボット

> [!NOTE]
> このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.3](/legal/marketplace/certification-policies#114043-bots) に沿ったものです。

アプリにボットが含まれている場合は、以下のガイドラインに従っていることを確認してください。

> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams ボット デザインのガイドライン](~/bots/design/bots.md)」を参照してください。

### <a name="bot-commands"></a>ボット コマンド

ユーザー入力を分析し、ユーザーの意図を予測することは困難です。 ボット コマンドでは、ボットが理解できる単語または語句のセットをユーザーに提供します。

* サポートされているボット コマンドをアプリ構成に一覧表示することを強く推奨します。 これらのコマンドは、ユーザーがボットにメッセージを送信しようとした場合に、作成ボックスに表示されます。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![一覧表示されたボット コマンド](~/assets/images/submission/validation-bot-commands-listed.png)    
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
  
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![リストにないボット コマンド](~/assets/images/submission/validation-bot-commands-not-listed.png)   
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::    
     

* **やあ**、**こんにちは**、**ヘルプ** などの汎用コマンドを含め、ボットがサポートするすべてのコマンドが正しく動作する必要があります。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![ボット ヘルプ コマンド](~/assets/images/submission/validation-bot-help-command.png)     
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::   
   

* ボット コマンドは、ユーザーを行き詰まらせるものではなく、常に前進する方法を提供するものでなければいけません。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
       ![ボット コマンドの行き詰まり](~/assets/images/submission/validation-bot-commands-deadend.png)     
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
   

> [!TIP]
> 個人用ボットの場合は、**[ヘルプ]** タブを設けて、ボットにできる機能を詳しく説明します。

### <a name="bot-welcome-messages"></a>ボットのウェルカム メッセージ


* アプリに複雑な構成フローがある場合 (エンタープライズ ライセンスが必要な場合、または直感的なサインアップ フローがない場合)、そのようなアプリのボットは初回実行時に必ずウェルカム メッセージを送信する必要があります。 最適なエクスペリエンスを得るために、ウェルカム メッセージには、ボットがユーザーに提供する価値、チャネルにボットをインストールしたユーザー、ボットを構成する方法、およびサポートされているすべてのボット コマンドの簡単な説明が含まれる必要があります。 ボタン付きのアダプティブ カードを使用してウェルカム メッセージを表示すると、より使いやすくなります。 詳細については、「[ボットのウェルカム メッセージをトリガーする方法](~/bots/how-to/conversations/send-proactive-messages.md)」を参照してください。 複雑な構成フローのないアプリの場合、ボットの初回実行時にウェルカム メッセージをトリガーすることを選択できます。 ただし、ウェルカム メッセージがトリガーされる場合は、ウェルカム メッセージのガイドラインに従う必要があります。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
     ![ウェルカム メッセージのあるボット](~/assets/images/submission/validation-bot-welcome-message.png)     
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::    
    
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![ウェルカム メッセージのないボット](~/assets/images/submission/validation-bot-no-welcome-message.png)     
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::      

    

* チャネルやチャットでのボットのウェルカム メッセージは、初回実行時には省略可能であり、特にボットが個人用に利用でき、同様のアクションを実行する場合は省略できます。 ボットはユーザーに個別にウェルカム メッセージを送信してはいけません ([スパム](#bot-message-spamming)と見なされます)。 メッセージには、ボットを追加したユーザーもメンションしなければなりません。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![ウェルカム メッセージがトリガーされない](~/assets/images/submission/validation-bot-welcome-message-not-triggered.png)      
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
     
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![ウェルカム メッセージがトリガーされる](~/assets/images/submission/validation-bot-welcome-message-triggered.png)      
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
    

> [!TIP]
> 個別のユーザーへのウェルカム メッセージでは、カルーセル ツアーでボットやその他のアプリ機能の概要を効果的に伝え、ユーザーにボット コマンドを試してもらうことができます。 たとえば、「**タスクを作成する**」などです。

### <a name="bot-message-spamming"></a>ボット メッセージのスパム

ボットは、短期間に複数のメッセージを連続して送信するようなスパム行為をしてはいけません。

* **チャネルやチャットでのボットメッセージ**: 別々の記事を作成してユーザーにスパム行為をしないでください。 1 つの記事を作成し、同じスレッドに返信してください。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![ボットによるワン メッセージのスパム](~/assets/images/submission/validation-bot-message-spamming-one-message.png)      
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
      
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![ボットによる複数のメッセージのスパム](~/assets/images/submission/validation-bot-message-spamming-multiple-messages.png)       
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
     


* **個人用アプリでのボット メッセージ**: 
  * 短期間に複数のメッセージを送信しないでください。 
  * 完全な情報を含む 1 件のメッセージを送信してください。 
  * 単一の反復的なワークフローを完了するために、何度も会話をすることを避けることができます。
  * フォーム (またはタスク モジュール) を使用して、ユーザーのすべての入力を一度に収集します。 
  * NLP ベースの会話型チャットボットは、複数回の会話を使用して、話し合いをより魅力的にし、ワークフローを完了させることができます。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
    ![タスク モジュールを使用するボット](~/assets/images/submission/validation-bot-messages-using-task-module.png)         
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
    
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![複数の会話を使用するボット](~/assets/images/submission/validation-bot-messages-using-mutliple-conversation.png)          
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

* **ウェルカム メッセージ**: 一定の間隔で同じウェルカム メッセージを繰り返さないでください。 たとえば、チームに新しいメンバーが加わったとき、他のメンバーにウェルカム メッセージを送るようなスパム行為はやめましょう。 新しいメンバーへの個人的なメッセージ。

### <a name="bot-notifications"></a>ボット通知

ボット通知には、ボットに定義された範囲 (チーム、チャット、個人用) に関連するコンテンツを含める必要があります。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
      ![関連性のあるボット通知](~/assets/images/submission/validation-bot-notifications-relevant.png)        
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![関連性のないボット通知](~/assets/images/submission/validation-bot-notifications-not-relevant.png)        
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::    

  

### <a name="bots-and-adaptive-cards"></a>ボットとアダプティブ カード

アダプティブ カードは、ボット メッセージを表示するのに最適な方法です。 カードは軽量で、6 つのアクションまでしか含めてはいけません。 より多くのコンテンツを表示するには、タスク モジュールやタブの使用を検討してください。

カードの詳細については、以下を参照してください。

* [アダプティブ カードをデザインする](~/task-modules-and-cards/cards/design-effective-cards.md)
* [カード リファレンス](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

ボット エクスペリエンスは、モバイルで完全に応答しなければなりません。 ボットの応答では、必要に応じて進む方法を提供する必要があります。 ボットは応答性が高く、失敗時にはわかりやすいエラー メッセージを表示しなければなりません。 共同作業範囲内でのトリガーに基づいてユーザーのベースに個人用の範囲で送信されるボット メッセージは、(メッセージの発信元を含む) コンテキスト情報を提供する必要があります。

### <a name="notification-only-bots"></a>通知専用ボット 

通知専用ボットで構成されるアプリは、コア アプリまたはバックエンドの特定のトリガーまたはイベントに基づいてユーザーの通知をトリガーすることにより、ユーザーに価値を提供します。 たとえば、営業チームがフォローアップするために新しい潜在顧客や見込み客が追加されることなどです。

通知は、次のような場合に Teams での価値を提供します。
1.  投稿されたカードやテキストで十分な情報が提供され、ユーザーが追加で操作する必要がない。
1.  投稿されたカードやテキストが、ユーザーがアクションを起こしたり、Teams 外部のリンクを開いて詳細を表示ことを決定するのに十分なプレビュー情報を提供している。

「**新しい通知があります。クリックして表示してください**」のような内容の通知のみを提供し、それ以外のことについてはユーザーが Teams 外部に移動する必要があるアプリは、Teams 内で十分な価値を提供するものではありません。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![ボットの不適切な情報](~/assets/images/submission/validation-bot-notification-only-inadequete-info.png)         
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![ボットの適切な情報](~/assets/images/submission/validation-bot-notification-only-adequete-info.png)        
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::     

     

> [!TIP]
> 投稿されたカードで情報をプレビューし、ユーザーの基本的な操作に沿って提供することで、すべての操作を行うために Teams 外部に移動する必要がなくなります (複雑さには関係ありません)。
 
## <a name="messaging-extensions"></a>メッセージング拡張機能

> [!NOTE]
> このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.4](/legal/marketplace/certification-policies#114044-messaging-extensions) に沿ったものです。

アプリにメッセージングの拡張機能が含まれている場合は、以下のガイドラインに従っていることを確認してください。

> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams メッセージング拡張機能デザインのガイドライン](~/messaging-extensions/design/messaging-extension-design.md)」を参照してください。

### <a name="action-commands"></a>操作コマンド

操作ベースのメッセージング拡張機能では、以下のことを行う必要があります。

* ユーザーがサインインなどの中間的な手順を行うことなく、メッセージに対するアクションを起こせるようにする。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![中間ステップなし ](~/assets/images/submission/validation-messaging-extension-no-intermediate-step.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![中間ステップが利用可能](~/assets/images/submission/validation-messaging-extension-intermediate-step-available.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::      

      
* メッセージ コンテキストを次の作業状態に渡す。 [*必須の修正プログラム*]

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![メッセージを伝達するアプリ](~/assets/images/submission/validation-messaging-extension-app-passes-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
      
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
        ![メッセージを伝達しないアプリ](~/assets/images/submission/validation-messaging-extension-app-doesnot-pass-message.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
      

* アプリ内のチャット メッセージ、チャネル投稿、アクションの呼び出しでトリガーされる操作コマンドには、一般的な動詞ではなくホスト アプリ名を入力します。 たとえば、**[Skype 会議を開始]** を **[会議を開始]** に、**[DocuSign にファイルをアップロード]** を **[ファイルをアップロード]** にするなどして使用します。 [*修正の提案*]

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![操作コマンド ホスト名](~/assets/images/submission/validation-messaging-extension-action-command-host-name.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
          ![操作コマンド 動詞](~/assets/images/submission/validation-messaging-extension-action-command-verb.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::      

     

### <a name="preview-links-link-unfurling"></a>プレビュー リンク (リンク展開)

メッセージング拡張機能では、認識したリンクを Teams 作成ボックスでプレビューする必要があります。 自分でコントロールできないドメイン (絶対 URL かワイルドカードのいずれか) は追加しないでください。 たとえば、`yourapp.onmicrosoft.com` は有効ですが、`*.onmicrosoft.com` は無効です。 トップレベル ドメインも禁止されています。 たとえば、`*.com` または `*.org` などです。 [*必須の修正プログラム*]

### <a name="search-commands"></a>検索コマンド

* 検索ベースのメッセージング拡張機能では、ユーザーが効果的に検索できるようなテキストが用意されている必要があります。 [*必須の修正プログラム*]

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![ヘルプ テキストが利用可能](~/assets/images/submission/validation-search-commands-text-available.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
      

* @メンション実行可能ファイルは、明確で、理解しやすく、読みやすいものである必要があります。
 
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::
         ![検索コマンド 不明な実行可能ファイル](~/assets/images/submission/validation-search-command-unclear-executable.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
     

### <a name="search-based-messaging-extension-only-apps"></a>検索ベースのメッセージング拡張機能専用アプリ

[*必須の修正プログラム*]

検索ベースのメッセージング拡張機能で構成されるアプリは、コンテキストの切り替えなしでコンテキストに沿った会話をできるようにしたカードを共有することで、ユーザーに価値を提供します。

検索ベースのメッセージ拡張機能専用アプリの検証に合格するには、ユーザー エクスペリエンスが壊れないようにするためのベースラインとして、以下の項目が必要です。 メッセージング拡張機能を介して共有されるカードは、次の場合に Teams に価値を提供します。
1.  投稿されたカードで十分な情報が提供され、ユーザーが追加で操作する必要がない。
1.  投稿されたカードが、ユーザーがアクションを起こしたり、Teams 外部のリンクを開いて詳細を表示ことを決定するのに十分なプレビュー情報を提供している。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::     
    ![不十分な検索ベースのメッセージング](~/assets/images/submission/validation-search-based-messaging-ext-inadequete-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::     
   ![十分な検索ベースのメッセージング](~/assets/images/submission/validation-search-based-messaging-ext-adequete-info.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::   

      

リンク展開のみのアプリは、Teams 内で十分な価値を提供しません。 アプリがリンクの展開のみをサポートし、他の機能がない場合は、アプリ内に追加のワークフローを構築することを検討してください。

## <a name="task-modules"></a>タスク モジュール

> [!NOTE]
> このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.5](/legal/marketplace/certification-policies#114045-task-modules) に沿ったものです。

タスク モジュールには、アイコンと関連付けられたアプリの短い名前を含める必要があります。 タスク モジュールは、アプリ全体を埋め込むものであったり、特定の操作を完了するために必要なコンポーネントのみを表示するものであったりしてはいけません。 [*必須の修正プログラム*]

詳細については、「[Teams タスク モジュールのデザイン ガイドライン](~\task-modules-and-cards\task-modules\design-teams-task-modules.md)」を参照してください。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::     
    ![コンポーネントを表示するタスク モジュール](~/assets/images/submission/validation-task-module-displays-components.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::  

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::     
     ![アプリを埋め込むタスク モジュール](~/assets/images/submission/validation-task-module-embeds-app.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::    

    

> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams タスク モジュール デザインのガイドライン](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)」を参照してください。

## <a name="meeting-extensions"></a>ミーディング拡張機能

> [!NOTE]
> このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.6](/legal/marketplace/certification-policies#114046-meeting-extensions) に沿ったものです。


> [!TIP]
> 高品質なアプリ エクスペリエンスを作成するための詳細については、「[Teams ミーティング拡張機能デザインのガイドライン](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)」を参照してください。

ミーティング拡張機能には、次のガイドラインを使用します。

* ミーティング拡張アプリは、会議中に応答性の高いエクスペリエンスを提供し、Teams 会議エクスペリエンスに沿ったものでなければなりません。 会議中のエクスペリエンスは必須で、会議前および会議後のエクスペリエンスは必須ではありません。

  * 会議前のアプリ エクスペリエンスでは、ユーザーは会議アプリを検索して追加できます。 ユーザーは、会議の参加者にアンケートを取るための投票機能の開発など、会議前のタスクを行うこともできます。 アプリが会議前のエクスペリエンスを提供する場合は、会議のワークフローに関連するものでなければなりません。

  * 会議後のアプリ エクスペリエンスでは、ユーザーは、投票されたアンケート結果、フィードバック、その他のアプリ コンテンツなど、会議の結果を表示できます。 アプリが会議後のエクスペリエンスを提供する場合は、会議のワークフローに関連するものでなければなりません。

  * 会議中のアプリ エクスペリエンスでは、会議中に会議参加者を積極的に関与させ、すべての出席者の会議エクスペリエンスを強化できます。 アプリのコア ユーザー ワークフローを完了させるために、出席者が Teams 会議の外部に移動するようにしてはいけません。

* ご使用のアプリは、Teams のカスタム Together モードのシーンを提供する以上の価値がなければなりません。 

* 共有された会議ステージ機能は、Teams のデスクトップ アプリからのみ起動できます。 ただし、共有された会議ステージの使用エクスペリエンスは、モバイル デバイスで表示する場合にも壊れずに使用できる必要があります。

> [!TIP]
> Teams モバイルで会議用アプリを有効にするには、マニフェストで `groupchat` を `configurableTabs` と `meetingDetailsTab` の下の範囲として宣言するか、`meetingChatTab` と `meetingSidePanel` をコンテキスト プロパティとして宣言する必要があります。

### <a name="pre-and-post-meeting-experience"></a>会議前後のエクスペリエンス

* 会議前後の画面は、一般的なタブ デザイン ガイドラインに準拠している必要があります。 詳細については、「[Teams デザイン ガイドライン](~/tabs/design/tabs.md)」を参照してください。
* タブは横スクロールしてはいけません。
* 複数の項目を表示する場合に、タブのレイアウトが整理されている必要があります。 たとえば、10 件を超える投票またはアンケートについては、「[レイアウトの例](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting)」を参照してください。
* アプリでアンケートや投票の結果がエクスポートされた場合に、「**結果が正常にダウンロードされました**」と表示してユーザーに通知する必要があります。

### <a name="in-meeting-experience"></a>会議中のエクスペリエンス

* アプリは、会議中のみダーク テーマを使用する必要があります。 詳細については、「[Teams デザイン ガイドライン](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming)」を参照してください。
* 会議中にアプリ アイコンにカーソルを合わせると、ツールヒントにアプリ名が表示される必要があります。

 :::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::     
      ![ツールヒント アプリ名の表示](~/assets/images/submission/validation-in-meeting-exp-display-app-name.png)
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
     

* メッセージング拡張機能は、会議中も会議以外のときと同じように機能する必要があります。

### <a name="in-meeting-tabs"></a>会議中のタブ

* 速く応答する必要があります。 
* パディングとコンポーネントのサイズを維持する必要があります。
* 複数のレベルのナビゲーションがある場合は、戻るボタンが必要です。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::     
      ![会議中の [戻る] ボタンが使用可能](~/assets/images/submission/validation-in-meeting-exp-back-button.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
     
:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::     
      ![会議中の [戻る] ボタンが存在しない](~/assets/images/submission/validation-in-meeting-exp-back-button-absent.png) 
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
      

* 閉じるボタンが複数あってはいけません。 タブを閉じるためのヘッダー ボタンがすでに埋め込まれているため、ユーザーを混乱させるかもしれません。
* 横スクロールさせてはいけません。

### <a name="in-meeting-dialogs"></a>会議中のダイアログ

* 軽くてタスク中心のシナリオには、頻繁に使用しないようにする必要があります。
* コンテンツが 1 列に表示され、複数のナビゲーション レベルがないことが必要です。
* タスク モジュールを使用してはいけません。
* 会議ステージの中心に位置合わせする必要があります。

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::     
      ![会議中のダイアログが位置揃えされない](~/assets/images/submission/validation-in-meeting-dialog-not-aligned.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end::: 
     

* ユーザーがボタンを選択したり、アクションを実行したり下後に閉じる必要があります。

* **Together モード**: 以下のベスト プラクティスを検討して、シーン構築を行ってください。 
  * 画像はすべて PNG 形式です。
  * すべてのイメージをまとめた最終的なパッケージの解像度は、1920x1080 を超えないようにしてください。 解像度は偶数です。 この解像度は、シーンを正常に表示するための必要条件です。
  * シーンの最大サイズは 10 MB です。
  * 各画像の最大サイズは 5 MB です。 シーンは、複数の画像のコレクションです。 制限は、個々の画像に対するものです。
  * 必要に応じて **[透明]** を選択します。 このチェック ボックスは、画像が選択されている場合に右パネルで使用できます。 重なり合う画像は、シーン内の画像が重なっているかどうかを示すために、透明としてマークする必要があります。

## <a name="notifications"></a>通知

> [!NOTE]
> このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.4.7](/legal/marketplace/certification-policies#114047-notification-apis) に沿ったものです。

アプリで [Microsoft Graph が提供するアクティビティ フィード API](/graph/teams-send-activityfeednotifications) を使用する場合は、以下のガイドラインを遵守してください。

### <a name="general"></a>全般

* アプリ構成で指定されたすべての通知トリガーが動作する必要があります。
* 通知は、アプリに構成されたサポートされている言語ごとにローカライズする必要があります。
* 通知は、ユーザーのアクションから 5 秒以内に表示される必要があります。

### <a name="avatars"></a>アバター

* 通知アバターは、アプリのカラー アイコンに一致する必要があります。
* ユーザーによる通知には、そのユーザーのアバターが表示されます。

### <a name="spamming"></a>スパム

* アプリは、1 分間に 10 件以上の通知をユーザーに送信してはいけません。
* ボットとアクティビティ フィードは、重複した通知をトリガーしてはいけません。
* 通知は、ユーザーに何らかの価値を提供するものである必要があり、些細なイベントや無関係なイベントに使用してはいけません。

### <a name="navigation-and-layout"></a>ナビゲーションとレイアウト

* 通知は、Teams アクティビティ フィードのレイアウトとエクスペリエンスに準拠する必要があります。
* 通知を選択する際、ユーザーは Teams 内の関連コンテンツに誘導される必要があります。

## <a name="microsoft-365-app-compliance-program"></a>Microsoft 365 アプリ コンプライアンス プログラム

> [!NOTE]
> このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.6](/legal/marketplace/certification-policies#11406-publisher-attestation) に沿ったものです。

Microsoft 365 アプリ コンプライアンス プログラムは、アプリに関するセキュリティおよびコンプライアンス情報を評価することにより、組織がリスクを評価し管理することを目的としています。 Teams ストアにアプリを公開する場合は、以下のレベルを完了する必要があります。 

  * **Publisher の検証** は、管理者とエンド ユーザーが、Microsoft ID プラットフォームと統合するアプリ開発者の信頼性について理解する上で役立ちます。 完了すると、Azure Active Directory (Azure AD) 同意ダイアログやその他の画面に青い「**確認済み**」バッジが表示されます。 詳細については、「[アプリを発行元確認済みとしてマークする](/azure/active-directory/develop/mark-app-as-publisher-verified)」を参照してください。  

:::row::: 
    :::column span="":::
   :::column-end:::
   :::column span="3":::     
      ![Publisher の検証](~/assets/images/submission/validation-365-compliance-publisher-verification.png)  
   :::column-end:::
   :::column span="":::
   :::column-end:::
:::row-end:::
        

  * **発行元の構成証明**: 潜在的な顧客がアプリの使用を適切な情報に基づいて判断できるように、一般的な情報、データの取り扱い、セキュリティとコンプライアンスに関する情報を共有するプロセス。

> [!NOTE] 
> 過去に表示されていないアプリを提出する場合は、アプリが Teams ストアに表示されるまで正式に発行元の構成証明を完了することができません。 一覧表示されているアプリを更新する場合は、アプリの最新バージョンを提出する前に発行元の構成証明証を完了します。

## <a name="advertising"></a>広告 

> [!NOTE]
> このセクションは、[Microsoft 商用マーケットプレース ポリシー 番号 1140.7](/legal/marketplace/certification-policies#11407-advertising) に沿ったものです。

アプリは、動的な広告、バナー広告、メッセージ内広告などの広告を表示してはいけません。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [パートナー センター アカウントを作成する](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)

## <a name="see-also"></a>関連項目

* [アプリを配布する](~/concepts/deploy-and-publish/apps-publish-overview.md)
* [ストア送信を準備する](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [アプリのテストおよびデバッグ](~/concepts/build-and-test/debug.md)
* [パートナー センターの開発者アカウントを作成する](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
