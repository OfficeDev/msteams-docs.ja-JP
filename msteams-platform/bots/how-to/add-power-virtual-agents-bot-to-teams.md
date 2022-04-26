---
title: Power Virtual Agents チャットボットを Teams に追加する
author: surbhigupta
description: Power Virtual Agents チャットボットを Teams プラットフォームに統合して、会話型チャットボットを作成し、Teams と統合する方法の詳細
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: a95b3fe3b9191facc2554262444bc4b558c372ed
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453839"
---
# <a name="add-power-virtual-agents-chatbot"></a>Power Virtual Agents チャットボットを追加する

Power Virtual Agents は、コード不要のガイド付きグラフィカル インターフェイス ソリューションであり、チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できるリッチで会話型のチャットボットを作成できるようにします。 Power Virtual Agents で作成されたすべてのコンテンツは、Teams で自然にレンダリングされます。 Power Virtual Agents ボットは、Teams のネイティブ チャット キャンバスでユーザーとやり取りします。 IT 管理者、ビジネス アナリスト、ドメイン スペシャリスト、および熟練したアプリ開発者は、開発環境をセットアップしなくても、Teams 用のインテリジェントな仮想エージェントを設計、開発、および公開できます。 Web サービスを作成することも、ボット フレームワークに直接登録することもできます。

このドキュメントでは、Power Virtual Agents ポータルを通じて Teams でチャットボットを利用できるようにする方法と、App Studio を使用してボットを Teams に追加する方法について説明します。

Power Virtual Agents を使用すると、顧客、他の従業員、または Web サイトやサービスへの訪問者からの質問に答えることができる強力なチャットボットを作成できます。

これらのボットは、データ サイエンティストや開発者を必要とせずに、簡単に作成できます。

> [!NOTE]
> * チャットボットを Microsoft Teams に追加することにより、ボット コンテンツやユーザー チャット コンテンツなどの一部のデータが Microsoft Teams と共有されます。 これは、データが[組織のコンプライアンスおよび地理的または地域的な境界](/power-virtual-agents/data-location)の外に流れることを意味します。 <br/>
> * Teams アプリ ストアに公開するアプリを作成するために Microsoft Power Platform を使用しないでください。 Microsoft Power Platform アプリは、組織のアプリ ストアにのみ公開できます。

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a>Power Virtual Agents ポータルを通じて Teams でチャットボットを利用できるようにする

Power Virtual Agents ポータルを通じて Teams でチャットボットを利用できるようにするには、次のプロセス手順を実行する必要があります。

Teams でチャットボットを利用できるようにするには:

1. **最新のボット コンテンツを公開する**  
Power Virtual Agents ポータルでチャットボットを作成した後、Teams ユーザーが操作する前に、ボットを公開する必要があります。 詳細については、「[最新のボット コンテンツを公開する](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)」を参照してください。

   ![Power Virtual Agents ポータルで公開する](../../assets/images/pva-publish.png)

1. **Teams チャネルを構成する**  
ボットを公開したら、Teams チャネルを追加して、Teams ユーザーがボットを利用できるようにします。

   ![Power Virtual Agents ポータルのチャネル](../../assets/images/pva-channels.png)

1. **チャットボットのアプリ ID を生成する**  
Teams チャネルをチャットボットに追加すると、ダイアログ ボックスに **アプリ ID** が生成されます。 アプリ ID は、ボットに対して Microsoft が生成した一意の識別子です。 アプリ ID を保存して、Teams 用のアプリ パッケージを作成します。

## <a name="add-your-bot-to-teams-using-app-studio"></a>App Studio を使用してボットを Teams に追加する

Teams インスタンスで[カスタム アプリのアップロードが有効になっている](/microsoftteams/admin-settings)場合は、Teams App Studio を使用してチャットボットを直接アップロードし、すぐに使用を開始できます。 チャットボットを共有するには、管理者にボットをテナント アプリ カタログで利用できるように要求するか、アプリ パッケージを他のユーザーに送信して、個別にアップロードするように依頼することができます。

1. **Teams に App Studio をインストールする**  
App Studio は Teams アプリです。 Teams ストアから App Studio をインストールします。これにより、Teams でのボットの作成と登録のプロセスが簡素化されます。

   1. Teams インスタンスからアプリ ストア アイコンを選択し、**App Studio** を検索します。

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>

   1. **App Studio** タイルを選択し、ポップアップ ダイアログ ボックスで **[インストール]** を選択します。

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. **App Studio で Teams アプリ マニフェストを作成する**  
Teams のボットは、ボットとその機能に関する基本情報を提供するアプリ マニフェスト JSON ファイルによって定義されます。 **App Studio** で、**[マニフェスト エディター]** を選択し、**[新しいアプリの作成]** を選択します。

    ![新しいアプリを作成する](../../assets/images/get-started/create-new-app.png)

1. **ボットの詳細を追加する**  
すべての必須フィールドに入力します。 各フィールドの詳細については、[マニフェスト スキーマ定義](../../resources/schema/manifest-schema.md)を参照してください。

    ![アプリの詳細を追加する](../../assets/images/get-started/add-app-details.png)

1. **ボットを設定する** ボットを設定するには、次の手順に従います。
     1. **[ボット]** タブを開きます。
     1. **[セットアップ]** > **[既存のボット]** の順に選択し、ボットの名前を入力します。

   ![ボットのセットアップ](../../assets/images/get-started/bot-set-up.png)

   次の画像は、既存のボットを設定する方法を示しています。

   ![既存のボットのセットアップ](../../assets/images/get-started/existing-bot-set-up.png)

1. **アプリ ID を追加する**  
アプリ ID を追加するには、次の手順を実行します。  
    1. **[別のボット ID に接続]** を選択し、前にコピーした **アプリ ID** を貼り付けます。
    1. **[スコープ]** > **[個人用]** > **[保存]** の順に選択します。

    ![アプリ ID を追加する](../../assets/images/get-started/add-app-id.png)

1. **ボットの有効なドメインを追加する**  
この手順は、ボットがユーザーにサインインを要求する場合にのみ必要です。 **[ドメインとアクセス許可]** を選択し、**[有効なドメイン]** フィールドに次の入力を行います。

    ```bash
       token.botframework.com
    ```

1. **ボットをテストして配布する**  
**[テストと配布]** タブを開き、**[インストール]** を選択して、ボットを Teams インスタンスに直接追加します。 または、完成したアプリ パッケージをダウンロードして Teams ユーザーと共有したり、管理者に提供してボットをテナント アプリ カタログで利用できるようにすることもできます。

1. **チャットを開始する** Power Virtual Agents チャットボットを Teams に追加するためのセットアップ プロセスが完了しました。 これで、個人用チャットでボットとの会話を開始できます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [仮想アシスタントを作成する](~/samples/virtual-assistant.md)

## <a name="see-also"></a>関連項目

* [Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  
* [Microsoft Power Virtual Agent を使用してTeams用のチャット ボットを作成する](../bot-features.md#bots-with-power-virtual-agents)
* [Power Virtual Agents ポータル](https://powervirtualagents.microsoft.com)
* [Power Virtual Agents ボットを公開する](/power-virtual-agents/publication-fundamentals-publish-channels)
* [Microsoft Teams のセキュリティとコンプライアンス](/MicrosoftTeams/security-compliance-overview)
