---
title: ストア送信を準備する
description: ストアに掲載するアプリを提出する前の最後の手順Microsoft Teams説明します。
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 975d3ef8fc8bdc8d6d7c336cf3a61a3a42ef5315
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566034"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a>Microsoft Teams ストアの提出を準備する

Microsoft Teams アプリを設計、構築、およびテストしました。 これで、ユーザーがアプリを見つけて使い始めることができるように、リストする準備が整いました。

[アプリをパートナー センター](/office/dev/store/use-partner-center-to-submit-to-appsource)に提出する前に、次の手順を実行していることを確認してください。

## <a name="validate-your-app-package"></a>アプリ パッケージの検証

アプリがテスト環境で動作している場合は、アプリ パッケージをチェックして、申請プロセス中に問題が発生しないようにする必要があります。

Microsoft Teams アプリ検証ツールを使用すると、パートナー センターに提出する前に問題を特定して修正できます。 このツールは、ストアの検証中に使用されたのと同じテスト ケースに対して、アプリの構成を自動的にチェックします。

1. [Microsoft Teams アプリ検証ツール](https://dev.teams.microsoft.com/appvalidation.html)に移動します。 (注:ツールは [、アプリケーションスタジオ](../../../build-and-test/app-studio-overview.md)でも利用可能です。
1. アプリ パッケージをアップロードして、自動テストを実行します。
1. **予備チェックリスト** に移動し、自動化が困難なテスト ケースを確認します。
1. 自動テストでエラーが発生した場合や、チェックリストのすべての条件を満たしていない場合は、一般的に構成またはアプリの[問題を修正](~/resources/schema/manifest-schema.md)します。

## <a name="compile-testing-instructions"></a>コンパイルテストの手順

レビュー担当者がアプリをテストするための手順とリソースを提供します。 パートナー センターで指示を追加するか、SharePointで一般に公開されている場所にアップロードできます。

### <a name="feature-list"></a>機能一覧

アプリの機能の詳細については、Teamsと各機能をテストするための手順を説明します。

### <a name="accounts"></a>アカウント

アプリでライセンスまたはバックエンドのセーフリストが必要な場合は、テスト アカウントを指定する必要があります。 テストを容易にするために、すべてのアカウントに事前入力データを含める必要があります。

アプリの機能によっては、次のすべてを提供する必要があります。

* 管理者アカウント (必須)
* 管理者以外のアカウント (必須)
* 初回実行サインイン エクスペリエンスを適切にテストするために事前設定されていないアカウント (必須)
* プレミアムまたはアップグレードされた機能へのアクセス権を持つアカウント(該当する場合)
* 共有コンテキストで動作するアプリのコラボレーション エクスペリエンスをテストする同じテナント内の 2 つのアカウント (該当する場合)

### <a name="tenant-configurations"></a>テナント構成

アプリを使用するようにTeamsテナントを構成する必要がある場合は、それらの手順と、検証用の管理者アカウントと管理者以外のアカウントを含めます。

### <a name="video-optional"></a>ビデオ (オプション)

Microsoft がアプリの機能を完全に理解できるように、アプリの記録を提供します。

## <a name="create-your-store-listing-details"></a>ストア登録情報の詳細を作成する

[パートナー センター](https://partner.microsoft.com)に送信する情報&#8212;、名前、説明、アイコン、およびイメージ&#8212;アプリのTeams ストアと Microsoft AppSource の一覧になります。

ストアの登録内容は、アプリの第一印象である可能性があります。 アプリのメリット、機能、ブランドを効果的に伝えるリストを使用して、インストールを増やします。

### <a name="specify-a-short-name"></a>短い名前を指定してください

アプリの名前 (具体的には、 [*その短い名前*](~/resources/schema/manifest-schema.md#name)) は、ユーザーがストア内でそれを検出する方法で重要な役割を果たします。

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="サンプル のスクリーンショットは、ストアの一覧にアプリの短い名前が表示される場所を示しています。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

短縮名が [ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)に準拠していることを確認してください。

### <a name="write-descriptions"></a>説明を書く

アプリの短い説明と長い説明が必要です。

#### <a name="short-description"></a>簡潔な説明

ターゲットオーディエンスに対してオリジナルで魅力的で、指示するアプリの簡潔な概要。 短い説明は 1 文に保ちます。

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="サンプル のスクリーンショットは、ストアの一覧でアプリの簡単な説明が表示される場所を示しています。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

簡単な説明が [ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)に準拠していることを確認します。

#### <a name="long-description"></a>詳しい説明

詳しい説明は、アプリの主な機能、解決する問題、ターゲット ユーザーを強調する説明を提供します。 この説明は 4,000 文字まで可能ですが、ほとんどのユーザーは 300 ~ 500 語の間でのみ読み取ります。

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="サンプル のスクリーンショットは、アプリの長い説明がストアの一覧に表示される場所を示しています。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

長い説明が [ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)に準拠していることを確認します。

### <a name="adhere-to-icon-design-guidelines"></a>アイコンのデザインガイドラインに従う

アイコンは、ストアを参照するときにユーザーが表示する主な要素の 1 つです。 アイコンは、アプリのブランドと目的を伝える一方で、Teams要件にも準拠する必要があります。

詳細については、「アプリ[アイコンの作成に関するガイダンスTeams](~/concepts/build-and-test/apps-package.md#app-icons)参照してください。

### <a name="capture-screenshots"></a>スクリーンショットをキャプチャする

スクリーンショットは、アプリの名前、アイコン、説明を補完する、目立つ視覚的プレビューを提供します。

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="サンプル のスクリーンショットは、ストアの一覧でアプリのスクリーンショットが表示される場所を示しています。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

スクリーンショットについて次の点に注意してください。

* リストごとに最大 5 つのスクリーンショットを作成できます。
* サポートされるファイルの種類には、PNG、JPEG、GIF などがあります。
* 寸法は 1366x768 ピクセルにする必要があります。
* 最大サイズは 1,024 KB です。

ベスト プラクティスについては、次のリソースを参照してください。

* [ストア検証ガイドラインTeams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [マイクロソフトのアプリ ストアの効果的な画像を作成する](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>ビデオを作成する

リスト内のビデオは、ユーザーがアプリを使用する理由を伝える最も効果的な方法です。 ビデオでは、次の質問に対処する必要があります。

* アプリはWhoですか?
* アプリで解決できる問題は何ですか。
* アプリの動作方法
* アプリを使用すると、他にどのようなメリットがありますか?

#### <a name="best-practices-for-videos"></a>ビデオのベスト プラクティス

* 30~90秒の間で動画を保存します。
* 品質を目指す。 リストでは、スクリーンショットの前にユーザーにビデオが表示されます。

### <a name="select-a-category-for-your-app"></a>アプリのカテゴリを選択する

申請中に、アプリを分類するように求められます。 次の表は、ストア カテゴリTeams パートナー[センター](https://aka.ms/PartnerCenterHomePage)に一覧表示されるカテゴリに対応付けます。

| Teamsカテゴリ       | パートナー センターのカテゴリ  |
|:---------------------|:---------------|
| 分析と BI | 分析、データ可視化、BI |
| 開発者と IT | 開発者ツール、 IT 管理者 |
| 教育 | 教育 |
| 人事管理 | 人材・人材採用 |
| 生産性 | コンテンツ管理、ファイルとドキュメント、生産性、トレーニングとチュートリアル、およびユーティリティ |
| プロジェクト管理 | コミュニケーション、Project管理、ワークフロー、およびビジネス管理 |
| 販売とサポート | 顧客と連絡先の管理、カスタマーサポート、財務管理、販売およびマーケティング |
| 社会的で楽しい | 画像ギャラリーとビデオギャラリー、ライフスタイル、ニュースと天気、ソーシャル、旅行、ナビゲーション |

### <a name="localize-your-store-listing"></a>店舗登録情報のローカライズ

パートナー センターでは [、ローカライズされたストア の一覧をサポートしています](/office/dev/store/prepare-localized-solutions)。 詳細については、「 [Teams アプリの一覧をローカライズする方法](../../../../concepts/build-and-test/apps-localization.md)」を参照してください。

## <a name="complete-publisher-verification"></a>Publisher検証の完了

[ストア](/azure/active-directory/develop/publisher-verification-overview)に一覧表示されているアプリTeams Publisher確認が必要です。 詳細については、「 [よく寄せられる質問](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)」、パブリッシャー [検証済みとしてアプリをマークする方法](/azure/active-directory/develop/mark-app-as-publisher-verified)、および [発行元の検証のトラブルシューティング](/azure/active-directory/develop/troubleshoot-publisher-verification)を参照してください。

## <a name="complete-publisher-attestation"></a>完全なPublisher構成証明

[Publisher構成証明](/microsoft-365-app-certification/docs/attestation)は、ストアに登録されているTeamsアプリにも必要です。 このプロセスには、アプリのセキュリティ、データ処理、コンプライアンスの実践に関する自己評価が含まれており、潜在的な顧客がアプリの使用に関する情報に基づいた意思決定を行う際に役立ちます。

> [!NOTE]
> 新しいアプリを申請する場合、アプリがTeams ストアに表示されるまで、Publisher構成証明を正式に完了することはできません。 一覧に表示されているアプリを更新する場合は、検証のためにアプリの最新バージョンを提出する前に、Publisher構成証明を完了します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アプリを送信する](/office/dev/store/add-in-submission-guide)
