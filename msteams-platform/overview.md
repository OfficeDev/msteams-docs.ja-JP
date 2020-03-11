---
title: Microsoft Teams 開発者プラットフォーム
author: clearab
description: Microsoft Teams 開発者プラットフォーム、また Microsoft Teams のアプリのビルドを開始する方法について説明する概要ページ。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: cb9d91f2de29bac00f4cdcd9672adf9d7d4ee734
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675120"
---
# <a name="what-are-microsoft-teams-apps"></a>Microsoft Teams アプリとは

Microsoft Teams は、メンバーが共同作業するために使用するアプリやサービスを統合する Office 365 のコラボレーション ワークスペースです。 Microsoft Teams 開発者プラットフォームでは、開発者が簡単に独自のアプリとサービスを統合して、生産性を向上させ、迅速に意思決定を行い、(コンテキストの切り替えを減らして) フォーカスを示し、既存のコンテンツとワークフロー関連のコラボレーションを作成できます。 Microsoft Teams プラットフォームにビルドされているアプリは、Teams クライアント、サービス、ワークフローの間のブリッジとして機能し、それらはコラボレーション プラットフォームのコンテキストに直接取り込まれます。

## <a name="what-can-teams-apps-do"></a>Teams アプリで実行できること

Microsoft Teams プラットフォームにビルドされているアプリは、コラボレーションの強化と生産性の向上に主に重点を置いています。 アプリは、他のシステムや複雑なマルチファセット アプリケーションからの通知を投稿するなど、シンプルなものにすることができます。 Teams がソーシャル コラボレーション プラットフォームであることにご注意ください。最適なアプリでは、メンバーが自身を表現し、共同作業を効率化することができます。

* **外部システムのアイテムで共同作業を行います。** カスタムの Teams アプリのコア シナリオの 1 つは、情報またはアイテムを別の場所から Teams に取り込んで、会話を行うことです。 情報を Teams にプッシュして、必要に応じてユーザーが検索して取得できるようにするか、埋め込み Web ビューで使用できるようにすることができます。

* **会話からワークフローをトリガーします。** 多くの場合、会話を行った後、いくつかのワークフローを開始するか、いくつかのアクションを完了する必要があります。それについてメモを取り、pull request を確認して、それを潜在顧客情報に反映します。Teams アプリを使用すると、Teams 内で直接そのワークフローへのアクセスを付与できます。

* **チームに重要なイベントを通知します。** メール通知を受け取りたくない場合、 代わりに Teams に通知を送信できます。 ユーザー、チャネル、アクティビティ フィード、またはそれらにサブスクライブしているユーザーに直接通知を送信します。

* **他のサイトまたはサービスの機能を埋め込みます。** アプリを見つけやすくするだけで済む場合があります。 既存のシングルページ アプリを埋め込むか、チーム用に一からビルドします。

## <a name="how-do-teams-apps-work"></a>Teams アプリのしくみ

Microsoft Teams のカスタム アプリについて (いかにすばらしいアプリであるかということ以外に) 最初に調べることは、Teams はホスティング サービスではないということです。 アプリ パッケージには、アプリについてのメタデータ (名前、アイコンなど) と、アプリを利用するホストの Web サービスへのポインターが含まれます。 Microsoft Teams には、配布メカニズム、利用できる UI/UX コンストラクト、アプリで利用できる情報やアクションを強化するために使用できる API が用意されています。

Teams アプリは 3 つの主要な部分で構成されています。

* ユーザーがアプリを操作する **Microsoft Teams クライアント (Web、デスクトップ、モバイル)**。
* ユーザーによってインストールされたアプリを作成し、アプリのメタデータとサービスへのポインターを含む **Teams アプリ パッケージ**。
* 必要なロジック、データ ストレージ、API 呼び出しを実行して、アプリを利用する**サービス、ワークフロー、Web サイト**。

Microsoft Teams アプリで公開する機能が、セキュリティで保護するための追加の手順を実行しない限り、インターネット経由で一般に使用可能であることに留意することが重要です。 機密情報または保護された情報へのアクセスを提供する場合、サービスでは少なくとも、アプリに接続されているエンドポイントを認証しているか、[ユーザーを認証](~/concepts/authentication/authentication.md)していることをご確認ください。

## <a name="how-can-you-share-your-teams-app"></a>Teams アプリの共有方法

Microsoft Teams アプリを共有する準備ができたら、対象ユーザーに応じて 3 つのオプションがあります。

* **[アプリを直接アップロードする](~/concepts/deploy-and-publish/apps-upload.md)** アプリをチームや組織内の少人数にのみ共有する必要がある場合は、アプリ パッケージを共有して直接アップロードできます。
* **[組織のアプリ カタログに公開する](~/concepts/deploy-and-publish/apps-publish.md)** アプリ カタログを使用してアプリを組織全体に共有できます。
* **[パブリック App Store に公開する](~/concepts/deploy-and-publish/apps-publish.md)** アプリがすべてのユーザー向けの場合、そのアプリをパブリック App Store に公開できます。 目標に応じて、マーケティングや販売のサポート対象になる可能性があります。

## <a name="get-started"></a>作業の開始

* [C# でボットとタブ アプリをビルドする](~/tutorials/get-started-dotnet-app-studio.md)
* [JavaScript または Node.js でボットとタブ アプリをビルドする](~/tutorials/get-started-nodejs-app-studio.md)

## <a name="learn-more"></a>詳細情報

* [Teams クライアントの拡張ポイント](~/concepts/extensibility-points.md)
* [Teams 用アプリをビルドする](~/concepts/building-an-app.md)
