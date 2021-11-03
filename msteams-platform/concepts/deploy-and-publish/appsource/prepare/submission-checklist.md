---
title: ストア送信を準備する
description: ストアに一覧表示するアプリをMicrosoft Teamsする前の最後の手順について説明します。
ms.topic: how-to
ms.localizationpriority: medium
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 617c7d962dc27964c28af74b73c252b08a39f307
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720352"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a>ストア申請Microsoft Teams準備する

アプリの設計、構築、テストMicrosoft Teamsしました。 これで、ユーザーがアプリを検出して使用を開始できるよう、リストを作成する準備ができました。

アプリをパートナー センターに [提出する前](/office/dev/store/use-partner-center-to-submit-to-appsource)に、次の手順を実行してください。

## <a name="validate-your-app-package"></a>アプリ パッケージの検証

アプリがテスト環境で動作している場合は、申請プロセス中に問題が発生しないようにアプリ パッケージを確認する必要があります。

> [!NOTE]
>  App Studio は間もなく非推奨になります。 新しい開発者ポータルを使用して、Teamsアプリを構成、配布、[および管理する](https://dev.teams.microsoft.com/)

アプリMicrosoft Teamsツールを使用すると、パートナー センターに提出する前に問題を特定して修正できます。 このツールは、ストアの検証中に使用したのと同じテスト ケースに対して、アプリの構成を自動的にチェックします。

1. アプリ検証ツール[Microsoft Teamsに移動します](https://dev.teams.microsoft.com/appvalidation.html)。 (注: このツールは App [Studio でも使用](../../../build-and-test/app-studio-overview.md)できます。)
1. アップロードテストを実行するには、アプリ パッケージをインストールします。
1. [予備チェックリスト] **に移動し** 、自動化が困難なテスト ケースを確認します。
1. [構成またはアプリ全般の問題](~/resources/schema/manifest-schema.md) を修正します。 これらの問題は、自動テストでエラーが発生した場合、またはチェックリストのすべての条件を満たしていない場合に発生します。

## <a name="compile-testing-instructions"></a>テスト手順のコンパイル

レビュー担当者がアプリをテストするのに役立つ手順とリソースを提供します。
* テスト アカウント
* 資格情報
* ライセンス キー

手順は、パートナー センターに追加するか、一般に公開されている場所にアップロードSharePoint。

### <a name="feature-list"></a>機能一覧

アプリの機能に関する詳細な情報を、Teamsテストする手順を示します。

### <a name="accounts"></a>アカウント

アプリでライセンスまたはバックエンドセーフリストが必要な場合は、テスト アカウントを提供します。 テストに役立つデータを事前に入力して提供するアカウントはすべて含める必要があります。

アプリの機能によっては、次のすべてのアカウントを提供する必要があります。

* 管理者アカウント (必須)
* 管理者以外のアカウント (必須)
* 最初の実行サインイン エクスペリエンスを適切にテストするように事前構成されていないアカウント (必須)
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

アプリの簡潔な説明と詳しい説明が備わっている必要があります。

#### <a name="short-description"></a>簡潔な説明

対象ユーザーに対して、元の、魅力的で、指示する必要があるアプリの簡潔な概要。 簡潔な説明を 1 文にまとめる。

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="スクリーンショットの例では、アプリの短い説明がストアの登録情報に表示される場所を強調表示します。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

短い説明がストアの検証ガイドラインに [準拠している必要があります](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#short-description)。

#### <a name="long-description"></a>詳しい説明

長い説明では、アプリを強調する説明を提供できます。

* 主な機能
* 解決する問題
* 対象となる読者

この説明は 4,000 文字にもなりますが、ほとんどのユーザーは 300 から 500 文字程度しか読みません。

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

スクリーンショットは、アプリ名、アイコン、説明を補完するために、アプリの視覚的なプレビューを提供します。

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="スクリーンショットの例では、アプリのスクリーンショットがストアの登録情報に表示される場所を強調表示します。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

スクリーンショットに関する次のベスト プラクティスを覚えておいてください。

* スクリーンショットは、1 つの一覧につき 5 枚まで設定できます。
* サポートされているファイルの種類は、PNG、JPEG、GIF です。
* 寸法は 1366×768 ピクセルである必要があります。
* 最大サイズは 1,024KB です。

ベスト プラクティスについては、次のリソースを参照してください。

* [Teamsストアの検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#screenshots)
* [Microsoft アプリ ストアの効果的なイメージを作成する](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>ビデオを作成する

リスト内のビデオは、ユーザーがアプリを使用する理由を伝える最も効果的な方法です。 ビデオで次の質問に対処します。

* Whoアプリは何ですか?
* アプリで解決できる問題は何ですか?
* アプリの動作方法
* アプリを使用して得るその他の利点は何ですか?

YouTube または Vimeo ビデオの URL を追加できます。

#### <a name="best-practices-for-videos"></a>ビデオのベスト プラクティス

* ビデオを 60 ~ 90 秒の間に保持します。
* 品質を目指します。 リストでは、スクリーンショットの前にユーザーにビデオが表示されます。
* 製品の価値をストーリー形式で伝えます。
* 製品の動作を示します。

### <a name="select-a-category-for-your-app"></a>アプリのカテゴリを選択する

申請中に、アプリの分類を求めるメッセージが表示されます。 次の表は、ストア Teamsパートナー センターに一覧表示されているカテゴリに[マップします](https://aka.ms/PartnerCenterHomePage)。

| Teamsカテゴリ       | パートナー センターのカテゴリ  |
|:---------------------|:---------------|
| 分析と BI | 分析、データ可視化、BI |
| 開発者と IT | 開発者ツール、IT 管理者 |
| 教育 | 教育 |
| 人事管理 | 人事と採用 |
| 生産性 | コンテンツ管理、ファイルとドキュメント、生産性、トレーニングとチュートリアル、ユーティリティ |
| プロジェクト管理 | コミュニケーション、Project管理、ワークフロー、およびビジネス管理 |
| 販売とサポート | 顧客と連絡先の管理、顧客サポート、財務管理、および販売とマーケティング |
| ソーシャルで楽しい | 画像とビデオ ギャラリー、ライフスタイル、ニュースと天気予報、ソーシャル、旅行、ナビゲーション |

### <a name="localize-your-store-listing"></a>ストアの登録情報をローカライズする

パートナー センターは、 [ローカライズされたストアの登録情報をサポートしています](/office/dev/store/prepare-localized-solutions)。 詳細については、「アプリの登録[情報をローカライズするTeams」を参照してください](../../../../concepts/build-and-test/apps-localization.md)。

## <a name="complete-publisher-verification"></a>完全なPublisher検証

[Publisherストアに](/azure/active-directory/develop/publisher-verification-overview)一覧表示されているアプリTeams検証が必要です。 詳細については、[よくある質問](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)、[アプリを発行元の確認済みとしてマークする方法](/azure/active-directory/develop/mark-app-as-publisher-verified)、[発行元の確認のトラブルシューティング](/azure/active-directory/develop/troubleshoot-publisher-verification)を参照してください。

## <a name="complete-publisher-attestation"></a>完全なPublisher構成証明

[Publisherストアに](/microsoft-365-app-certification/docs/attestation)一覧表示されているアプリTeams構成証明も必要です。 このプロセスには、アプリのセキュリティ、データ処理、コンプライアンスプラクティスの自己評価の完了が含まれます。 このプロセスは、潜在的な顧客がアプリの使用に関する情報に基づいた意思決定を行う際に役立ちます。

> [!NOTE]
> 新しいアプリを提出する場合は、アプリが Teams ストアに表示されるまで、Publisher 構成証明を正式にTeamsできます。 リストされているアプリを更新する場合は、検証Publisher最新バージョンのアプリを提出する前に、構成証明を完了してください。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アプリを送信する](/office/dev/store/add-in-submission-guide)
