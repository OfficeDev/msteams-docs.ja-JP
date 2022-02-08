---
title: カスタム アプリをアップロードする
description: Microsoft Teams でアプリをサイドロードする方法について説明します。 サイドローディングは、開発中にアプリをテストおよびデバッグするときに一般的です。
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: bcb5661c4f6d09499700456bc44ce962ac710ea9
ms.sourcegitcommit: 83d67e73427ea1e93bb9aea5a8ca8ae05b68e302
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2022
ms.locfileid: "62430300"
---
# <a name="upload-your-app-in-microsoft-teams"></a>Microsoft Teams でアプリをアップロードする

組織や Teams ストアに公開しなくても、Microsoft Teams アプリをサイドロードできます。 これは、次のシナリオで意味があります。

* アプリをローカルで、または他の開発者とテストしてデバッグする必要があります。
* 自分専用のアプリを作成しました。 たとえば、ワークフローを自動化する場合などです。
* 作業グループなど、少数のユーザー向けのアプリを作成しました。

> [!IMPORTANT]
> 現時点では、サイドローディング アプリは Government Community Cloud (GCC) で利用できますが、GCC-High および国防総省 (DOD) では使用できません。

## <a name="prerequisites"></a>前提条件

* [アプリ パッケージ](~/concepts/build-and-test/apps-package.md)を作成し、エラーを[検証](https://dev.teams.microsoft.com/appvalidation.html)します。
* Teams で[カスタム アプリのアップロード を有効](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)にします。
* アプリが実行されていて、HTTP 経由でアクセスできることを確認します。

## <a name="upload-your-app"></a>アプリをアップロードする

アプリのスコープの構成方法に応じて、チーム、チャット、会議、または個人用にアプリをサイドロードできます。

1. [Microsoft 365開発アカウント](~/build-your-first-app/build-and-run.md#prerequisites)を使用して Teams クライアントにログインします。
1. [ **Apps** ] を選択し ［**カスタム アプリをアップロードする**] を選択します。
1. アプリ パッケージの .zip ファイルを選択します。 インストール ダイアログが表示されます。
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Teams アプリのインストール ダイアログの例を示すスクリーンショット。":::
1. アプリを Teams に追加します。

> [!NOTE]
> `onInstallationUpdateActivityAsync()` メソッドは、ボットを Microsoft Teams に追加するときに Microsoft Teams Locale を取得するために使用されます。

## <a name="troubleshoot-upload-issues"></a>アップロードに関する問題のトラブルシューティング

アプリがサイドロードに失敗した場合は、問題が解決するまで次の操作を行います。

1. [アプリ パッケージ作成](../../concepts/build-and-test/apps-package.md)手順に戻ります。
1. [アプリ パッケージ](https://dev.teams.microsoft.com/appvalidation.html) をもう一度検証します。
1. アプリ マニフェストが最新の [スキーマ](../../resources/schema/manifest-schema.md)と一致していることを確認します。

## <a name="access-your-app"></a>アプリにアクセスする

Teams には、アプリを開く方法がいくつか用意されています。 詳細については、「 [Teamsでアプリにアクセスする](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)」を参照してください。

## <a name="update-your-app"></a>アプリを更新する

コードを変更する場合は、アプリを再びサイドロードする必要はありません (これらはリアルタイムで Teams に反映されます)。 ただし、アプリの構成を変更する場合は、再インストールする必要があります。

## <a name="remove-your-app"></a>アプリを削除する

アプリを削除するには、Teams のアプリ アイコンを右クリックし、**[アンインストール]** を選択します。

> [!NOTE]
> 個人のボット アクティビティを完全に削除することはできません。 アプリを削除してもう一度追加すると、ボットとの新しい通信が以前の会話に追加されます。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [Teams アプリを使用する](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)

## <a name="see-also"></a>関連項目

* [既定のインストール オプションを構成する](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [公開された Microsoft Teams アプリを管理する](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
