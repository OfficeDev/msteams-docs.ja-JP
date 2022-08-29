---
title: Teams の開発者ポータル
description: この記事では、開発者ポータルの詳細と、まったく新しいアプリを作成し、Teams 開発者ポータルで既存のアプリをインポートする方法について説明します。
ms.localizationpriority: medium
ms.topic: overview
ms.author: surbhigupta
ms.openlocfilehash: 0e099700d6129dc2db7b12e0a699fc903c9d32c8
ms.sourcegitcommit: b060a3901a3ba770ea6fca96d0ab477c252af1a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2022
ms.locfileid: "67417501"
---
# <a name="developer-portal-for-teams"></a>Teams の開発者ポータル

<a href="https://dev.teams.microsoft.com" target="_blank">Teams 用開発者ポータル</a>は、Microsoft Teams アプリを構成、配布、管理するための主要なツールです。 開発者ポータルを使用すると、アプリで同僚と共同作業したり、ランタイム環境を設定したりできます。

:::image type="content" source="../../assets/images/tdp/tdp_home_1.png" alt-text="スクリーンショットは、Teams 用開発者ポータルのホーム ページを示す例です。":::

> [!NOTE]
>
> * 現在、開発者ポータルは Government Community Cloud (GCC)、GCC-High、または国防総省 (DOD) テナントでは使用できません。
> * ただし、通常のテナントを使用して、開発者ポータルでアプリを構築し、アプリをダウンロードし、 [Microsoft Graph](/graph/api/teamsapp-publish?view=graph-rest-1.0&tabs=http&preserve-view=true) を使用してアプリを国内クラウドにアップロードすることができます。 詳細については、「 [国内クラウドデプロイ](/graph/deployments)」を参照してください。
> * 現時点では、AdBlocker が有効になっている場合、開発者ポータルはブラウザーに読み込まれません。 ブラウザーで開発者ポータルを続行するには、AdBlocker を無効にします。

## <a name="register-an-app"></a>アプリを登録します

開発者ポータルには、Teams アプリを登録する次の方法があります。

* まったく新しいアプリを作成して登録します。
* 既存のアプリ パッケージをインポートします。

### <a name="create-and-register-a-brand-new-app"></a>まったく新しいアプリを作成して登録する

開発者ポータルを使用すると、まったく新しいアプリを作成できます。

1. [開発者ポータル](https://dev.teams.microsoft.com)にログインし、左側のウィンドウで **[アプリ**] を選択します。

   :::image type="content" source="../../assets/images/tdp/home-page.png" alt-text="スクリーンショットは、Teams 向け開発者ポータルのホーム ページを示す例です。":::

1. [ **新しいアプリ** ] を選択し、アプリ名を入力します。

   :::image type="content" source="../../assets/images/tdp/enter-app-name-tdp.png" alt-text="スクリーンショットは、Teams 用開発者ポータルでまったく新しいアプリを作成する方法を示しています。" lightbox="../../assets/images/tdp/create-new-app-in-tdp.png":::

1. **[追加]** を選択します。

これで、まったく新しいアプリが正常に作成され、新しいアプリのすべての基本情報が表示されます。

:::image type="content" source="../../assets/images/tdp/basic-information-app-tdp.png" alt-text="スクリーンショットは、Teams 用開発者ポータルで作成したアプリの基本情報を示す例です。":::

### <a name="import-an-existing-app"></a>既存のアプリをインポートする

開発者ポータルで既存のアプリをインポートして管理する手順に従います。

1. 開発者ポータルで、左側のウィンドウで **[アプリ** ] を選択します。
1. [ **アプリのインポート] を選択します**。

   :::image type="content" source="../../assets/images/tdp/import-app.png" alt-text="このスクリーンショットは、Teams 用開発者ポータルで既存のアプリをインポートしてアプリを管理する方法を示しています。":::

1. アプリ マニフェスト ファイルを選択し、[ **開く**] を選択します。
1. **[インポート]** を選択します。

> [!NOTE]
>
> * 開発者ポータルは、一意のアプリ ID を作成し、登録済みの Teams アプリの ID をロックします。 任意の ID を編集または指定することはできません。これにより、複数のアプリに対して重複するアプリ ID を持つことができなくなります。
> * Microsoft Teams Toolkit for Visual Studio Code を使用してアプリを作成する場合は、開発者ポータルでアプリを管理できます。 詳細については、「 [Teams ツールキットと Visual Studio コードを使用してアプリをビルド](~/toolkit/visual-studio-code-overview.md)する」を参照してください。
> * App Studio で作成した既存のアプリを開発者ポータルにインポートできます。

## <a name="see-also"></a>関連項目

[Microsoft Teams アプリに SaaS オファーを含める](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
