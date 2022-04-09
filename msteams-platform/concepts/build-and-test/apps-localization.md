---
title: アプリをローカライズする
description: Microsoft Teams アプリのローカライズに関する考慮事項について説明します。
ms.topic: conceptual
ms.localizationpriority: medium
keywords: Teams 発行ストア オフィス発行 AppSource ローカライズ言語
ms.date: 05/15/2018
ms.openlocfilehash: 25a7694017cc8002ac23cf7075c59488ceb9773d
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737037"
---
# <a name="localize-your-app"></a>アプリをローカライズする

Microsoft Teams アプリをローカライズするには、次の要素を考慮してください。

1. [AppSource の一覧をローカライズします](#localize-your-appsource-listing)。
1. [アプリ マニフェスト内の文字列をローカライズします](#localize-strings-in-your-app-manifest)。
1. [ユーザーからのローカライズされたテキスト送信を処理します](#handle-localized-text-submissions-from-your-users)。

## <a name="localize-your-appsource-listing"></a>AppSource の一覧をローカライズする

アプリをストアに公開する場合は、アプリを一覧表示する言語のメタデータ (説明、スクリーンショット、名前) を指定し、パートナー センターの **Marketplace の一覧** ページでこれらの言語を明示的に指定します。 詳細については、 [ローカライズされた Microsoft AppSource のフロントを](/office/dev/store/prepare-localized-solutions#localized-microsoft-appsource-fronts)参照してください。 アプリ ストアでローカライズされたリストをサポートするために、追加の言語を登録情報に追加できます。 リストの [パートナー センター](/office/dev/store/submit-to-appsource-via-partner-center) で指定する既定の言語情報は、 [アプリの AppSource Web サイト](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource は、チームのニーズに合わせて 1 つの場所です。チャット、会議、通話、ファイル、ツールなど、すべてをまとめ、より生産性の高いチームワークを実現します。") の一覧に表示されます。 現在、既定の言語は英語です。

### <a name="configure-localization"></a>ローカライズを構成する

アプリの追加言語を構成するには、 [パートナー センター](/office/dev/store/submit-to-appsource-via-partner-center)で英語とアプリの追加言語の両方を選択します。 フランス語は、次の例の追加言語として使用されます。

1. 英語を追加する
    * アプリ名を入力します。
    * アプリの簡単な説明を英語で入力します。
    * アプリの長い説明を英語で入力します。
    * 長い説明に「 **:このアプリはフランス語で利用できます**。」と入力します。
    * アプリ UI のイメージをアップロードします (英語)。
2. フランス語を追加する
    * アプリ名を入力します。
    * フランス語でアプリの簡単な説明を入力します。
    * アプリの長い説明をフランス語で入力します。
    * アプリ UI のイメージをアップロードします (フランス語)。

英語でアップロードする画像は、AppSource で使用されます。

## <a name="localize-strings-in-your-app-manifest"></a>アプリ マニフェスト内の文字列をローカライズする

Microsoft Teamsアプリ スキーマ`v1.5`以降を使用して、アプリをローカライズします。 これを行うには、manifest.json ファイルの属性を以上に設定`$schema`し、プロパティを`manifestVersion`バージョンに`$schema`更新します (`1.5`この`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`場合)。

アプリケーションが `localizationInfo` サポートする既定の言語でプロパティを追加します。 既定の言語は、ユーザーのクライアント設定が追加の言語と一致しない場合に、最終的なフォールバック言語として使用されます。

### <a name="example-manifestjson-change"></a>manifest.json の変更例

次 `manifest.json` は、アプリケーションで `localizationInfo` サポートされている既定の言語と共 `additionalLanguages`にプロパティを追加するのに役立ちます。

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

マニフェスト内のすべてのユーザー向け文字列の翻訳を含む追加の .json ファイルを提供できます。 これらのファイルは [、ローカリゼーション ファイルの JSON スキーマ](../../resources/schema/localization-schema.md) に準拠している必要があり、マニフェストの `localizationInfo` プロパティに追加する必要があります。 各ファイルは言語タグに関連付けられます。このタグは、Teams クライアントが適切な文字列を選択するために使用します。 言語タグは形式を取りますが、目的の `<language>-<region>` 言語を `<region>` サポートするすべてのリージョンを対象とする部分を省略できます。

Teams クライアントは、既定の言語文字列 -> ユーザーの言語のみの文字列 -> ユーザーの言語とユーザーのリージョン文字列の順に文字列を適用します。

たとえば、既定の言語として 'fr' (フランス語、すべてのリージョン)、および 'en' (英語、すべてのリージョン) と 'en-gb' (英語、英国) の追加言語ファイルを指定すると、ユーザーの言語は 'en-gb' に設定されます。 言語の選択に基づいて、次の変更が行われます。

1. Teams クライアントは 'fr' 文字列を受け取り、'en' 文字列で上書きします。
1. 'en' 文字列を 'en-gb' 文字列で上書きします。

ユーザーの言語が 'en-ca' に設定されている場合、言語の選択に基づいて次の変更が行われます。

1. Teams クライアントは 'fr' 文字列を受け取り、'en' 文字列で上書きします。
1. 'en-ca' ローカライズは提供されていないため、'en' ローカライズが使用されます。

ユーザーの言語が 'es-es' に設定されている場合、Teams クライアントは 'fr' 文字列を受け取ります。 Teams クライアントは、'es' または 'es-es' 翻訳が提供されていないため、言語ファイルで文字列をオーバーライドしません。

そのため、マニフェストでトップレベルの言語のみの翻訳を提供する必要があります。 たとえば、 `en` `en-us`. リージョン レベルのオーバーライドは、必要な少数の文字列に対してのみ指定する必要があります。

### <a name="example-manifestjson-change"></a>manifest.json の変更例

この変更は `manifest.json` 、次の例に示されています。

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

 この変更は `localization.json` 、次の例に示されています。

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

## <a name="handle-localized-text-submissions-from-your-users"></a>ユーザーからのローカライズされたテキスト送信を処理する

ローカライズされたバージョンのアプリケーションを提供する場合、ユーザーは同じ言語で応答します。 Teamsはユーザーの提出を既定の言語に翻訳しないため、アプリはローカライズされた言語応答を処理する必要があります。 たとえば、ローカライズされた `commandList`テキストを指定した場合、ボットに対する応答はコマンドのローカライズされたテキストであり、既定の言語ではありません。 アプリは適切に応答する必要があります。

## <a name="code-sample"></a>コード サンプル

| サンプルの名前 | 説明 | .NET | Node.js |
|-------------|-------------|------|------|
| アプリのローカライズ | ボットとタブを使用してアプリのローカライズをMicrosoft Teamsします。 | [表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[表示](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>関連項目

[JSON スキーマの参照のローカライズ](~/resources/schema/localization-schema.md)
