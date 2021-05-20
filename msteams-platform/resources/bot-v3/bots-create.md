---
title: ボットを作成する
description: Microsoft Teamsでボットを作成する方法について説明します。
ms.topic: how-to
keywords: チームボットの作成
localization_priority: Normal
ms.date: 12/07/2018
ms.openlocfilehash: 67aa3e2cfd1950dced84785a9f6f35cfd4d5ff85
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566776"
---
# <a name="create-a-bot"></a>ボットを作成する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Bot Frameworkを使用して作成されたすべてのボットは構成され、Microsoft Teamsで動作する準備が整います。

詳細については、「ボットの一般的な情報」の [「Bot Framework ドキュメント」を参照してください](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) 。

## <a name="create-a-bot-for-microsoft-teams"></a>Microsoft Teams 用にボットを作成する

**Teamsアプリスタジオ** は、ボットの作成に役立つツールと、ボットを参照するアプリ パッケージです。 React 制御ライブラリとカード用の構成可能なサンプルも含まれています。 詳細については、「[アプリケーションスタジオの概要Teams](~/concepts/build-and-test/app-studio-overview.md)参照してください。 以下の手順では、ボットを手で構成し **、App Studio を** 使用していないことを前提Teams。

1. このリンクを使用してボットを作成 https://dev.botframework.com/bots/new します。 **ボットの作成後は必ず、おすすめのチャネル一覧に Microsoft Teams をチャネルとして登録します。** アプリ パッケージまたはマニフェストを既に作成した場合は、生成した Microsoft App ID はどれでも再利用できます。

   ![Bot Framework の登録ページ](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Azure でボットを作成しない場合は、このリンクを使用して新しいボットを作成 **する必要があります** https://dev.botframework.com/bots/new 。 [Bot Framework ポータルで **ボットを作成** する] をクリックすると、代わりに [Microsoft Azureでボットを作成します](#bots-and-microsoft-azure)。

2. NuGet パッケージ[、Teams ボット](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)フレームワーク SDK 、または[ボット コネクタ API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)を使用して[ボット](https://github.com/microsoft/botframework-sdk)をビルドします。

3. [Bot Framework Emulator](/bot-framework/debug-bots-emulator)を使用してボットをテストします。

4. Microsoft Azure[などのクラウド](https://azure.microsoft.com/)サービスにボットを展開します。 または、アプリをローカルで実行し [、ngrok](https://ngrok.com) などのトンネリング サービスを使用して、ボットの https:// エンドポイントを公開 `https://45az0eb1.ngrok.io/api/messages` します。

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>ボットとMicrosoft Azure
> 2017 年 12 月現在、bot Framework ポータルは、Microsoft Azureでのボットの登録に最適化されています。 留意事項がいくつかあります。
>
> * Azure で登録したボット用の Microsoft Teams チャネルは無料です。 Teams チャネルを介して送信されたメッセージは、ボットで使用されたメッセージにはカウントされません。
> * Azure を使用せずに [新しいボット フレームワーク ボットを作成](https://dev.botframework.com/bots/new) することはできますが、その URL https://dev.botframework.com/bots/new) ( はボット フレームワーク ポータルで公開されなくなった URL) を使用する必要があります。
> * ボットを最初に開発するときに一般的な 「メッセージング エンドポイント」など、[ボットのリストにある既存のボットの](https://dev.botframework.com/bots)プロパティを編集すると、特に[ngrok](https://ngrok.com)を使用すると、"移行状態" 列と青い [移行] ボタンが表示され、Microsoft Azure ポータルに移動します。 あなたがやりたいことがない限り、「移行」ボタンをクリックしないでください。代わりに、ボットの名前をクリックして、そのプロパティを編集することができます。</br>
   ![ボットのプロパティを編集する](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Microsoft Azureを使用してボットを登録する場合、ボット コードをMicrosoft Azureで *ホスト* する必要はありません。
> * Microsoft Azure ポータルを使用してボットを登録する場合は、Microsoft Azure アカウントを持っている必要があります。 このアカウントは[無料で作成](https://azure.microsoft.com/free/)できます。 作成時に身元を確認するには、クレジットカードを提供する必要がありますが、課金されません。Microsoft Teamsでボットを作成して使用することは常に無料です。
> * アプリスタジオを使用して、Microsoft Teams内で直接アプリやボットの情報を登録/更新できるようになりました。 ダイレクトライン、Webチャット、Skype、Facebookメッセンジャーなどの他のBot Frameworkチャンネルを追加または設定するには、Microsoft Azureポータルを使用するだけです。

## <a name="see-also"></a>関連項目

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)