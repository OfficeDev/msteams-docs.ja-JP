---
title: アプリをパッケージ化する
description: テスト、アップロード、およびストア発行Microsoft Teamsアプリをパッケージ化する方法について学習します。
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 44b8f21361c39bd723ff375b385569125b65ea27
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889308"
---
# <a name="create-a-microsoft-teams-app-package"></a>アプリ パッケージMicrosoft Teams作成する

ただし、アプリ パッケージは必要ですが、アプリパッケージを配布Microsoft Teamsします。 有効なパッケージは、次を含む ZIP ファイルです。

* **アプリ マニフェスト**: アプリの機能、必要なリソース、その他の重要な属性など、アプリの構成方法について説明します。
* **アプリアイコン**: 各パッケージには、アプリの色とアウトラインアイコンが必要です。

## <a name="app-manifest"></a>アプリ マニフェスト

アプリ マニフェスト ファイルは、パッケージのトップ レベルに名前が付けられている必要があります `manifest.json` 。 

ストアに発行するTeams、マニフェストが最新のスキーマを参照している必要[があります](~/resources/schema/manifest-schema.md)。

## <a name="app-icons"></a>アプリのアイコン

アプリ パッケージには、2 つの PNG バージョンのアプリ アイコン (色とアウトライン バージョン) が含まれる必要があります。

> [!Note]
> アプリにボットまたはメッセージング拡張機能がある場合は、ボット サービスの登録にアイコンMicrosoft Azure含まれます。

アプリがストア レビューに合格Teams、これらのアイコンは次のサイズ要件を満たしている必要があります。

### <a name="color-icon"></a>色アイコン

アイコンのカラー バージョンは、ほとんどの Teams シナリオで表示され、192x192 ピクセルである必要があります。 アイコン 記号 (96x96 ピクセル) は任意の色を指定できますが、単色または完全に透明な四角形の背景に位置する必要があります。

Teamsアイコンが自動的にトリミングされ、複数のシナリオで角が丸く、ボットのシナリオでは六角形が表示されます。 詳細を失わずにシンボルをトリミングするには、シンボルの周囲に 48 ピクセルのパディングを含める必要があります。

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teamsアイコンとデザインガイダンスを参照してください。" border="false":::

### <a name="outline-icon"></a>アウトライン アイコン

アウトライン アイコンは、次の 2 つのシナリオで表示されます。

* アプリが使用されている場合は、アプリの左側にあるアプリ バーに "起Teams。
* ユーザーがアプリのメッセージング拡張機能をピンで固定する場合。

アイコンは 32x32 ピクセルである必要があります。 透明な背景を持つ白、または白い背景を持つ透明な色を指定できます (他の色は使用できません)。 アウトライン アイコンには、シンボルの周囲に余分なパディングを配置する必要はありません。

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teamsアイコンの設計ガイダンスを参照してください。" border="false":::

### <a name="best-practices"></a>ベスト プラクティス

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="アプリ アイコンを設計する方法を示す図。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>Do: 正確なアウトライン アイコンのガイドラインに従います

アイコンで使用する白の RGB 値は、赤: 255、緑: 255、青: 255 である必要があります。 アウトライン アイコンの他のすべての部分は完全に透明で、アルファ チャネルは 0 に設定されている必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="アプリ アイコンをデザインしない方法を示す図。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>[しない]: 円形または丸い四角形でトリミングする

アプリ パッケージで送信される色アイコンは正方形である必要があります。 アイコンの角を丸めない。 Teamsコーナーの半径を自動的に調整します。

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>[しない]: 他のブランドをコピーする

アイコンは、自分が所有していない著作権で保護された製品を模倣しなけらねない。 たとえば、Microsoft 製品やブランドに似たデザインです。

### <a name="examples"></a>例

さまざまな機能とコンテキストでアプリ アイコンTeams次に示します。

#### <a name="personal-app"></a>個人用アプリ

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="個人用アプリでアプリ アイコンがどのように表示されるのか示す例。" border="false":::

#### <a name="bot-channel"></a>ボット (チャネル)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="チャネル内のボットでアプリ アイコンがどのように表示されるのか示す例。" border="false":::

#### <a name="messaging-extension"></a>メッセージング拡張機能

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<代替テキスト>" border="false":::

## <a name="next-step"></a>次のステップ

アプリの配布方法を選択します。

> [!div class="nextstepaction"]
> [アプリをサイドロードTeams](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [組織にアプリを発行する](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [アプリをストアに発行する](~/concepts/deploy-and-publish/appsource/publish.md)

## <a name="see-also"></a>関連項目

[開発者ポータルを使用してアプリを管理Microsoft Teams](~/concepts/build-and-test/teams-developer-portal.md)