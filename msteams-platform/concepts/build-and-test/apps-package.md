---
title: アプリをパッケージ化する
description: テスト、アップロード、ストア発行用にMicrosoft Teams アプリをパッケージ化する方法について説明します。
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 219e2d5341707ed51b7e0a3a8077f93df9eac640
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565215"
---
# <a name="create-a-microsoft-teams-app-package"></a>Microsoft Teams アプリ パッケージを作成する

Microsoft Teams アプリを配布する予定のアプリ パッケージが必要です。 有効なパッケージは、次の内容を含む ZIP ファイルです。

* **アプリ マニフェスト**: アプリの機能、必要なリソース、その他の重要な属性など、アプリの構成方法を説明します。
* **アプリアイコン**: 各パッケージには、アプリの色とアウトラインアイコンが必要です。

## <a name="app-manifest"></a>アプリ マニフェスト

アプリ マニフェスト ファイルは、パッケージの最上位レベルにという名前を付ける必要があります `manifest.json` 。 

Teams ストアに発行する場合は、マニフェストが最新[のスキーマ](~/resources/schema/manifest-schema.md)を参照していることを確認します。

## <a name="app-icons"></a>アプリアイコン

アプリ パッケージには、アプリ アイコンの 2 つの PNG バージョン (色とアウトライン バージョン) を含める必要があります。

> [!Note]
> アプリにボットまたはメッセージング拡張機能がある場合、アイコンもMicrosoft Azure Bot サービス登録に含まれます。

アプリがストアレビュー Teams渡すためには、これらのアイコンが次のサイズ要件を満たしている必要があります。

### <a name="color-icon"></a>カラーアイコン

アイコンの色バージョンは、ほとんどのTeamsシナリオで表示され、192x192 ピクセルである必要があります。 アイコンシンボル(96x96 ピクセル)は任意の色にできますが、塗りつぶされた四角形または完全に透明な四角形の背景に置く必要があります。

Teamsは自動的にアイコンをトリミングして、複数のシナリオで角丸い四角形、ボットシナリオでは六角形の形状を表示します。 詳細を失うことなくシンボルをトリミングするには、シンボルの周囲に 48 ピクセルのパディングを含めます。

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="色のアイコンとデザイン ガイダンスをTeamsします。" border="false":::

### <a name="outline-icon"></a>アウトライン アイコン

アウトライン アイコンは、次の 2 つのシナリオで表示されます。

* アプリが使用中で、Teamsの左側のアプリ バーで "買い上げ" を行った場合。
* ユーザーがアプリのメッセージング拡張機能をピンで固定する場合。

アイコンは 32x32 ピクセルである必要があります。 透明な背景を持つ白、または白い背景を持つ透明にすることができます(他の色は許可されません)。 アウトライン アイコンには、記号の周囲に余分なパディングを付けないでください。

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teamsアウトライン アイコンのデザイン ガイダンスです。" border="false":::

### <a name="best-practices"></a>ベスト プラクティス

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="アプリ アイコンのデザイン方法を示す図。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>行う: アウトライン アイコンのガイドラインに従う

アイコンで使用する白の RGB 値は、赤:255、緑:255、青:255 でなければなりません。 アウトライン アイコンの他のすべての部分は、アルファ チャネルが 0 に設定された完全に透明である必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="アプリ アイコンをデザインしない方法を示す図。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>しない: 円形または丸い正方形の形でトリミング

アプリ パッケージに提出される色アイコンは、正方形である必要があります。 アイコンの角を丸めないでください。 Teamsは、コーナー半径を自動的に調整します。

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>しない: 他のブランドをコピーする

アイコンは、所有していない著作権で保護された製品を模倣してはなりません。 たとえば、Microsoft 製品やブランドに似たデザインです。

### <a name="examples"></a>例

さまざまなTeams機能とコンテキストでアプリアイコンがどのように表示されるのかは次のとおりです。

#### <a name="personal-app"></a>パーソナルアプリ

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="個人用アプリでのアプリ アイコンの外観を示す例。" border="false":::

#### <a name="bot-channel"></a>ボット (チャネル)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="チャネル内のボットでアプリ アイコンがどのように表示されるかを示す例。" border="false":::

#### <a name="messaging-extension"></a>メッセージング拡張機能

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text=" 代替テキスト>を<" border="false":::

## <a name="next-step"></a>次の手順

アプリの配布方法を選択します。

> [!div class="nextstepaction"]
> [Teamsでアプリをサイドロードする](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [組織へのアプリの公開](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [アプリをストアに公開する](~/concepts/deploy-and-publish/appsource/publish.md)
