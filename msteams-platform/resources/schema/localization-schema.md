---
title: ローカリゼーションファイル JSON スキーマリファレンス
description: Microsoft Teams のローカリゼーションファイルでサポートされているローカライズスキーマについて説明します。
keywords: teams マニフェストスキーマのローカライズ
ms.date: 05/20/2019
ms.openlocfilehash: 14e08c582f065d1b09ff0f4906ca6788037460f1
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "44590866"
---
# <a name="reference-localization-file-json-schema"></a>リファレンス: ローカライズファイル JSON スキーマ

Microsoft Teams のローカリゼーションファイルでは、クライアントの言語設定に基づいて提供される言語の翻訳について説明します。 ファイルは、でホストされているスキーマに準拠している必要があり [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) ます。 詳細については、「[アプリのローカライズ](~/concepts/build-and-test/apps-localization.md)」を参照してください。

## <a name="sample"></a>サンプル

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

マニフェストの JSON スキーマを参照する https://URL。

> [!TIP]
> マニフェストの最初にスキーマを指定して、コードエディターで IntelliSense または同様のサポートを有効にします。`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>名前。 short

**文字列、最大長30**

アプリマニフェストの対応する文字列を、ここで指定した値に置き換えます。

## <a name="namefull"></a>名前。完全

**文字列、最大長100**

アプリマニフェストの対応する文字列を、ここで指定した値に置き換えます。

## <a name="descriptionshort"></a>説明。 short

**文字列、最大長80**

アプリマニフェストの対応する文字列を、ここで指定した値に置き換えます。

## <a name="descriptionfull"></a>詳細

**文字列、最大長4000**

アプリマニフェストの対応する文字列を、ここで指定した値に置き換えます。

## <a name="statictabs0-910-5name"></a>staticTabs \\ [([0-9] | 1 [0-5]) \\ ] \\ . 名前

**文字列、最大長128**

対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。

## <a name="bots0commandlists0-2commands0-9title"></a>bot \\ [0 \\ ] \\ commandlists \\ [[0-2]] \\ \\ . コマンド \\ [[0-9] \\ \\ ]. title

**文字列、最大長32**

対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。

## <a name="bots0commandlists0-2commands0-9description"></a>bot \\ [0 \\ ] \\ commandlists \\ [[0-2]] \\ \\ . コマンド \\ [[0-9] \\ \\ ]. 説明

**文字列、最大長128**

対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。

## <a name="composeextensions0commands0-9title"></a>この機能 \\ [0 \\ ] \\ コマンド \\ [[0-9] \\ ] \\ . タイトル

**文字列、最大長32**

対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。

## <a name="composeextensions0commands0-9description"></a>この機能 \\ [0 \\ ] \\ コマンド \\ [[0-9] \\ ] \\ . 説明

**文字列、最大長128**

対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。

## <a name="composeextensions0commands0-9parameters0-4title"></a>スキーマの [ \\ 0 \\ ] \\ コマンド \\ [[0-9]]. \\ \\ パラメーター \\ [[0-4] \\ ] \\ . タイトル

**文字列、最大長32**

対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。

## <a name="composeextensions0commands0-9parameters0-4description"></a>この機能 [ \\ 0 \\ ] \\ コマンド \\ [[0-9]]. \\ \\ パラメーター \\ [[0-4] \\ ] \\ . 説明

**文字列、最大長128**

対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。

## <a name="composeextensions0commands0-9parameters0-4value"></a>この機能 [ \\ 0 \\ ] \\ コマンド \\ [[0-9]]. \\ \\ パラメーター \\ [[0-4]] \\ \\ . 値

**文字列、最大長512**

対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>\\色の設定 [0 \\ ] \\ コマンド \\ [[0-9]]. \\ \\ パラメーター [[ \\ 0-4] \\ ]. \\ 選択肢 \\ [[0-9] \\ ] \\ . タイトル

**文字列、最大長128**

対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。

## <a name="composeextensions0commands0-9taskinfotitle"></a>オブジェクトの \\ [0 \\ ] \\ . コマンド \\ [[0-9] \\ ] \\ \\ .

**文字列、最大長64**

対応する文字列を、アプリマニフェストからここで提供される値で置き換えます。