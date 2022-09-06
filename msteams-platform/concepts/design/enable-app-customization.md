---
title: 管理者が許可するまでアプリのカスタマイズを有効にし、アプリをブロックする
author: heath-hamilton
description: このモジュールでは、Teams 管理者が組織用に Teams アプリをカスタマイズし、管理者が承認するまで Teams アプリを非表示にする方法について説明します。
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 7d71e341bd1613e9efe6c900f29e1bd340006b49
ms.sourcegitcommit: d92e14fad6567fe91fd52ee6c213836740316683
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2022
ms.locfileid: "67604955"
---
# <a name="enable-app-customization-and-block-apps-till-admin-allows"></a>管理者が許可するまでアプリのカスタマイズを有効にし、アプリをブロックする

Microsoft Teams を使用すると、管理者は Teams アプリをカスタマイズしてストア エクスペリエンスを強化し、組織のブランディングを進めることができます。 アプリ開発者は、Teams 管理者によるアプリのカスタマイズを許可できます。詳細については、「 [Teams 管理センターでアプリをカスタマイズする](/MicrosoftTeams/customize-apps)」を参照してください。

## <a name="enable-customization-for-your-microsoft-teams-app"></a>Microsoft Teams アプリのカスタマイズを有効にする

開発者は、Microsoft Teams アプリのいくつかの側面を顧客が Teams 管理センターでカスタマイズできるようにすることができます。 この機能は、Teams ストアに公開されたアプリでのみサポートされます。 サイドロードされたアプリや組織用に公開されたアプリはカスタマイズできません。

この機能の考えられる例を次に示します。

* 組織のブランドに合わせてアプリのアクセント カラーを変更する。
* アプリ名を "*Contoso*" から "*Contoso エージェント*" に更新する。この名前が組織内のユーザーに表示されます。
(注: チャットまたはチャネルにコネクタを追加しているユーザーには、元のアプリ名 *Contoso* が引き続き表示されます)。

この機能を有効にするには、バージョン 1.11 以降の [Teams アプリ マニフェストのセクションで`configurableProperties`顧客が](/microsoftteams/platform/resources/schema/manifest-schema#configurableproperties)カスタマイズできるアプリ プロパティを定義します。 開発者ポータルを使用してアプリのマニフェストを編集することを選択した場合は、 [Teams 用開発者ポータル](https://dev.teams.microsoft.com/home) で行うことができます。

> [!IMPORTANT]
> 開発中にこの機能をテストすることはできません。 組織のアプリ カタログにサイドロードまたは公開する場合、アプリのカスタマイズはサポートされません。

### <a name="user-considerations"></a>ユーザーに関する考慮事項

アプリをカスタマイズしたい顧客 (具体的には Teams 管理者) 向けにガイドラインを提供します。 詳細については、[Teams でのアプリのカスタマイズ](/MicrosoftTeams/customize-apps)に関する記事を参照してください。

## <a name="block-apps-by-default-for-users-until-an-admin-approves"></a>管理者が承認するまで、ユーザーのアプリを既定でブロックする

Teams アプリのエクスペリエンスを向上させるために、開発者は、管理者がアプリの再表示を許可するまで、既定でユーザーからアプリを非表示にすることができます。 たとえば、Contoso Electronics では Teams 用のヘルプ デスク アプリを作成しました。 Contoso Electronics は、アプリの適切な機能を実現するために、顧客が最初にアプリの特定のプロパティを設定することを望んでいます。 このアプリは既定では非表示になっており、管理者が許可してはじめてユーザーが使用できるようになります。

アプリを非表示にするには、アプリ マニフェスト ファイルで `defaultBlockUntilAdminAction` プロパティを `true` に設定します。 このプロパティが `true` に設定されている場合、Teams 管理センター > **[アプリの管理]** では、**[Blocked by publisher]\(発行元によってブロック済み\)** がアプリの **[状態]** に表示されます。

:::image type="content" source="../../assets/images/manage-apps-status.png" alt-text="スクリーンショットは、発行元によってブロックされたアプリを示す例です。" lightbox="../../assets/images/manage-apps-status-expanded.png":::

管理者は、ユーザーがアプリにアクセスできるようになる前にアクションを実行する要求を受け取ります。 **[アプリの管理]** で、管理者は **[許可]** を選択して、**[Blocked by publisher]\(発行元によってブロック済み\)** 状態のアプリを許可できます。

:::image type="content" source="../../assets/images/manage-apps-allow.png" alt-text="スクリーンショットは、発行元によってブロックされたアプリの許可オプションを示す例です。" lightbox="../../assets/images/manage-apps-allow-expanded.png":::

既定でアプリを非表示にしたくない場合は、`defaultBlockUntilAdminAction` プロパティを `false` に更新できます。 そのアプリの新しいバージョンが承認された場合、管理者が明示的なアクションを実行していない限り、アプリは既定で許可されます。

> [!NOTE]
> LOB アプリの場合、 `defaultBlockUntilAdminAction` サポートされていません。 このプロパティを使用して LOB アプリをアップロードしても、アプリはブロックされません。

## <a name="see-also"></a>関連項目

* [アプリ マニフェストのスキーマ](/microsoftteams/platform/resources/schema/manifest-schema)
* [Teams 管理センターでアプリをカスタマイズする](/MicrosoftTeams/customize-apps)
