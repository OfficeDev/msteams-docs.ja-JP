---
title: Teams ツールキットを使用して Teams アプリを公開する
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit を使用して Teams アプリを発行し、個々のスコープまたはサイドロードアクセス許可に発行する方法について説明します
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 6188072b2d4ca73aae4e7ea91715869d968a9b9c
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616748"
---
# <a name="publish-teams-apps-using-teams-toolkit"></a>Teams ツールキットを使用して Teams アプリを公開する

アプリを作成した後は、個人、チーム、組織、すべてのユーザーなど、さまざまなスコープにアプリを配布できます。 分布は、ニーズ、ビジネス要件、技術要件、アプリの目標など、複数の要因によって異なります。 異なるスコープへの配布には、異なるレビュー プロセスが必要な場合があります。 一般に、スコープが大きいほど、セキュリティとコンプライアンスに関する懸念のためにアプリが通過する必要があるレビューが多くなります。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/publish-flow.png" alt-text="フローを発行する":::

このセクションで学習する内容は次のとおりです。

* [個々のスコープまたはサイドロード アクセス許可に発行する](#publish-to-individual-scope-or-sideload-permission)
* [組織にアプリを公開する](#publish-to-your-organization)
* [Microsoft Teams ストアに発行する](#publish-to-microsoft-teams-store)

## <a name="prerequisites"></a>前提条件

* [アプリ パッケージ](~/concepts/build-and-test/apps-package.md)を作成し、[アプリ パッケージを検証](https://dev.teams.microsoft.com/appvalidation.html)することを確かめて下さい。
* Teams で[カスタム アプリのアップロード を有効](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)にします。
* アプリが実行されていて、HTTP 経由でアクセスできることを確認してください。
* アプリを発行する Microsoft Teams ストアにアプリを発行する際のガイドラインのセットに従っていることを確認します。

## <a name="publish-to-individual-scope-or-sideload-permission"></a>個々のスコープまたはサイドロード アクセス許可に発行する

*.zip ファイル内の [アプリ パッケージ](../concepts/build-and-test/apps-package.md) をチームまたは個人のコンテキストに直接アップロードすることで、Teams にカスタム アプリを追加できます。 アプリ パッケージをアップロードしてカスタム アプリを追加することは、サイドローディングと呼ばれます。 これにより、Teams でアップロード中にアプリをテストできます。 次のシナリオでは、アプリをビルドしてテストできます。

* アプリをローカルでテストしてデバッグします。
* ワークフローを自動化するために、自分用のアプリを構築しました。
* 作業グループなど、少数のユーザー向けのアプリを作成しました。

社内専用のアプリを作成し、Teams アプリ ストアの Teams アプリ カタログに送信せずにチームと共有することもできます。 詳細については、「 [Teams でアプリをアップロードする](../concepts/deploy-and-publish/apps-upload.md)」を参照してください。

### <a name="to-build-your-app-to-zip-app-package-file"></a>アプリを zip アプリ パッケージ ファイルにビルドするには

アプリ パッケージをビルドする前に、最初に実行 `Provision in the cloud` する必要があります。 次の手順は、アプリ パッケージのビルドに役立ちます。

* [展開] **で [Zip Teams メタデータ パッケージ****] を選択します**。<br>
    生成されたアプリ パッケージは `{your project folder}/build/appPackage/appPackage.{env}.zip` にあります。

### <a name="to-upload-app-package"></a>アプリ パッケージをアップロードするには

アプリ パッケージをアップロードするには、次の手順を実行します。

1. Teams クライアントで、[**アプリ** > の管理] を選択 **してアプリ** > **をアップロードします**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/publish1.png" alt-text="アプリを発行する":::

   **[アプリのアップロード]** ウィンドウが表示されます。

2. **[カスタム アプリをアップロードする]** を選択します。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/upload.png" alt-text="アプリをアップロードする":::

   これで、アプリが Teams クライアントにサイドロードされ、アプリを追加して表示できるようになります。

## <a name="publish-to-your-organization"></a>組織にアプリを公開する

アプリを運用環境で使用する準備ができたら、Graph APIから呼び出された Teams アプリ申請 API を使用してアプリを送信できます。 Teams アプリ申請 API は、Teams ツールキットと共にインストールされた Microsoft Visual Studio Code などの統合開発環境 (IDE) です。 次の手順は、組織にアプリを発行するのに役立ちます。

* [Teams Toolkit から発行する](#publish-from-teams-toolkit)
* [管理 センターで承認する](#approve-on-admin-center)

### <a name="publish-from-teams-toolkit"></a>Teams Toolkit から発行する

次の手順は、Teams Toolkit からアプリを発行するのに役立ちます。

1. Teams アプリは、次のいずれかの方法で発行できます。
     * Teams Toolkit のツリー ビューで **[展開]** で [Teams **に発行**] を選択します。
     * トリガー **Teams を入力します。コマンド パレットから Teams に発行** します。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-publish.png" alt-text="[発行] を選択する":::

2 **組織の [インストール**] を選択します。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/installforyourorganization.png" alt-text="組織用にインストール":::

  これで、アプリが管理者ポータルに正常に発行され、次の通知が表示されます。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/confirm-publish.png" alt-text="発行の確認":::

  これで、アプリは Microsoft Teams 管理センターの **アプリの管理** で利用できるようになります。ここで、ユーザーと管理者はそれを確認して承認できます。

  > [!NOTE]
  > アプリはまだ組織のアプリ ストアに発行されません。 この手順では、アプリを Microsoft Teams 管理センターに送信し、組織のアプリ ストアへの発行を承認できます。

### <a name="approve-on-admin-center"></a>管理 センターで承認する

Teams アプリ申請 API の上に構築された Visual Studio Code 用の Teams ツールキットを使用すると、Teams 上のカスタム アプリの申請から承認へのプロセスを自動化できます。

  > [!NOTE]
  > VS コードに Teams アプリ プロジェクトがあることを確認します。 [Microsoft Teams 管理センター](https://admin.teams.microsoft.com/policies/manage-apps)の **[アプリの管理]** は、管理者が組織用のすべての Teams アプリを表示および管理できる場所です。 管理センターでは、次のアクティビティを実行できます。
  >
  > * アプリの組織レベルの状態とプロパティを確認します。
  > * 組織のアプリ ストアに新しいカスタム アプリを承認またはアップロードします。
  > * 組織レベルでアプリをブロックまたは許可します。
  > * Teams にアプリを追加します。
  > * サード パーティ製アプリのサービスを購入します。
  > * アプリによって要求されたアクセス許可を表示します。
  > * アプリに管理者の同意を付与します。
  > * [組織全体のアプリ設定を管理します](https://admin.teams.microsoft.com/policies/manage-apps)。

次の手順は、管理 センターから承認するのに役立ちます。

1. [ **管理ポータルに移動] を選択します**。

1. **Teams アプリ** 管理:::image type="icon" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Showall.PNG":::アプリ > >アイコンを選択 **します**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manage-apps.png" alt-text="[アプリの管理] を選択する":::

   組織のすべての Teams アプリを表示できます。

   ページの上部にある [承認の保留中] ウィジェットでは、承認のためにカスタム アプリがいつ送信されたのかがわかります。 この表では、新しく送信されたアプリによって、送信されたアプリとブロックされたアプリの状態が自動的に発行されます。 発行状態列を降順で並べ替えて、アプリを見つけることができます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/admin-approval-for-teams-app-1.png" alt-text="承認":::

1. アプリ名を選択して、アプリの詳細ページに移動します。 [ **バージョン情報** ] タブでは、説明、状態、アプリ ID など、アプリに関する詳細を表示できます。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/about-submitted-app-1.png" alt-text="送信されたアプリ":::

1. 状態ドロップダウンを選択し、[ **送信済み]** から **[発行**] に変更します。

   アプリを公開すると、[公開ステータス] が [公開済み] に変わり、[ステータス] が自動的に [許可] に変わります。

   詳細については、「[組織に発行する」を参照してください](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2Fmicrosoftteams%2Fplatform%2Fbreadcrumb%2Ftoc.json)。

## <a name="publish-to-microsoft-teams-store"></a>Microsoft Teams ストアに発行する

アプリを Microsoft Teams 内のストアに直接配信して、世界中の何百万ものユーザーに届けることができます。 アプリがストアでも紹介されている場合は、潜在的な顧客に即座にリーチできます。 Teams ストアに公開されたアプリは、Microsoft 365 アプリおよびソリューションの公式マーケットプレイスである Microsoft AppSource にも自動的に一覧表示されます。

詳細については、「 [Microsoft Teams ストアにアプリを発行する」を参照してください](../concepts/deploy-and-publish/appsource/publish.md#publish-your-app-to-the-microsoft-teams-store)。

## <a name="see-also"></a>関連項目

* [Microsoft Teams アプリを配布する](../concepts/deploy-and-publish/apps-publish-overview.md)
* [Teams アプリ パッケージを作成する](../concepts/build-and-test/apps-package.md)
* [Microsoft 365 テナントを準備する](../concepts/build-and-test/prepare-your-o365-tenant.md)
* [Microsoft Teams ストアにアプリを公開する](../concepts/deploy-and-publish/appsource/publish.md)
* [Teams でアプリをアップロードする](../concepts/deploy-and-publish/apps-upload.md)
* [Microsoft Teams 管理センターで Teams アプリを管理する](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2Fmicrosoftteams%2Fplatform%2Fbreadcrumb%2Ftoc.json)
