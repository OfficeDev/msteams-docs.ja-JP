---
title: ボットを作成する
description: ボットを作成する方法について説明Microsoft Teams
ms.topic: how-to
keywords: teams ボットの作成
ms.localizationpriority: medium
ms.date: 12/07/2018
ms.openlocfilehash: 6898f6bf30c41cd5e373db323a0e5ce742129aa8
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453153"
---
# <a name="create-a-bot"></a>ボットを作成する

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

このツールを使用して作成Microsoft Bot Frameworkボットはすべて構成され、そのボットで作業Microsoft Teams。

詳細については、「 [Bot Framework Documentation for general information on bots](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) 」を参照してください。

## <a name="create-a-bot-for-microsoft-teams"></a>Microsoft Teams 用にボットを作成する

**Teams App Studio** は、ボットの作成に役立つツールであり、ボットを参照するアプリ パッケージです。 React 制御ライブラリとカード用の構成可能なサンプルも含まれています。 詳細については、「[Getting started with app Studio」をTeamsしてください](~/concepts/build-and-test/app-studio-overview.md)。 以下の手順では、ボットを手で構成し、App Studio を使用Teams **想定しています**。

1. ボット フレームワークを使用して [ボットを作成します](https://dev.botframework.com/bots/new)。 **ボットの作成後は必ず、おすすめのチャネル一覧に Microsoft Teams をチャネルとして登録します。** アプリ パッケージまたはマニフェストを既に作成した場合は、生成した Microsoft App ID はどれでも再利用できます。

   ![Bot Framework の登録ページ](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Azure でボットを作成しない場合は、このリンクを使用して新しいボット (Bot Framework) を[作成する必要があります](https://dev.botframework.com/bots/new)。 代わりにボット フレームワーク **ポータルで [** ボットの作成] をクリックすると、代わりにボット [Microsoft Azureされます。](#bots-and-microsoft-azure)

2. [Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)[ボット フレームワーク SDK](https://github.com/microsoft/botframework-sdk)、ボット コネクタ API を使用してボット[をビルドします](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)。

3. ボットをテストするには、次の[Bot Framework Emulator](/bot-framework/debug-bots-emulator)。

4. ボットをクラウド サービス (クラウド サービスなど) [に展開](https://azure.microsoft.com/)Microsoft Azure。 または、アプリをローカルで実行し、 [ngrok](https://ngrok.com) などのトンネリング サービスを使用して、ボット https:// エンドポイント (など) を公開します `https://45az0eb1.ngrok.io/api/messages`。

> [!NOTE]
>
> ## <a name="bots-and-microsoft-azure"></a>ボットとMicrosoft Azure
>
> 2017 年 12 月現在、ボット フレームワーク ポータルは、ボットを 2017 年 12 月に登録Microsoft Azure。 留意事項がいくつかあります。
>
> * Azure で登録したボット用の Microsoft Teams チャネルは無料です。 チャネルで送信Teams、ボットで使用されるメッセージにはカウントされません。
> * Azure を使用せずに新しい[](https://dev.botframework.com/bots/new)ボット フレームワーク ボットを作成することもできますが、ボット フレームワーク ポータルで公開[](https://dev.botframework.com/bots/new)されなくなった新しいボット フレームワーク ボットを作成する必要があります。
> * ボット フレームワークのボットの一覧にある既存のボットの[](https://dev.botframework.com/bots)プロパティ (特に [ngrok](https://ngrok.com) を使用する場合は特に、ボットの開発時に一般的な"メッセージング エンドポイント" など) を編集すると、"移行状態" 列と青い "移行" ボタンが表示され、Microsoft Azure ポータルに移動します。 [移行] ボタンをクリックしない場合は、実行する操作を行う必要があります。代わりに、ボットの名前をクリックすると、そのプロパティを編集できます。</br>
   ![ボットのプロパティを編集する](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * アプリを使用してボットを登録Microsoft Azure、ボット コードを *ホストする必要* Microsoft Azure。
> * Azure portal を使用してボットを登録する場合は、ユーザーアカウントMicrosoft Azureがあります。 このアカウントは[無料で作成](https://azure.microsoft.com/free/)できます。 ID を作成するときに確認するには、クレジット カードを提供する必要がありますが、課金されません。この機能を使用してボットを作成および使用する方法は、常にMicrosoft Teams。
> * App Studio を使用して、アプリとボットの情報をアプリ内で直接登録/更新Microsoft Teams。 Azure portal を使用して、Direct Line、Web チャット、Skype、Facebook Messenger などの他のボット フレームワーク チャネルを追加または構成する必要があります。

## <a name="see-also"></a>関連項目

[ボット フレームワークのサンプル](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
