---
title: ローカライズ ファイルの JSON スキーマ リファレンス
description: Microsoft Teams のローカライズ ファイルでサポートされているローカライズ スキーマについて説明します。
ms.topic: reference
keywords: teams マニフェスト スキーマのローカライズ
ms.date: 05/20/2019
ms.openlocfilehash: 696a65de70a63e767f8fcdb040364fe90cde8716
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014601"
---
# <a name="reference-localization-file-json-schema"></a>リファレンス: ローカライズ ファイルの JSON スキーマ

Microsoft Teams ローカライズ ファイルには、クライアントの言語設定に基づいて提供される言語翻訳が記述されています。 ファイルは、ホストされているスキーマに準拠している必要があります [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) 。 詳しくは、アプリのローカライズ [に関するページをご覧ください](~/concepts/build-and-test/apps-localization.md)。

## <a name="sample"></a>サンプル

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

## <a name="schema"></a>$schema

**URI**

次https://マニフェストの JSON スキーマを参照する URL を示します。

> [!TIP]
> マニフェストの先頭にスキーマを指定して、コード エディター IntelliSense同様のサポートを有効にしてください。 `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>name.short

**String、Max Length 30**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="namefull"></a>name.full

**文字列、最大長 100**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="descriptionshort"></a>description.short

**文字列、最大長 80**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="descriptionfull"></a>description.full

**String、Max Length 4000**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="statictabs0-910-5name"></a>staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name

**文字列、最大長 128**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="bots0commandlists0-2commands0-9title"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ \\ .title

**文字列、最大長 32**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="bots0commandlists0-2commands0-9description"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ \\ .description

**文字列、最大長 128**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="composeextensions0commands0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ \\ .title

**文字列、最大長 32**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="composeextensions0commands0-9description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**文字列、最大長 128**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="composeextensions0commands0-9parameters0-4title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ \\ .title

**文字列、最大長 32**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="composeextensions0commands0-9parameters0-4description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ . \\ description

**文字列、最大長 128**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="composeextensions0commands0-9parameters0-4value"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value

**文字列、最大長 512**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ \\ .title

**文字列、最大長 128**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。

## <a name="composeextensions0commands0-9taskinfotitle"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title

**文字列、最大長 64**

アプリ マニフェストの対応する文字列を、ここで指定した値に置き換します。
