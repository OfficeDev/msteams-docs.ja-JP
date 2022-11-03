---
title: Teams ツールキットの概要
author: zyxiaoyuer
description: このモジュールでは、Teams Toolkit、Teams Toolkit のインストール、および Teams Toolkit のユーザー体験について説明します
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: cb3508bdd22f9d05c48e71b1b90ec4ffbf4c56af
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833164"
---
# <a name="teams-toolkit-overview"></a>Teams ツールキットの概要

Teams Toolkit を使用すると、Visual Studio と Visual Studio Code を使用して Microsoft Teams のアプリ開発を簡単に開始できます。

* プロジェクト テンプレートまたはサンプルから開始します。
* 自動アプリの登録と構成により、セットアップ時間を節約できます。
* 使い慣れたツールから Teams を直接実行してデバッグします。
* コードとしてのインフラストラクチャと Bicep を使用した Azure でのホスティングのスマートな既定値。
* 環境機能を使用して、開発、テスト、prod などの一意の構成を作成します。
* 組み込みの発行ツールを使用して、アプリを組織または Teams App Storeに持ち込みます。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Teams ツールキットのユーザー体験" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

## <a name="available-for-visual-studio-and-visual-studio-code"></a>Visual Studio および Visual Studio Code で使用できます

Teams Toolkit は Visual Studio Code で無料で利用でき、Visual Studio 2022 Community、Professional、Enterprise をサポートしています。 インストールとセットアップの詳細については、 [Teams Toolkit](./install-Teams-Toolkit.md) のインストールに関するドキュメントを参照してください。

| Teams ツールキット | Visual Studio | Visual Studio Code |
| - | ------------- | ------------------ |
| インストール | Visual Studio インストーラーで利用可能 | VS Marketplace で使用できる |
| を使用してビルドする | C#、.NET、ASP.NET、Blazor | JavaScript、TypeScript、React、SPFx |

## <a name="features"></a>機能

### <a name="project-templates"></a>プロジェクト テンプレート

Teams Toolkit を使用すると、一般的な基幹業務アプリのシナリオとスマートな既定値のテンプレートの使用を開始する際の複雑さが軽減され、運用までの時間が短縮されます。 Teams アプリ開発に既に精通している場合は、機能に焦点を当てたテンプレートから直接開始することもできます。 つまり、Tab、Bot、Messaging Extension です。

::: zone pivot="visual-studio-code"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app.png" alt-text="VS Code で新しい Teams アプリ メニューを作成する":::
::: zone-end

::: zone pivot="visual-studio"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app-vs.png" alt-text="VS Code で新しい Teams アプリ メニューを作成する":::
::: zone-end

### <a name="automatic-registration-and-configuration"></a>自動登録と構成

時間を節約し、ツールキットが Teams 開発者ポータルでアプリを自動的に登録し、アプリを初めて実行またはデバッグするときに Azure Active Directory などの設定を自動的に構成できるようにします。 Microsoft 365 アカウントでサインインして、アプリを構成する場所を制御し、より柔軟性が必要な場合に含まれる Azure AD マニフェストをカスタマイズします。

::: zone pivot="visual-studio-code"

### <a name="multiple-environments"></a>複数の環境

環境機能を使用すると、クラウド リソースのさまざまなグループを作成して、アプリの実行とテストを簡単にすることができます。 Azure サブスクリプションで "dev" 環境を使用するか、ステージング、テスト、運用用に別のサブスクリプションを持つ新しい環境を作成します。

### <a name="quick-access-to-teams-developer-portal"></a>Teams 開発者ポータルへのクイック アクセス

Teams 開発者ポータルにすばやくアクセスします。このポータルでは、アプリの構成、配布、管理を行うことができます。 詳細については、「 [開発者ポータルを使用して Teams アプリを管理](../concepts/build-and-test/manage-your-apps-in-developer-portal.md)する」を参照してください。

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

* [Visual Studio で新しい Teams アプリを作成する](create-new-project.md)
* [Visual Studio を使用してクラウド リソースをプロビジョニングする](provision-cloud-resources.md)
* [Visual Studio を使用して Teams アプリをクラウドに展開する](deploy.md)
