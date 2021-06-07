---
title: ストア送信を準備する
description: ストアに一覧表示するアプリをMicrosoft Teamsする前の最後の手順について説明します。
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: c0f9c3328018884290c86a49b8026ce81022cd83
ms.sourcegitcommit: 25539046d408c4270b988fd826d7cf1275f4b9dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2021
ms.locfileid: "52763109"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a>ストア申請Microsoft Teams準備する

アプリの設計、構築、テストMicrosoft Teamsしました。 これで、ユーザーがアプリを検出して使用を開始できるよう、リストを作成する準備ができました。

アプリをパートナー センターに [提出する前](/office/dev/store/use-partner-center-to-submit-to-appsource)に、次の手順を実行してください。

## <a name="validate-your-app-package"></a>アプリ パッケージの検証

アプリがテスト環境で動作している場合は、申請プロセス中に問題が発生しないようにアプリ パッケージを確認する必要があります。

アプリMicrosoft Teamsツールを使用すると、パートナー センターに提出する前に問題を特定して修正できます。 このツールは、ストアの検証中に使用したのと同じテスト ケースに対して、アプリの構成を自動的にチェックします。

1. アプリ検証ツール[Microsoft Teamsに移動します](https://dev.teams.microsoft.com/appvalidation.html)。 (注: このツールは App [Studio でも使用](../../../build-and-test/app-studio-overview.md)できます。)
1. アップロードテストを実行するには、アプリ パッケージをインストールします。
1. [予備チェックリスト] **に移動し** 、自動化が困難なテスト ケースを確認します。
1. [自動テストでエラーが](~/resources/schema/manifest-schema.md) 発生したり、チェックリストのすべての条件を満たしていない場合は、構成やアプリの一般的な問題を修正します。

## <a name="compile-testing-instructions"></a>テスト手順のコンパイル

テスト アカウント、資格情報、ライセンス キーなど、レビュー担当者がアプリをテストするのに役立つ手順とリソースを提供します。 手順は、パートナー センターに追加するか、一般に公開されている場所にアップロードSharePoint。

### <a name="feature-list"></a>機能一覧

アプリの機能に関する詳細な情報を、Teamsテストする手順を示します。

### <a name="accounts"></a>アカウント

アプリでライセンスまたはバックエンドセーフリストが必要な場合は、テスト アカウントを指定する必要があります。 テストを容易にするために、すべてのアカウントに事前入力されたデータが含まれる必要があります。

アプリの機能によっては、以下の情報を提供する必要がある場合があります。

* 管理者アカウント (必須)
* 管理者以外のアカウント (必須)
* 最初の実行サインイン エクスペリエンスを適切にテストするために事前構成されていないアカウント (必須)
* プレミアム機能またはアップグレードされた機能にアクセスできるアカウント (該当する場合)
* 共有コンテキストで動作するアプリのコラボレーション エクスペリエンスをテストする同じテナント内の 2 つのアカウント (該当する場合)

### <a name="tenant-configurations"></a>テナント構成

アプリを使用する Teamsテナントを構成する必要がある場合は、検証のためにこれらの手順と管理者アカウントと管理者以外のアカウントを含める必要があります。

### <a name="video-optional"></a>ビデオ (オプション)

Microsoft が機能を完全に理解できるよう、アプリの記録を提供します。

## <a name="create-your-store-listing-details"></a>ストア登録情報の詳細を作成する

パートナー センター&#8212;[](https://partner.microsoft.com)に送信する情報 (名前、説明、アイコン、画像など)&#8212;は、Teams ストアとアプリの Microsoft AppSource リストになります。

ストアの登録情報は、アプリの第一印象である可能性があります。 アプリの利点、機能、ブランドを効果的に伝えるリストを使用してインストールを増やします。

### <a name="specify-a-short-name"></a>短い名前を指定する

アプリの名前 (具体的には短い名前 [*)*](~/resources/schema/manifest-schema.md#name)は、ユーザーがストアでアプリを検出する方法において重要な役割を果たします。

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="スクリーンショットの例は、アプリの短い名前がストアの登録情報に表示される場所を強調表示します。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

短い名前がストアの検証ガイドラインに [準拠している必要があります](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#app-name)。

### <a name="write-descriptions"></a>説明の書き込み

アプリの短い説明と長い説明が必要です。

#### <a name="short-description"></a>簡潔な説明

対象ユーザーに対して、元の、魅力的で、指示する必要があるアプリの簡潔な概要。 短い説明を 1 つの文に保つ。

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="スクリーンショットの例では、アプリの短い説明がストアの登録情報に表示される場所を強調表示します。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

短い説明がストアの検証ガイドラインに [準拠している必要があります](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#short-description)。

#### <a name="long-description"></a>詳しい説明

長い説明では、アプリの主な機能、解決する問題、ターゲットユーザーを強調する説明を提供できます。 この説明は 4,000 文字までですが、ほとんどのユーザーは 300 ~ 500 語しか読み取りできません。

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="スクリーンショットの例では、アプリの長い説明がストア登録情報に表示される場所を強調表示します。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

長い説明がストアの検証ガイドラインに [準拠している必要があります](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#long-description)。

### <a name="adhere-to-icon-design-guidelines"></a>アイコンの設計ガイドラインに従う

アイコンは、ユーザーがストアを閲覧するときに表示される主な要素の 1 つです。 アイコンは、アプリのブランドと目的を伝える一方で、ユーザーの要件にTeamsがあります。

詳細については、「アプリ アイコンの[作成に関するガイダンスTeams参照してください](~/concepts/build-and-test/apps-package.md#app-icons)。

### <a name="capture-screenshots"></a>スクリーンショットのキャプチャ

スクリーンショットは、アプリ名、アイコン、説明を補完するアプリの目立つ視覚的なプレビューを提供します。

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="スクリーンショットの例では、アプリのスクリーンショットがストアの登録情報に表示される場所を強調表示します。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

スクリーンショットについては、次の情報を覚えておいてください。

* リストごとに最大 5 つのスクリーンショットを作成できます。
* サポートされているファイルの種類には、PNG、JPEG、GIF が含まれます。
* ディメンションは 1366x768 ピクセルである必要があります。
* 最大サイズは 1,024 KB です。

ベスト プラクティスについては、次のリソースを参照してください。

* [Teamsの検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#screenshots)
* [Microsoft アプリ ストアの効果的なイメージを作成する](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>ビデオを作成する

リスト内のビデオは、ユーザーがアプリを使用する理由を伝える最も効果的な方法です。 ビデオで次の質問に対処する必要があります。

* Whoアプリは何ですか?
* アプリで解決できる問題は何ですか?
* アプリの動作方法
* アプリを使用して得るその他の利点は何ですか?

#### <a name="best-practices-for-videos"></a>ビデオのベスト プラクティス

* ビデオを 30 ~ 90 秒の間に保持します。
* 品質を目指します。 リストでは、スクリーンショットの前にユーザーにビデオが表示されます。

### <a name="select-a-category-for-your-app"></a>アプリのカテゴリを選択する

申請中に、アプリの分類を求めるメッセージが表示されます。 次の表は、Teamsのカテゴリをパートナー センターに一覧表示するカテゴリ[にマップします](https://aka.ms/PartnerCenterHomePage)。

| Teamsカテゴリ       | パートナー センターのカテゴリ  |
|:---------------------|:---------------|
| 分析と BI | 分析、データ可視化、BI |
| 開発者と IT | 開発者ツール、IT 管理者 |
| 教育 | 教育 |
| 人事管理 | 人事と採用 |
| 生産性 | コンテンツ管理、ファイルとドキュメント、生産性、トレーニングとチュートリアル、ユーティリティ |
| プロジェクト管理 | コミュニケーション、Project管理、ワークフロー、およびビジネス管理 |
| 販売とサポート | 顧客と連絡先の管理、カスタマー サポート、財務管理、営業およびマーケティング |
| ソーシャルで楽しい | 画像とビデオ ギャラリー、ライフスタイル、ニュースと天気予報、ソーシャル、旅行、ナビゲーション |

### <a name="localize-your-store-listing"></a>ストアの登録情報をローカライズする

パートナー センターは、 [ローカライズされたストアの登録情報をサポートしています](/office/dev/store/prepare-localized-solutions)。 詳細については、「アプリの登録[情報をローカライズするTeams」を参照してください](../../../../concepts/build-and-test/apps-localization.md)。

## <a name="complete-publisher-verification"></a>完全なPublisher検証

[Publisherストアに](/azure/active-directory/develop/publisher-verification-overview)一覧表示されているアプリTeams検証が必要です。 詳細については、「よく寄せられる質問[」、](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)アプリを[](/azure/active-directory/develop/mark-app-as-publisher-verified)発行元の検証済みとしてマークする方法、および発行元の検証の[トラブルシューティングを参照してください](/azure/active-directory/develop/troubleshoot-publisher-verification)。

## <a name="complete-publisher-attestation"></a>完全なPublisher構成証明

[Publisher一覧に](/microsoft-365-app-certification/docs/attestation)表示されるアプリTeams構成証明も必要です。 このプロセスには、潜在的な顧客がアプリの使用に関する情報に基づいた意思決定を行うのに役立つ、アプリのセキュリティ、データ処理、コンプライアンスプラクティスの自己評価が含まれます。

> [!NOTE]
> 新しいアプリを提出する場合は、アプリが Teams ストアに表示されるまで、Publisher 構成証明を正式にTeamsできます。 リストされているアプリを更新する場合は、検証Publisher最新バージョンのアプリを提出する前に、構成証明を完了してください。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アプリを送信する](/office/dev/store/add-in-submission-guide)
