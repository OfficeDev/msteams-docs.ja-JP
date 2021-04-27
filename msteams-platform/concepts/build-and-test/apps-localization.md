---
title: アプリのローカライズ
description: Microsoft Teams アプリのローカライズに関する考慮事項について説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: teams publishs store office publishing AppSource ローカライズ言語
ms.date: 05/15/2018
ms.openlocfilehash: 8490230ad0b268d402a9ad7deb5f8b1e3f420f9d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020850"
---
# <a name="localization-for-microsoft-teams-apps"></a>Microsoft Teams アプリのローカライズ

Microsoft Teams アプリをローカライズする場合、考慮する必要がある主な 3 つの領域があります。

1. AppSource リスト (アプリ ストアに発行する場合)。
1. アプリ マニフェスト内のエンド ユーザー向け文字列 (ボット コマンドなど)。
1. ユーザーから送信されたローカライズされたテキストへの応答。

## <a name="localizing-your-appsource-listing"></a>AppSource リストのローカライズ

アプリ ストアに発行する場合は、AppSource リストのローカライズがまだサポートされていないことに注意する必要があります。 ただし、アプリ ストアでのローカライズされたリストのサポートに備えて、リスティングに追加の言語を追加できます。 現在、登録情報のパートナー センターで指定した既定[](/office/dev/store/submit-to-appsource-via-partner-center)の (英語) 言語情報だけが、アプリの[AppSource Web](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)サイトの一覧に表示されます。

アプリの追加の言語を構成するには、 [パートナー](/office/dev/store/submit-to-appsource-via-partner-center)センターで、英語とアプリの追加言語の両方を選択します。 この例ではフランス語を使用します。

1. 英語を追加する
    * アプリ名を入力します。
    * アプリの簡単な説明を英語で入力します。
    * アプリの長い説明を英語で入力します。
    * 長い説明では、「このアプリは"フランス語"で利用可能です」という行も追加してください。
    * アプリ UI の画像をアップロードします (英語)。
2. フランス語を追加する
    * アプリ名を入力します。
    * フランス語でアプリの簡単な説明を入力します。
    * フランス語でアプリの長い説明を入力します。
    * アプリ UI の画像をアップロードします (フランス語)。

英語でアップロードする画像は、AppSource で使用されるイメージです。

## <a name="localizing-the-strings-in-your-app-manifest"></a>アプリ マニフェスト内の文字列のローカライズ

アプリを適切にローカライズするには、Microsoft Teams アプリ スキーマ v1.5 以上を使用する必要があります。 これを行うには、manifest.json ファイルの属性を ' に設定し `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json 、'manifestVersion' プロパティを '1.7' に更新します。

### <a name="example-manifestjson-change"></a>変更時manifest.js例

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

次に、アプリケーションでサポートされている既定の言語で 'localizationInfo' プロパティを追加します。 ユーザーのクライアント設定が追加の言語と一致しない場合は、既定の言語が最終的なフォールバック言語として使用されます。

### <a name="example-manifestjson-change"></a>変更時manifest.js例

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

マニフェスト内のすべてのユーザー向け文字列の翻訳を含む追加の .json ファイルを提供できます。 これらのファイルは、ローカライズ ファイル [JSON](../../resources/schema/localization-schema.md) スキーマに準拠している必要があります。マニフェストの 'localizationInfo' プロパティに追加する必要があります。 各ファイルは、Teams クライアントが適切な文字列を選択するために使用する言語タグに関連付けされます。 言語タグの形式を使用しますが、目的の言語をサポートしているすべての地域を対象とする部分を省略 <language> - <region> <region> することが推奨されます。

Teams クライアントは、既定の言語文字列 -> ユーザーの言語のみ -> ユーザーの言語 + ユーザーの地域文字列という順序で文字列を適用します。

たとえば、'fr' (フランス語、すべての地域) の既定の言語と、'en' (英語、すべての地域) と 'en-gb' (英語、英国) の追加言語ファイルを指定します。 ユーザーの言語が 'en-gb' に設定されている場合:

1. Teams クライアントは、'fr' 文字列を 'en' 文字列で上書きします。
2. 'en-gb' 文字列で上書きします。

ユーザーの言語が 'en-ca' に設定されている場合: 

1. Teams クライアントは、'fr' 文字列を 'en' 文字列で上書きします。
2. 'en-ca' ローカライズは指定されていないので、'en' ローカライズが使用されます。

ユーザーの言語が 'es-es' に設定されている場合、Teams クライアントは 'fr' 文字列を受け取り、どの言語ファイルでも上書きしません。

したがって、マニフェストに言語専用のトップ レベルの翻訳 ('en-us' ではなく'en') を提供し、それらを必要とする少数の文字列に対して地域レベルのオーバーライドのみを提供する方が強く推奨されます。

### <a name="example-manifestjson-change"></a>変更時manifest.js例

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

## <a name="handling-localized-text-submissions-from-your-users"></a>ユーザーからのローカライズされたテキスト送信の処理

アプリケーションのローカライズされたバージョンを提供する場合、ユーザーが同じ言語で応答する可能性が非常に高い可能性があります。 Teams はユーザー申請を既定の言語に変換しないので、アプリで処理する必要があります。 たとえば、ローカライズを指定した場合、ボットに対する応答は、既定の言語ではなく、コマンドのローカライズされたテキスト `commandList` になります。 アプリは適切に対応する必要があります。
