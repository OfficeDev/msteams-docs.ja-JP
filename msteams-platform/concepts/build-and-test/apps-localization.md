---
title: アプリのローカライズ
description: Microsoft Teams アプリをローカライズする際の考慮事項について説明します。
ms.topic: conceptual
localization_priority: Normal
keywords: チームは、ストア オフィス発行の AppSource ローカライズ言語を公開します。
ms.date: 05/15/2018
ms.openlocfilehash: a55b8af97e5306843858e5844a017dd402ab3516
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566048"
---
# <a name="localization-for-microsoft-teams-apps"></a>Microsoft Teamsアプリのローカライズ

Microsoft Teams アプリをローカライズする際には、次の点を考慮する必要があります。

1. Teamsストアの登録情報 (該当する場合)
1. アプリ マニフェスト内のエンド ユーザー向け文字列。 たとえば、ボット コマンドです。
1. ユーザーから送信されたローカライズされたテキストに応答します。

## <a name="localizing-your-appsource-listing"></a>アプリソースの一覧をローカライズする

ストアに発行する場合は、AppSource のリスティングのローカライズがまだサポートされていない点に注意する必要があります。 ただし、アプリ ストアでローカライズされた一覧のサポートの準備として、リストに言語を追加できます。 現在、 [パートナー センター](/office/dev/store/submit-to-appsource-via-partner-center) で提供する既定の (英語) 言語情報のみが、アプリの [AppSource Web サイト](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) の一覧に表示されます。

### <a name="example-of-configuring-localization"></a>ローカリゼーションの構成例

アプリの追加言語を構成するには、パートナー [センター](/office/dev/store/submit-to-appsource-via-partner-center)で、英語とアプリの追加言語の両方を選択します。 この例ではフランス語が使用されています。

1. 英語を追加する
    * アプリ名を入力します。
    * 英語でアプリの簡単な説明を記入してください。
    * 英語でアプリの長い説明を記入してください。
    * 長い説明では、「このアプリは"フランス語で利用可能です"という行も追加してください。
    * アプリの UI のイメージをアップロードします (英語)。
2. フランス語を追加する
    * アプリ名を入力します。
    * フランス語でアプリの簡単な説明を入力します。
    * フランス語でアプリの長い説明を入力します。
    * アプリの UI のイメージをアップロードします (フランス語)。

英語でアップロードする画像は、AppSource で使用される画像になります。

## <a name="localizing-the-strings-in-your-app-manifest"></a>アプリ マニフェストでの文字列のローカライズ

アプリを適切にローカライズするには、Microsoft Teams アプリ スキーマ v1.5+ を使用する必要があります。 これを行うには、 `$schema` ファイルのmanifest.jsの属性を ' ' に設定 https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json し、'manifestVersion' プロパティを '1.7' に更新します。

### <a name="example-manifestjson-change"></a>変更時のmanifest.js例

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

その後、アプリケーションがサポートする既定の言語で 'localizationInfo' プロパティを追加します。 ユーザーのクライアント設定が追加の言語と一致しない場合、既定の言語が最終的なフォールバック言語として使用されます。

### <a name="example-manifestjson-change"></a>変更時のmanifest.js例

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

マニフェスト内のすべてのユーザー向け文字列の翻訳を使用して、追加の .json ファイルを提供できます。 これらのファイルは [、ローカライズ ファイルの JSON スキーマ](../../resources/schema/localization-schema.md) に準拠する必要があり、マニフェストの 'localizationInfo' プロパティに追加する必要があります。 各ファイルは、Teamsクライアントが適切な文字列を選択するために使用する言語タグに関連付けられます。 言語タグはの形式をと <language> - <region> りますが、目的の言語を <region> サポートするすべてのリージョンを対象とする部分を省略することをお勧めします。

Teamsクライアントは、既定の言語文字列 ->ユーザーの言語のみの文字列 ->ユーザーの言語 + ユーザーの地域文字列の順に文字列を適用します。

たとえば、既定の言語である 'fr' (フランス語、すべての地域)、および 'en' (英語、すべての地域) と 'en-gb' (英語、英国) の追加言語ファイルを指定します。 ユーザーの言語が 'en-gb' に設定されている場合:

1. Teamsクライアントは'fr'文字列を'en'文字列で上書きします。
2. 'en-gb' 文字列で上書きします。

ユーザーの言語が 'en-ca' に設定されている場合: 

1. Teamsクライアントは'fr'文字列を'en'文字列で上書きします。
2. 'en-ca' のローカライズは提供されていないので、'en' のローカリゼーションが使用されます。

ユーザーの言語が 'es-es' に設定されている場合、Teamsクライアントは 'fr' 文字列を受け取り、どの言語ファイルでも上書きしません。

したがって、マニフェストにトップレベルの言語のみの翻訳を提供し('en-us'ではなく'en')、必要な少数の文字列に対してのみリージョンレベルのオーバーライドを提供することを強くお勧めします。

### <a name="example-manifestjson-change"></a>変更時のmanifest.js例

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

### <a name="example-localization-json-file"></a>ローカリゼーション .json ファイルの例

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

## <a name="handling-localized-text-submissions-from-your-users"></a>ユーザーからのローカライズされたテキストの送信の処理

アプリケーションのローカライズ版を提供する場合、ユーザーが同じ言語で応答する可能性が非常に高くなります。 Teamsはユーザーの提出を既定の言語に変換しないため、アプリで処理する必要があります。 たとえば、ローカライズされた を提供する場合 `commandList` 、ボットへの応答は、既定の言語ではなく、コマンドのローカライズされたテキストになります。 アプリは適切に対応する必要があります。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | .NET |
|-------------|-------------|------|
| アプリのローカライズ | ボットとタブを使用してアプリのローカライズをMicrosoft Teamsします。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


