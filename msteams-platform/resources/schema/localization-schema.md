---
title: JSON スキーマの参照のローカライズ
description: スキーマの例を使用して、ローカライズ ファイルでサポートされるローカライズ Microsoft Teamsを説明します。
ms.topic: reference
ms.localizationpriority: medium
keywords: teams マニフェスト スキーマのローカライズ
ms.date: 05/20/2019
ms.openlocfilehash: cbe408deb8788c9b047eb6bd954f79c73dbd057f
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768393"
---
# <a name="localize-json-schema-reference"></a>JSON スキーマの参照のローカライズ

ローカライズ Microsoft Teamsは、クライアント言語の設定に基づいて提供される言語の翻訳について説明します。 ファイルは、 でホストされるスキーマに準拠している必要があります [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) 。

> [!TIP]
> マニフェストの先頭にスキーマを指定して、コード エディターからのサポートを有効にするか、同様 `IntelliSense` のサポートを行います。 `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="example"></a>例

ローカライズ JSON スキーマの例は次のとおりです。

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
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

|プロパティ|種類|最大の長さ|Description|
|---------------|--------|---------|------------------|
|`$schema`|URI|該当なし|マニフェスト https:// JSON スキーマを参照する URL を指定します。|
|`name.short`|String|30|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`name.full`|文字列|100|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`description.short`|String|80|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`description.full`|String|4000|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|String|32|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|String|32|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|String|32|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|String|512|アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|String|64|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.description`|String|128|通知の簡単な説明|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.templateText`|String|128|例: "{actor} が作成したタスク {taskId} for you"|

## <a name="see-also"></a>関連項目

[アプリをローカライズする](~/concepts/build-and-test/apps-localization.md)
