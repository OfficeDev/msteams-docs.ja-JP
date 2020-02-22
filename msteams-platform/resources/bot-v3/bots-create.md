---
title: ボットの作成
description: Microsoft Teams でボットを作成する方法について説明します。
keywords: teams のボットの作成
ms.date: 12/07/2018
ms.openlocfilehash: 6d8441cb3bc89ae7a923cad72567eb52dd99dc4b
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228018"
---
# <a name="create-a-bot"></a>ボットの作成

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Bot フレームワークを使用して作成されたすべての bot が構成され、Microsoft Teams で作業できるようになります。

Bot の一般的な情報については、[ボットフレームワークのドキュメント](/azure/bot-service/?view=azure-bot-service-3.0)を参照してください。

## <a name="create-a-bot-for-microsoft-teams"></a>Microsoft Teams 用にボットを作成する

*Teams App Studio*は、ボットを作成するのに役立つツールで、ボットを参照するアプリパッケージです。 React 制御ライブラリとカード用の構成可能なサンプルも含まれています。 「[Teams App Studio を使う](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。 次の手順は、 *Teams アプリ*を使用せずに bot を手動で構成することを前提としています。

1. このリンクhttps://dev.botframework.com/bots/newを使用して bot を作成します。 **ボットの作成後は必ず、おすすめのチャネル一覧に Microsoft Teams をチャネルとして登録します。** アプリ パッケージまたはマニフェストを既に作成した場合は、生成した Microsoft App ID はどれでも再利用できます。

   ![Bot Framework の登録ページ](~/assets/images/bots/bfregister.png)

> [!NOTE]
> ボットを Azure に作成しない場合は、このリンクを使用して新しい bot https://dev.botframework.com/bots/newを作成する**必要があり**ます。 Bot フレームワークポータルで [ *bot の作成*] ボタンをクリックすると、代わりに[Microsoft Azure に bot が作成](#bots-and-microsoft-azure)されます。

2. [Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージ、 [bot フレームワーク SDK](https://github.com/microsoft/botframework-sdk)、または[bot コネクタ API](https://docs.microsoft.com/bot-framework/rest-api/bot-framework-rest-connector-api-reference)を使用して bot をビルドします。 [Bot フレームワークサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)*も参照してください*。

3. [Bot フレームワークエミュレーター](https://docs.microsoft.com/bot-framework/debug-bots-emulator)を使用して bot をテストします。

4. Bot を[Microsoft Azure](https://azure.microsoft.com/)などのクラウドサービスに展開します。 または、アプリをローカルで実行し、 [ngrok](https://ngrok.com)などのトンネリングサービスを使用して、などの bot の`https://45az0eb1.ngrok.io/api/messages`https://エンドポイントを公開します。

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>ボットと Microsoft Azure
> 2017年12月の場合、Bot フレームワークポータルは Microsoft Azure でボットを登録するために最適化されています。 留意事項がいくつかあります。
>
> * Azure で登録したボット用の Microsoft Teams チャネルは無料です。 Teams チャネルを介して送信されるメッセージは、bot の使用されたメッセージにカウントされません。
> * Azure を使用せずに[新しい Bot フレームワーク Bot を作成](https://dev.botframework.com/bots/new)することは可能ですが、その URLhttps://dev.botframework.com/bots/new)を使用する必要があります (これは bot フレームワークポータルで公開されなくなりました)。
> * 最初に bot を開発する際によくあるボットの[リスト](https://dev.botframework.com/bots)にある既存の bot のプロパティを編集すると、特に[ngrok](https://ngrok.com)を使用している場合は、[移行の状態] 列と青い [移行] ボタンが表示され、Microsoft Azure portal に移動します。 目的の操作を行わない限り、[移行] ボタンをクリックしないでください。代わりに、bot の名前をクリックすると、そのプロパティを編集できます。</br>
   ![ボットのプロパティを編集する](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Microsoft Azure を使用して bot を登録した場合、ボットコードを Microsoft Azure で*ホスト*する必要はありません。
> * Microsoft Azure ポータルを使用してボットを登録する場合は、Microsoft Azure アカウントを持っている必要があります。 このアカウントは[無料で作成](https://azure.microsoft.com/free/)できます。 Id を作成するときに身元を確認するには、クレジットカードを指定する必要がありますが、請求されません。Microsoft Teams でボットを作成して使用することは常に自由です。
> * アプリ Studio を使用して、Microsoft Teams 内でアプリと bot 情報を直接登録または更新できるようになりました。 直接回線、Web チャット、Skype、Facebook Messenger など、他の Bot フレームワークチャネルを追加または構成する場合にのみ、Microsoft Azure ポータルを使用する必要があります。
