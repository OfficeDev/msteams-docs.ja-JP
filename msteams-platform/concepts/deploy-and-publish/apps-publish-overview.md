---
title: 概要 - アプリを配布する
description: Microsoft Teams アプリの発行、アプリのアップロード、GCCのオプションについて説明します。
ms.topic: conceptual
author: v-rpatkur
ms.author: surbhigupta
ms.localizationpriority: none
keywords: 発行アプリのアップロード gcc をデプロイする
ms.openlocfilehash: f691edee8f4e3aab34aa616f9bbf0ed451874070
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073070"
---
# <a name="distribute-your-microsoft-teams-app"></a>Microsoft Teams アプリを配布する

Microsoft Teams アプリは、個人、チーム、組織、またはそれを使用する任意のユーザーに提供できます。 配布方法は、ユーザーのニーズ、ビジネス、技術的要件、アプリの目標など、いくつかの要因によって異なります。

## <a name="configure-default-install-options"></a>既定のインストール オプションを構成する

既定のインストール オプションを構成します。 たとえば、アプリの主な機能がボットの場合、ユーザーがアプリをチームにインストールするときに、ボットを既定の機能にすることもできます。

## <a name="create-your-app-package"></a>アプリ パッケージを作成する

Microsoft Teams アプリを配布するには、有効なアプリ パッケージが必要です。  アプリ パッケージは、アプリ **マニフェスト** と **アプリ アイコン** を含む zip ファイルです。

## <a name="upload-your-app-in-teams"></a>Teamsでアプリをアップロードする

個人で使用したり、チームと共同作業したり、テストやデバッグを行ったりするために、アプリをサイドロードします。 この種の配布では、正式なレビュー プロセスは必要ありません。

> [!IMPORTANT]
> 現時点では、サイドローディング アプリは Government Community Cloud (GCC) で利用できますが、GCC-High および国防総省 (DOD) では使用できません。

詳細については、「[Teamsでアプリをアップロードする](apps-upload.md)」を参照してください。

## <a name="publish-your-app-to-your-org"></a>組織にアプリを発行する

組織内のユーザーがアプリを利用できるようにします。この種の配布には、Teams管理者の承認が必要です。

詳細については、[Teams管理センターでアプリを管理する](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json)方法に関するページを参照してください。

### <a name="government-community-cloud-gcc-organizations"></a>Government Community Cloud (GCC) 組織

GCC Teams環境では、準拠している Microsoft アプリが既定で有効になっています。 ただし、アプリを発行する前に、すべてのアプリのエンドポイントがGCC組織の要件に準拠していることを確認してください。 詳細については、「[Government Community Cloud](../app-fundamentals-overview.md#government-community-cloud)」を参照してください。

> [!IMPORTANT]
>アプリにボットまたはメッセージング拡張機能が含まれている場合は、Azure でボットとTeamsの間にチャネルを設定するときに **、Government** オプションのMicrosoft Teamsを選択する必要があります。 詳細については、「 [ボットをチャネルに接続する」を](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true)参照してください。

## <a name="publish-your-app-to-the-teams-store"></a>Teams ストアにアプリを発行する

すべてのユーザーがアプリを利用できるようにします。 この種の配布には、Microsoft の承認が必要です。

詳細については、「[Teams ストアへの発行](~/concepts/deploy-and-publish/appsource/publish.md)」を参照してください。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アプリの既定のインストール オプションを構成する](~/concepts/deploy-and-publish/add-default-install-scope.md)

## <a name="see-also"></a>関連項目

[Microsoft 365 アプリ コンプライアンス プログラム](/microsoft-365-app-certification/overview)
