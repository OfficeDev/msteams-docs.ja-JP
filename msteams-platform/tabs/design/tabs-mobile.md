---
title: モバイルのタブ
description: モバイルで使用できるタブの設計ガイドラインについて説明します。
keywords: teams デザインガイドラインリファレンスフレームワーク個人用アプリモバイルタブ
ms.openlocfilehash: a1939465b04a1fe4b803efaf83402852ca536059
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279781"
---
# <a name="tabs-on-mobile"></a>モバイルのタブ

> [!NOTE]
> Teams モバイル クライアントに [チャネル/グループ] タブを表示するように選択した場合は、`setSettings()` 構成には `websiteUrl` プロパティの値を設定する必要があります (下記参照)。

カスタムタブは、チャネル、グループチャット、または個人アプリの一部にすることができます (静的タブを含むアプリ、または1対1の bot を含むアプリ)。

個人用アプリは、アプリケーションドロワーのモバイルクライアントで使用できます。 アプリは、デスクトップまたは web クライアントからのみインストールでき、モバイルクライアントに表示されるまでに最大24時間かかることがあります。

[チャネル] タブは、モバイルでも使用できます。 既定の動作では、を使用して、 `websiteUrl` ブラウザーウィンドウでタブを起動します。 ただし、[] タブの横にあるオーバーフローメニューをクリックし、[開く] を選択することによって、モバイルクライアントに読み込むことができます `...` 。これは**Open**、を使用して、 `contentUrl` Teams モバイルクライアント内にタブをロードします。

## <a name="accessing-personal-tabs"></a>個人用タブへのアクセス

次の図は、モバイルの [個人用] タブにアクセスする方法を示しています。

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="Teams モバイルアプリドロワーを示す図" border="false":::

## <a name="accessing-channel-tabs"></a>チャネルタブへのアクセス

次の図は、モバイルの [チャネル] タブにアクセスする方法を示しています。

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="Teams の [モバイル] タブを示す図。" border="false":::

## <a name="design-considerations"></a>設計上の考慮事項

弊社のモバイルプラットフォームを使用すると、アプリのコンテンツがメインの Teams ナビゲーションとは別にすべての画面を占有しているため、アプリをイマーシブ操作とすることができます。 Teams に適したイマーシブ環境を作成するには、次のガイドラインに従ってください。

### <a name="responsive-design"></a>レスポンシブ デザイン

タブはさまざまな画面サイズのデバイス上で開くことができるため、 [応答性](https://www.w3schools.com/html/html_responsive.asp) の高い設計原則に従う必要があります。 すべてのキーの構成はモバイルデバイスでアクセスできる必要があり、ビューがゆがんではないことが必要です。 タブがモバイルデバイスにロードされている場合、すべてのボタンとリンクは、finger ベースのナビゲーションを使用して簡単にアクセスできます。

### <a name="layouts"></a>レイアウト

タブの正しいレイアウトを選択することは重要です。 表示する情報の種類を検討し、簡単に使用できるように整理されたレイアウトを選択する必要があります。 考えられるオプションには、次のようなものがあります。

#### <a name="single-canvas"></a>1つのキャンバス

これは、作業が行われる大きな領域の1つです。 Teams Wiki アプリは、このパターンに従います。 コンテンツを小さなコンポーネントに分離しないアプリがある場合は、それに適しています。

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="Teams の [モバイルシングルキャンバス] タブを示す図" border="false":::

#### <a name="list"></a>リスト

リストは大量のデータの並べ替えとフィルター処理を行うのに適しており、最も重要なものを最上位に保持するのに適しています。 並べ替え可能な列を使用すると便利です。 アクションは、省略記号メニューの各リスト項目に追加できます。

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="Teams モバイルリストタブを示す図" border="false":::

#### <a name="grid"></a>グリッド

グリッドは、ビジュアルの高い要素を表示するのに便利です。 フィルターまたは検索コントロールを上部に含めることができます。

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="グリッドレイアウトを含む Teams mobile タブを示す図" border="false":::

### <a name="tabs-with-bots-on-mobile"></a>モバイルに bot があるタブ

次の例は、タブと bot を備えた個人のアプリです。

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="タブと bot を備えたモバイル Teams アプリを示す図" border="false":::

## <a name="ui-components"></a>UI コンポーネント

### <a name="color-palettes"></a>カラー パレット

背景、通知、テキスト、およびボタンに対して承認されたニュートラルパレットを使用すると、アプリが Teams での自宅をよりよく理解できるようになります。 Teams mobile には2つの色のテーマ (軽いと濃) があるため、アプリが両方に適したものになるようにすることをお勧めします。

#### <a name="light-color"></a>明るい色

![ライトカラーパレット](../../assets/images/light-color.png)

#### <a name="dark-color"></a>暗い色

![濃い色パレット](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a>ボタンとコントロール

ボタンのスタイルを設定すると、どのような種類の動作が発生したかを伝えることができます。 さまざまな強調レベルを表示するように書式設定されたさまざまなボタンを維持しています。 ボタンには、テキスト、アイコン、またはテキストとアイコンの組み合わせを含めることができます。 階層内のさまざまなレベルを通信するために、各カテゴリ内に主ボタンと副ボタンを設計しました。

#### <a name="buttons"></a>ボタン

主ボタンとセカンダリボタン。

![ボタンの画像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a>選択コントロール

ラジオボタン、チェックボックス、および切り替え。

![選択コントロール](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a>Chiclets および pills

![chiclets および pills](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a>文字体裁

文字体裁はクリアで、意図的にする必要があります。 重要な情報を強調して、混乱を減らすために複数のフォントとサイズを使用しないようにします。 ローカライズと読みやすくするために、文のケースを使用し、すべての cap の使用を回避することをお勧めします。

![モバイル typograph](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a>フィールドと flyouts

フィールドは、ユーザーがテキストを入力できる領域です。 Flyouts はダイアログよりも軽量で、上部のウィンドウに表示されます。

#### <a name="list-controls"></a>コントロールを一覧表示する

![モバイルリストコントロール](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a>フィールドコントロール

![モバイルフィールドコントロール](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a>開発者の考慮事項

タブを含むアプリを構築する場合は、Android と iOS の Microsoft Teams クライアントの両方でタブがどのように機能するかを考慮する必要があります (およびテストする必要があります)。 以下のセクションでは、考慮する必要がある主なシナリオのいくつかについて概説します。

### <a name="testing-on-mobile-clients"></a>モバイルクライアントでのテスト

さまざまなサイズと品質のモバイルデバイスでタブが正しく機能することを検証する必要があります。 Android デバイスの場合、 [Devtools](~/tabs/how-to/developer-tools.md) を使用して、実行中にタブをデバッグできます。 高および低パフォーマンスのデバイスに加えて、タブレット上でテストすることをお勧めします。

### <a name="authentication"></a>認証

モバイルクライアントで認証を行うには、Teams JavaScript SDK を少なくともバージョン1.4.1 にアップグレードする必要があります。

### <a name="low-bandwidth-and-intermittent-connections"></a>低帯域幅および断続的な接続

モバイルクライアントは、低帯域幅および断続的な接続で通常に機能する必要があります。 アプリでは、ユーザーにコンテキストメッセージを提供することによって、すべてのタイムアウトを適切に処理する必要があります。 また、長時間実行されているプロセスのユーザーにフィードバックを提供するために、ユーザーの進捗状況インジケーターを表示する必要があります。
