---
title: Teams アプリをカスタマイズする
author: heath-hamilton
description: このモジュールでは、Teams 管理者が組織用に Teams アプリをカスタマイズし、管理者が承認するまで Teams アプリを非表示にする方法について説明します。
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: c63a901aba88b8f9f77c3a3e54217204a3e91cc9
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503446"
---
# <a name="customize-your-teams-app"></a>Teams アプリをカスタマイズする

## <a name="enable-your-microsoft-teams-app-to-be-customized"></a>Microsoft Teams アプリをカスタマイズできるようにする

開発者は、Microsoft Teams アプリのいくつかの側面を顧客が Teams 管理センターでカスタマイズできるようにすることができます。 この機能は、Teams ストアに公開されたアプリでのみサポートされます。 サイドロードされたアプリや組織用に公開されたアプリはカスタマイズできません。

この機能の考えられる例を次に示します。

* 組織のブランドに合わせてアプリのアクセント カラーを変更する。
* アプリ名を "*Contoso*" から "*Contoso エージェント*" に更新する。この名前が組織内のユーザーに表示されます。 (注: チャットまたはチャネルにコネクタを追加しているユーザーには、元のアプリ名 *Contoso* が引き続き表示されます)。

この機能は、[Teams の開発者ポータル](https://dev.teams.microsoft.com/home)で有効にできます。 これは `configurableProperties` を構成します。この構成は Teams アプリ マニフェストの 1.10 より前のバージョンでは使用できません。

### <a name="test-your-app"></a>アプリのテスト

開発中にこの機能をテストすることはできません。 組織のアプリ カタログにサイドロードまたは公開する場合、アプリのカスタマイズはサポートされません。

### <a name="user-considerations"></a>ユーザーに関する考慮事項

アプリをカスタマイズしたい顧客 (具体的には Teams 管理者) 向けにガイドラインを提供します。 詳細については、[Teams でのアプリのカスタマイズ](/MicrosoftTeams/customize-apps)に関する記事を参照してください。

## <a name="hide-teams-app-until-admin-approves"></a>管理者が承認するまで Teams アプリを非表示にする

Teams アプリのエクスペリエンスを向上させるために、開発者は、管理者がアプリの再表示を許可するまで、既定でユーザーからアプリを非表示にすることができます。 たとえば、Contoso Electronics では Teams 用のヘルプ デスク アプリを作成しました。 Contoso Electronics は、アプリの適切な機能を実現するために、顧客が最初にアプリの特定のプロパティを設定することを望んでいます。 このアプリは既定では非表示になっており、管理者が許可してはじめてユーザーが使用できるようになります。

> [!NOTE]
> Teams ストアが進化しました。
> 
> 以前は、タイルの省略記号を選択すれば LOB アプリが更新されました。 Teams ストア エクスペリエンスが更新され、[Teams 管理センター](https://admin.teams.microsoft.com)にログインして LOB アプリを更新できるようになりました。

アプリを非表示にするには、アプリ マニフェスト ファイルで `defaultBlockUntilAdminAction` プロパティを `true` に設定します。 このプロパティが `true` に設定されている場合、Teams 管理センター > **[アプリの管理]** では、**[Blocked by publisher]\(発行元によってブロック済み\)** がアプリの **[状態]** に表示されます。

:::image type="content" source="../../assets/images/apps-in-meetings/manageappsblockedapps.png" alt-text="発行元によってブロックされたアプリを管理します。":::

管理者は、ユーザーがアプリにアクセスできるようになる前にアクションを実行する要求を受け取ります。 **[アプリの管理]** で、管理者は **[許可]** を選択して、**[Blocked by publisher]\(発行元によってブロック済み\)** 状態のアプリを許可できます。

![アプリを管理する](../../assets/images/apps-in-meetings/manageapp.png)

既定でアプリを非表示にしたくない場合は、`defaultBlockUntilAdminAction` プロパティを `false` に更新できます。 そのアプリの新しいバージョンが承認された場合、管理者が明示的なアクションを実行していない限り、アプリは既定で許可されます。

> [!NOTE]
> `defaultBlockUntilAdminAction` は LOB アプリではサポートされていません。 このプロパティを使用して LOB アプリをアップロードした場合、アプリはブロックされません。

## <a name="see-also"></a>関連項目

* [アプリ マニフェストのスキーマ](/microsoftteams/platform/resources/schema/manifest-schema)
* [Teams 管理センターでアプリをカスタマイズする](/MicrosoftTeams/customize-apps)