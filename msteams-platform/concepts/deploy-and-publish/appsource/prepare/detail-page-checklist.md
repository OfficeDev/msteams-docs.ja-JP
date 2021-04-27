---
title: アプリの詳細ページを作成する
description: アプリの詳細ページの要件について説明します。
ms.topic: reference
localization_priority: Normal
keywords: teams publish store office publishing policy AppSource content Metadata screenshot logo description app name icons short description
ms.openlocfilehash: 6b763180cc2beb1cef6095110af0f37169e1f7c8
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020794"
---
# <a name="build-a-great-app-details-page"></a>アプリの詳細ページを作成する

詳細ページでは、アプリの第一印象がユーザーに表示されます。 詳細ページの各要素を使用して、ビジョンを伝え、ダウンロードを駆動できます。限られたスペースでアプリを紹介する方法を検討します。 ユーザーがアプリをインストールする前にユーザーを引き付けるのに役立つヒントとコツを次に示します。

> [!NOTE]
> アプリ情報が、効果的なストア登録情報 [を作成するための AppSource ガイダンスに従ってください](/office/dev/store/create-effective-office-store-listings)。

## <a name="app-name"></a>アプリ名

> [!div class="checklist"]
>
> * アプリの名前は、ユーザーが AppSource アプリ ストアでアプリを検出する方法において重要な役割を果たします。 アプリの短い名前が詳細ページに表示されます。
>* アプリ名は、Microsoft または Microsoft 製品への参照なしでアプリを反映する必要があります。
>

> **注**: アプリが Microsoft との公式なパートナーシップである場合は、サード パーティ製アプリの名前を最初に指定する必要があります。たとえば *、Microsoft Teams 用の Salesforce Connector* などです。

> [!div class="checklist"]
>
>* ガイダンスには、次のリソースを使用します。

* [アプリ名ガイド](#app-name)
* [Microsoft 商標とブランド ガイドライン](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)

**Do's:**

* アプリの動作をヒントにした、簡単で思い出に残る名前を選択します。
* 独特の特徴を持つ。
* 必要に応じて、365 の代わりに Microsoft 365 Officeしてください。

**T'ts:**

* スペースを省略しない、大文字と小文字が正しくない、またはアプリ名に言語エラーが含まれている。
* 既存のアプリに似た一般的な用語や名前を使用しない。
* アプリ名に "Teams"、"Microsoft"、既存/今後の Microsoft 製品名、または "app" を使用しない。
* かっこを使用して Microsoft 製品 ( *たとえば、Your-App-Name (Microsoft Teams の場合) を含めない*。

![アプリ名ストア ビュー](../../../../assets/images/store-detail-page/AppName-02.png)

![アプリ名 App Studio ビュー](../../../../assets/images/store-detail-page/AppName-01.png)

## <a name="color-icon"></a>色アイコン

これは、ユーザーに表示される最初の要素の 1 つです。 アプリ ストアをスクロールするときに魅力的で目を引く必要があります。 良い第一印象を与え、ブランドのイメージと目的を伝えます。 AppSource には、一貫性のあるビジュアル ID [の作成に関するヒントが追加されています](/office/dev/store/create-effective-office-store-listings#create-a-consistent-visual-identity)。

![アプリ アイコン ストア ビュー](~/assets/images/store-detail-page/AppIcon-02.png)

![アプリ アイコン App Studio ビュー](~/assets/images/store-detail-page/AppIcon-01.png)

**T'ts:**

* アイコンは、自分が所有していない著作権で保護された製品を模倣しなけらねない。
* アイコンは、Microsoft の製品/ブランドと似て表示される必要があります。

## <a name="outline-icon"></a>アウトライン アイコン

このアイコンは、ピン留めされたメッセージング拡張機能や、アプリが Teams の左側に表示される場合に使用されます。 アウトライン [アイコンの設計ガイダンスを参照してください](../../../../concepts/build-and-test/apps-package.md#outline-icon)。

![アプリ アイコン アウトライン ストア ビュー ](../../../../assets/images/store-detail-page/AppIconOutline-02.png)
 ![ アプリ アイコンアウトライン App Studio ビュー](../../../../assets/images/store-detail-page/AppIconOutline-01.png)

**T'ts:**

* アイコンは、自分が所有していない著作権で保護された製品を模倣しなけらねない。
* アイコンは、Microsoft の製品/ブランドと似て表示される必要があります。

## <a name="short-description"></a>簡潔な説明

これは、アプリの簡潔な概要です。 これは、対象ユーザーに直接伝わる独創性に満ちた魅力的なものにします。 理想的には、ソリューションとその値をユーザーに 1 つの文で説明します。

**Do's:**

* 最も重要な情報を最初に説明します。
* 顧客が検索する可能性が高いキーワードを含める。
* Microsoft Teams について言及する必要がある場合は、Microsoft Teams の最初のメンションを Microsoft Teams として完全に *記述する必要があります*。 Teams が同じ説明でもう一度説明されている場合は、名前を Teams に短縮 *できます*。
* Microsoft または Microsoft Teams への参照は、説明の一部であり、Microsoft のブランド基準とガイドラインに従う必要があります。
* すべての説明は、言語エラーを含めずに文法的に正しく記述する必要があります。
* "ユーザー" ではなく "Users" など、大文字を不必要に使用しないようにします。

**T'ts:**

* タイトルを繰り返し使用しない。
* Microsoft を "MS" または "MSFT" に省略しない。
* 専門用語や専門用語を使用しない - ユーザーが何を探すのかを知っているという前提にすることはできません。
* 絶対に必要な場合を除き、Microsoft 製品名への不必要な参照を避ける。
* アプリが Microsoft からの提供物である場合は、そのアプリを示したり、示したりしない。
* 所有しない著作権で保護されたブランド名を使用しない。
* 短い名前で "for Teams" を使用しない。

![短い説明ストア ビュー](~/assets/images/store-detail-page/ShortDescription-02.png)

App Studio のビューを [次に示します](https://aka.ms/InstallTeamsAppStudio)。

![短い説明 App Studio ビュー](~/assets/images/store-detail-page/ShortDescription-01.png)

## <a name="long-description"></a>詳しい説明

> [!div class="checklist"]
>
>* これにより、ソリューションの主な機能、解決する問題、ターゲットユーザーを強調する魅力的なストーリーが提供されます。 アプリの固有の機能を伝え、最初の文を使って対象ユーザーを引き込む。 説明は 4000 文字以下である必要があります。ほとんどのユーザーは、300 ~ 500 の単語のみを読み取る必要があります。
>* 何が許可されていますか?

* `<your_app>`  "Microsoft Teams と一緒に動作する"
* `<for users>`  "Microsoft Teams の操作"
* `<for tasks>`  "Microsoft Teams 内"
* `<an app>`  "for Microsoft Teams"
* `<your_app>`  "Microsoft Teams との統合"
* "...Microsoft Teams と統合」
* "...上に構築されています。。。
* "...on..."
* "...によって有効になります。."。
* "...用に開発されました。。
* "...用に設計されています。."。

> **注**: 上記の用語は、Microsoft 365 の使用にも適用されます。 Office 365 は Microsoft 365 と呼ばれる。 これを反映するようにアプリの説明を更新してください。

>[!IMPORTANT]
> AppSource エントリに記述した説明をアプリ マニフェストに正確にコピーしてください。値は一致する必要があります。 Microsoft Teams では、アプリ マニフェストで指定した説明のみを使用します。

**Do's:**

* Markdown [書式を使用して](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) 説明を照らします。  
* 説明のスキャンに役立つ機能を一覧表示します。
* アクティブな音声を使用し、ユーザーに直接話します。
* 箇条書きを使用して機能を一覧表示します。
* ユーザーが質問がある場合に連絡する方法をユーザーに知って、ヘルプまたはサポート リンクを含める。
* Microsoft Teams の最初の言及が"Microsoft Teams" として完全に書き出されている *必要があります*。 同じ説明で Teams が後でもう一度言及されている場合は、名前を *"Teams" に短縮できます*。
* Microsoft または Microsoft Teams への参照 (必要な場合のみ) は、長い説明の一部であり、Microsoft のブランド基準とガイドラインに従う必要があります。
* すべての説明は、言語エラーを含めずに文法的に正しく記述する必要があります。
* 説明の用語に大文字を不必要に使用しないようにします (たとえば、「ユーザー」ではなく「ユーザー」と指定します)。
* 頭字語は避ける。
* 制限、アカウントの依存関係、構成のセットアップ、リリースの今後の更新、または使用上の制約を必ず呼び出してください。

>[!NOTE]
> Microsoft Teams では、次の Markdown 構文がサポートされています。  
> **リンク 。** `[title](url/address/here)`.  
>**画像** `![alt text](url/address/here)` . .  
> **太字**。 `**bold text**`   `__bold text__`.  
> **Italics**. `*italicized text*`  `_italicized text`.  
>**[順序付きリスト](https://www.markdownguide.org/basic-syntax/#ordered-lists)**<br>
>`1. first` 
<br>` 1. second ` 
<br>`1.third`<br>
>**[順序なしリスト](https://www.markdownguide.org/basic-syntax/#unordered-lists)**<br>
` - short` <br>`- bulleted` <br>`- list`<br>
>**改行 。** 改行を `\n` 指定するには、文字を使用します。
 >**エスケープ。** 特殊文字をエスケープするには、インライン円記号を使用します。 `\*asterisk`.

**Markdown 形式の例**

|Markdown 形式 |Markdown 形式 |表示されるテキスト|
|:---------|:---------------|:-------------|
|リンク  |` [App name guide](#app-name)`| [アプリ名ガイド](#app-name) |
|Image |` ![App long description store view](~/assets/images/store-detail-page/LongDescription-02.png)`| ![アプリの長い説明ストア ビュー](~/assets/images/store-detail-page/LongDescription-02.png)|
|太字 |` **HR Tools**` | **HR ツール**  |
|斜体 |`*HR Tools*` |*HR ツール*|
|改行 |` HR Tools provide wide range of solutions that help your organization to manage day-to-day HR activities effectively. <br> No more flipping through paper records or juggling among 5 different apps.` |HR ツールは、組織が毎日の人事活動を効果的に管理するのに役立つ幅広いソリューションを提供します。 <br>  5 つの異なるアプリ間で紙の記録やジャグリングを切り返す必要はありません。|
|Escape|`\*Payroll tools that help you manage your payroll and tax documents.` |\*給与計算および税ドキュメントの管理に役立つ給与計算ツール。 

**T'ts:**

* 説明にキーワードを多く入れすぎないようにしてください。気を散らすので、アプリの検出に役立つ必要があります。
* 短い名前で *"Teams"* または *"Microsoft Teams"* を使用しない。
* 絶対に必要な場合を除き、Microsoft 製品名への不必要な参照を避ける。
* アプリが Microsoft からのオファリングである場合は示す必要があります。
* 所有しない著作権で保護されたブランド名を使用しない。
* アプリが公式の認定プロセスを通過しない限り、次の言語を使用しない。

  * "...の認定を受けています。。
  * "...によって動力を与えられた。.."

* "Microsoft" を "MS" または "MSFT" に省略し、Microsoft を完全に書き込む必要があります。
* 説明やメタデータの一部が、アプリを公式の Microsoft 製品として示す場合はありません。
* パートナーは、Microsoft のタグラインを使用または模倣したり、スローガンまたはタグラインで Microsoft 製品またはサービスの名前を使用したりすることはできません。
* ロゴは、アプリを公式の Microsoft 製品/機能として誤って表示したり、既存または今後の Microsoft 製品を模倣したりしなけってはなかっていません。

![アプリの長い説明ストア ビュー](~/assets/images/store-detail-page/LongDescription-02.png)

App Studio のビューを [次に示します](https://aka.ms/InstallTeamsAppStudio)。

![アプリの長い説明 App Studio ビュー](~/assets/images/store-detail-page/LongDescription-01.png)

## <a name="screenshots"></a>スクリーンショット

パートナー センターにアップロードされたスクリーンショット[は](https://partner.microsoft.com)[、AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)と Teams クライアントのアプリ一覧の両方に表示されます。 アプリの説明と共にアプリの視覚的なプレビューが提供されます。
.png、.jpg、または .gif ファイルとして書式設定された 1 ~ 5 つのスクリーンショットを提供できます。 スクリーンショットは、最大サイズが 1024 KB の 1366 x 768 ピクセルである必要があります。

**Do's:**

* アプリのすべての機能の強調表示に重点を置きます。
* コンテンツはアプリを正確に表す必要があります。
* テキストは、過剰に設定せずに十分に入力する必要があります。
* スクリーンショットを背景色で囲み [、Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) の例のようなマーケティング コンテンツを追加できます。ただし、サイズはスクリーンショットの 1 つではなく、全体的なイメージが含まれます。

<img width="800px" alt="Freshdesk screenshot" src="../../../../assets/images/freshdesk.png" />

**T'ts:**

* 電話やノート PC など、特定のデバイスを表示しない。
* アプリの外部からクロム/UI を表示しない。
* スクリーンショットに Teams やブラウザーの UI をキャプチャしない。
* [Teams] タブの代わりに Web サイトを表示するなどのアプリの実際の UI を不正確に反映するモックアップは含めない。

その他のベスト プラクティスについては、「有効 *な* [AppSource ストア イメージの作成」を参照してください](/office/dev/store/craft-effective-appsource-store-images)。

## <a name="videos"></a>ビデオ

画像が 1000 単語の価値がある場合、ビデオは 10000 の画像の価値があります。 ビデオは、アプリを使用する利点を伝える最も効果的な方法です。 アプリの詳細ページのすべてのスクリーンショットの前に配置されます。 次の情報を必ず指定してください。

* アプリの動作方法。
* アプリで実現できる機能。
* アプリを使用する利点。
* ユーザーのユーザー。

プレゼンテーションを短く、甘く保ち、30 ~90 秒の間のどこかに置いておきます。

## <a name="learn-more"></a>詳細情報

[アプリの申請に関するチェックリスト](~/concepts/deploy-and-publish/appsource/publish.md)。  
[Microsoft Teams アプリのアプリ パッケージを作成します](~/concepts/build-and-test/apps-package.md)。  
[パートナー センターを使用して AppSource にソリューションを送信します](/office/dev/store/use-partner-center-to-submit-to-appsource)。
