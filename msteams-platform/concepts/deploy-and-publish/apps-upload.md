---
title: カスタム アプリをアップロードする
description: Microsoft Teams でアプリをサイドロードする方法について説明します。 サイドローディングは、開発中にアプリをテストおよびデバッグするときに一般的です。
ms.topic: how-to
author: surbhigupta
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: ffa7cdb0fabf07254c90590fe94fe2347c35658c
ms.sourcegitcommit: 377a4b712b50a211851aeecc1029414939945390
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2022
ms.locfileid: "68044680"
---
# <a name="upload-your-app-in-teams"></a>Teams でアプリをアップロードする

組織または Teams ストアに公開しなくても、Microsoft Teams アプリを脇で発行できます。これは、以下のシナリオで有効です:

* アプリをローカルで、または他の開発者とテストしてデバッグする必要があります。
* ワークフローを自動化するために、自分用のアプリを構築しました。
* 作業グループなど、少数のユーザー向けのアプリを作成しました。

> [!NOTE]
> メッセージング拡張機能アプリを複数回サイドローディングすると、メッセージング拡張機能の複数のインスタンスが表示されます。

> [!IMPORTANT]
>
> * 現在、アプリのサイドローディングは Government Community Cloud (GCC) でのみ可能であり、GCC-Highおよび国防総省 (DOD) では不可能です。
> * アプリのインストールは、Teams デスクトップ アプリでのみサポートされます。

## <a name="prerequisites"></a>前提条件

* [アプリ パッケージ](~/concepts/build-and-test/apps-package.md)を作成し、[アプリ パッケージを検証](https://dev.teams.microsoft.com/appvalidation.html)することを確かめて下さい。
* Teams で[カスタム アプリのアップロード を有効](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)にします。
* アプリが実行されていて、HTTP 経由でアクセスできることを確認してください。

## <a name="upload-your-app"></a>アプリをアップロードする

アプリのスコープの構成方法に応じて、チーム、チャット、会議、または個人用にアプリをサイドロードできます。

1. [Microsoft 365開発アカウント](https://developer.microsoft.com/en-us/microsoft-365/dev-program)を使用して Teams クライアントにログインします。
1. **[アプリ]** > **[アプリの管理]** と **[アプリの公開]** を選択します。

    :::image type="content" source="~/assets/images/publish-app/manage-apps.png" alt-text="アプリを発行します。":::

1. **[カスタム アプリをアップロードする]** を選択します。

   :::image type="content" source="~/assets/images/publish-app/publish-app.png" alt-text="カスタム アプリをアップロード":::

1. アプリ パッケージの .zip ファイルを選択します。
1. 要件に従ってアプリを Teams に追加します。</br>

   a. Select **Add** to add your personal app.</br>
   b. Use the dropdown menu to add your app to a Team or chat.

    :::image type="content" source="~/assets/images/publish-app/teams-app-detail.png" alt-text="アプリの説明":::

## <a name="troubleshoot"></a>トラブルシューティング

アプリのサイドロードに失敗した場合、またはアップロードする問題が発生した場合は、次のオプションを確認します。

1. [アプリ パッケージを作成する](../../concepts/build-and-test/apps-package.md)ための、全ての指示通りに操作を済ませたことを確かめてください。
1. [アプリ パッケージ を検証する](https://dev.teams.microsoft.com/appvalidation.html)。
1. アプリ マニフェストが最新のスキーマと一致していることを確認 [します](../../resources/schema/manifest-schema.md)。

## <a name="manage-your-apps"></a>アプリを管理する

Manage your apps allows users to have a dedicated place to manage, update and remove their apps, permissions, and subscriptions on the Teams client. The users can install the apps from **Manage your apps**.

### <a name="access-your-app"></a>アプリにアクセスする

**[アプリを管理]** からアプリにアクセスするには、次の手順に従います。

1. **[アプリ]** に移動し、Teams で **[アプリを管理]** を選択して、すべてのチャネルにインストールされているアプリを表示するか、リスト形式で個人使用します。

    :::image type="content" source="~/assets/images/publish-app/manage-apps-list.png" alt-text="チームのアプリ一覧にアクセスする":::

1. アプリのドロップダウンを選択して、アプリがインストールされているすべてのスコープを表示します。

    :::image type="content" source="~/assets/images/publish-app/app-scopes.png" alt-text="チームのアプリ スコープにアクセスする":::

1. アプリのスコープを選択して、チャネルまたは個人用ビューでアプリに移動します。 スコープの一覧は、個人スコープとチーム スコープのみで構成されています。 グループ チャット スコープにインストールされているアプリは、現在このビューに表示されていません。

Teams には、アプリを開く方法がいくつか用意されています。 詳細については、「 [Teamsでアプリにアクセスする](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)」を参照してください。

### <a name="update-your-app"></a>アプリを更新する

コードを変更する場合は、アプリを再びサイドロードする必要はありません (これらはリアルタイムで Teams に反映されます)。 ただし、アプリの構成を変更する場合は、再インストールする必要があります。

アプリで更新プログラムが利用可能な場合は、**[利用可能な更新プログラム]** オプションが有効になります。 更新するには、次の手順に従います。

1. 更新を表示するには、**[利用可能な更新プログラム]** を選択します。

     :::image type="content" source="~/assets/images/publish-app/update-available.png" alt-text="Teams アプリを更新する。":::

1. [ **更新の表示**] を選択します。 更新オプションを含むウィンドウが表示されます。
1. アプリを更新するには、**[更新]** ボタンを選択します。

     :::image type="content" source="~/assets/images/publish-app/update-window.png" alt-text="アプリの管理で Teams アプリを更新する。":::

     :::image type="content" source="~/assets/images/publish-app/updated-app.png" alt-text="更新されたアプリ。":::

### <a name="remove-your-app"></a>アプリを削除する

Teams からアプリを削除するには、次の手順に従います。

1. **[アプリの管理]** でアプリを見つけます。

1. インストールされたアプリのスコープで、&nbsp;:::image type="content" source="~/assets/images/publish-app/bin-icon.png" alt-text="[Teams のアプリを削除。]":::&nbsp; を選択します。

    :::image type="content" source="~/assets/images/publish-app/uninstall-from-channel.png" alt-text="チャネル内のアプリを削除する。":::

1. アプリを削除するには、**[削除]** を選択します。

    :::image type="content" source="~/assets/images/publish-app/remove-app-teams.png" alt-text="Teams からアプリを削除する。":::

> [!NOTE]
>
> * You can't remove personal bot activity entirely. If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.
> * 現在、カスタム アプリを Teams ストアに移行することはできません。 アプリを Teams ストアにリスト表示する場合は、「[Microsoft Teams ストアにアプリを公開する](appsource/publish.md)」 を参照してください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
>[Teams 会議用のアプリを作成する](../../apps-in-teams-meetings/teams-apps-in-meetings.md)

## <a name="see-also"></a>関連項目

* [既定のインストール オプションを構成する](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [公開された Microsoft Teams アプリを管理する](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
* [アプリをチャットに追加する](/graph/api/chat-post-installedapps)
