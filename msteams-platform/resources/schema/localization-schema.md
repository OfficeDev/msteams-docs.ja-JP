---
title: JSON スキーマの参照のローカライズ
description: スキーマの例を使用して、ローカライズ ファイルでサポートされるローカライズ Microsoft Teamsを説明します。
ms.topic: reference
ms.localizationpriority: medium
keywords: teams マニフェスト スキーマのローカライズ
ms.date: 05/20/2019
ms.openlocfilehash: 46a17e488d9c8c5598eab3ff53a9322a80f606ca
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887881"
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

|プロパティ|型|最大の長さ|説明|
|---------------|--------|---------|------------------|
|`$schema`|URI|該当なし|マニフェスト https:// JSON スキーマを参照する URL を指定します。|
|`name.short`|String|30|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`name.full`|文字列|100|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`description.short`|String|80|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`description.full`|String|4000|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|String|32|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`## bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|String|32|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|String|32|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|String|512|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|String|64|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|

## <a name="see-also"></a>関連項目

> [アプリをローカライズする](~/concepts/build-and-test/apps-localization.md)
