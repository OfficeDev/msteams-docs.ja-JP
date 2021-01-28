---
title: アプリのローカライズ
description: Microsoft Teams アプリをローカライズする際の考慮事項について説明します。
ms.topic: conceptual
keywords: teams publish store office publishing AppSource ローカライズ言語
ms.date: 05/15/2018
ms.openlocfilehash: 69bee0ee11238dc0e461e4fddf8ed01f0cfcccde
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014300"
---
# <a name="localization-for-microsoft-teams-apps"></a>Microsoft Teams アプリのローカライズ

Microsoft Teams アプリをローカライズする場合、考慮する必要がある主な領域は 3 つがあります。

1. AppSource 登録情報 (アプリ ストアに公開する場合)。
1. アプリ マニフェスト内のエンドユーザー向け文字列 (ボット コマンドなど)。
1. ユーザーから送信されたローカライズされたテキストへの応答。

## <a name="localizing-your-appsource-listing"></a>AppSource 登録情報のローカライズ

アプリ ストアに公開する場合、AppSource 登録情報のローカライズはまだサポートされていないことに注意する必要があります。 ただし、アプリ ストアでのローカライズされた登録情報のサポートの準備として、登録情報に言語を追加できます。 現在、登録情報のパートナー センターで指定した既定[](/office/dev/store/submit-to-appsource-via-partner-center)の (英語) 言語情報だけが、アプリの[AppSource Web](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1)サイトの登録情報に表示されます。

アプリの追加言語を構成するには、パートナー[](/office/dev/store/submit-to-appsource-via-partner-center)センターで、英語とアプリの追加言語の両方を選択します。 この例ではフランス語が使用されています。

1. 英語を追加する
    * アプリ名を入力します。
    * アプリの簡単な説明を英語で入力します。
    * アプリの詳細な説明を英語で入力します。
    * 詳しい説明では、「このアプリはフランス語で利用できます」という行も追加してください。
    * アプリ UI の画像をアップロードします (英語)。
2. フランス語を追加する
    * アプリ名を入力します。
    * アプリの簡単な説明をフランス語で入力します。
    * アプリの詳細な説明をフランス語で入力します。
    * アプリ UI の画像をアップロードします (フランス語)。

英語でアップロードする画像は、AppSource で使用される画像です。

## <a name="localizing-the-strings-in-your-app-manifest"></a>アプリ マニフェスト内の文字列のローカライズ

アプリを適切にローカライズするには、Microsoft Teams アプリ スキーマ v1.5+ を使用する必要があります。 これを行うには、manifest.json ファイルの属性を ' に設定し、'manifestVersion' プロパティを `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json '1.7' に更新します。

### <a name="example-manifestjson-change"></a>変更manifest.jsの例

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

次に、アプリケーションがサポートする既定の言語で "localizationInfo" プロパティを追加します。 ユーザーのクライアント設定が追加の言語と一致しない場合、既定の言語が最終的なフォールバック言語として使用されます。

### <a name="example-manifestjson-change"></a>変更manifest.jsの例

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

マニフェスト内のすべてのユーザー向け文字列の翻訳を含む追加の .json ファイルを提供できます。 これらのファイルは、ローカライズ ファイル [の JSON](../../resources/schema/localization-schema.md) スキーマに準拠し、マニフェストの 'localizationInfo' プロパティに追加する必要があります。 各ファイルは、Teams クライアントが適切な文字列を選択するために使用する言語タグに関連付けられている。 言語タグは形式をとっていますが、目的の言語をサポートしているすべての地域を対象とする部分を省略 <language> - <region> <region> することが推奨されます。

Teams クライアントは、次の順序で文字列を適用します。既定の言語文字列 -> ユーザーの言語のみ文字列 -> ユーザーの言語 + ユーザーの地域文字列。

たとえば、"fr" (フランス語、すべての地域) の既定の言語と、'en' (英語、すべての地域) と 'en-gb' (英語、英国) の追加の言語ファイルを指定します。 ユーザーの言語が 'en-gb' に設定されている場合:

1. Teams クライアントは、'fr' 文字列を 'en' 文字列で上書きします。
2. 'en-gb' 文字列で上書きします。

ユーザーの言語が 'en-ca' に設定されている場合: 

1. Teams クライアントは、'fr' 文字列を 'en' 文字列で上書きします。
2. 'en-ca' ローカライズは提供されていないので、'en' ローカライズが使用されます。

ユーザーの言語が 'es-es' に設定されている場合、Teams クライアントは "fr" 文字列を受け取り、どの言語ファイルでも上書きしません。

したがって、言語専用のトップ レベルの翻訳をマニフェストで提供し ('en-us' ではなく'en')、それらを必要とする少数の文字列に対する地域レベルのオーバーライドのみを提供する方法を強く推奨します。

### <a name="example-manifestjson-change"></a>変更manifest.jsの例

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

アプリケーションのローカライズバージョンを提供する場合は、ユーザーが同じ言語で応答する可能性が高い可能性があります。 Teams はユーザーの申請を既定の言語に変換し戻すのではないので、アプリで処理する必要があります。 たとえば、ローカライズを指定した場合、ボットへの応答は、既定の言語ではなく、コマンドのローカライズされたテキスト `commandList` になります。 アプリは適切に応答する必要があります。
