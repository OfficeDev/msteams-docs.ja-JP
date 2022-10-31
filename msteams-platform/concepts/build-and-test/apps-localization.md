---
title: アプリをローカライズする
description: Microsoft Teams アプリをローカライズし、アプリ マニフェストで文字列をローカライズする際の考慮事項について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/15/2018
ms.openlocfilehash: bd8b579178598b1d485e908f80e9590b27652101
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789871"
---
# <a name="localize-your-app"></a>アプリをローカライズする

Microsoft Teams アプリをローカライズするには、次の要因を考慮してください。

1. [AppSource の一覧をローカライズします](#localize-your-appsource-listing)。
1. [アプリ マニフェスト内の文字列をローカライズします](#localize-strings-in-your-app-manifest)。
1. [ユーザーからのローカライズされたテキストの送信を処理します](#handle-localized-text-submissions-from-your-users)。

## <a name="localize-your-appsource-listing"></a>AppSource の一覧をローカライズする

アプリをストアに発行する場合は、アプリを一覧表示する言語のメタデータ (説明、スクリーンショット、名前) を指定し、パートナー センターの **Marketplace 登録情報** ページでこれらの言語を明示的に指定します。 詳細については、「 [ローカライズされた Microsoft AppSource フロント」を](/office/dev/store/prepare-localized-solutions#localized-microsoft-appsource-fronts)参照してください。 アプリ ストアでローカライズされた登録情報をサポートするには、登録情報に言語を追加できます。 登録情報の [パートナー センター](/office/dev/store/submit-to-appsource-via-partner-center) で指定する既定の言語情報は、 [アプリの AppSource Web サイト](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource は、チームのすべてのニーズに対応する 1 つの場所です。チャット、会議、通話、ファイル、ツールなど、すべてをまとめ、生産性の高いチームワークを実現します。") の一覧に表示されます。 現在、既定の言語は英語です。

### <a name="configure-localization"></a>ローカライズを構成する

アプリの追加の言語を構成するには、 [パートナー センター](/office/dev/store/submit-to-appsource-via-partner-center)で、英語とアプリの追加の言語の両方を選択します。 次の例では、フランス語を追加の言語として使用します。

1. 英語を追加する
    * アプリ名を入力します。
    * アプリの簡単な説明を英語で入力します。
    * アプリの長い説明を英語で入力します。
    * 長い説明に「: **このアプリはフランス語で使用できます**」と入力します。
    * アプリ UI の画像 (英語) をアップロードします。
2. フランス語の追加
    * アプリ名を入力します。
    * フランス語でアプリの簡単な説明を入力します。
    * フランス語でアプリの長い説明を入力します。
    * アプリ UI の画像 (フランス語) をアップロードします。

英語でアップロードした画像は、AppSource で使用されます。

## <a name="localize-strings-in-your-app-manifest"></a>アプリ マニフェストで文字列をローカライズする

Microsoft Teams アプリ スキーマ `v1.5` 以降を使用して、アプリをローカライズします。 これを行うには、manifest.json ファイルの属性を 以上に設定`$schema`し、プロパティを`manifestVersion`バージョン (`1.5`この場合) に`$schema`更新`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`します。

アプリケーションで `localizationInfo` サポートされている既定の言語で プロパティを追加します。 既定の言語は、ユーザーのクライアント設定が追加の言語と一致しない場合、最終的なフォールバック言語として使用されます。

> [!NOTE]
> マニフェスト のバージョンは、manifest.json ファイルと localization.json ファイルの両方で同じである必要があります。

### <a name="example-manifestjson-change"></a>manifest.json の変更の例

次 `manifest.json` は、アプリケーションで `localizationInfo` サポートされている既定の言語と共 `additionalLanguages`に プロパティを追加するのに役立ちます。

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "localizationInfo": {
  "defaultLanguageTag": "en",
  "additionalLanguages": [
   {
    "languageTag": "es-mx",
    "file": "es-mx.json"
   }
  ]
 }
  ...
}
```

### <a name="example-localization-json-change"></a>ローカライズの例 .json の変更

ローカライズ .json の例を次に示します。

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```

マニフェスト内のすべてのユーザー向け文字列の翻訳を含む追加の .json ファイルを提供できます。 これらのファイルは [ローカライズ ファイル JSON スキーマ](../../resources/schema/localization-schema.md) に準拠している必要があり、マニフェストのプロパティに `localizationInfo` 追加する必要があります。 各ファイルは、Teams クライアントが適切な文字列を選択するために使用する言語タグに関連付けられます。 言語タグは の形式をとりますが、目的の `<language>-<region>` 言語を `<region>` サポートするすべてのリージョンをターゲットにするには、この部分を省略できます。

Teams クライアントは、文字列を次の順序で適用します。既定の言語文字列 ->ユーザーの言語のみ文字列 ->ユーザーの言語 + ユーザーのリージョン文字列です。

たとえば、'fr' (フランス語、すべてのリージョン) の既定の言語と、'en' (英語、すべてのリージョン) と 'en-gb' (英語、英国) の追加言語ファイルを指定すると、ユーザーの言語は 'en-gb' に設定されます。 言語の選択に基づいて、次の変更が行われます。

1. Teams クライアントは、'fr' 文字列を受け取り、それらを 'en' 文字列で上書きします。
1. 'en' 文字列を 'en-gb' 文字列で上書きします。

ユーザーの言語が 'en-ca' に設定されている場合、言語の選択に基づいて次の変更が行われます。

1. Teams クライアントは、'fr' 文字列を受け取り、それらを 'en' 文字列で上書きします。
1. 'en-ca' ローカライズは提供されないので、'en' ローカライズが使用されます。

ユーザーの言語が 'es-es' に設定されている場合、Teams クライアントは 'fr' 文字列を受け取ります。 Teams クライアントは、'es' または 'es-es' の翻訳が提供されていないため、言語ファイルの文字列をオーバーライドしません。

そのため、マニフェストで最上位レベルの言語のみの翻訳を指定する必要があります。 たとえば、 `en` ではなく `en-us`です。 リージョン レベルのオーバーライドは、それらを必要とするいくつかの文字列に対してのみ指定する必要があります。

### <a name="example-manifestjson-change"></a>manifest.json の変更の例

変更は `manifest.json` 、次の例に示されています。

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en",
    "additionalLanguages": [
      {
        "languageTag": "en-gb",
        "file": "en-gb.json"
      },
      {
        "languageTag": "fr",
        "file": "fr.json"
      },
      {
        "languageTag": "pl",
        "file": "pl.json"
      }
    ]
  }
  ...
}
```

### <a name="example-localization-json-file"></a>ローカライズ .json ファイルの例

 変更は `localization.json` 、次の例に示されています。

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "name.short": "Le App",
  "name.full": "App pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

## <a name="handle-localized-text-submissions-from-your-users"></a>ユーザーからのローカライズされたテキストの送信を処理する

ローカライズされたバージョンのアプリケーションを指定すると、ユーザーは同じ言語で応答します。 Teams ではユーザーの申請が既定の言語に翻訳されないため、アプリはローカライズされた言語の応答を処理する必要があります。 たとえば、ローカライズされた を指定した `commandList`場合、ボットへの応答は、既定の言語ではなく、コマンドのローカライズされたテキストです。 アプリは適切に応答する必要があります。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | .NET | Node.js |
|-------------|-------------|------|------|
| アプリのローカライズ | ボットとタブを使用した Teams アプリのローカライズ。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>関連項目

* [JSON スキーマの参照のローカライズ](~/resources/schema/localization-schema.md)
