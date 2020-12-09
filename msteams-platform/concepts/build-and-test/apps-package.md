---
title: アプリをパッケージ化する
description: 発行をテスト、アップロード、および保存するために Microsoft Teams アプリをパッケージ化する方法について説明します。
ms.topic: conceptual
ms.openlocfilehash: 6929375c8d6a1602f01d83d15bfa0dab7f02a664
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605289"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>Microsoft Teams アプリのアプリ パッケージを作成する

Teams のアプリは、アプリ マニフェスト JSON ファイルによって定義され、各アイコンがアプリ パッケージにバンドルされます。 アプリをアップロードして Teams にインストールし、基幹業務アプリカタログまたは AppSource に発行するには、アプリパッケージが必要です。

Teams アプリ パッケージは、次のものを含む .zip ファイルです。

* という名前のマニフェストファイル。アプリの属性を指定して、その機能に `manifest.json` 必要なリソースをポイントします。たとえば、そのタブの構成ページの場所や、その bot の Microsoft アプリ ID を指定します。
* [アプリの色とアウトラインアイコン](#app-icons)。

## <a name="creating-a-manifest"></a>マニフェストの作成

*Teams App Studio* は、マニフェストを構成する際に役立ちます。 React 制御ライブラリとカード用の構成可能なサンプルも含まれています。 「[App Studio の概要](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。

マニフェスト ファイルは、"manifest.json" という名前で、アップロード パッケージの最上位レベルになければなりません。 以前に作成されたマニフェストとパッケージは、古いバージョンのスキーマをサポートしている可能性があることに注意してください。 Teams アプリ、特に AppSource (以前の Office ストア) 配信の場合は、最新の[マニフェスト スキーマ](~/resources/schema/manifest-schema.md)を使用する必要があります。

> [!TIP]
> マニフェストの最初にスキーマを指定して、コード エディターで IntelliSense または同様のサポートを有効にします。
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="app-icons"></a>アプリのアイコン

アプリパッケージには、2つの PNG バージョンのアプリアイコン (カラーアイコンとアウトラインアイコン) が含まれている必要があります。 アプリが AppSource レビューに合格するには、これらのアイコンが次のサイズ要件を満たしている必要があります。

> [!Note]
> アプリに bot またはメッセージングの拡張機能がある場合は、それらのアイコンも Microsoft Azure Bot サービスの登録に含まれます。

### <a name="color-icon"></a>色アイコン

アイコンのカラーバージョンは、ほとんどの Teams のシナリオで表示され、192x192 ピクセルである必要があります。 アイコン記号 (96x96 ピクセル) は任意の色または色にすることができますが、単色または完全に透明な四角形の背景上に配置する必要があります。

Teams では、複数のシナリオで角の丸い四角形が表示されるように自動的にアイコンがトリミングされます。 シンボルの周囲に48ピクセルのパディングを含めることにより、ディテールを失わずにこれらのトリミングを行うことができるようにします。

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams のカラーアイコン設計ガイダンス。" border="false":::

### <a name="outline-icon"></a>アウトラインアイコン

アウトラインアイコンは2つのシナリオで表示されます。

* アプリが使用中で、Teams の左側にあるアプリバーで "ホイストされた"。
* ユーザーがアプリのメッセージング拡張機能を固定するとき。

アイコンは32x32 ピクセルでなければなりません。 背景を透明にする、または背景を透明にすることができます (他の色は使用できません)。 アウトラインアイコンには、記号の周りに特別なスペースを含めることはできません。

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams のカラーアイコン設計ガイダンス。" border="false":::

### <a name="best-practices"></a>ベスト プラクティス

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="アプリアイコンを設計する方法を示す図。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>Do: 正確なアウトラインアイコンのガイドラインに従う

アイコンで使用される白の RGB 値は、赤である必要があります: 255、Green: 255、Blue: 255。 アウトラインアイコンの他の部分はすべて完全に透明にする必要があり、アルファチャネルを0に設定します。

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="アプリアイコンをデザインする方法を示す図。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>[いいえ: 円形または角丸正方形] 図形でトリミングします。

アプリパッケージで送信されるカラーアイコンは、正方形である必要があります。 アイコンの角を丸くしないようにしてください。 Teams では、角の半径が自動的に調整されます。

   :::column-end:::
:::row-end:::

### <a name="examples"></a>例

アプリアイコンをさまざまなチームの機能やコンテキストで表示する方法は次のとおりです。

#### <a name="personal-app"></a>個人用アプリ

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="アプリアイコンが個人用アプリでどのように表示されるかを示す例。" border="false":::

#### <a name="bot-channel"></a>Bot (チャネル)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="アプリアイコンがチャネル内のボットをどのように表示されるかを示す例。" border="false":::

#### <a name="messaging-extension"></a>メッセージング拡張機能

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<代替テキスト>" border="false":::
