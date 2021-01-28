---
title: ボットを作成する
description: Microsoft Teams でボットを作成する方法について説明します。
ms.topic: how-to
keywords: チーム ボットの作成
ms.date: 12/07/2018
ms.openlocfilehash: d7c618adc99f814bd677e919923c4b616f293e17
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014090"
---
# <a name="create-a-bot"></a>ボットを作成する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Bot Framework を使用して作成されたボットはすべて構成され、Microsoft Teams で作業する準備が整っています。

ボットに関 [する一般的な情報については、Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0) のドキュメントを参照してください。

## <a name="create-a-bot-for-microsoft-teams"></a>Microsoft Teams 用にボットを作成する

*Teams App Studio* は、ボットの作成に役立つツールであり、ボットを参照するアプリ パッケージです。 React 制御ライブラリとカード用の構成可能なサンプルも含まれています。 「[Teams App Studio を使う](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。 以下の手順では、Teams App Studio を使用してではなく、ボットを手で *構成している必要があります*。

1. 次のリンクを使用してボットを作成します https://dev.botframework.com/bots/new 。 **ボットの作成後は必ず、おすすめのチャネル一覧に Microsoft Teams をチャネルとして登録します。** アプリ パッケージまたはマニフェストを既に作成した場合は、生成した Microsoft App ID はどれでも再利用できます。

   ![Bot Framework の登録ページ](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Azure でボットを作成しない場合は、このリンクを使用して新しいボットを作成する必要があります https://dev.botframework.com/bots/new 。 代わりに Bot  Framework ポータルの [ボットの作成] ボタンをクリックすると、代わりに[Microsoft Azure](#bots-and-microsoft-azure)でボットが作成されます。

2. [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet パッケージ[、Bot Framework SDK、](https://github.com/microsoft/botframework-sdk)または Bot Connector API を使用してボット[をビルドします](https://docs.microsoft.com/bot-framework/rest-api/bot-framework-rest-connector-api-reference)。 *Bot* Framework の [サンプルも参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

3. Bot Framework エミュレーターを使用して [ボットをテストします](https://docs.microsoft.com/bot-framework/debug-bots-emulator)。

4. Microsoft Azure などのクラウド サービスにボットを [展開します](https://azure.microsoft.com/)。 または、アプリをローカルで実行し [、ngrok](https://ngrok.com) などのトンネリング サービスを使用して、ボットの https:// エンドポイントを公開します `https://45az0eb1.ngrok.io/api/messages` 。

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>ボットと Microsoft Azure
> 2017 年 12 月の現在、Bot Framework ポータルは Microsoft Azure にボットを登録するように最適化されています。 留意事項がいくつかあります。
>
> * Azure で登録したボット用の Microsoft Teams チャネルは無料です。 Teams チャネルを使用して送信されたメッセージは、ボットで使用されたメッセージにはカウントされません。
> * Azure を使用せずに新しい [Bot Framework](https://dev.botframework.com/bots/new) ボットを作成することもできますが、その URL (Bot Framework ポータルでは公開されなくなった URL) を使用する https://dev.botframework.com/bots/new) 必要があります。
> * Bot [Framework](https://dev.botframework.com/bots) のボットの一覧にある既存のボットのプロパティ ("メッセージング エンドポイント" など) を編集すると、最初にボットを開発するときによく使用されます。特に [ngrok](https://ngrok.com)を使用する場合は、"移行状態" 列と青色の [移行] ボタンが表示され、Microsoft Azure Portal に移動します。 [移行] ボタンをクリックしない場合は、この操作を行います。代わりに、ボットの名前をクリックすると、そのプロパティを編集できます。</br>
   ![ボットのプロパティを編集する](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Microsoft Azure を使用してボットを登録する場合、ボット コードを Microsoft Azure でホスト *する* 必要はありません。
> * Microsoft Azure ポータルを使用してボットを登録する場合は、Microsoft Azure アカウントを持っている必要があります。 このアカウントは[無料で作成](https://azure.microsoft.com/free/)できます。 ID を作成するときに ID を確認するには、クレジット カードを提供する必要がありますが、請求はされません。Microsoft Teams でボットを作成して使用する方法は常に自由です。
> * App Studio を使用して、Microsoft Teams 内で直接アプリとボットの情報を登録/更新できます。 You'll only have to use the Microsoft Azure portal for adding/configuring other Bot Framework channels such as Direct Line, Web Chat, Skype, and Facebook Messenger.
