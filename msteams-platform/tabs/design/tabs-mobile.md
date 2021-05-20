---
title: モバイルのタブ
description: モバイルで機能するタブをデザインするためのガイドラインについて説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: チーム設計ガイドライン 参照フレームワーク個人用アプリ モバイル タブ
ms.openlocfilehash: 853ab2c52edd1f4faedcc92e6f0e8d0821b580c7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566699"
---
# <a name="tabs-on-mobile"></a>モバイルのタブ

モバイルチャンネル、チャット、個人用アプリTeamsタブを含めることができます。

## <a name="accessing-personal-tabs"></a>個人用タブへのアクセス

アプリの引き出しにある個人用タブにアクセスできます。

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Teamsモバイル アプリの引き出しを示す図。" border="false":::

## <a name="accessing-channel-tabs"></a>チャンネルタブへのアクセス

チャンネルタブやグループタブにアクセスするには、チャンネルまたはチャットで追加したチャンネルまたはチャットの[ **その他** ]ボタンを選択します。

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Teamsモバイル タブを示す図。" border="false":::

## <a name="design-considerations"></a>設計上の考慮事項

当社のモバイルプラットフォームでは、アプリがメインTeamsナビゲーションとは別に、すべての画面を占めるアプリコンテンツで没入型体験をすることができます。 Teamsに合った没入型エクスペリエンスを作成するには、次のガイドラインに従います。

### <a name="responsive-design"></a>レスポンシブ デザイン

幅広い画面サイズのデバイスでタブを開くことができるため、 [レスポンシブデザイン](https://www.w3schools.com/html/html_responsive.asp) の原則に従う必要があります。 すべてのキーコンストラクトはモバイルデバイス上でアクセス可能であり、ビューは歪んではなりません。 タブがモバイル デバイスに読み込まれるときに、すべてのボタンとリンクに指ベースのナビゲーションを使用して簡単にアクセスできることを確認します。

### <a name="layouts"></a>レイアウト

タブに適したレイアウトを選択することが重要です。 表示する情報の種類を考慮し、使いやすいレイアウトを選択する必要があります。 いくつかの潜在的なオプションは以下に概説されています。

#### <a name="single-canvas"></a>シングルキャンバス

これは作業が行われる1つの広い領域です。 Teams Wiki アプリは、このパターンに従います。 コンテンツを小さなコンポーネントに分割しないアプリがある場合は、この機能が適しています。

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="モバイルシングルキャンバスタブTeamsを示す図。" border="false":::

#### <a name="list"></a>List

リストは大量のデータを並べ替えたりフィルタリングする場合に最適であり、最も重要なデータを一番上に保持することに最適です。 並べ替え可能な列を使用すると便利です。 アクションは、省略記号メニューの各リスト項目に追加できます。

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Teamsモバイル リスト タブを示す図。" border="false":::

#### <a name="grid"></a>グリッド

グリッドは、視覚的に優れた要素を表示する場合に便利です。 これは、上部にフィルターまたは検索コントロールを含めるのに役立ちます。

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="グリッド レイアウトを使用したTeamsモバイル タブを示す図。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a>モバイルでボットを持つタブ

次の例は、タブとボットを持つ個人用アプリです。

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="タブとボットを備えたモバイル Teams アプリの様子を示す図。" border="false":::

## <a name="ui-components"></a>UI コンポーネント

### <a name="color-palettes"></a>カラー パレット

バックグラウンド、通知、テキスト、ボタンに対して承認されたニュートラルパレットを使用すると、アプリがTeamsにくつろぐのに役立ちます。 モバイルTeams 2 つの色テーマ (明るいテーマと暗色テーマ) があるため、アプリが両方とも見栄えが良いことを確認することをお勧めします。

#### <a name="light-color"></a>明るい色

![淡色パレット](../../assets/images/light-color.png)

#### <a name="dark-color"></a>暗い色

![暗色パレット](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a>ボタンとコントロール

ボタンのスタイル設定は、どのようなアクションがトリガーされるのかを伝えるのに役立ちます。 私たちは、強調の異なるレベルを示すようにフォーマットされているボタンの広い範囲を維持します。 ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを含めることができます。 階層内のさまざまなレベルを伝達するために、各カテゴリ内のプライマリ ボタンとセカンダリ ボタンを設計しました。

#### <a name="buttons"></a>ボタン

プライマリ ボタンとセカンダリ ボタン。

![ボタンイメージ](../../assets/images/buttons.png)

#### <a name="selection-controls"></a>選択コントロール

ラジオ ボタン、チェック ボックス、およびトグル。

![選択コントロール](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a>チクレットと丸薬

![チクレットと丸薬](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a>文字体裁

タイポグラフィは明確かつ意図的であるべきです。 重要な情報を強調し、複数のフォントやサイズを使用して混乱を避けてください。 文章の大文字小文字を使用し、ローカライズと読みやすさを目的としてすべてのキャップを使用しないようにすることをお勧めします。

![モバイルタイポグラフ](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a>フィールドとポップアップ

フィールドは、ユーザーがテキストを入力できる領域です。 ポップアップはダイアログよりも軽量で、上部のペインから表示されます。

#### <a name="list-controls"></a>コントロールを一覧表示する

![モバイル リスト コントロール](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a>フィールド コントロール

![モバイル フィールド コントロール](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a>開発者の考慮事項

タブを含むアプリを構築する場合は、Android と iOS の両方のクライアントでタブがどのように機能するかを検討 (およびテスト) Microsoft Teams必要があります。 以下のセクションでは、考慮する必要があるいくつかの主要なシナリオについて説明します。

### <a name="authentication"></a>認証

モバイル クライアントで認証を実行するには、JavaScript SDK Teams少なくともバージョン 1.4.1 にアップグレードする必要があります。

### <a name="low-bandwidth-and-intermittent-connections"></a>低帯域幅と断続的な接続

モバイル クライアントは、帯域幅が低く、断続的な接続で定期的に機能する必要があります。 アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。 また、実行時間の長いプロセスについてユーザーにフィードバックを提供するために、ユーザーの進行状況インジケータを表示する必要があります。

> [!NOTE]
> モバイルでタブが有効になるのは、承認チームの入力に基づいて、アプリケーションが許可リストに追加された後のみです。 モバイルの応答性を確認するには、teamsubm@microsoft.com に連絡します。

### <a name="testing-on-mobile-clients"></a>モバイル クライアントでのテスト

さまざまなサイズと品質のモバイル デバイスでタブが正しく機能することを検証する必要があります。 Android デバイスの場合、実行中に [DevTools を](~/tabs/how-to/developer-tools.md) 使用してタブをデバッグできます。 タブレットを含む高パフォーマンスと低パフォーマンスの両方のデバイスでテストすることをお勧めします。

### <a name="distribution"></a>配布

Teamsストアに登録されているアプリは、モバイルクライアントでモバイルが正常に機能するために承認Teams必要があります。 タブの可用性と動作は、アプリが承認されているかどうかによって異なります。

#### <a name="apps-on-teams-store-approved-for-mobile"></a>モバイル向けに承認Teamsストア上のアプリ

次の表は、アプリがTeams ストアに表示され、モバイルでの使用が承認されたときのタブの可用性と動作を示しています。

|機能   |モバイルの可用性?   |モバイル動作|
|----------|-----------|------------|
|チャネル <br /> およびグループ タブ|はい|タブは、アプリの構成を使用してTeamsモバイルクライアントで開きます `contentUrl` 。|
|パーソナルアプリ|はい|[個人用アプリ] タブの各タブは、それぞれの構成を使用してTeamsモバイル クライアントに表示されます `contentUrl` 。|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a>Teamsストアのアプリがモバイルで承認されていません

次の表は、アプリがTeams ストアに表示されているが、モバイルでの使用が承認されていない場合のタブの可用性と動作を示しています。

| 機能 | モバイルの可用性? | モバイル動作 |
|----------|-----------|------------|
|[チャンネルとグループ] タブ|はい|アプリの構成を使用するモバイル クライアントの Teams代わりに、デバイスの既定のブラウザー `websiteUrl` でタブが開きます `setSettings()` [](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)。 ただし、ユーザーは、アプリの横にある **[その他]** を選択し、アプリの構成をトリガーする [**開く**] を選択することで、Teamsモバイル クライアントのタブを表示できます `contentUrl` 。|
|パーソナルアプリ|なし|該当なし|

#### <a name="apps-not-on-teams-store"></a>ストアにないアプリTeams

アプリをサイドローディングしたり、組織のアプリカタログに公開したりする場合、タブの動作は、モバイル向けに Microsoft が承認したストアアプリTeamsと同じになります。
