---
title: チャットボットPower Virtual Agentsを追加Teams
author: surbhigupta
description: チャットボットをPower Virtual Agentsプラットフォームに統合Teamsする
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: 5a4aa24ceb5a73be56cfd069b02ca7b980d17055
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156870"
---
# <a name="add-power-virtual-agents-chatbot"></a>Power Virtual Agents チャットボットを追加する 

Power Virtual Agentsはコードなしガイド付きグラフィカル インターフェイス ソリューションで、チームのすべてのメンバーが、Teams プラットフォームと簡単に統合できるリッチで会話型のチャットボットを作成できます。 このドキュメントで作成Power Virtual Agentsコンテンツはすべて、Teams。 Power Virtual Agentsボットは、ネイティブ チャット キャンバスTeamsユーザーと対話します。 IT 管理者、ビジネス アナリスト、ドメイン スペシャリスト、および熟練したアプリ開発者は、開発環境をセットアップすることなく、Teams 用のインテリジェント仮想エージェントを設計、開発、発行できます。 Web サービスを作成したり、ボット フレームワークに直接登録することができます。 

このドキュメントでは、Teams ポータルを通じてチャットボットを Teams で利用し、Power Virtual Agents App Studio を使用してボットを Teams追加する方法についてガイドします。 

Power Virtual Agentsを使用すると、顧客、他の従業員、または Web サイトやサービスへの訪問者から得た質問に答える強力なチャットボットを作成できます。

これらのボットは、データ サイエンティストや開発者を必要とせずに簡単に作成できます。

> [!NOTE]
> チャットボットを Microsoft Teamsに追加すると、ボット コンテンツやユーザー チャット コンテンツなどの一部のデータがユーザーと共有Microsoft Teams。 つまり、データは組織のコンプライアンスや地理的または地域的な境界の外 [に流れます](/power-virtual-agents/data-location)。 <br/>

## <a name="make-your-chatbot-available-in-teams-through-the-power-virtual-agents-portal"></a>チャットボットをポータルからTeams利用Power Virtual Agentsする

チャットボットを TeamsポータルでPower Virtual Agentsするには、次のプロセス手順を実行する必要があります。

**チャットボットをチャット ボットで使用Teams**

1. **最新のボット コンテンツを発行する**  
ポータルでチャットボットを作成Power Virtual Agents、ユーザーがボットを操作する前Teamsボットを発行する必要があります。 詳細については、「最新のボット [コンテンツを発行する」を参照してください](/power-virtual-agents/publication-fundamentals-publish-channels#publish-the-latest-bot-content)。

   ![Power Virtual Agents ポータルで発行する](../../assets/images/pva-publish.png)

1. **チャネルの構成Teamsする**  
ボットを発行した後、Teamsチャネルを追加して、ユーザーがボットをTeamsします。

   ![電源仮想エージェント ポータルのチャネル](../../assets/images/pva-channels.png)

1. **チャットボットのアプリ ID を生成する**  
チャットボットにTeamsを追加すると、ダイアログ ボックスにアプリ **ID** が生成されます。 アプリ ID は、ボットの Microsoft が生成した一意の識別子です。 アプリ ID を保存して、アプリ パッケージを作成Teams。

## <a name="add-your-bot-to-teams-using-app-studio"></a>App Studio を使用Teamsボットを追加する

カスタム[アプリのアップロード](/microsoftteams/admin-settings)が Teams インスタンスで有効になっている場合は、Teams App Studio を使用してチャットボットを直接アップロードし、すぐに使用を開始できます。 チャットボットを共有するには、管理者に、テナント アプリ カタログでボットを利用できるよう要求するか、アプリ パッケージを他のユーザーに送信し、個別にアップロードを依頼できます。

1. **Teams に App Studio をインストールする**  
App Studio は、Teamsアプリです。 アプリ ストアから App Studio をTeamsし、ボットの作成と登録のプロセスを簡略化Teams。 

   1. インスタンスからアプリ ストア アイコンを選択Teams App Studio **を検索します**。

      &emsp;&emsp; <img  width="450px" alt="Finding App Studio in the Store" src="../../assets/images/get-started/app-studio-store.png"/>   

   1. [App **Studio] タイルを** 選択し **、ポップアップ** ダイアログ ボックスで [インストール] を選択します。

      &emsp;&emsp; <img  width="450px" alt="Installing App Studio" src="../../assets/images/get-started/app-studio-install.png"/>

1. **App Studio でTeamsアプリ マニフェストを作成する**  
アプリ内のボットTeams、ボットとその機能に関する基本情報を提供するアプリ マニフェスト JSON ファイルによって定義されます。 **App Studio で、[マニフェスト** エディター]**を選択し**、[新しい **アプリの作成] を選択します**。

    ![新しいアプリを作成する](../../assets/images/get-started/create-new-app.png)

1. **ボットの詳細を追加する**  
必要なすべてのフィールドに入力します。 各フィールドの詳細については、「マニフェスト スキーマ定義 [」を参照してください](../../resources/schema/manifest-schema.md)。

    ![アプリの詳細を追加する](../../assets/images/get-started/add-app-details.png)

1. **ボットをセットアップする** ボットをセットアップするには、次の手順を実行します。 
     1. [ボット **] タブを開** きます。 
     1. [**既存**  >  **のボットのセットアップ] を** 選択し、ボットの名前を入力します。

   ![ボットのセットアップ](../../assets/images/get-started/bot-set-up.png) 

   次の図は、既存のボットをセットアップする方法を示しています。      

   ![既存のボットのセットアップ](../../assets/images/get-started/existing-bot-set-up.png)
       
1. **アプリ ID の追加**  
アプリ ID を追加するには、次の手順を実行します。  
    1. **[Connectボット ID にコピーし、** 前にコピーした **アプリ ID** を貼り付けます。 
    1. [スコープ **個人用保存**  >  **]**  >  **を選択します**。

    ![アプリ ID の追加](../../assets/images/get-started/add-app-id.png)

1. **ボットに有効なドメインを追加する**  
この手順は、ボットがユーザーにサインインを要求する場合にのみ必要です。 [ **ドメインとアクセス許可] を選択し** 、[有効な **ドメイン** ] フィールドで、次の入力を入力します。

    ```bash
       token.botframework.com
    ```

1. **ボットのテストと配布**  
[**テストと配布] タブを** 開き、[**インストール]** を選択して、ボットをインスタンスに直接Teamsします。 または、完成したアプリ パッケージをダウンロードして、Teams ユーザーと共有したり、管理者に提供して、テナント アプリ カタログでボットを利用したりすることもできます。

1. **チャットを開始する**   
チャット ボットをチャット ボットに追加Power Virtual Agentsセットアップ プロセスTeams完了です。 これで、個人用チャットでボットとの会話を開始できます。

## <a name="see-also"></a>関連項目

* [Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)  
* [Microsoft アカウントを使用して、TeamsチャットボットをPower Virtual Agents。](../bot-features.md#bots-with-power-virtual-agents)  
* [Power Virtual Agents ポータル](https://powervirtualagents.microsoft.com)
* [ボットをPower Virtual Agentsする](/power-virtual-agents/publication-fundamentals-publish-channels)
* [セキュリティとコンプライアンスのMicrosoft Teams。](/MicrosoftTeams/security-compliance-overview)

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [仮想アシスタントを作成する](~/samples/virtual-assistant.md)
