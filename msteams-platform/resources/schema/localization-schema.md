---
title: ローカライズ ファイル JSON スキーマ参照
description: ローカライズ ファイルでサポートされているローカライズ スキーマについて説明Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: teams マニフェスト スキーマのローカライズ
ms.date: 05/20/2019
ms.openlocfilehash: 3e4207fb3e862eac18c80ffc49e7c5648ae05c28
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019707"
---
# <a name="reference-localization-file-json-schema"></a>リファレンス: ローカライズ ファイル JSON スキーマ

ローカライズ Microsoft Teamsは、クライアント言語の設定に基づいて提供される言語翻訳について説明します。 ファイルは、 でホストされるスキーマに準拠している必要があります [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) 。 詳細については、「アプリのローカライズ [」を参照してください](~/concepts/build-and-test/apps-localization.md)。

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

マニフェスト https:// JSON スキーマを参照する URL を指定します。

> [!TIP]
> マニフェストの先頭にスキーマを指定して、コード エディター IntelliSenseサポートを有効にしてください。`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>name.short

**文字列、最大長 30**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。

## <a name="namefull"></a>name.full

**文字列、最大長 100**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。

## <a name="descriptionshort"></a>description.short

**文字列、最大長 80**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。

## <a name="descriptionfull"></a>description.full

**文字列、最大長 4000**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換わります。

## <a name="statictabs0-910-5name"></a>staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name

**文字列、最大長 128**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。

## <a name="bots0commandlists0-2commands0-9title"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .command \\ [[0-9] \\ ] \\ .title

**文字列、最大長 32**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。

## <a name="bots0commandlists0-2commands0-9description"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .command \\ [[0-9] \\ ] \\ .description

**文字列、最大長 128**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。

## <a name="composeextensions0commands0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title

**文字列、最大長 32**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。

## <a name="composeextensions0commands0-9description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**文字列、最大長 128**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。

## <a name="composeextensions0commands0-9parameters0-4title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title

**文字列、最大長 32**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。

## <a name="composeextensions0commands0-9parameters0-4description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description

**文字列、最大長 128**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。

## <a name="composeextensions0commands0-9parameters0-4value"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value

**文字列、最大長 512**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>composeExtensions \\ [0] \\ \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title

**文字列、最大長 128**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。

## <a name="composeextensions0commands0-9taskinfotitle"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title

**文字列、最大長 64**

アプリ マニフェストの対応する文字列を、ここに指定した値に置き換えてください。
