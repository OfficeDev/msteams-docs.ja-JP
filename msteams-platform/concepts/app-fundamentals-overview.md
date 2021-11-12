---
title: アプリ開発の基本の概要
author: heath-hamilton
description: アプリの機能やエントリ ポイントなど、Teams プラットフォーム開発の基本的な概念、使用例の理解、アプリ機能へのマッピング、アプリの計画について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
keywords: エントリ ポイントの拡張性の使用例デバイスの機能
ms.openlocfilehash: fcb5da4fd7feac225b67341d6fe22187dd30a713
ms.sourcegitcommit: 781f34af2a95952bf437d0b7236ae995f4e14a08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2021
ms.locfileid: "60948426"
---
# <a name="microsoft-teams-app-development-fundamentals"></a>Microsoft Teams開発の基本

Microsoft Teamsの基本は、カスタム アプリを作成する必要がある方向Teamsします。 アプリの計画に必要なフレームワークをTeamsできます。 このドキュメントは、ユーザー アプリの通信を理解し、使用する必要があるアプリサーフェスの種類や、プロセスでアプリが必要とする可能性がある API を把握するのに役立ちます。 対話機能を受け入れるインスピレーションを得て、アプリと統合するときにアプリのエクスペリエンスを深Teams。

## <a name="capabilities-and-entry-points"></a>機能とエントリ ポイント

アプリを複数のTeams拡張できます。 アプリを拡張するには、すべてのコア機能と、共同作業スペースで機能するエントリ ポイントを理解する必要があります。 アプリを構築する拡張機能ポイントを試してみろ。 重要なアプリ プロジェクト コンポーネントは、アプリ ページを正しく構成するのに役立ちます。 Teamsは、複数の[機能とエントリ ポイント](../concepts/capabilities-overview.md)[を持つ可能性があります](../concepts/extensibility-points.md)。

## <a name="understand-your-use-cases"></a>ユース ケースを理解する

ユーザーの問題を認識し、ユーザーが直面する一般的な問題に対する回答を特定できます。 ユーザーのニーズを満Teams適切な組み合わせを見つけることで、アプリをビルドできます。 [使用例を理解して](../concepts/design/understand-use-cases.md) 、エンド ユーザーがアプリとやり取りする方法を知る。 ユーザーとその問題を理解する方法について説明します。 一般的な質問の回答は次のとおりです。

* 認証が必要ですか?
* アプリが解決する問題は何ですか?
* Whoのエンドユーザーは何ですか?
* オンボーディングエクスペリエンスの方法と、アプリが他に何を行う必要がありますか?

## <a name="map-your-use-cases-to-teams-app-capabilities"></a>使用例をアプリの機能Teamsマップする

[使用例をマップするには、](../concepts/design/map-use-cases.md) 一般的なシナリオとアプリの機能を選択する方法について説明します。 アプリを共有し、外部システム内のアイテムで共同作業を行う情報が提供されます。 ワークフローを開始し、ユーザーに通知を送信する方法も説明します。 開始する場所、ユーザーとのソーシャルを取得する方法、会話型ボット、複数の機能の組み合わせに関するその他のヒントを取得します。

## <a name="plan-responsive-tabs-for-teams-mobile"></a>Teams モバイルの応答タブを計画する
[モバイルの応答性の高いタブTeams、](../concepts/design/plan-responsive-tabs-for-teams-mobile.md)モバイル向けアプリの計画に役立つ一般的なシナリオTeamsします。 ドキュメント ガイドでは、モバイル上のアプリを戦略化する方法について示します。 また、さまざまなサッジとさまざまな種類のアプリについてTeamsできます。

## <a name="integrate-device-capabilities"></a>デバイス機能の統合

Microsoft Teamsプラットフォームは、組み込みのファースト パーティ エクスペリエンスと一致する開発者機能を継続的に強化しています。 拡張された Teams プラットフォームを使用すると、パートナーは、Microsoft Teams JavaScript クライアント SDK で利用できる専用 API を使用して、カメラ、QR またはバーコード スキャナー、フォト ギャラリー、マイク、場所などのネイティブ デバイス機能にアクセスして統合できます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アプリTeamsについて](capabilities-overview.md)

## <a name="see-also"></a>関連項目

* [統合のTeams検討事項](../samples/integrating-web-apps.md)
* [最初のアプリをMicrosoft Teamsする](../build-your-first-app/build-first-app-overview.md)
