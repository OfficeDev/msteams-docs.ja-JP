---
title: Live Share の概要
author: surbhigupta
description: このモジュールでは、Microsoft Live Share SDK とそのユーザー シナリオについて説明します。
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: c242faa57809bb967a29b7ab224e6cc0e859247b
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560555"
---
---

# <a name="live-share-sdk"></a>Live Share SDK

> [!VIDEO https://www.youtube.com/embed/971YIvosuUk]

Live Share は、専用のバックエンド コードを記述することなく、Teams アプリをコラボレーション マルチユーザー エクスペリエンスに変換するように設計された SDK です。 Live Share を使用すると、ユーザーは会議中に共同視聴、共同作成、共同編集を行うことができます。

画面共有だけでは不十分な場合があります。そのため、Microsoft はPowerPoint Liveやホワイトボードなどのツールを Teams に直接組み込んでいます。 Web アプリケーションを会議インターフェイスのセンター ステージに直接取り込むことにより、ユーザーは会議や通話中にシームレスに共同作業を行うことができます。

> [!div class="nextstepaction"]
> [概要](teams-live-share-quick-start.md)

## <a name="feature-overview"></a>機能の概要

Live Share には、無制限の共同作業シナリオをサポートする 3 つのパッケージがあります。 これらのパッケージは、プリミティブな構成要素やターン キーシナリオを含む一連の分散データ構造 (DDS) を公開します。

Live Share は、会議を [Fluid Framework](https://fluidframework.com/) とシームレスに統合します。 流動フレームワークは、共有状態を分散および同期するためのクライアント ライブラリの集合体です。 Live Share は、セキュリティとグローバル規模の Teams に支えられた [Azure Fluid Relay](/azure/azure-fluid-relay/) を無料かつフル マネージドですぐに使用できます。

### <a name="live-share-core"></a>Live Share コア

Live Share を使用すると、数行のコードで各会議に関連付けられた特殊なフルード コンテナーに接続できます。 Live Share では、Fluid Framework によって提供されるデータ構造に加えて、会議でのアプリの状態の同期を簡略化するために、新しい DDS クラスのセットもサポートされています。

Live Share コア パッケージでサポートされている機能は次のとおりです。

- 会議の Live Share セッションに `LiveShareClient`参加します。.
- 会議のプレゼンスを追跡し、ユーザー メタデータを `LivePresence`.
- でセッション `LiveEvent`内の他のクライアントにリアルタイム イベントを送信します。
- ユーザーがセッション `LiveState`を終了したときに消えるアプリの状態を調整します。
- カウントダウン タイマー `LiveTimer`を .
- Fluid Framework の任意の機能を活用します 。たとえば`SharedMap``SharedString`、.

このパッケージの詳細については、 [コア機能のページ](./teams-live-share-capabilities.md)を参照してください。

### <a name="live-share-media"></a>Live Share メディア

:::image type="content" source="../assets/images/teams-live-share/teams-live-share-contoso-video.gif" alt-text="スクリーンショットは、Live Share ビデオ共有エクスペリエンスの例を示しています。":::

ビデオとオーディオは、現代の世界と職場の重要な部分です。 Live Share メディアを使用すると、数行のコードだけで任意のメディア プレーヤーのメディア **同期** が可能になります。 プレーヤーの状態とトランスポート コントロールレイヤーでメディアを同期することで、ビューを個別に属性化しながら、アプリで利用可能な最高の品質を提供できます。 Microsoft はメディア コンテンツを再ブロードキャストしていないため、ライセンスとアクセスの要件はそのまま保持されます。

Live Share メディアでサポートされている機能は次のとおりです。

- メディア プレーヤーの状態を同期し、.`MediaPlayerSynchronizer`
- 会議中にユーザーが話す際のメディア ボリュームに対するインテリジェントな調整。
- プレイヤーの状態を変更できるユーザーを制限します。
- メディア同期を中断し、その場で、またはスケジュールされた待機ポイントで再開します。

このパッケージの詳細については、 [Live Share メディア ページ](./teams-live-share-media-capabilities.md)を参照してください。

> [!NOTE]
> Live Share では、メディア コンテンツの再ブロードキャストは行われません。 HTML5 `<video>` や Azure Media Player などの埋め込み Web プレーヤーで使用するように設計されています。

### <a name="live-share-canvas"></a>Live Share キャンバス

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-schematics.png" alt-text="スクリーンショットは、会議中にキャンバスに複数のユーザーが描画する例を示しています。":::

会議で共同作業を行う場合、ユーザーが画面上のコンテンツをポイントして強調できることが不可欠です。 Live Share キャンバスを使用すると、シームレスなコラボレーションのために、インク、レーザー ポインター、カーソルをアプリに簡単に追加できます。

Live Share キャンバスでサポートされている機能は次のとおりです。

- を使用してアプリ`LiveCanvas`にコラボレーション`<canvas>`を追加します。
- ペン、蛍光ペン、線、矢印ツールを使用してアイデアを伝えます。
- レーザー ポインターを使用して効果的に表示します。
- リアルタイムのマウス カーソルに従います。
- 可変デバイスの設定を構成し、状態を表示します。
- 完全にサポートされているマウス、タッチ、スタイラスの入力を使用します。

このパッケージの詳細については、 [Live Share キャンバス ページ](./teams-live-share-canvas.md)を参照してください。

## <a name="why-build-apps-with-live-share"></a>Live Share を使用してアプリをビルドする理由

コラボレーション アプリの構築は、困難で、時間とコストがかかり、複雑なコンプライアンス要件が含まれるため、規模が大きくなると大変です。 Teams ユーザーは、画面共有を通してチームメイトと作業を確認したり、一緒にビデオを見たり、新しいアイデアを出し合ったりして、多くの時間を過ごしています。 Live Share SDK を使用すると、最小限の投資でアプリをより協調的なものに変換できます。

Live Share SDK の主な利点を次に示します。

- 手間のいらないセッション管理とセキュリティ。
- ステートフル分散データ構造とステートレス分散データ構造。
- ビデオとオーディオを簡単に同期するためのメディア拡張機能。
- ターンキー インク、レーザー ポインター、カーソル。
- 役割検証を使用して会議の特権を尊重する。
- 待ち時間が短く、無料で完全に管理されたサービス。

Live Share がコラボレーション シナリオに適しているかどうかを理解するには、次のような Live Share と他のコラボレーション フレームワークの違いを理解しておくことが役立ちます。

- [Web ソケット](#web-sockets)
- [Azure Fluid Relay](#azure-fluid-relay)
- [ライブ共有](#live-share-hosted-service)

### <a name="web-sockets"></a>Web ソケット

Web ソケットは、Web でリアルタイム通信を行うためのユビキタス なテクノロジであり、一部のアプリでは独自のカスタム Web ソケット バックエンドを使用することをお勧めします。 REST API とは異なり、Web ソケットはセッション内のサーバーとクライアント間のオープン接続を保持します。

他のカスタム API サービスと同様に、要件には通常、セッションの認証、地域マッピング、メンテナンス、スケーリングが含まれます。 多くの共同シナリオでは、サーバー内のセッション状態を維持する必要もあります。これには、ストレージ インフラストラクチャ、競合の解決などが必要です。

Live Share を使用すると、オーバーヘッドなしで Web ソケットのすべての機能を利用できます。

### <a name="azure-fluid-relay"></a>Azure Fluid Relay

[Azure Fluid Relay](/azure/azure-fluid-relay/) は、開発者がリアルタイムのコラボレーション エクスペリエンスを構築し、接続された JavaScript クライアント間で状態をレプリケートするのに役立つ、Fluid Framework 用のマネージド オファリングです。 Microsoft Whiteboard、Loop、OneNote はすべて、Fluid Framework で今日構築されたアプリの例です。

他の Azure サービスと同様に、Azure Fluid Relay は、複雑さを最小限に抑えて個々のプロジェクトのニーズに合わせて設計されています。 要件には、Fluid コンテナーの認証ストーリーの開発と地域コンプライアンスが含まれます。 構成が完了すると、開発者は高品質のコラボレーション エクスペリエンスを提供することに専念できます。

### <a name="live-share-hosted-service"></a>Live Share ホステッド サービス

Live Share は、Microsoft Teams 会議のセキュリティに支えられたターンキーの Azure Fluid Relay サービスを提供します。 Live Share コンテナーは、会議参加者に制限され、テナントの居住要件を維持し、数行のクライアント コードでアクセスできます。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, LivePresence } from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { presence: LivePresence },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, LivePresence } from "@microsoft/live-share";
import { ContainerSchema } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { presence: LivePresence },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

---

> [!IMPORTANT]
> Live Share SDK のホストされている Azure Fluid Relay サービスを介して送信または保存されたデータには、最大 24 時間アクセスできます。 詳細については、「[MyAnalytics のよくある質問](teams-live-share-faq.md)」を参照してください。

#### <a name="using-a-custom-azure-fluid-relay-service"></a>カスタム Azure Fluid Relay サービスの使用

ほとんどの場合、無料のホステッド サービスを使用することをお勧めしますが、Live Share アプリに独自の Azure Fluid Relay サービスを使用することが有益な状況が残っています。

次の場合は、カスタム サービスの使用を検討してください。

- 会議の有効期間を超えて、Fluid コンテナーにデータを格納する必要があります。
- カスタム セキュリティ ポリシーを必要とするサービスを介して機密データを送信します。
- たとえば、Teams の外部のアプリケーション用に、 `SharedMap`Fluid Framework を使用して機能を開発します。

詳細については、カスタム Azure Fluid Relay サービス [のハウツー ガイドを](./teams-live-share-how-to/how-to-custom-azure-fluid-relay.md)参照してください。

## <a name="user-scenarios"></a>ユーザーのシナリオ

| シナリオ                                                                                | 例                                                                                                                                                                                            |
| :-------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| マーケティング レビュー中に、ユーザーは最新のビデオ編集に関するフィードバックを収集したいと考えています。 | ユーザーがビデオを会議ステージに共有し、ビデオを開始します。 必要に応じて、ユーザーはビデオを一時停止してシーンについて話し合い、参加者は画面の一部を描画して重要なポイントを強調します。 |
| プロジェクト マネージャーは、計画中にチームとアジャイル のゲームを行います。                    | マネージャーは、チームが合意するまで計画ゲームをプレイできる会議ステージにアジャイル のゲーム アプリを共有します。                                                                        |
| 財務アドバイザーは、署名する前にクライアントと PDF ドキュメントを確認します。                  | 財務アドバイザーは、PDF コントラクトを会議ステージに共有します。 すべての出席者は、PDF で互いのカーソルと強調表示されたテキストを表示できます。その後、両者は契約に署名します。        |

> [!IMPORTANT]
> Live Share は [、Microsoft Live Share SDK ライセンス](https://github.com/microsoft/live-share-sdk/blob/main/LICENSE)の下でライセンスされています。 アプリでこれらの機能を使用するには、まずこれらの用語を読んで同意する必要があります。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [使用を開始する](teams-live-share-quick-start.md)

## <a name="see-also"></a>関連項目

- [GitHub リポジトリ](https://github.com/microsoft/live-share-sdk)
- [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
- [Live Share Media SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-media/)
- [Live Share 機能](teams-live-share-capabilities.md)
- [Live Share 機能](teams-live-share-media-capabilities.md)
- [Live Share FAQ](teams-live-share-faq.md)
- [会議の Teams アプリ](teams-apps-in-meetings.md)
