---
title: Teams ツールキットの概要
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit、Teams Toolkit のインストール、Teams Toolkit のユーザー体験について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 786bfd318f1cefa4329e54b5a19cba89a823bb5b
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615339"
---
# <a name="teams-toolkit-overview"></a>Teams ツールキットの概要

Teams Toolkit を使用すると、Visual Studio と Visual Studio Code を使用して Microsoft Teams のアプリ開発を簡単に開始できます。

* プロジェクト テンプレートまたはサンプルから開始する
* アプリの自動登録と構成でセットアップ時間を節約する
* 使い慣れたツールから Teams に直接実行してデバッグする
* コードとしてのインフラストラクチャと Bicep を使用した Azure でのホスティングのスマート な既定値
* 環境機能を使用して、開発、テスト、プローブなどの一意の構成を作成する
* 組み込みの発行ツールを使用して、アプリを組織または Teams App Storeに持ち込む

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Teams Toolkit のユーザー体験" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

## <a name="available-for-visual-studio-and-visual-studio-code"></a>Visual Studio と Visual Studio Code で使用できます

Teams Toolkit は Visual Studio Code で無料で利用でき、Visual Studio 2022 コミュニティ、プロフェッショナル、エンタープライズをサポートしています。 インストールとセットアップの詳細については [、Teams Toolkit のインストールに](./install-Teams-Toolkit.md) 関するドキュメントを参照してください。

| Teams ツールキット | Visual Studio | Visual Studio Code |
| - | ------------- | ------------------ |
| インストール | Visual Studio インストーラーで使用できます | VS Marketplace で使用可能 |
| を使用してビルドする | C#、.NET、ASP.NET、Blazor | JavaScript、TypeScript、React、SPFx |

## <a name="features"></a>機能

### <a name="project-templates"></a>プロジェクト テンプレート

Teams Toolkit を使用すると、一般的な基幹業務アプリのシナリオとスマート な既定値のテンプレートを使い始める作業の複雑さが軽減され、運用までの時間が短縮されます。 Teams アプリの開発に既に精通している場合は、機能に焦点を当てたテンプレートから直接開始することもできます。 タブ、ボット、メッセージング拡張機能などです。

::: zone pivot="visual-studio-code"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app.png" alt-text="VS Code で新しい Teams アプリ メニューを作成する":::
::: zone-end

::: zone pivot="visual-studio"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app-vs.png" alt-text="VS Code で新しい Teams アプリ メニューを作成する":::
::: zone-end

### <a name="automatic-registration-and-configuration"></a>自動登録と構成

時間を節約し、ツールキットが Teams 開発者ポータルにアプリを自動的に登録し、アプリを初めて実行またはデバッグするときに Azure Active Directory などの設定を自動的に構成できるようにします。 Microsoft 365 アカウントでサインインして、アプリを構成する場所を制御し、より柔軟性が必要な場合は、付属の Azure AD マニフェストをカスタマイズします。

::: zone pivot="visual-studio-code"

### <a name="multiple-environments"></a>複数の環境

環境機能を使用すると、さまざまなクラウド リソースのグループを作成して、アプリの実行とテストを簡単にすることができます。 Azure サブスクリプションで "dev" 環境を使用するか、ステージング、テスト、運用用に別のサブスクリプションを持つ新しいサブスクリプションを作成します。

### <a name="quick-access-to-teams-developer-portal"></a>Teams 開発者ポータルへのクイック アクセス

Teams 開発者ポータルにすばやくアクセスし、アプリを構成、配布、管理できます。 詳細については、 [開発者ポータルを使用した Teams アプリの管理に](../concepts/build-and-test/manage-your-apps-in-developer-portal.md)関するページを参照してください。

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="開発者ポータル":::

::: zone-end

::: zone pivot="visual-studio"

#### <a name="teamsfx-net-sdk-reference-docs"></a>TeamsFx .NET SDK リファレンス ドキュメント

* [Microsoft.Extensions.DependencyInjection 名前空間](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Microsoft.TeamsFx 名前空間](/../dotnet/api/Microsoft.TeamsFx)
* [Microsoft.TeamsFx.Configuration 名前空間](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Microsoft.TeamsFx.Conversation 名前空間](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Microsoft.TeamsFx.Helper 名前空間](/../dotnet/api/Microsoft.TeamsFx.Helper)

::: zone-end

## <a name="see-also"></a>関連項目

* [Visual Studio で新しい Teams アプリを作成する](create-new-teams-app-for-Visual-Studio.md)
* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy-teams-app.md)
