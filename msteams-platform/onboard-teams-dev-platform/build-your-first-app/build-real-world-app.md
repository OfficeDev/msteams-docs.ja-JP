---
title: 初めて Teams アプリを作成する
author: heath-hamilton
description: 現実の Microsoft Teams アプリを構築するためのチュートリアル
ms.openlocfilehash: 4915dde4ef5a852f4fc5d1e4c83e3349db2eaf6b
ms.sourcegitcommit: 80bf79a952bb14cbc38c0bd1e3cf8a346158e28e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2020
ms.locfileid: "46655675"
---
# <a name="learn-how-to-build-your-first-teams-app"></a>最初の Teams アプリを構築する方法について説明します。

**最初のアプリ**を作成するときに、チュートリアルを使用して基本的な Teams アプリを作成する方法について説明します。 各レッスンは相互に構築されており、簡単な実世界の Teams アプリを作成する手順を説明します。 一般的なツール、基本概念、および便利なリンクについて紹介します。

最初に、"Hello, World!" の作成と実行について説明します。 タブアプリ 次に、いくつかの簡単な UI を作成し、Microsoft Teams Javascript SDK を使用して役に立つコンテキストを取得する方法について説明します。

## <a name="what-youll-learn"></a>学習内容

> [!div class="checklist"]
  >
  > - **Teams ツールキットを使用**して迅速に作業を開始します。 Visual Studio 用の Microsoft Teams toolkit は、アプリプロジェクトとスキャフォールディングを作成するためのものであり、実行中のアプリを数分で利用できるようにします。
  > - **マニフェストを使用**してアプリを定義します。マニフェストは、Teams アプリが使用する機能とサービスを指定する青写真です。
  > - **対象ユーザーの範囲**: 個人使用またはコラボレーション用に Teams アプリを構築できます。 このチュートリアルでは、チャネルまたはチャットで、個々のユーザーまたはユーザーグループにタブを作成する方法について説明します。
  > - **TEAMS sdk を利用してコンテキストを取得**する: Microsoft TEAMS JavaScript SDK を使用してテーマの変更を実行する方法と構成の操作を設定する方法について説明します。  
  > - **アプリの展開**: チュートリアル全体を通して、よくある関連トピックにリンクしています (認証とデザインのガイドラインを含む)。

## <a name="teams-app-fundamentals"></a>Teams アプリの基礎

チュートリアルを開始する前に、Teams 用のアプリの作成に関する以下の情報を確認する必要があります。

### <a name="apps-can-have-multiple-capabilities"></a>アプリは複数の機能を持つことができる

Teams アプリは、[タブ](../doc-links/what-are-tabs.md)、[ボット](../doc-links/what-are-bots.md )、[メッセージング拡張](../doc-links/what-are-messaging-extensions.md)機能、および[webhook やコネクタ](../doc-links/what-are-webhooks-and-connectors.md)など、1つ以上の[プラットフォーム機能](../capabilities-overview.md)で構成されます。 Teams アプリには、カード、タスクモジュール、詳細なリンクなど、多くの[UI 規則や要素](../doc-links/teams-ui-conventions.md)があります。これを使用して、最高のユーザー環境を構築することができます。

このチュートリアルでは、タブのみを作成しますが、ボットまたはその他の機能をアプリに追加することもできます。

### <a name="teams-doesnt-host-your-app"></a>Teams がアプリをホストしていない  

Teams アプリは 3 つの主要な部分で構成されています。

1. ユーザーがアプリと対話する Microsoft Teams クライアント (web、デスクトップ、またはモバイル)。
1. アプリ、サービス、ワークフロー、または web サイトで、必要なロジック、データストレージ、および API 呼び出しを実行してアプリの電源を入れます。
1. アプリパッケージ。 Teams にアプリをインストールするために使用します。 このファイルには、アプリのメタデータ (名前、アイコンなど) と、サービスへのポインターが含まれています。

## <a name="next-step"></a>次の手順

これですべてが始まったので、始めましょう。

> [!div class="nextstepaction"]
> [最初のアプリをビルドして実行する](build-and-run-with-toolkit.md)
