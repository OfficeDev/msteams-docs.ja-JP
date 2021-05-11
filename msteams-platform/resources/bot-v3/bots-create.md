---
title: ボットを作成する
description: アプリでボットを作成する方法についてMicrosoft Teams
ms.topic: how-to
keywords: teams ボットの作成
localization_priority: Normal
ms.date: 12/07/2018
ms.openlocfilehash: 95e87538bf9c5c5883ef0b735b01070f0aea810a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019777"
---
# <a name="create-a-bot"></a>ボットを作成する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

このツールを使用して作成Microsoft Bot Frameworkボットは構成され、そのボットで作業Microsoft Teams。

ボットの [一般的な情報については、「Bot Framework の](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) ドキュメント」を参照してください。

## <a name="create-a-bot-for-microsoft-teams"></a>Microsoft Teams 用にボットを作成する

*Teams App Studio* は、ボットの作成に役立つツールであり、ボットを参照するアプリ パッケージです。 React 制御ライブラリとカード用の構成可能なサンプルも含まれています。 「[Teams App Studio を使う](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。 以下の手順では、ボットを手で構成し、App Studio を使用Teams *前提とします*。

1. 次のリンクを使用してボットを作成します https://dev.botframework.com/bots/new 。 **ボットの作成後は必ず、おすすめのチャネル一覧に Microsoft Teams をチャネルとして登録します。** アプリ パッケージまたはマニフェストを既に作成した場合は、生成した Microsoft App ID はどれでも再利用できます。

   ![Bot Framework の登録ページ](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Azure でボットを作成しない場合は、次のリンクを使用して新しいボットを作成する必要があります https://dev.botframework.com/bots/new 。 代わりにボット フレームワーク ポータルの *[* ボットの作成] ボタンをクリックすると、代わりにボット [Microsoft Azureされます。](#bots-and-microsoft-azure)

2. [Microsoft.Bot.Connector.Teams NuGet、Bot](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) [Framework SDK、](https://github.com/microsoft/botframework-sdk)またはボット コネクタ API を使用してボット[をビルドします](https://docs.microsoft.com/bot-framework/rest-api/bot-framework-rest-connector-api-reference)。 *「Bot* [Framework のサンプル」も参照してください](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

3. ボットをテストするには、[次の](https://docs.microsoft.com/bot-framework/debug-bots-emulator)Bot Framework Emulator。

4. ボットをクラウド サービス (クラウド サービスなど)[に展開](https://azure.microsoft.com/)Microsoft Azure。 または、アプリをローカルで実行し [、ngrok](https://ngrok.com) などのトンネリング サービスを使用して、ボット https:// エンドポイント (など) を公開します `https://45az0eb1.ngrok.io/api/messages` 。

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>ボットとMicrosoft Azure
> 2017 年 12 月現在、ボット フレームワーク ポータルは、ボットを 2017 年 12 月に登録Microsoft Azure。 留意事項がいくつかあります。
>
> * Azure で登録したボット用の Microsoft Teams チャネルは無料です。 チャネルで送信Teams、ボットで使用されるメッセージにはカウントされません。
> * Azure を使用せずに新しい [ボット フレームワーク](https://dev.botframework.com/bots/new) ボットを作成することもできますが、ボット フレームワーク ポータルで公開されなくなった URL ( を使用する https://dev.botframework.com/bots/new) 必要があります)。
> * ボット フレームワークのボットの一覧にある既存のボット[](https://dev.botframework.com/bots)のプロパティ (特に[ngrok](https://ngrok.com)を使用する場合は特に、ボットの開発時に一般的な"メッセージング エンドポイント" など) を編集すると、"移行状態" 列と青い "移行" ボタンが表示され、Microsoft Azure ポータルに移動します。 [移行] ボタンをクリックしない場合は、実行する操作を行う必要があります。代わりに、ボットの名前をクリックすると、そのプロパティを編集できます。</br>
   ![ボットのプロパティを編集する](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * アプリを使用してボットを登録Microsoft Azure、ボット コードをホストする必要Microsoft Azure。 
> * Microsoft Azure ポータルを使用してボットを登録する場合は、Microsoft Azure アカウントを持っている必要があります。 このアカウントは[無料で作成](https://azure.microsoft.com/free/)できます。 ID を作成するときに確認するには、クレジット カードを提供する必要がありますが、課金されません。ボットを作成して使用する場合は、常に無料でMicrosoft Teams。
> * App Studio を使用して、アプリとボットの情報をアプリ内で直接登録/更新Microsoft Teams。 Direct Line、Web Chat、Skype、Facebook Messenger などの他のボット フレームワーク チャネルを追加または構成するには、Microsoft Azure ポータルを使用する必要があります。
