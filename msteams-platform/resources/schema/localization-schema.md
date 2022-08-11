---
title: JSON スキーマの参照のローカライズ
description: スキーマの例を使用して、Microsoft Teams のローカライズ ファイルでサポートされているローカライズ スキーマについて説明します
ms.topic: reference
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: f4ffd9a4b722ccc414f70b19e3020ab39d1ce779
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2022
ms.locfileid: "67311947"
---
# <a name="localize-json-schema-reference"></a>JSON スキーマの参照のローカライズ

Microsoft Teams のローカライズ ファイルでは、クライアント言語の設定に基づいて提供される言語翻訳について説明します。 ファイルは、.. でホストされているスキーマに準拠している [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json)必要があります。

> [!TIP]
> マニフェストの先頭にスキーマを指定して、コード エディターで同様のサポートを有効 `IntelliSense` にします。 `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="example"></a>例

ローカライズ JSON スキーマの例は次のとおりです。

```json
{
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.9/MicrosoftTeams.Localization.schema.json",
    "name.short": "Portail de Développement",
    "name.full": "Portail des développeurs",
    "description.short": "Configurer, distribuer et gérer vos applications Microsoft Teams",
    "description.full": "Anciennement App Studio, le portail des développeurs peut vous aider où que vous soyez dans votre parcours de développement d’applications Microsoft Teams.1. Configurez une nouvelle application ou importez une application existante.2. Configurez les fonctionnalités de votre application et d’autres métadonnées importantes.3. Obtenez des ressources pour vous aider à créer une application de haute qualité.3. Testez votre application directement dans Teams.4. Distribuez votre application dans votre organisation ou dans le Store Teams.5. Analysez l’utilisation, l’engagement et d’autres informations sur votre application. Le portail inclut également des outils pour concevoir des scènes virtuelles personnalisées, des cartes adaptatives et l’intégration à la Plateforme d’identités Microsoft.",
    "staticTabs[0].name": "Accueil",
    "staticTabs[1].name": "Applications",
    "staticTabs[2].name": "Outils",
    "staticTabs[3].name": "Developer Portal",
    "bots[0].commandLists[0].commands[0].title": "Rechercher",
    "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams appropriée"
}
```

スキーマは次のプロパティを定義します。

|プロパティ|種類|最大の長さ|説明|
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
