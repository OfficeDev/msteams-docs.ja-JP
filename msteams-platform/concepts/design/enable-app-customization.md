---
title: アプリのカスタマイズを有効にする
author: heath-hamilton
description: 管理者が組織Teamsアプリをカスタマイズする方法について説明します。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 0af96eebb50aeb650cdd5a1b3bd6a93439fb57b8
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345566"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a>アプリMicrosoft Teamsカスタマイズを有効にする

顧客が管理センターでアプリのMicrosoft TeamsをカスタマイズTeamsできます。 この機能は、アプリ ストアに発行されたアプリTeamsされます。 組織用に公開されたサイドロードされたアプリとアプリはカスタマイズできません。

> [!IMPORTANT]
> 現在、サイドローディング アプリは Government Community Cloud (GCC) で使用できますが、GCC-Highおよび国防総省 (DOD) では使用できません。

この機能のいくつかの考えられる例は次のとおりです。

* アプリのアクセントカラーを組織のブランドに合わせて変更する。
* Contoso から Contoso *エージェント**にアプリ* 名を更新すると、組織のユーザーに表示される名前が表示されます。 (注: チャットまたはチャネルにコネクタを追加するユーザーには、元のアプリ名 Contoso .) が引き続き *表示* されます。

開発者ポータルでこの機能を有効に[Teams。](https://dev.teams.microsoft.com/home) これは、アプリ マニフェストの `configurableProperties` 1.10 より前のバージョンではTeams構成されます。

## <a name="test-your-app"></a>アプリのテスト

開発中にこの機能をテストすることはできません。 アプリのカスタマイズは、組織のアプリ カタログへのサイドローディングまたは発行ではサポートされていません。

## <a name="user-considerations"></a>ユーザーの考慮事項

アプリの発行元として、管理者のユーザーに次の情報Teamsします。
* 実稼働環境で変更を加える前に、Teamsテナントでカスタマイズの変更をテストすることをお勧めのメモを含めます。 
* アプリをカスタマイズする方法のベスト プラクティスを提供します。

## <a name="see-also"></a>関連項目

* [管理センターでアプリTeamsカスタマイズする](/MicrosoftTeams/customize-apps)
