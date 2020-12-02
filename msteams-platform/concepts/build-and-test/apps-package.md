---
title: アプリをパッケージ化する
description: Microsoft Teams で、テスト用、アップロード用、公開用のアプリをパッケージ化する方法について説明します
keywords: Teams のアプリのパッケージ化
ms.topic: conceptual
ms.openlocfilehash: 4c20e2c1b3c8d7ef13d16b354449887b3c0f1147
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552571"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>Microsoft Teams アプリのアプリ パッケージを作成する

Teams のアプリは、アプリ マニフェスト JSON ファイルによって定義され、各アイコンがアプリ パッケージにバンドルされます。 Teams にアプリをアップロードしてインストールし、基幹業務アプリ カタログまたは AppSource に公開するには、アプリ パッケージが必要です。

Teams アプリ パッケージは、次のものを含む .zip ファイルです。

* "manifest.json" という名前のマニフェスト ファイル。これは、アプリの属性を指定し、ユーザーが操作するために必要なリソースを指し示します。たとえば、タブ構成ページの場所や、ボット用の Microsoft アプリ ID などです。
* 透明な "outline" アイコンと、完全な "color" アイコン。 詳細については、このトピックで後述する「[アイコン](#icons)」を参照してください。

## <a name="creating-a-manifest"></a>マニフェストの作成

*Teams App Studio* は、マニフェストを構成する際に役立ちます。 React 制御ライブラリとカード用の構成可能なサンプルも含まれています。 「[App Studio の概要](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。

マニフェスト ファイルは、"manifest.json" という名前で、アップロード パッケージの最上位レベルになければなりません。 以前に作成されたマニフェストとパッケージは、古いバージョンのスキーマをサポートしている可能性があることに注意してください。 Teams アプリ、特に AppSource (以前の Office ストア) 配信の場合は、最新の[マニフェスト スキーマ](~/resources/schema/manifest-schema.md)を使用する必要があります。

> [!TIP]
> マニフェストの最初にスキーマを指定して、コード エディターで IntelliSense または同様のサポートを有効にします。
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="icons"></a>アイコン

> [!Note]
> アプリにボットまたはメッセージングの拡張機能が含まれている場合、使用されるアイコンは Bot Framework のボット登録にアップロードされたアイコンになります。

Microsoft Teams では、アプリを製品内で使用するために、2 つのアイコンが必要です。 アイコンは、パッケージに含められ、マニフェストの相対パスで参照されている必要があります。 各パスの最大長は 2048 バイトで、アイコンの形式は .png です。

### <a name="color"></a>color

`color` アイコンは Microsoft Teams のあらゆる箇所で使用されます (アプリやタブのギャラリー、ボット、フライアウトなど)。 このアイコンは、192x192 ピクセルである必要があります。 アイコンにはどんな色 (または複数色) でも指定できますが、背景はブランド化されたアクセント カラーにする必要があります。 また、ボット バージョンのアイコンでの六角形のトリミングに対応するために、アイコンの周囲に少しパディングを設ける必要があります。

### <a name="outline"></a>outline

`outline` アイコンは、ユーザーが "お気に入り" としてマークしたアプリ バーやメッセージングの拡張機能で使用されます。 このアイコンは、32x32 ピクセルである必要があります。 outline アイコンには、白色と透明色のみを含めます (その他の色は使用できません)。 このアイコンは、背景が透明な白色、または背景が白の透明色にできます。 outline アイコンでは、アイコンの周囲に特別なパディングを設けないようにする必要があります。また、32x32 のサイズを維持したまま、できるだけタイトにトリミングする必要があります。 次にいくつかの良い例を示します。

![outline アイコンの例](~/assets/images/icons/sample20x20s.png)

[!ヒントを作成して透明アイコンを作成する

* 色は RGB では "白" にする必要があります (赤: 255, Green: 255, Blue: 255)。
* その他のアイコンの一部は透明にする必要があります。
* 渡す場合は、アルファチャネルの値が0の小さいアイコンが完全に透明である必要があります。その他の値は fail です。

たとえば、会社が Contoso であるとします。 2 つのアイコンを提出します。

![アイコン ショーケース](~/assets/images/framework/framework_submit_icon.png)

アイコンは以下のように UI に表示されます。

#### <a name="bot-and-chiclet-in-channel-view"></a>[チャネル] ビューのボットとチクレット

![ボットとチクレット UX](~/assets/images/icons/botandchiclet.png)

#### <a name="flyout"></a>ポップアップ

![サンプル Contoso フライアウト](~/assets/images/icons/flyout.png)

#### <a name="app-bar-and-home-screen"></a>アプリ バーとホーム画面

![サンプル Contoso app bar homescreen](~/assets/images/icons/appbarhomescreen.png)
