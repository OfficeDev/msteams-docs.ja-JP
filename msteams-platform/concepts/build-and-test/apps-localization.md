---
title: アプリをローカライズする
description: アプリのローカライズに関する考慮事項Microsoft Teams説明します。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams publishs store office publishing AppSource ローカライズ言語
ms.date: 05/15/2018
ms.openlocfilehash: 13325d323ec1d4d87f6cd5ff64c4a6c71552e01c
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452698"
---
# <a name="localize-your-app"></a>アプリをローカライズする

アプリをローカライズするには、次のMicrosoft Teamsしてください。

1. [AppSource リストをローカライズします](#localize-your-appsource-listing)。
1. [アプリ マニフェスト内の文字列をローカライズします](#localize-strings-in-your-app-manifest)。
1. [ユーザーからのローカライズされたテキスト送信を処理します](#handle-localized-text-submissions-from-your-users)。

## <a name="localize-your-appsource-listing"></a>AppSource リストをローカライズする

アプリをストアに発行する場合は、アプリを一覧表示する言語にメタデータ (説明、スクリーン ショット、名前) を入力し、パートナー センターの [Marketplace リスト] ページでこれらの言語を明示的に指定します。 詳細については、「ローカライズされた [Microsoft AppSource フロント」を参照してください](/office/dev/store/prepare-localized-solutions#localized-microsoft-appsource-fronts)。 アプリ ストアでローカライズされたリストをサポートするには、リスティングに追加の言語を追加できます。 登録情報のパートナー センターで指定[](/office/dev/store/submit-to-appsource-via-partner-center)した既定の言語情報は、アプリの [AppSource Web](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource は、チームのすべてのニーズに対応する 1 つの場所です。チャット、会議、通話、ファイル、ツールなど、すべての情報をまとめ、チームワークを高めることができます。") サイトの一覧に表示されます。 現在、既定の言語は英語です。

### <a name="configure-localization"></a>ローカライズの構成

アプリの追加言語を構成するには、 [パートナー](/office/dev/store/submit-to-appsource-via-partner-center) センターで、英語とアプリの追加言語の両方を選択します。 次の例では、フランス語を追加の言語として使用します。

1. 英語を追加する
    * アプリ名を入力します。
    * アプリの簡単な説明を英語で入力します。
    * アプリの長い説明を英語で入力します。
    * 長い説明で、「このアプリ **はフランス語で使用できます。」と入力します**。
    * アップロード UI のイメージを確認します (英語)。
2. フランス語を追加する
    * アプリ名を入力します。
    * アプリの簡単な説明をフランス語で入力します。
    * アプリの長い説明をフランス語で入力します。
    * アップロード UI のイメージを確認します (フランス語)。

英語でアップロードする画像は、AppSource で使用されます。

## <a name="localize-strings-in-your-app-manifest"></a>アプリ マニフェスト内の文字列をローカライズする

アプリをローカライズするには、Microsoft Teamsスキーマ以降`v1.5`を使用する必要があります。 これを行うには、`$schema`manifest.json `$schema` **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** `manifestVersion` ファイルの属性を以上に設定し、プロパティをバージョン (`1.5`この場合) に更新します。

アプリケーションでサポートされている既定 `localizationInfo` の言語でプロパティを追加する必要があります。 既定の言語は、ユーザーのクライアント設定が追加の言語と一致しない場合、最終的なフォールバック言語として使用されます。

### <a name="example-manifestjson-change"></a>manifest.json の変更例

次の manifest.json は、アプリケーションでサポート `localizationInfo` されている既定の言語でプロパティを追加するのに役立ちます `additionalLanguages`。

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

### <a name="example-localization-json-change"></a>ローカライズ .json の変更例

ローカライズ .json の例を次に示します。

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```

マニフェスト内のすべてのユーザー向け文字列の翻訳を含む追加の .json ファイルを提供できます。 これらのファイルは、ローカライズ ファイル JSON スキーマに準拠している[必要があります](../../resources/schema/localization-schema.md)`localizationInfo`。マニフェストのプロパティに追加する必要があります。 各ファイルは言語タグに関連付け、Teamsを使用して適切な文字列を選択します。 言語タグの形式を使用 `<language>-<region>` します `<region>` が、目的の言語をサポートしているすべての地域を対象とする部分を省略できます。

Teams クライアントは、既定の言語文字列 -> ユーザーの言語のみ -> ユーザーの言語 + ユーザーの地域文字列の順序で文字列を適用します。

たとえば、'fr' (フランス語、すべての地域) の既定の言語と、'en' (英語、すべての地域) と 'en-gb' (英語、英国) の追加言語ファイルを指定すると、ユーザーの言語は 'en-gb' に設定されます。 次の変更は、言語の選択に基づいて行います。

1. クライアントTeams'fr' 文字列を受け取り、'en' 文字列で上書きします。
1. 'en' 文字列を 'en-gb' 文字列で上書きします。

ユーザーの言語が 'en-ca' に設定されている場合、言語の選択に基づいて次の変更が行います。

1. クライアントTeams'fr' 文字列を受け取り、'en' 文字列で上書きします。
1. 'en-ca' ローカライズは指定されていないので、'en' ローカライズが使用されます。

ユーザーの言語が 'es-es' に設定されている場合、Teamsは 'fr' 文字列を受け取る。 このTeamsクライアントは、言語ファイルの文字列を上書きしません。'es' または 'es-es' 変換が提供されていない。

したがって、マニフェストにトップ レベルの言語翻訳のみを提供する必要があります。 たとえば、'en-us' の代わりに 'en' を使用します。 地域レベルのオーバーライドは、必要な少数の文字列にのみ指定する必要があります。

### <a name="example-manifestjson-change"></a>manifest.json の変更例

manifest.json の変更を次の例に示します。

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

 localization.json の変更を次の例に示します。

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

## <a name="handle-localized-text-submissions-from-your-users"></a>ユーザーからのローカライズされたテキスト送信を処理する

アプリケーションのローカライズされたバージョンを提供する場合、ユーザーは同じ言語で応答します。 ユーザー Teams既定の言語に変換されないので、アプリはローカライズされた言語の応答を処理する必要があります。 たとえば、ローカライズされた言語を `commandList`指定した場合、ボットに対する応答はコマンドのローカライズされたテキストで、既定の言語ではありません。 アプリは適切に対応する必要があります。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | .NET | Node.js |
|-------------|-------------|------|------|
| アプリのローカライズ | Microsoft Teamsタブを使用してアプリのローカライズを行います。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>関連項目

[JSON スキーマの参照のローカライズ](~/resources/schema/localization-schema.md)
