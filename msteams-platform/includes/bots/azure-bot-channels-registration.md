---
title: Azure ボット チャネル登録
description: 登録用の Azure ボット チャネルについて説明します
localization_priority: Normal
ms.topic: overview
ms.author: surbhigupta12
ms.openlocfilehash: 3cbbd204daf98f1c3528dcb6efcfde299a402912
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020950"
---
1. Azure ポータル [の [Azure サービス](https://ms.portal.azure.com/#home)] で、[リソースの作成] **を選択します**。
1. 検索ボックスに「bot」と入力します。 ドロップダウン リストで、[ボット チャネル登録] **を選択します**。
1. [作成] **ボタンを選択** します。
1. [ボット チャネル **登録] ブレード** で、ボットに関する要求された情報を入力します。
1. [メッセージング **エンドポイント] ボックスを** 空のままにしておき、ボットの展開後に必要な URL を入力します。 次の図は、登録設定の例を示しています。

    ![ボット アプリ チャネルの登録](../../assets/images/authentication/auth-bot-channels-registration.png)

1. [Microsoft **App ID とパスワード] をクリックし、[** 新規作成 **] をクリックします**。

    ![Create Microsoft App ID ](../../assets/images/authentication/CreateMicrosoftAppID.png) ![ Create New Microsoft App ID](../../assets/images/authentication/CreateNewMicrosoftAppID.png)    

1. [アプリ **登録ポータル] リンクの [アプリ ID の作成] を** クリックします。

   ![アプリの登録](../../assets/images/authentication/AppRegistration.png)
   
1. 表示されたアプリ **登録ウィンドウで** 、左上の **[新規登録** ] タブをクリックします。
1. 登録するボット アプリケーションの名前を入力します *。BotTeamsAuth* を使用しました (独自の一意の名前を選択する必要があります)。
1. [サポートされている **アカウント** の種類] で、[任意の組織ディレクトリのアカウント] ([任意の Azure AD ディレクトリ - マルチテナント] と個人用 Microsoft アカウント *(Skype、Xbox など) を* 選択します。
1. [登録] **ボタンをクリック** します。 完了すると、Azure はアプリケーションの *[概要* ] ページを表示します。
1. アプリケーション (クライアント) ID 値 **をファイルにコピーして保存** します。
1. 左側のパネルで、[証明書とシークレット **] をクリックします**。
    1. [ *クライアント シークレット] で、[* 新しい **クライアント シークレット] をクリックします**。
    1. このアプリ用に作成する必要がある他のユーザーからこのシークレットを識別するための説明を追加します。
    1. [ *有効期限] を選択* に設定します。
    1. **[追加]** をクリックします。
    1. クライアント シークレットをコピーし、ファイルに保存します。
1. [ボット チャネル登録 **] ウィンドウ** に戻り、アプリ IDとクライアント シークレットをそれぞれ [Microsoft アプリ *ID]* ボックスと **[** パスワード] ボックスにコピーします。 
1. [**OK**] をクリックします。
1. 最後に、[作成] を **クリックします**。

Azure が登録リソースを作成すると、リソース グループの一覧に含まれます。  

![ボット アプリ チャネル登録グループ](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

ボット チャネルの登録が作成されると、ボット チャネルを有効Teamsがあります。

1. Azure ポータル [の [Azure](https://ms.portal.azure.com/#home)サービス] で、作成 **したボット チャネル登録** を選択します。
1. 左側のパネルで、[チャネル] を **クリックします**。
1. [保存] Microsoft Teamsクリックし、[保存] を **選択します**。
