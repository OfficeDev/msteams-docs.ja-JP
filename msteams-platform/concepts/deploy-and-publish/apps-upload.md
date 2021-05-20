---
title: カスタム アプリのアップロード
description: Microsoft Teamsでアプリをサイドロードする方法について説明します。 サイドローディングは、開発中にアプリをテストおよびデバッグするときに一般的です。
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 39e94317ceb615ecd7d5481276ffafed5afe5cde
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565194"
---
# <a name="upload-your-app-in-microsoft-teams"></a>アプリをMicrosoft Teamsでアップロードする

組織やTeamsストアに公開しなくても、Microsoft Teamsアプリをサイドロードできます。 これは、次のシナリオで意味をなします。

* ローカルで、または他の開発者と共にアプリをテストおよびデバッグする場合。
* 自分のためだけにアプリを構築しました。 たとえば、ワークフローを自動化します。
* 作業グループなど、少数のユーザー向けのアプリを構築しました。

## <a name="prerequisites"></a>前提条件

* アプリ [パッケージ](~/concepts/build-and-test/apps-package.md) を作成し、エラーを [検証](https://dev.teams.microsoft.com/appvalidation.html) します。
* Teams[でカスタム アプリのアップロードを有効にします](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)。
* アプリが実行され、HTTP 経由でアクセス可能であることを確認します。

## <a name="upload-your-app"></a>アプリをアップロードする

アプリのスコープの構成方法に応じて、チーム、チャット、会議、または個人向けにアプリをサイドロードできます。

1. [Microsoft 365開発アカウント](~/build-your-first-app/build-and-run.md#prerequisites)でTeamsクライアントにログインします。
1. [**アプリ] を** 選択し、[**カスタム アプリアップロード]** を選択します。
1. アプリ パッケージ.zipファイルを選択します。 インストールダイアログが表示されます。
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Teamsアプリのインストール ダイアログの例を示すスクリーンショット。":::
1. アプリをTeamsに追加します。

## <a name="troubleshoot-upload-issues"></a>アップロードに関する問題のトラブルシューティング

アプリがサイドロードに失敗した場合は、問題が解決するまで次の操作を行います。

1. [アプリ パッケージの作成](../../concepts/build-and-test/apps-package.md)手順に戻ります。
1. [アプリ パッケージを](https://dev.teams.microsoft.com/appvalidation.html) もう一度検証します。
1. アプリ マニフェストが最新 [のスキーマ](../../resources/schema/manifest-schema.md)と一致していることを確認します。

## <a name="access-your-app"></a>アプリにアクセスする

Teamsは、アプリを開く方法を複数提供します。 詳細については、「 Teams[でアプリにアクセスする](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)」を参照してください。

## <a name="update-your-app"></a>アプリを更新する

コードを変更した場合に、アプリを再度サイドロードする必要はありません (これらはリアルタイムでTeamsに反映されます)。 ただし、アプリの構成を変更する場合は、再インストールする必要があります。

## <a name="remove-your-app"></a>アプリを削除する

アプリを削除するには、Teamsのアプリ アイコンを右クリックし、[**アンインストール**] を選択します。

> [!NOTE]
> 個人用ボットアクティビティを完全に削除することはできません。 アプリを削除して再度追加すると、ボットとの新しい通信が以前の会話に追加されます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [Teams アプリを使用する](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
