---
title: 概要 - アプリを配布する
description: Microsoft Teams ストアまたは組織にアプリを配布、発行する方法について説明します。アプリのエンドポイントが Government Community Cloud (GCC) 組織の要件に準拠する必要がある方法を理解します。
ms.topic: conceptual
author: v-rpatkur
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: df17129ce1e51093351683ad01db3be9e65c5770
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100722"
---
# <a name="distribute-your-microsoft-teams-app"></a>Microsoft Teams アプリを配布する

Microsoft Teams アプリは、個人、チーム、組織、またはそれを使用する任意のユーザーに提供できます。 配布方法は、ユーザーのニーズ、ビジネス、技術要件、アプリの目標など、いくつかの要因によって異なります。

## <a name="configure-default-install-options"></a>既定のインストール オプションを構成する

既定のインストール オプションを構成できます。 たとえば、アプリの主な機能がボットの場合、ユーザーがアプリをチームにインストールするときに、ボットを既定の機能にすることができます。

## <a name="create-your-app-package"></a>アプリ パッケージを作成する

Teams アプリを配布するには、有効なアプリ パッケージが必要です。  アプリ パッケージは、**アプリ マニフェスト** と **アプリ アイコン** を含む zip ファイルです。

## <a name="upload-your-app-in-teams"></a>Teams でアプリをアップロードする

個人的な使用、チームとの共同作業、またはテストとデバッグのためにアプリをサイドロードします。 この種の配布には、正式なレビュー プロセスは必要ありません。

> [!IMPORTANT]
> 現時点では、サイドローディング アプリは Government Community Cloud (GCC) で利用できますが、GCC-High および国防総省 (DOD) では使用できません。

詳細については、「[Teams でのアプリのアップロード](apps-upload.md)」を参照してください。

## <a name="publish-your-app-to-your-org"></a>組織にアプリを発行する

組織内のユーザーがアプリを利用できるようにします。この種類の配布には、Teams 管理者の承認が必要です。

詳細については、「[Teams 管理センターでチームを管理する](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2FMicrosoftTeams%2Fbreadcrumb%2Ftoc.json)」を参照してください。

### <a name="government-community-cloud-gcc-organizations"></a>Government Community Cloud (GCC) 組織

GCC Teams 環境では、準拠した Microsoft アプリが既定で有効になっています。 ただし、アプリを公開する前に、すべてのアプリのエンドポイントが GCC 組織の要件に準拠していることを確認してください。 詳細については、「[Government Community Cloud](../app-fundamentals-overview.md#government-community-cloud)」を参照してください。

> [!IMPORTANT]
>アプリにボットまたはメッセージ拡張機能が含まれている場合は、ボットと Azure の Teams の間にチャネルを設定するときに、**Microsoft Teams 政府機関用** オプションを選択する必要があります。 詳細については、「[ボットをチャネルに接続する](/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0&preserve-view=true)」を参照してください。

## <a name="publish-your-app-to-the-teams-store"></a>アプリを Teams ストアに公開する

アプリをすべてのユーザーが利用できるようにします。 この種の配布には、Microsoft の承認が必要です。

詳細については、「[Teams ストアに発行する](~/concepts/deploy-and-publish/appsource/publish.md)」を参照してください。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [アプリの既定のインストール オプションを構成する](~/concepts/deploy-and-publish/add-default-install-scope.md)

## <a name="see-also"></a>関連項目

[Microsoft 365 アプリ コンプライアンス プログラム](/microsoft-365-app-certification/overview)
