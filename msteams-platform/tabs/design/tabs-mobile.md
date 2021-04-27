---
title: モバイルのタブ
description: モバイルで動作するタブを設計する際のガイドラインについて説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: teams デザイン ガイドライン リファレンス フレームワーク 個人用アプリ モバイル タブ
ms.openlocfilehash: 6459d6af7899859f25b28587021e26ce6440fbef
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020409"
---
# <a name="tabs-on-mobile"></a>モバイルのタブ

> [!NOTE]
> Teams モバイル クライアントに [チャネル/グループ] タブを表示するように選択した場合は、`setSettings()` 構成には `websiteUrl` プロパティの値を設定する必要があります (下記参照)。

カスタム タブは、チャネル、グループ チャット、または個人用アプリ (静的タブや 1 対 1 ボットを含むアプリ) に含まれる場合があります。

個人用アプリは、アプリ ドロワー内のモバイル クライアントで利用できます。 アプリはデスクトップまたは Web クライアントからのみインストールできます。モバイル クライアントに表示するには最大 24 時間かかります。 または、サインアウトしてサインインすることで、モバイル クライアントに再読み込みを適用できます。 これにより、モバイル アプリがすぐ利用できる必要があります。

チャネル タブは、モバイルでも使用できます。 既定の動作は現在、ブラウザー ウィンドウ `websiteUrl` でタブを起動するために使用します。 ただし、タブの横にあるオーバーフロー メニューをクリックし、[開く] を選択すると、モバイル クライアントに読み込まれ、Teams モバイル クライアント内にタブが読み込 `...`  `contentUrl` まれます。

## <a name="accessing-personal-tabs"></a>個人用タブへのアクセス

次の図は、モバイルで個人用タブにアクセスする方法を示しています。

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Teams モバイル アプリの引き出しを示す図。" border="false":::

## <a name="accessing-channel-tabs"></a>チャネル タブへのアクセス

次の図は、モバイルでチャネル タブにアクセスする方法を示しています。

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Teams モバイル タブを示す図。" border="false":::

## <a name="design-considerations"></a>設計上の考慮事項

モバイル プラットフォームを使用すると、アプリのコンテンツが主要な Teams ナビゲーションとは別に、すべての画面を取り上げ、アプリを臨場感のあるエクスペリエンスにできます。 Teams に合った臨場感のあるエクスペリエンスを作成するには、次のガイドラインに従います。

### <a name="responsive-design"></a>レスポンシブ デザイン

タブはさまざまな画面サイズのデバイスで開くことができるため、応答性の高い設計原則に従 [う必要](https://www.w3schools.com/html/html_responsive.asp) があります。 すべての主要な構成は、モバイル デバイスでアクセス可能で、ビューを歪めずに行う必要があります。 タブがモバイル デバイスに読み込まれると、指ベースのナビゲーションを使用してすべてのボタンとリンクに簡単にアクセスできます。

### <a name="layouts"></a>レイアウト

タブの適切なレイアウトを選択することが重要です。 提示する情報の種類を検討し、簡単に使用するためにそれを整理するレイアウトを選択する必要があります。 いくつかの潜在的なオプションの概要を以下に示します。

#### <a name="single-canvas"></a>単一のキャンバス

これは、作業が行われる 1 つの大きな領域です。 Teams Wiki アプリは、このパターンに従います。 コンテンツを小さなコンポーネントに分けないアプリがある場合は、これは適しています。

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Teams モバイル単一キャンバス タブを示す図。" border="false":::

#### <a name="list"></a>一覧表示

リストは、大量のデータを並べ替え、フィルター処理する場合に最適で、最も重要な情報を一番上に保つことに最適です。 並べ替え可能な列を使用すると便利です。 省略記号メニューの下の各リスト アイテムにアクションを追加できます。

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Teams モバイル リスト タブを示す図。" border="false":::

#### <a name="grid"></a>グリッド

グリッドは、視覚的な要素を表示する場合に便利です。 上部にフィルターまたは検索コントロールを含めるのに役立ちます。

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="グリッド レイアウトの Teams モバイル タブを示す図。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a>モバイル上のボットを含むタブ

次の例は、タブとボットを持つ個人用アプリです。

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="タブとボットを持つモバイル Teams アプリの方法を示す図。" border="false":::

## <a name="ui-components"></a>UI コンポーネント

### <a name="color-palettes"></a>カラー パレット

承認済みのニュートラル パレットを背景、通知、テキスト、ボタンに使用すると、アプリが Teams で自宅で使い分けるのに役立ちます。 Teams モバイルには 2 つの色のテーマ (明るいテーマと暗いテーマ) が用意されていますので、両方でアプリが優れたものに見えるのを確認すると良い考えです。

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

タブを含むアプリを構築する場合は、Android クライアントと iOS Microsoft Teams クライアントの両方でタブがどのように機能するのか検討 (およびテスト) する必要があります。 以下のセクションでは、考慮する必要がある主要なシナリオの一部について説明します。

### <a name="testing-on-mobile-clients"></a>モバイル クライアントでのテスト

さまざまなサイズと品質のモバイル デバイスでタブが適切に機能するを検証する必要があります。 Android デバイスの場合 [、DevTools](~/tabs/how-to/developer-tools.md) を使用して、実行中にタブをデバッグできます。 パフォーマンスの高いデバイスと低パフォーマンスデバイスの両方とタブレットでテストすることをお勧めします。

### <a name="authentication"></a>認証

モバイル クライアントで認証を機能するには、Teams JavaScript SDK を少なくともバージョン 1.4.1 にアップグレードする必要があります。

### <a name="low-bandwidth-and-intermittent-connections"></a>低帯域幅と断続的な接続

モバイル クライアントは、低帯域幅と断続的な接続で定期的に機能する必要があります。 アプリは、ユーザーにコンテキスト メッセージを提供することで、タイムアウトを適切に処理する必要があります。 また、長時間実行されるプロセスに対してユーザーにフィードバックを提供するユーザー進行状況インジケーターも必要です。

> [!NOTE]
> タブは、承認チームの入力に基づいて、アプリケーションが許可リストに追加された後にのみ、モバイルで有効になります。 モバイルの応答性を確認するには、ユーザーに teamsubm@microsoft.com。 
