---
title: アプリをパッケージ化する
description: テスト、アップロード、ストア発行用に Microsoft Teams アプリをパッケージ化する方法について説明します。
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: d0315f641d345faf58429729d01e187899a4790f
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123991"
---
# <a name="create-a-microsoft-teams-app-package"></a>Microsoft Teams アプリ パッケージを作成する

Microsoft Teams アプリの配布を計画している場合は、アプリ パッケージが必要です。 有効なパッケージは、次を含む ZIP ファイルです。

* **アプリ マニフェスト**: アプリの機能、必要なリソース、その他の重要な属性など、アプリの構成方法について説明します。
* **アプリ アイコン**: 各パッケージには、アプリの色とアウトライン アイコンが必要です。

## <a name="teams-doesnt-host-your-app"></a>Teams でアプリがホストされない

ユーザーが Teams にアプリをインストールすると、構成ファイル (アプリ マニフェストとも呼ばれます) とアプリのアイコンのみを含むアプリ パッケージがインストールされます。 アプリのロジックとデータ ストレージは、開発中のローカルホストや Azure Web サービスなど、他の場所でホストされます。 Teams は HTTPS 経由でこれらのリソースにアクセスします。

:::image type="content" source="../../assets/images/teams-app-host.png" alt-text="Teams アプリのアプリホスティングを示す図" border="true":::

## <a name="app-manifest"></a>アプリ マニフェスト

アプリ マニフェスト ファイルは、名前が付けられている状態で、パッケージのトップ レベルにある必要があります`manifest.json`。

Teams ストアに発行する場合は、マニフェストが最新の [スキーマ](~/resources/schema/manifest-schema.md)を参照していることを確認します。

## <a name="app-icons"></a>アプリのアイコン

アプリ パッケージには、アプリ アイコンの 2 つの .png バージョン (色とアウトライン バージョン) を含める必要があります。

> [!Note]
> アプリにボットまたはメッセージ拡張機能がある場合は、アイコンもMicrosoft Azure Bot Service 登録に含まれます。

アプリが Teams ストア レビューに合格するには、これらのアイコンが次のサイズ要件を満たしている必要があります。

### <a name="color-icon"></a>カラー アイコン

アイコンのカラー バージョンは、ほとんどの Teams シナリオで表示され、192x192 ピクセルである必要があります。 アイコン記号 (96 x 96 ピクセル) は任意の色にすることができますが、単色または完全に透明な正方形の背景に配置する必要があります。

Teams では、アイコンが自動的にトリミングされ、複数のシナリオで角が丸い四角形とボット シナリオの六角形が表示されます。 詳細を失わずにシンボルをトリミングするには、シンボルの周囲に 48 ピクセルのパディングを含める必要があります。

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams のカラーアイコンと設計ガイダンス。" border="false":::

### <a name="outline-icon"></a>アウトライン アイコン

アウトライン アイコンは、次の 2 つのシナリオで表示されます。

* アプリが使用されていて、Teams の左側のアプリ バーで「ホスト」と表示されている場合。
* ユーザーがアプリのメッセージ拡張機能をピン留めする場合。

アイコンは 32x32 ピクセルである必要があります。 透明な背景を持つ白または白の背景を持つ透明にすることができます (他の色は許可されていません)。 アウトライン アイコンは、シンボルの周囲に余分なパディングを含めないことが必要です。

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams アウトライン アイコンの設計ガイダンス。" border="false":::

### <a name="best-practices"></a>ベスト プラクティス

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="アプリ アイコンをデザインする方法を示す図。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>実行: 正確なアウトライン アイコンのガイドラインに従う

アイコンで使用する白の RGB 値は、赤 255、緑: 255、青: 255 である必要があります。 アウトライン アイコンの他のすべての部分は、アルファ チャネルを 0 に設定して、完全に透明にする必要があります。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="アプリ アイコンをデザインしない方法を示す図。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>しないでください: 円形または丸い四角形でトリミングする

アプリ パッケージで送信されるカラーアイコンは正方形である必要があります。 アイコンの角を丸めないでください。 Teams では、角の半径が自動的に調整されます。

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>しないでください: 他のブランドをコピーする

アイコンは、所有していない著作権で保護された製品を模倣してはなりません。 たとえば、Microsoft 製品やブランドに似たデザインです。

### <a name="examples"></a>例

さまざまな Teams の機能とコンテキストでのアプリ アイコンの表示方法を次に示します。

#### <a name="personal-app"></a>個人用アプリ

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="個人用アプリでアプリ アイコンがどのように表示されるかを示す例。" border="false":::

#### <a name="bot-channel"></a>ボット (チャネル)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="チャネル内のボットでアプリ アイコンがどのように表示されるかを示す例。" border="false":::

#### <a name="message-extension"></a>メッセージ拡張機能:

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="代替テキスト" border="false":::

## <a name="next-step"></a>次のステップ

アプリの配布方法を選択します。

> [!div class="nextstepaction"]
> [Teams でアプリをサイドロード](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [組織にアプリを発行する](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [アプリをストアに発行する](~/concepts/deploy-and-publish/appsource/publish.md)

## <a name="see-also"></a>関連項目

[Microsoft Teams の開発者ポータルを使用してアプリを管理する](~/concepts/build-and-test/teams-developer-portal.md)
