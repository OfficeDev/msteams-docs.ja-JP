---
title: アップロードアプリを作成する
description: アプリをアプリにサイドロードする方法についてMicrosoft Teams。 サイドローディングは、開発中にアプリをテストおよびデバッグする場合に一般的です。
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 93df0d92ce6912888dd1932be3295ca92fa5a967
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345263"
---
# <a name="upload-your-app-in-microsoft-teams"></a>アップロードでアプリをMicrosoft Teams

組織または組織のMicrosoft Teamsストアに発行することなく、アプリをサイドロードTeamsできます。 これは、次のシナリオで理にかなっています。

* 自分または他の開発者と一緒にアプリをローカルでテストおよびデバッグする場合。
* 自分だけのアプリを構築しました。 たとえば、ワークフローを自動化します。
* 作業グループなどの小さなユーザー セット用のアプリを構築しました。

> [!IMPORTANT]
> 現在、サイドローディング アプリは Government Community Cloud (GCC) で使用できますが、GCC-Highおよび国防総省 (DOD) では使用できません。

## <a name="prerequisites"></a>前提条件

* アプリ パッケージ[を作成し、](~/concepts/build-and-test/apps-package.md)[エラーを検証](https://dev.teams.microsoft.com/appvalidation.html)します。
* [カスタム アプリのアップロードを有効](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)にするには、Teams。
* アプリが実行され、HTTP 経由でアクセス可能な状態にしてください。

## <a name="upload-your-app"></a>アプリをアップロードする

アプリのスコープの構成方法に応じて、チーム、チャット、会議、または個人用にアプリをサイドロードできます。

1. 開発アカウントを使用Teamsクライアント[にMicrosoft 365します](~/build-your-first-app/build-and-run.md#prerequisites)。
1. [アプリ **] を** 選択し **、アップロードを選択します**。
1. アプリ パッケージファイルを.zipします。 インストール ダイアログが表示されます。
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="アプリのインストール ダイアログの例Teamsスクリーンショット。":::
1. アプリをアプリに追加Teams。

## <a name="troubleshoot-upload-issues"></a>アップロードに関する問題のトラブルシューティング

アプリがサイドロードに失敗した場合は、問題が解決するまで次の手順を実行します。

1. アプリ パッケージの作成手順に [戻ってください](../../concepts/build-and-test/apps-package.md)。
1. [アプリ パッケージを再度検証](https://dev.teams.microsoft.com/appvalidation.html) します。
1. アプリ マニフェストが最新のスキーマと一致する必要 [があります](../../resources/schema/manifest-schema.md)。

## <a name="access-your-app"></a>アプリにアクセスする

Teamsアプリを開く方法がいくつか提供されています。 詳細については、「アプリに[アクセスする」を参照Teams。](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)

## <a name="update-your-app"></a>アプリを更新する

コードを変更する場合は、アプリを再びサイドロードする必要はありません (これらは、リアルタイムでTeams反映されます)。 ただし、アプリの構成を変更する場合は、再インストールする必要があります。

## <a name="remove-your-app"></a>アプリを削除する

アプリを削除するには、アプリのアイコンを右クリックし、[アンインストールTeams選択 **します**。

> [!NOTE]
> 個人用ボットアクティビティを完全に削除できない。 アプリを削除してもう一度追加すると、ボットとの新しい通信が以前の会話に追加されます。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アプリをTeamsする](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
