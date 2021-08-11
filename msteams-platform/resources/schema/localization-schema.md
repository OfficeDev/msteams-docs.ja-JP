---
title: JSON スキーマの参照のローカライズ
description: ローカライズ ファイルでサポートされているローカライズ スキーマについて説明Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: teams マニフェスト スキーマのローカライズ
ms.date: 05/20/2019
ms.openlocfilehash: 7a7c5e61e8e9db2526a725d676a237d9c37f7d71ea74d42117e0b59b51cae969
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705546"
---
# <a name="localize-json-schema-reference"></a>JSON スキーマの参照のローカライズ

ローカライズ Microsoft Teamsは、クライアント言語の設定に基づいて提供される言語の翻訳について説明します。 ファイルは、 でホストされるスキーマに準拠している必要があります [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json) 。 

> [!TIP]
> マニフェストの先頭にスキーマを指定して、コード エディターからのサポートを有効にするか、同様 `IntelliSense` のサポートを行います。 `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`

## <a name="example"></a>例 

ローカライズ JSON スキーマの例は次のとおりです。

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "name.short": "Le App Studio",
  "name.full": "App Studio pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App Studio.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App Studio.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

スキーマは、次のプロパティを定義します。

|プロパティ|種類|最大の長さ|説明|
|---------------|--------|---------|------------------|
|`$schema`|URI|該当なし|マニフェスト https:// JSON スキーマを参照する URL を指定します。|
|`name.short`|文字列|30|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`name.full`|文字列|100|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`description.short`|文字列|80|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`description.full`|文字列|4000|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|文字列|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|文字列|32|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`## bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|文字列|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|文字列|32|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|文字列|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|文字列|32|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|文字列|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|文字列|512|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|文字列|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|文字列|64|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|

## <a name="see-also"></a>関連項目

> [アプリをローカライズする](~/concepts/build-and-test/apps-localization.md)
