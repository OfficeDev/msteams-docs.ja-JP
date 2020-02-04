---
title: アプリをパッケージ化する
description: Microsoft Teams でのテスト、アップロード、発行用にアプリをパッケージ化する方法について説明します。
keywords: teams アプリのパッケージ化
ms.topic: conceptual
ms.openlocfilehash: b76041b129e766dba2b401aaac0e12958a4e9b0d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674994"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a>Microsoft Teams アプリ用のアプリパッケージを作成する

Teams のアプリは、アプリマニフェスト JSON ファイルによって定義され、アプリパッケージにアイコンが付いてバンドルされます。 アプリをアップロードして Teams にインストールし、基幹業務アプリカタログまたは AppSource に発行するには、アプリパッケージが必要です。

Teams アプリパッケージは、次のものを含む .zip ファイルです。

* "Manifest.xml" という名前のマニフェストファイル。このファイルには、アプリの属性を指定し、そのユーザーのために必要なリソースをポイントします。たとえば、そのタブの構成ページの場所や、その bot の Microsoft アプリ ID があります。
* 透明な "アウトライン" アイコンと完全な "色" アイコン。 詳細については、このトピックで後述する[アイコン](#icons)を参照してください。

## <a name="creating-a-manifest"></a>マニフェストの作成

*Teams App Studio*は、マニフェストを構成する際に役立ちます。 また、カードの反応コントロールライブラリと構成可能なサンプルも含まれています。 「 [App Studio の概要](~/concepts/build-and-test/app-studio-overview.md)」を参照してください。

マニフェストファイルの名前は "manifest.xml" で、アップロードパッケージのトップレベルである必要があります。 以前に作成されたマニフェストとパッケージは、古いバージョンのスキーマをサポートしている可能性があることに注意してください。 Teams アプリおよび特に AppSource (以前の Office ストア) 送信の場合は、現在の[マニフェストスキーマ](~/resources/schema/manifest-schema.md)を使用する必要があります。

> [!TIP]
> マニフェストの最初にスキーマを指定して、コードエディターで IntelliSense または同様のサポートを有効にします。
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`

## <a name="icons"></a>アイコン

> [!Note]
> アプリに bot またはメッセージングの拡張機能が含まれている場合、使用されるアイコンは bot フレームワークの bot 登録にアップロードされます。

Microsoft Teams では、アプリの環境で使用するために、2つのアイコンが必要です。 アイコンは、パッケージに含める必要があり、マニフェストの相対パスで参照されている必要があります。 各パスの最大長は2048バイトで、アイコンの形式は .png です。

### <a name="color"></a>color

この`color`アイコンは、Microsoft Teams (アプリとタブ、ボット、flyouts など) 全体で使用されます。 このアイコンは、192x192 ピクセルである必要があります。 アイコンには色 (または色) を指定できますが、背景はブランド化された色にする必要があります。 また、アイコンの bot バージョンのトリミングに対応するために、アイコンの周囲のパディングを小さくする必要があります。

### <a name="outline"></a>outline

この`outline`アイコンは、次の場所で使用されます。ユーザーが "お気に入り" としてマークしたアプリバーとメッセージング拡張機能。 このアイコンは32x32 ピクセルでなければなりません。 アウトラインアイコンには、白と透明度のみが含まれている必要があります (その他の色は使用できません)。 このアイコンは、背景が透明な白色または白の背景で透明にすることができます。 アウトラインアイコンは、アイコンの周囲に特別なパディングを持たないようにする必要があります。32x32 の次元を維持したまま、できるだけトリミングする必要があります。 次に、いくつかの良い例を示します。

![サンプルのアウトラインアイコン](~/assets/images/icons/sample20x20s.png)

たとえば、会社が Contoso であるとします。 2つのアイコンを送信します。

![アイコンショーケース](~/assets/images/framework/framework_submit_icon.png)

UI にアイコンを表示する方法は次のとおりです。

#### <a name="bot-and-chiclet-in-channel-view"></a>[チャネル] ビューのボットと chiclet

![Bot と chiclet UX](~/assets/images/icons/botandchiclet.png)

#### <a name="flyout"></a>ポップアップ

![サンプルの Contoso アイコン](~/assets/images/icons/flyout.png)

#### <a name="app-bar-and-home-screen"></a>アプリバーとホーム画面

![サンプルの Contoso アイコン](~/assets/images/icons/appbarhomescreen.png)
