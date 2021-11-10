---
title: アプリをTeamsする
author: heath-hamilton
description: 管理者が組織Teamsアプリをカスタマイズする方法について説明します。
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
keywords: アクセント カラー ブランドアプリの承認を非表示にする
ms.openlocfilehash: 3519ad5dc91b27d947c752161bfe3c477281f1f7
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888168"
---
# <a name="customize-your-teams-app"></a>アプリをTeamsする

## <a name="enable-your-microsoft-teams-app-to-be-customized"></a>アプリMicrosoft Teamsカスタマイズを有効にする

顧客が管理センターでアプリのMicrosoft TeamsをカスタマイズTeamsできます。 この機能は、アプリ ストアに発行されたアプリTeamsされます。 組織用に公開されたサイドロードされたアプリとアプリはカスタマイズできません。

この機能のいくつかの考えられる例は次のとおりです。

* アプリのアクセントカラーを組織のブランドに合わせて変更する。
* Contoso から Contoso *エージェント**にアプリ* 名を更新すると、組織のユーザーに表示される名前が表示されます。 (注: チャットまたはチャネルにコネクタを追加するユーザーには、元のアプリ名 Contoso .) が引き続き *表示* されます。

開発者ポータルでこの機能を有効に[Teams。](https://dev.teams.microsoft.com/home) これにより、アプリ マニフェストの `configurableProperties` 1.10 より前のバージョンTeams構成されます。

### <a name="test-your-app"></a>アプリのテスト

開発中にこの機能をテストできない。 組織のアプリ カタログにサイドローディングまたは発行を行う場合、アプリのカスタマイズはサポートされません。

### <a name="user-considerations"></a>ユーザーの考慮事項

アプリをカスタマイズするユーザー (特Teams管理者) にガイドラインを提供します。 詳細については、「アプリのカスタマイズ[」を参照Teams。](/MicrosoftTeams/customize-apps)

## <a name="hide-teams-app-until-admin-approves"></a>管理者がTeamsするまでアプリを非表示にする

アプリエクスペリエンスTeams強化するには、管理者がアプリの表示を解除するまで、既定でユーザーからアプリを非表示にできます。 たとえば、Contoso Electronics は、ユーザー向けヘルプ デスク アプリを作成Teams。 アプリの適切な機能を有効にするために、Contoso Electronics では、顧客が最初にアプリの特定のプロパティを設定する必要があります。 アプリは既定で非表示にされ、管理者が許可した後にのみユーザーが利用できます。

アプリを非表示にする場合は、アプリ マニフェスト ファイルでプロパティをに `defaultBlockUntilAdminAction` 設定します `true` 。 プロパティがに設定されている場合は、Teams管理センター>アプリの管理、発行者によるブロックがアプリの状態 `true` に表示 **されます**。

![発行元によってブロックされたアプリを管理する](../../assets/images/apps-in-meetings/manageappsblockedapps.png)

管理者は、ユーザーがアプリにアクセスする前にアクションを実行する要求を取得します。 [ **アプリの管理]** で、管理者は [許可] を **選択して、** 発行元の状態でブロック **されたアプリを許可** できます。

![アプリを管理する](../../assets/images/apps-in-meetings/manageapp.png)

既定では、アプリを非表示にしない場合は、プロパティをに `defaultBlockUntilAdminAction` 更新できます `false` 。 新しいバージョンのアプリが承認されると、管理者が明示的なアクションを実行しない限り、アプリは既定で許可されます。

> [!NOTE]
> `defaultBlockUntilAdminAction` LOB アプリではサポートされていません。 このプロパティを使用して LOB アプリをアップロードすると、アプリはブロックされません。

## <a name="see-also"></a>関連項目

* [アプリの manifesh スキーマ](/MicrosoftTeams/manifest-schema)
* [管理センターでアプリTeamsカスタマイズする](/MicrosoftTeams/customize-apps)

