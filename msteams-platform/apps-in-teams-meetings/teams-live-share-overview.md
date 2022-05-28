---
title: Live Share の概要
description: このモジュールでは、Microsoft Live Share SDK とそのユーザー シナリオについて説明します。
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: 5fa509ee7835db80a99487ed7d42ab7d6ed8341d
ms.sourcegitcommit: 09ee0305b827ad6d1368d892db3824c5dbad886f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2022
ms.locfileid: "65759656"
---
---

# <a name="live-share-sdk"></a>Live Share SDK

> [!Note]
> Live Share SDK は現在、[パブリック開発者プレビュー](../resources/dev-preview/developer-preview-intro.md)でのみ使用できます。 Live Share SDK を使用するには、Microsoft Teams の開発者向けパブリック プレビューの一部である必要があります。

Live Share は、専用のバックエンド コードを記述することなく、Teams アプリをコラボレーション マルチユーザー エクスペリエンスに変換するように設計された SDK です。 Live Share SDK は、会議と[流動フレームワーク](https://fluidframework.com/)をシームレスに統合します。 流動フレームワークは、共有状態を分散および同期するためのクライアント ライブラリの集合体です。 Live Share は、セキュリティとグローバル規模の Teams に支えられた [Azure Fluid Relay](/azure/azure-fluid-relay/) を無料かつフル マネージドですぐに使用できます。

> [!div class="nextstepaction"]
> [使用を開始する](teams-live-share-quick-start.md)

Live Share SDK は、数行のコードで各会議に関連付けられた特殊な Fluid Container に接続するための `TeamsFluidClient` クラスを提供します。 流動フレームワークによって提供されるデータ構造に加えて、Live Share は、新しい分散データ構造 (DDS) クラスのセットもサポートし、共有メディアの再生などの一般的な会議シナリオ用のアプリケーションの構築を簡略化します。

:::image type="content" source="../assets/images/teams-live-share/teams-live-share-contoso-video.gif" alt-text="Live Share ビデオ共有エクスペリエンス":::

## <a name="why-build-apps-using-the-live-share-sdk"></a>Live Share SDK を使用してアプリをビルドする理由

コラボレーション アプリの構築は、困難で、時間とコストがかかり、複雑なコンプライアンス要件が含まれるため、規模が大きくなると大変です。 Teams ユーザーは、画面共有を通してチームメイトと作業を確認したり、一緒にビデオを見たり、新しいアイデアを出し合ったりして、多くの時間を過ごしています。 Live Share SDK を使用すると、最小限の投資でアプリをより協調的なものに変換できます。

Live Share SDK の主な利点を次に示します。

* 手間のいらないセッション管理とセキュリティ
* ステートフル分散データ構造とステートレス分散データ構造
* ビデオとオーディオを簡単に同期するためのメディア拡張機能
* 役割検証を使用して会議の特権を尊重する
* 待ち時間が短く、無料で完全に管理されたサービス
* インテリジェント オーディオ ダッキング

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-schematics.png" alt-text="Teams Live Share":::

## <a name="user-scenarios"></a>ユーザーのシナリオ

|シナリオ|例|
| :------- | :--------------------- |
| ユーザーとその同僚は、今後のリーダーシップ レビューでマーケティング ビデオの早期編集を発表する会議をスケジュールしており、フィードバックのために特定のセクションを強調したいと考えています。 | ユーザーは会議ステージにビデオを共有し、ビデオを開始します。 必要に応じて、ユーザーはビデオを一時停止してシーンについて話し合います。 ユーザーは、画面の一部を順番に描画して、重要なポイントを強調することもできます。|
| あなたは、チームと Agile Poker をするアジャイル チームのプロジェクト マネージャーであり、今後のスプリントに必要な作業量を見積もる仕事をしています。| チームが合意に達するまで、Live Share SDK を使用し、計画ゲームをプレイする会議ステージに Agile Poker 計画アプリを共有します。|

> [!IMPORTANT]
> Live Share SDK のホストされている Azure Fluid Relay サービス経由で送信または保存されたすべてのデータには、24 時間アクセスできます。 詳細については、「[MyAnalytics のよくある質問](teams-live-share-faq.md)」を参照してください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [使用を開始する](teams-live-share-quick-start.md)

## <a name="see-also"></a>関連項目

* [GitHub リポジトリ](https://github.com/microsoft/live-share-sdk)
* [LIVE SHARE SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share/)
* [Live Share Media SDK リファレンス ドキュメント](/javascript/api/@microsoft/live-share-media/)
* [Live Share 機能](teams-live-share-capabilities.md)
* [Live Share 機能](teams-live-share-media-capabilities.md)
* [Live Share FAQ](teams-live-share-faq.md)
* [会議の Teams アプリ](teams-apps-in-meetings.md)
