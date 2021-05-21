---
title: モバイルのタブ
description: モバイルで動作するタブを設計する際のガイドラインについて説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: teams デザイン ガイドライン リファレンス フレームワーク 個人用アプリ モバイル タブ
ms.openlocfilehash: 853ab2c52edd1f4faedcc92e6f0e8d0821b580c7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566699"
---
# <a name="tabs-on-mobile"></a>モバイルのタブ

モバイル チャネル、チャット、個人用Teamsにタブを含めできます。

## <a name="accessing-personal-tabs"></a>個人用タブへのアクセス

アプリドロワーの個人用タブにアクセスできます。

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="モバイル アプリの引き出Teamsを示す図。" border="false":::

## <a name="accessing-channel-tabs"></a>チャネル タブへのアクセス

チャネルタブとグループ タブにアクセスするには、追加されたチャネルまたはチャットで [その他] ボタンを選択します。

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="モバイル タブのTeams図。" border="false":::

## <a name="design-considerations"></a>設計上の考慮事項

モバイル プラットフォームを使用すると、アプリのコンテンツがメインのナビゲーションとは別に、すべての画面を取り上げ、アプリの臨場感Teamsできます。 ユーザーに合った臨場感のあるエクスペリエンスをTeamsガイドラインに従います。

### <a name="responsive-design"></a>レスポンシブ デザイン

タブはさまざまな画面サイズのデバイスで開くことができるため、応答性の高い設計原則に従 [う必要](https://www.w3schools.com/html/html_responsive.asp) があります。 すべての主要な構成は、モバイル デバイスでアクセス可能で、ビューを歪めずに行う必要があります。 タブがモバイル デバイスに読み込まれると、指ベースのナビゲーションを使用してすべてのボタンとリンクに簡単にアクセスできます。

### <a name="layouts"></a>レイアウト

タブの適切なレイアウトを選択することが重要です。 提示する情報の種類を検討し、簡単に使用するためにそれを整理するレイアウトを選択する必要があります。 いくつかの潜在的なオプションの概要を以下に示します。

#### <a name="single-canvas"></a>単一のキャンバス

これは、作業が行われる 1 つの大きな領域です。 Wiki Teamsは、このパターンに従います。 コンテンツを小さなコンポーネントに分けないアプリがある場合は、これは適しています。

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="モバイル単一のTeamsタブを示す図。" border="false":::

#### <a name="list"></a>List

リストは、大量のデータを並べ替え、フィルター処理する場合に最適で、最も重要な情報を一番上に保つことに最適です。 並べ替え可能な列を使用すると便利です。 省略記号メニューの下の各リスト アイテムにアクションを追加できます。

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="[モバイル リスト] タブTeamsを示す図。" border="false":::

#### <a name="grid"></a>グリッド

グリッドは、視覚的な要素を表示する場合に便利です。 上部にフィルターまたは検索コントロールを含めるのに役立ちます。

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="グリッド レイアウトがTeamsモバイル タブを示す図。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a>モバイル上のボットを含むタブ

次の例は、タブとボットを持つ個人用アプリです。

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="タブとボットを持つTeamsモバイル アプリの表示方法を示す図。" border="false":::

## <a name="ui-components"></a>UI コンポーネント

### <a name="color-palettes"></a>カラー パレット

承認済みのニュートラル パレットを背景、通知、テキスト、およびボタンに使用すると、アプリがユーザーの自宅で使いTeams。 モバイルTeams色のテーマが 2 つ (明るいと暗い) ので、両方でアプリが優れた外観を示すのは良い考えです。

#### <a name="light-color"></a>明るい色

![明るいカラー パレット](../../assets/images/light-color.png)

#### <a name="dark-color"></a>濃い色

![濃色パレット](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a>ボタンとコントロール

ボタンのスタイルを設定する方法は、トリガーするアクションの種類を伝えるのに役立ちます。 さまざまなレベルの強調を表示するために書式設定されたボタンの広い範囲を維持します。 ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを指定できます。 階層内の異なるレベルを伝える目的で、各カテゴリ内のプライマリ ボタンとセカンダリ ボタンを設計しました。

#### <a name="buttons"></a>ボタン

プライマリ ボタンとセカンダリ ボタン。

![ボタンの画像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a>選択コントロール

ラジオ ボタン、チェック ボックス、およびトグル。

![選択コントロール](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a>シックレットと丸薬

![シックレットと丸薬](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a>文字体裁

タイポグラフィは明確で目的に合ったものにしてください。 重要な情報を強調し、複数のフォントとサイズを使用して混乱を軽減しないようにします。 文の大文字と小文字を使用し、ローカライズと読み取り可能性のためにすべての大文字を使用しないようにすることをお勧めします。

![モバイルタイポグラフ](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a>フィールドとフライアウト

フィールドは、ユーザーがテキストを入力できる領域です。 フライアウトはダイアログよりも軽量で、上部ウィンドウから表示されます。

#### <a name="list-controls"></a>コントロールを一覧表示する

![モバイル リスト コントロール](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a>フィールド コントロール

![モバイル フィールド コントロール](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a>開発者の考慮事項

タブを含むアプリを構築する場合は、Android クライアントと iOS クライアントの両方でタブがどのように機能Microsoft Teamsがあります。 以下のセクションでは、考慮する必要がある主要なシナリオの一部について説明します。

### <a name="authentication"></a>認証

モバイル クライアントで認証を機能するには、JavaScript SDK Teamsバージョン 1.4.1 以上にアップグレードする必要があります。

### <a name="low-bandwidth-and-intermittent-connections"></a>低帯域幅と断続的な接続

モバイル クライアントは、低帯域幅と断続的な接続で定期的に機能する必要があります。 アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。 また、長時間実行されるプロセスに対してユーザーにフィードバックを提供するユーザー進行状況インジケーターも必要です。

> [!NOTE]
> タブは、承認チームの入力に基づいて、アプリケーションが許可リストに追加された後にのみ、モバイルで有効になります。 モバイルの応答性を確認するには、ユーザーに teamsubm@microsoft.com。

### <a name="testing-on-mobile-clients"></a>モバイル クライアントでのテスト

さまざまなサイズと品質のモバイル デバイスでタブが適切に機能するを検証する必要があります。 Android デバイスの場合 [、DevTools](~/tabs/how-to/developer-tools.md) を使用して、実行中にタブをデバッグできます。 タブレットを含む、高パフォーマンスデバイスと低パフォーマンスデバイスの両方でテストすることをお勧めします。

### <a name="distribution"></a>配布

モバイル クライアントで適切にTeams機能するには、モバイル ストアに一覧表示されているアプリTeams必要があります。 タブの可用性と動作は、アプリが承認されたかどうかによって異なります。

#### <a name="apps-on-teams-store-approved-for-mobile"></a>モバイル用にTeamsストア上のアプリ

次の表では、アプリがモバイル ストアに表示され、モバイルTeams承認された場合のタブの可用性と動作について説明します。

|機能   |モバイルの可用性   |モバイル動作|
|----------|-----------|------------|
|チャネル <br /> [グループ] タブ|必要|アプリの構成を使用Teamsモバイル クライアントのタブが開 `contentUrl` きます。|
|個人用アプリ|必要|[個人用アプリ] タブの各タブが、Teamsを使用してモバイル クライアントに表示 `contentUrl` されます。|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a>モバイルで承認Teamsアプリストアのアプリ

次の表は、アプリがモバイル ストアに一覧表示されているが、モバイルTeams承認されていない場合のタブの可用性と動作について説明します。

| 機能 | モバイルの可用性 | モバイル動作 |
|----------|-----------|------------|
|[チャネルとグループ] タブ|必要|タブは、アプリの構成を使用して Teams モバイル クライアントではなく、デバイスの既定のブラウザーで開きます。これは、ソース コードの関数にも含める `websiteUrl` 必要 `setSettings()` [があります](/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions&preserve-view=true)。 ただし、アプリの横にある [詳細] を選択し、[開く]を選択すると、Teams モバイルクライアントのタブが表示され、アプリの構成がトリガー `contentUrl` されます。|
|個人用アプリ|なし|該当なし|

#### <a name="apps-not-on-teams-store"></a>アプリがストアTeamsしない

アプリをサイドロードする場合や、組織のアプリ カタログに発行する場合、タブの動作は、モバイル向け Microsoft によって承認された Teams ストア アプリと同じです。
