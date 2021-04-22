---
title: アプリをパッケージ化する
description: テスト、アップロード、およびストア発行のために Microsoft Teams アプリをパッケージ化する方法について説明します。
ms.topic: conceptual
ms.openlocfilehash: 222ea5459b3496c00b1186f15a68c3288ce419f7
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922511"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>Microsoft Teams アプリのアプリ パッケージを作成する

Teams のアプリは、アプリ マニフェスト JSON ファイルによって定義され、各アイコンがアプリ パッケージにバンドルされます。 アプリを Teams にアップロードしてインストールし、Line of Business アプリ カタログまたは AppSource に発行するには、アプリ パッケージが必要です。

Teams アプリ パッケージは、次のものを含む .zip ファイルです。

* アプリの属性を指定し、そのタブ構成ページの場所やボットの Microsoft アプリ ID など、エクスペリエンスに必要なリソースを示すという名前のマニフェスト ファイル `manifest.json` 。
* [アプリの色とアウトラインのアイコン](#app-icons)です。

## <a name="creating-a-manifest"></a>マニフェストの作成

**Teams App Studio** は、マニフェストを構成する際に役立ちます。 React 制御ライブラリとカード用の構成可能なサンプルも含まれています。 詳細については [、「App Studio の概要」を参照してください](~/concepts/build-and-test/app-studio-overview.md)。

マニフェスト ファイルは、"manifest.json" という名前で、アップロード パッケージの最上位レベルになければなりません。 以前に作成されたマニフェストとパッケージは、古いバージョンのスキーマをサポートしている可能性があることに注意してください。 Teams アプリ、特に AppSource (以前の Office ストア) 配信の場合は、最新の[マニフェスト スキーマ](~/resources/schema/manifest-schema.md)を使用する必要があります。

> [!TIP]
> マニフェストの最初にスキーマを指定して、コード エディターで IntelliSense または同様のサポートを有効にします。
>
> `"$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",`
 
## <a name="app-icons"></a>アプリのアイコン

アプリ パッケージには、色アイコンとアウトライン アイコンという 2 つの PNG バージョンのアプリ アイコンが含まれる必要があります。 アプリが AppSource レビューに合格するには、これらのアイコンが次のサイズ要件を満たしている必要があります。

> [!Note]
> アプリにボットまたはメッセージング拡張機能がある場合は、Microsoft Azure Bot Service 登録にもアイコンが含まれます。

### <a name="color-icon"></a>色アイコン

アイコンの色バージョンは、ほとんどの Teams シナリオに表示され、192x192 ピクセルである必要があります。 アイコン 記号 (96x96 ピクセル) は、任意の色または色を指定できますが、単色または完全に透明な四角形の背景に位置する必要があります。

Teams では、アイコンが自動的にトリミングされ、複数のシナリオで角が丸く、ボットのシナリオでは六角形が表示されます。 シンボルの周囲に 48 ピクセルのパディングを含めるので、詳細を失わずにこれらのトリミングを行います。

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams カラー アイコンの設計ガイダンス。" border="false":::

### <a name="outline-icon"></a>アウトライン アイコン

アウトライン アイコンは、次の 2 つのシナリオで表示されます。

* Teams の左側のアプリ バーでアプリが使用され、"起重" されている場合。
* ユーザーがアプリのメッセージング拡張機能をピンで固定する場合。

アイコンは 32x32 ピクセルである必要があります。 透明な背景を持つ白、または白い背景を持つ透明な色を指定できます (他の色は使用できません)。 アウトライン アイコンには、シンボルの周囲に余分なパディングを配置する必要はありません。

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams のアウトライン アイコンの設計ガイダンス。" border="false":::

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

アプリ パッケージで送信される色アイコンは正方形である必要があります。 アイコンの角を丸めない。 Teams はコーナーの半径を自動的に調整します。

   :::column-end:::
:::row-end:::

### <a name="examples"></a>例

さまざまな Teams の機能とコンテキストでアプリ アイコンを表示する方法を次に示します。

#### <a name="personal-app"></a>個人用アプリ

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="個人用アプリでアプリ アイコンがどのように表示されるのか示す例。" border="false":::

#### <a name="bot-channel"></a>ボット (チャネル)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="チャネル内のボットでアプリ アイコンがどのように表示されるのか示す例。" border="false":::

#### <a name="messaging-extension"></a>メッセージング拡張機能

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<代替テキスト>" border="false":::
