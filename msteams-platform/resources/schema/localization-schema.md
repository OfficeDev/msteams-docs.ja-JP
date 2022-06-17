---
title: JSON スキーマの参照のローカライズ
description: スキーマの例を使用して、Microsoft Teamsのローカライズ ファイルでサポートされているローカライズ スキーマについて説明します。
ms.topic: reference
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 23d02e845e4fcdc1c2fc76d8e9c376479fe1fa1f
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144277"
---
# <a name="localize-json-schema-reference"></a>JSON スキーマの参照のローカライズ

Microsoft Teamsローカリゼーション ファイルでは、クライアント言語の設定に基づいて提供される言語翻訳について説明します。 ファイルは、.. でホストされているスキーマに準拠している [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json)必要があります。

> [!TIP]
> マニフェストの先頭にスキーマを指定して、コード エディターで同様のサポートを有効 `IntelliSense` にします。 `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

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

スキーマは次のプロパティを定義します。

|プロパティ|型|最大の長さ|説明|
|---------------|--------|---------|------------------|
|`$schema`|URI|該当なし|マニフェストの JSON スキーマを参照する https:// URL。|
|`name.short`|String|30|アプリ マニフェストの対応する文字列を、ここに示す値に置き換えます。|
|`name.full`|文字列|100|アプリ マニフェストの対応する文字列を、ここに示す値に置き換えます。|
|`description.short`|String|80|アプリ マニフェストの対応する文字列を、ここに示す値に置き換えます。|
|`description.full`|String|4000|アプリ マニフェストの対応する文字列を、ここに示す値に置き換えます。|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|String|32|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|String|32|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|String|32|アプリ マニフェストの対応する文字列を、ここに示す値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|String|512|アプリ マニフェストの対応する文字列を、ここに示す値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|String|128|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|String|64|アプリ マニフェストの対応する文字列を、ここで指定した値に置き換えます。|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.description`|String|128|通知の簡単な説明|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.templateText`|String|128|例: "あなたに {actor} が作成したタスク {taskId}"|

## <a name="see-also"></a>関連項目

[アプリをローカライズする](~/concepts/build-and-test/apps-localization.md)
