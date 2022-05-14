---
title: カスタム アプリをアップロードする
description: Microsoft Teams でアプリをサイドロードする方法について説明します。 サイドローディングは、開発中にアプリをテストおよびデバッグするときに一般的です。
ms.topic: how-to
author: surbhigupta
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 5929b98d055d8a4b180df55f4298f12a617040c9
ms.sourcegitcommit: 05285653b2548e0b39e788cd07d414ac87ba3eaf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2022
ms.locfileid: "65191202"
---
# <a name="upload-your-app-in-microsoft-teams"></a>Microsoft Teams でアプリをアップロードする

組織または Teams ストアに公開しなくても、Microsoft Teams アプリを脇で発行できます。これは、以下のシナリオで有効です:

* アプリをローカルで、または他の開発者とテストしてデバッグする必要があります。
* ワークフローを自動化するために、自分用のアプリを構築しました。
* 作業グループなど、少数のユーザー向けのアプリを作成しました。

> [!IMPORTANT]
> 現時点では、サイドローディング アプリは Government Community Cloud (GCC) で利用できますが、GCC-High および国防総省 (DOD) では使用できません。

## <a name="prerequisites"></a>前提条件

* [アプリ パッケージ](~/concepts/build-and-test/apps-package.md)を作成し、[アプリ パッケージを検証](https://dev.teams.microsoft.com/appvalidation.html)することを確かめて下さい。
* Teams で[カスタム アプリのアップロード を有効](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)にします。
* アプリが実行されていて、HTTP 経由でアクセスできることを確認してください。

## <a name="upload-your-app"></a>アプリをアップロードする

アプリのスコープの構成方法に応じて、チーム、チャット、会議、または個人用にアプリをサイドロードできます。

1. [Microsoft 365開発アカウント](https://developer.microsoft.com/en-us/microsoft-365/dev-program)を使用して Teams クライアントにログインします。
1. **[アプリ]** > **[アプリの管理]** と **[アプリの公開]** を選択します。

    :::image type="content" source="~/assets/images/publish-app/manage-apps.png" alt-text="アプリを発行します。" border="true":::

1. **[カスタム アプリをアップロードする]** を選択します。

   :::image type="content" source="~/assets/images/publish-app/publish-app.png" alt-text="カスタム アプリをアップロード" border="true":::

1. アプリ パッケージの .zip ファイルを選択します。
1. 要件に従ってアプリを Teams に追加します。</br>

   a. **［追加］** を選択して、個人用アプリを追加します。</br> b. ドロップダウン メニューを使用して、アプリをチームまたはチャットに追加します。

    :::image type="content" source="~/assets/videos/app-teams.gif" alt-text="Teams アプリを作成する" border="true":::

## <a name="troubleshoot"></a>トラブルシューティング

アプリを脇で発行することに失敗した場合や、アップロードに関する問題がある場合は、次のオプションを確認します:

1. [アプリ パッケージを作成する](../../concepts/build-and-test/apps-package.md)ための、全ての指示通りに操作を済ませたことを確かめてください。
1. [アプリ パッケージ を検証する](https://dev.teams.microsoft.com/appvalidation.html)。
1. アプリ マニフェストが最新の [スキーマ](../../resources/schema/manifest-schema.md)と一致していることを確かめてください。

## <a name="manage-your-apps"></a>アプリを管理する

アプリを管理すると、ユーザーは Teams クライアントでアプリ、アクセス許可、サブスクリプションを管理、更新、削除するための専用の場所を持つことができます。ユーザーは、**[アプリを管理]** からアプリをインストールできます。

### <a name="access-your-app"></a>アプリにアクセスする

**[アプリを管理]** からアプリにアクセスするには、次の手順に従います。

1. **[アプリ]** に移動し、Teams で **[アプリを管理]** を選択して、すべてのチャネルにインストールされているアプリを表示するか、リスト形式で個人使用します。

    :::image type="content" source="~/assets/images/publish-app/manage-apps-list.png" alt-text="チームのアプリ一覧にアクセスする" border="true":::
    
1. アプリのドロップダウンを選択して、アプリがインストールされているすべてのスコープを表示します。
    
    :::image type="content" source="~/assets/images/publish-app/app-scopes.png" alt-text="チームのアプリ スコープにアクセスする" border="true":::
    
1. アプリのスコープを選択して、チャネルまたは個人用ビューでアプリに移動します。 スコープの一覧は、個人スコープとチーム スコープのみで構成されています。 グループ チャット スコープにインストールされているアプリは、現在このビューに表示されていません。
    
Teams には、アプリを開く方法がいくつか用意されています。 詳細については、「 [Teamsでアプリにアクセスする](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)」を参照してください。

### <a name="update-your-app"></a>アプリを更新する

コードを変更する場合は、アプリを再びサイドロードする必要はありません (これらはリアルタイムで Teams に反映されます)。 ただし、アプリの構成を変更する場合は、再インストールする必要があります。

アプリで更新プログラムが利用可能な場合は、**[利用可能な更新プログラム]** オプションが有効になります。更新するには、次の手順に従います。

1. 更新を表示するには、**[利用可能な更新プログラム]** を選択します。

     :::image type="content" source="~/assets/images/publish-app/update-available.png" alt-text="Teams アプリを更新する" border="true":::

1. **[更新の表示]** を選択すると、更新オプションのあるウィンドウが表示されます。
1. アプリを更新するには、**[更新]** ボタンを選択します。
    
     :::image type="content" source="~/assets/images/publish-app/update-window.png" alt-text="アプリの管理で Teams アプリを更新する" border="true":::

     :::image type="content" source="~/assets/images/publish-app/updated-app.png" alt-text="更新されたアプリ" border="true":::

### <a name="remove-your-app"></a>アプリを削除する

Teams からアプリを削除するには、次の手順に従います。

1. **[アプリの管理]** でアプリを見つけます。
1. インストールされたアプリのスコープで、&nbsp;:::image type="content" source="~/assets/images/publish-app/bin-icon.png" alt-text="[Teams のアプリを削除]" border="false":::&nbsp; を選択します。
        
    :::image type="content" source="~/assets/images/publish-app/uninstall-from-channel.png" alt-text="チャネル内のアプリを削除する" border="true":::

1. アプリを削除するには、**[削除]** を選択します。
    
    :::image type="content" source="~/assets/images/publish-app/remove-app-teams.png" alt-text="Teams からアプリを削除する" border="true":::

> [!NOTE]
>
> * 個人のボット アクティビティを完全に削除することはできません。アプリを削除してもう一度追加すると、ボットとの新しい通信が以前の会話に追加されます。
> * 現在、カスタム アプリを Teams ストアに移行することはできません。 アプリを Teams ストアにリスト表示する場合は、「[Microsoft Teams ストアにアプリを公開する](appsource/publish.md)」 を参照してください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
>[Teams 会議用のアプリを作成する](../../apps-in-teams-meetings/teams-apps-in-meetings.md)

## <a name="see-also"></a>関連項目

* [既定のインストール オプションを構成する](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [公開された Microsoft Teams アプリを管理する](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
