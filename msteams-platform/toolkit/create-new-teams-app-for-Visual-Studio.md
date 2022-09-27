---
title: Visual Studio で新しい Teams アプリを作成する
author: surbhigupta
description: このモジュールでは、Visual Studio 用 Teams ツールキットを使用して新しい Teams アプリを作成する方法について説明します
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: 12f0b74726aed8cdca50d9f5c078acd0f22cbeaa
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027454"
---
# <a name="create-new-teams-app-in-visual-studio"></a>Visual Studio で新しい Teams アプリを作成する

Teams ツールキットは、Teams アプリを作成するための Microsoft Teams アプリ テンプレートを Visual Studio に用意しています。  新しいプロジェクトを作成するときに必要な Teams アプリ テンプレートを検索して選択できます。 作成するための Teams アプリ テンプレートを使用できます。

* タブ アプリ
* コマンド ボット
* 通知ボット
* メッセージ拡張機能:

## <a name="prerequisites"></a>前提条件

| &nbsp; | インストール | 使用するには... |
| --- | --- | --- |
| &nbsp; | **必須** | &nbsp; |
| &nbsp; | Visual Studio バージョン 17.3 | Visual Studio のエンタープライズ エディションをインストールし、"ASP.NET" ワークロードと Microsoft Teams 開発ツールをインストールできます。 |
| &nbsp; | Teams ツールキット | アプリのプロジェクト スキャフォールディングを作成する Visual Studio 拡張機能。 最新バージョン​​を使用します。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams を使用して、チャット、会議、通話用のアプリを通じて共同作業を行うすべてのユーザーと 1 か所で共同作業を行うことができます。 |
 | &nbsp; | [Microsoft 365 テナントを準備する](../concepts/build-and-test/prepare-your-o365-tenant.md) | アプリをインストールするための適切なアクセス許可を持つ Teams アカウントにアクセスします。 |

1. Visual Studio を起動したら、**[作業の開始]** セクションで **[新規プロジェクトを作成する]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project1.png" alt-text="[作業の開始] から新規プロジェクトを作成する":::

   アプリケーションから直接新しいプロジェクトを作成することもできます。

1. **[ファイル]** メニューを選択します。
1. **[新規]** を選択します。
1. **[プロジェクト]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-create-new-project2.png" alt-text="[ファイル] メニューから新規プロジェクトを作成する":::

1. 一覧で Microsoft **Teams** アプリを検索します。
1. **[Microsoft Teams アプリ]** を選択します。
1. **[次へ]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app.png" alt-text="Microsoft Teams アプリを検索して選択する":::

1. **[プロジェクト名]** を選択し、プロジェクト名を入力します。
1. **[作成]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-project-name.png" alt-text="アプリケーションに名前を付ける":::

1. 作成する **Teams アプリの種類** を選択します。
1. **[作成]** を選択します。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Create-new-app-VS/vs-ms-teams-app-type.png" alt-text="Teams アプリの種類を選択する":::

## <a name="teams-app-templates-in-teams-toolkit-for-visual-studio"></a>Visual Studio 用 Teams ツールキットの Teams アプリ テンプレート

Teams ツールキットで、Teams アプリ テンプレートが既にさまざまな種類の Teams アプリ用に設定されていることがわかります。 次の表に、使用可能なすべてのテンプレートを示します。

|Teams アプリのテンプレート  |説明  |
|---------|---------|
|通知ボット     |通知ボット アプリは Teams クライアントに通知を送信できます。通知をトリガーする方法は複数あります。 たとえば、HTTP 要求または時間単位で通知をトリガーします。 また、ビジネス シナリオに基づいて通知のトリガーを選択することもできます。         |
|コマンド ボット     |ユーザーは、コマンドを入力してボットと対話するためにコマンド ボット アプリを使用できます。         |
|Tab     |タブ アプリは Teams 内に Web ページを表示し、Teams アカウントを使用してシングル サインオンを有効にします。         |
|メッセージ拡張機能     |メッセージ拡張機能アプリには、アダプティブ カードの作成、Nugget パッケージの検索、"dev.botframework.com" ドメインのリンクの展開などの簡単な機能が実装されています。         |

> [!NOTE]
>プロジェクトが作成されると、Teams ツールキットによって [作業の開始] が自動的に開きます。 ここで、[作業の開始] の手順を確認し、Teams ツールキットのさまざまな機能を確認できます。

## <a name="see-also"></a>関連項目

* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy-teams-app.md)
