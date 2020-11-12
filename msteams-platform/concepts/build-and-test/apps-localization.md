---
title: チームアプリのローカライズ
description: アプリのローカライズに関する問題について説明します。
keywords: teams 発行ストア office 発行アプリソースのローカライズ言語
ms.date: 05/15/2018
ms.openlocfilehash: 7af8018414b6ec72c45639a2a370166c24185af6
ms.sourcegitcommit: 0aeb60027f423d8ceff3b377db8c3efbb6da4d17
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "48997980"
---
# <a name="localization-for-microsoft-teams-apps"></a>Microsoft Teams アプリのローカライズ

Microsoft Teams アプリをローカライズする場合は、考慮する必要がある3つの主要な領域があります。

1. AppSource リスト (アプリストアに公開している場合)。
1. アプリケーションマニフェスト内のエンドユーザーが使用している文字列 (bot コマンドなど)。
1. ユーザーから送信されるローカライズされたテキストに応答する。

## <a name="localizing-your-appsource-listing"></a>AppSource リストのローカライズ

アプリストアに発行している場合は、AppSource リストのローカライズがまだサポートされていないことに注意する必要があります。 ただし、アプリストアでローカライズされたリストをサポートするための準備として、追加の言語を一覧に追加することができます。 現在、リストの [パートナーセンター](/office/dev/store/submit-to-appsource-via-partner-center) で提供される既定の (英語) の言語情報のみが、アプリの [appsource web サイト](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) の一覧に表示されます。

アプリの追加の言語を構成するには、 [パートナーセンター](/office/dev/store/submit-to-appsource-via-partner-center)で、英語とアプリの追加言語を選択します。 この例では、フランス語が使用されています。

1. 英語の言語を追加する
    * アプリ名を入力します。
    * アプリの簡単な説明を英語で入力します。
    * アプリの詳しい説明を英語で入力します。
    * 詳細については、「このアプリは、フランス語で利用可能です」という行も追加してください。
    * アプリ UI の画像 (英語) をアップロードします。
2. フランス語を追加する
    * アプリ名を入力します。
    * フランス語でアプリの簡単な説明を記入します。
    * アプリの詳しい説明をフランス語で入力します。
    * アプリの UI のイメージ (フランス語) をアップロードします。

英語を使用してアップロードする画像は、AppSource で使用されているものになります。

## <a name="localizing-the-strings-in-your-app-manifest"></a>アプリマニフェスト内の文字列のローカライズ

アプリを適切にローカライズするには、Microsoft Teams アプリスキーマ v1.1 を使用する必要があります。 これを行うには、 `$schema` ファイルの manifest.jsの属性を ' ' に設定 https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json し、' manifestversion ' プロパティを ' 1.7 ' に更新します。

### <a name="example-manifestjson-change"></a>変更時の manifest.js例

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

次に、アプリケーションでサポートされている既定の言語で ' localizationInfo ' プロパティを追加します。 ユーザーのクライアント設定がその他の言語と一致しない場合、既定の言語が最終的なフォールバック言語として使用されます。

### <a name="example-manifestjson-change"></a>変更時の manifest.js例

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

マニフェスト内のすべてのユーザーが接続した文字列の翻訳を含む、追加の json ファイルを提供できます。 これらのファイルは、 [ローカライズファイル JSON スキーマ](../../resources/schema/localization-schema.md) に準拠している必要があり、マニフェストの ' localizationInfo ' プロパティに追加されている必要があります。 各ファイルは、Teams クライアントが適切な文字列を選択するために使用する言語タグに関連付けています。 言語タグはの形式を取り <language> - <region> ますが、目的の言語を <region> サポートするすべての地域を対象とした部分を省略することをお勧めします。

Teams クライアントは、次の順序で文字列を適用します。 default language strings-> user's language only 文字列-> ユーザーの言語 + ユーザーの地域文字列。

たとえば、既定の言語である "fr" (フランス語、すべての地域)、および ' en ' (英語、すべての地域) と ' en gb ' (英語、英国) の追加の言語ファイルを指定します。 ユーザーの言語が "en gb" に設定されている場合:

1. Teams クライアントは、' fr ' 文字列を ' en ' 文字列で上書きする必要があります。
2. これらの文字列を ' en gb ' の文字列で上書きします。

ユーザーの言語が "en-us" に設定されている場合: 

1. Teams クライアントは、' fr ' 文字列を ' en ' 文字列で上書きする必要があります。
2. ' En-ca ' ローカライズは提供されていないため、' en ' ローカライズが使用されます。

ユーザーの言語が "es-es" に設定されている場合、Teams クライアントは ' fr ' 文字列を受け取ります。これらの言語ファイルでは上書きされません。

そのため、マニフェストには、("en-us" の代わりに ' en ' ではなく) 最上位レベルの翻訳を言語のみで提供し、地域レベルの上書きのみを必要とする少数の文字列に対して提供することを強くお勧めします。

### <a name="example-manifestjson-change"></a>変更時の manifest.js例

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

### <a name="example-localization-json-file"></a>ローカライズの例-json ファイル

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a>ユーザーからのローカライズされたテキストの送信を処理する

アプリケーションのローカライズ版を提供している場合は、ユーザーが同じ言語で応答することが非常に高い可能性があります。 Teams はユーザーの送信を既定の言語に変換しないので、アプリでそれを処理する必要があります。 たとえば、ローカライズを指定すると、 `commandList` ボットへの応答は、既定の言語ではなく、コマンドのローカライズされたテキストになります。 アプリは適切に応答する必要があります。
