---
title: ボットを作成する
description: このモジュールでは、Microsoft Bot Frameworkを使用してボットを作成し、Microsoft Teams で作業する準備をする方法について説明します
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 12/07/2018
ms.openlocfilehash: 66b0557308e2d76332e1a5b0fcba06ac596822c4
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2022
ms.locfileid: "67312101"
---
# <a name="create-a-bot"></a>ボットを作成する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Bot Framework を使用して作成されたすべてのボットは構成済みであり、Microsoft Teams で動作する準備ができています。

詳細については、 ボットに関する一般的な情報のための「[Bot Framework ドキュメント](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true)」を参照してください。

## <a name="create-a-bot-for-microsoft-teams"></a>Microsoft Teams 用にボットを作成する

**Teams 開発者ポータル** は、ボットの作成に役立つツールであり、ボットを参照するアプリ パッケージです。 React 制御ライブラリとカード用の構成可能なサンプルも含まれています。 詳細については、「 [Teams 開発者ポータル for Teams の概要](~/concepts/build-and-test/teams-developer-portal.md)」を参照してください。 次の手順は、 **Teams 用 Teams 開発者ポータル** を使用せず、ボットを手動で構成していることを前提としています。

1. [Bot Framework](https://dev.botframework.com/bots/new) を使用してボットを作成します。 **ボットの作成後は必ず、おすすめのチャネル一覧に Microsoft Teams をチャネルとして登録します。** アプリ パッケージまたはマニフェストを既に作成した場合は、生成した Microsoft App ID はどれでも再利用できます。

   ![Bot Framework の登録ページ](~/assets/images/bots/bfregister.png)

> [!NOTE]
> ボットを Azure で作成しない場合は、こちらのリンクを使用して新しいボットを作成する **必要があります** ([Bot Framework](https://dev.botframework.com/bots/new))。 代わりに、Bot Framework ポータルで **[ボットを作成する]** をクリックすると、代わりに [Microsoft Azure でボットが作成](#bots-and-microsoft-azure)されます。

2. [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージ、[Bot Framework SDK](https://github.com/microsoft/botframework-sdk)、または [Bot Connector API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference) を使用してボットをビルドします。

3. [Bot Framework Emulator](/bot-framework/debug-bots-emulator) を使用してボットをテストします。

4. [Microsoft Azure](https://azure.microsoft.com/) などのクラウド サービスにボットをデプロイします。 または、アプリをローカルで実行し、[ngrok](https://ngrok.com) などのトンネリング サービスを使用して、`https://45az0eb1.ngrok.io/api/messages` など、ボットの https:// エンドポイントを公開します。

> [!NOTE]
>
> ## <a name="bots-and-microsoft-azure"></a>ボットと Microsoft Azure
>
> 2017 年 12 月の時点で、Bot Framework ポータルは、Microsoft Azure でのボットの登録に最適化されています。 留意事項がいくつかあります。
>
> * Azure で登録したボット用の Microsoft Teams チャネルは無料です。 Teams チャネル経由で送信されるメッセージは、ボットの消費メッセージとしてはカウントされません。
> * Azure を使用せずに[新しい Bot Framework ボットの作成](https://dev.botframework.com/bots/new)は可能ですが、Bot Framework ポータルで公開されなくなった、[新しい Bot Framework ボットの作成](https://dev.botframework.com/bots/new)を使用する必要があります。
> * [Bot Framework 内のボットのリスト](https://dev.botframework.com/bots)で既存のボットのプロパティを編集する際、特に [ngrok](https://ngrok.com) を使用している場合、ボットを初めて開発するときに一般的な "メッセージングエンドポイント" などを編集すると、[移行の状態] 列と青い [移行] ボタンが表示され、Microsoft Azure portal に移動します。 必要な場合を除き、[移行] ボタンをクリックしないでください。代わりに、ボットの名前をクリックすると、そのプロパティを編集できます。</br>
   ![ボットのプロパティを編集する](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Microsoft Azure を使用してボットを登録する場合、ボット コードは Microsoft Azure で *ホストされる* 必要はあります。
> * Azure ポータルを使用してボットを登録する場合は、Microsoft Azure アカウントを持っている必要があります。 このアカウントは[無料で作成](https://azure.microsoft.com/free/)できます。 作成時に ID を確認するには、クレジット カードを指定する必要がありますが、料金は発生しません。Teams でボットを作成して使用することは常に自由です。
> * 開発者ポータル for Teams を使用して、Teams 内でアプリとボットの情報を直接登録/更新できるようになりました。 Direct Line、Web チャット、Skype、Facebook Messenger などの他のBot Framework チャネルを追加または構成する場合にのみ、Azure portal を使用する必要があります。

## <a name="see-also"></a>関連項目

[Bot Framework サンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
