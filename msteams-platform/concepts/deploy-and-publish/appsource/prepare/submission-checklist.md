---
title: ストア送信を準備する
description: Microsoft Teams アプリをストアに登録する前の最後の手順について説明します。 アプリ パッケージなどを検証する方法について説明します。
ms.topic: how-to
ms.localizationpriority: high
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 29f98b024330c562e82722ddefffe68e94543bf6
ms.sourcegitcommit: 46a2955f89b6a0e72449732eaa2bfea274191f67
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2022
ms.locfileid: "66163493"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a>Microsoft Teams のストア送信を準備する

Microsoft Teams アプリの設計、構築、テストが完了しました。 これで、ユーザーがアプリを検出して使用を開始できるように登録する準備ができました。

Microsoft Teams アプリ ストアへのアプリの発行の詳細については、次のビデオを参照してください。
<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4WG3l]
<br>

アプリを[パートナー センター](/office/dev/store/use-partner-center-to-submit-to-appsource)に送信する前に、次の手順を実行していることを確認してください。

## <a name="validate-your-app-package"></a>アプリ パッケージの検証

アプリがテスト環境で動作している場合がありますが、送信プロセス中に問題が発生しないようにアプリ パッケージを確認する必要があります。

> [!WARNING]
> App Studio を使用している場合は、Teams アプリを構成、配布、管理するための[開発者ポータル](https://dev.teams.microsoft.com/)を試してみることをお勧めします。 App Studio は、2022 年 6 月 30 日までに廃止されます。

Microsoft Teams アプリ検証ツールを使用すると、パートナー センターに送信する前に問題を特定して修正できます。 このツールは、ストアの検証中に使用したものと同じテスト ケースに対して、アプリの構成を自動的にチェックします。

1. [Microsoft Teams アプリ検証ツール](https://dev.teams.microsoft.com/appvalidation.html)に移動します。 (注: このツールは [App Studio](../../../build-and-test/app-studio-overview.md) でも入手できます。)
1. アプリ パッケージをアップロードして、自動化されたテストを実行します。
1. **[事前チェックリスト]** に移動し、自動化が困難なテスト ケースを確認します。
1. [構成の問題](~/resources/schema/manifest-schema.md)またはアプリ全般の問題を修正します。これらの問題は、自動化されたテストでエラーが発生した場合、またはチェックリストのすべての条件を満たしていない場合に発生します。

## <a name="compile-testing-instructions"></a>コンパイルのテスト手順

レビュー担当者がアプリをテストするのに役立つ手順とリソースを提供します。これには、次のものが含まれます。

* テスト アカウント
* 資格情報
* ライセンス キー

手順は、パートナー センターで追加するか、一般公開されている SharePoint 上の場所にアップロードできます。

### <a name="feature-list"></a>機能一覧

Teams でのアプリの機能に関する詳細と、それぞれをテストするための手順を示します。

### <a name="accounts"></a>アカウント

アプリでライセンスまたはバックエンド セーフ リストが必要な場合は、テスト アカウントを提供します。 提供するすべてのアカウントには、テストに役立つ事前に入力されたデータを含める必要があります。

アプリの機能によっては、次のすべてのアカウントを提供する必要があります。

* 管理者アカウント (必須)
* 管理者以外のアカウント (必須)
* 初回実行時のサインイン エクスペリエンスを適切にテストするための事前構成されていないアカウント (必須)
* プレミアム機能またはアップグレードされた機能にアクセスできるアカウント (該当する場合)
* 共有コンテキストで動作するアプリのコラボレーション エクスペリエンスをテストするための、同じテナント内の 2 つのアカウント (該当する場合)

### <a name="tenant-configurations"></a>テナント構成

アプリを使用するために Teams テナントを構成する必要がある場合は、検証のために、それらの手順、管理者アカウント、管理者以外のアカウントを含める必要があります。

### <a name="video-optional"></a>ビデオ (省略可能)

Microsoft が機能を完全に理解できるよう、アプリの録画を提供します。

## <a name="create-your-store-listing-details"></a>ストア登録情報を作成する

[パートナー センター](https://partner.microsoft.com)に送信する情報 (名前、説明、アイコン、画像など) は、Teams ストアと Microsoft AppSource でのアプリの登録情報となります。

ストア登録情報は、ユーザーに与えるアプリの第一印象となる可能性があります。 アプリの利点、機能、ブランドを効果的に伝える登録情報を使用して、インストールを増やします。

### <a name="specify-a-short-name"></a>短い名前を指定する

アプリの名前 (具体的には *[短い名前](~/resources/schema/manifest-schema.md#name)*) は、ユーザーがストアでアプリを検出する方法において重要な役割を果たします。

:::row:::

:::column span="3":::
:::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="アプリの短い名前が表示されるストア登録情報の場所を強調表示するスクリーンショットの例。":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

短い名前が[ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#app-name)に準拠していることを確認します。

### <a name="write-descriptions"></a>説明を書く

アプリの簡潔な説明と詳しい説明が備わっている必要があります。

#### <a name="short-description"></a>簡潔な説明

アプリの簡潔な概要です。対象ユーザーに直接伝わり、独創性に満ちた魅力的なものにする必要があります。簡潔な説明を 1 文にまとめます。

:::row:::

:::column span="3":::
:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="アプリの短い説明が表示されるストア登録情報の場所を強調表示するスクリーンショットの例。":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

短い説明が[ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#short-description)に準拠していることを確認します。

#### <a name="long-description"></a>詳しい説明

長い説明では、アプリについて次の情報を示す説明を提供できます。

* 主な機能
* 解決する問題
* 対象となる読者

この説明は 4,000 文字にもなりますが、ほとんどのユーザーは 300 から 500 文字程度しか読みません。

:::row:::

:::column span="3":::
:::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="アプリの長い説明が表示されるストア登録情報の場所を強調表示するスクリーンショットの例。":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

長い説明が[ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#long-description)に準拠していることを確認します。

### <a name="adhere-to-icon-design-guidelines"></a>アイコン デザインのガイドラインに準拠する

アイコンは、ユーザーがストアを閲覧する際に目にする主要な要素の 1 つです。 アイコンは、アプリのブランドや目的を伝えるとともに、Teams の要件を満たす必要があります。

詳細については、「[Teams アプリのアイコンの作成に関するガイダンス](~/concepts/build-and-test/apps-package.md#app-icons)」を参照してください。

### <a name="capture-screenshots"></a>スクリーンショットのキャプチャ

スクリーンショットは、アプリ名、アイコン、説明を補完するために、アプリの視覚的なプレビューを提供します。

:::row:::

:::column span="3":::
:::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="アプリのスクリーンショットが表示されるストア登録情報の場所を強調表示するスクリーンショットの例。":::
:::column-end:::
:::column span="1":::
:::column-end:::

:::row-end:::

スクリーンショットに関する以下のベスト プラクティスを覚えておいてください。

* スクリーンショットは、1 つの一覧につき 5 枚まで設定できます。
* サポートされているファイルの種類には、,png、.jpeg、gif などの画像形式があります。
* 寸法は 1366 x 768 ピクセルである必要があります。
* 最大サイズは 1,024KB です。

ベスト プラクティスについては、以下のリソースを参照してください。

* [Teams ストア検証ガイドライン](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#screenshots)
* [Microsoft アプリ ストアに使用する効果的なイメージを作成する](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a>ビデオを作成する

アプリを使用する理由を伝えるには、登録情報にビデオを使用することが最も効果的です。ビデオで次の質問に答えます。

* アプリの対象ユーザーは?
* アプリで解決できる問題は?
* アプリの動作方法は?
* アプリを使用して得ることのできるその他の利点は何ですか?

YouTube または Vimeo ビデオの URL を追加できます。

#### <a name="best-practices-for-videos"></a>ビデオのベスト プラクティス

* ビデオを 60 - 90 秒の間にします。
* 品質を目指します。登録情報で、ビデオはスクリーンショットの前に表示されます。
* 製品の価値をストーリー形式で伝えます。
* 製品の動作を示します。

### <a name="select-a-category-for-your-app"></a>アプリのカテゴリを選択する

送信のときに、アプリを分類するように求められます。 次の表は、Teams ストアのカテゴリを[パートナー センター](https://aka.ms/PartnerCenterHomePage)に一覧表示されているカテゴリにマップします。

| Teams カテゴリ       | パートナー センターのカテゴリ  |
|:---------------------|:---------------|
| 分析と BI | 分析、データ可視化、BI |
| 開発者と IT | 開発者ツール、IT 管理者 |
| 教育 | 教育 |
| 人事管理 | 人事と採用 |
| 生産性 | コンテンツ管理、ファイルとドキュメント、生産性、トレーニングとチュートリアル、ユーティリティ |
| プロジェクト管理 | コミュニケーション、プロジェクト管理、ワークフロー、ビジネス管理 |
| セールスおよびサポート | 顧客と連絡先の管理、カスタマー サポート、財務管理、営業およびマーケティング |
| ソーシャルとエンタメ | 画像とビデオ ギャラリー、ライフスタイル、ニュースと天気、ソーシャル、旅行、ナビゲーション |

### <a name="localize-your-store-listing"></a>ストアの登録情報をローカライズする

パートナー センターでは、[ローカライズされたストア登録情報](/office/dev/store/prepare-localized-solutions)がサポートされています。 詳細については、「[Teams アプリの登録情報をローカライズする方法](../../../../concepts/build-and-test/apps-localization.md)」を参照してください。

## <a name="complete-publisher-verification"></a>発行元の検証を完了する

Teams アプリをストアに登録するには、[発行元の検証](/azure/active-directory/develop/publisher-verification-overview)が必要です。 詳細については、[よくある質問](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)、[アプリを発行元の確認済みとしてマークする方法](/azure/active-directory/develop/mark-app-as-publisher-verified)、[発行元の確認のトラブルシューティング](/azure/active-directory/develop/troubleshoot-publisher-verification)を参照してください。

## <a name="complete-publisher-attestation"></a>発行元の構成証明を完了する

ストアに登録されている Teams アプリには、[発行元の構成証明](/microsoft-365-app-certification/docs/attestation)も必要です。 このプロセスには、アプリのセキュリティ、データ処理、コンプライアンス プラクティスの自己評価を完了することが含まれます。 このプロセスは、潜在的な顧客がアプリの使用について十分な情報に基づいて判断するのに役立ちます。

> [!NOTE]
> 新しいアプリを送信する場合は、アプリが Teams ストアに表示されるまで正式に発行元の構成証明を完了することができません。 登録されたことのあるアプリを更新する場合は、アプリの最新バージョンを送信する前に、発行元の構成証明を完了します。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [アプリを送信する](/office/dev/store/add-in-submission-guide)

## <a name="see-also"></a>関連項目

[Microsoft Teams ストアの送信に失敗した場合に問題を解決する](~/concepts/deploy-and-publish/appsource/resolve-submission-issues.md)
