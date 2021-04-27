---
title: ボット メッセージの形式
description: ボット メッセージの書式設定の詳細について説明します。
keywords: teams シナリオ チャネルの会話ボット メッセージ
ms.topic: reference
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: 06037bd3fb23ace11eea763747dc64d763ac3c42
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020647"
---
# <a name="message-formatting-for-bots"></a>ボットのメッセージの書式設定

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

省略可能なプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) を制御できます。

Microsoft Teams では、次の書式設定オプションがサポートされています。

| TextFormat 値 | 説明 |
| --- | --- |
| プレーン | テキストは、書式が適用されずに生テキストとして扱われる必要があります。 |
| markdown | テキストは Markdown 書式設定として扱い、必要に応じてチャネルにレンダリングする必要があります。「サポート [されているスタイルのテキスト コンテンツ](#formatting-text-content) の書式設定」を参照してください。 |
| xml | テキストは単純な XML マークアップです。「サポート [されているスタイルのテキスト コンテンツ](#formatting-text-content) の書式設定」を参照してください。 |

## <a name="formatting-text-content"></a>テキスト コンテンツの書式設定

Microsoft Teams では、Markdown タグと XML (HTML) 書式タグのサブセットがサポートされています。

現時点では、次の制限が適用されます。

* テキスト専用メッセージはテーブルの書式設定をサポートしません
* リッチ カードは、タイトルまたは字幕プロパティではなく、text プロパティの書式設定のみをサポートします。
* リッチ カードは Markdown またはテーブルの書式設定をサポートしていない

## <a name="cross-platform-support"></a>クロスプラットフォームのサポート

書式設定が Microsoft Teams でサポートされているすべてのプラットフォームで確実に機能するには、一部のスタイルが現在すべてのプラットフォームでサポートされていない点に注意してください。

| Style                     | テキスト専用メッセージ | リッチ カード (XML のみ) |
| ---                       | :---: | :---: |
| bold                      | ✔ | ✖ |
| italic                    | ✔ | ✔ |
| ヘッダー (レベル 1 &ndash; 3) | ✖ | ✔ |
| 取り消し線             | ✖ | ✔ |
| 水平ルール           | ✖ | ✖ |
| 順序なしリスト            | ✖ | ✔ |
| 順序付きリスト              | ✖ | ✔ |
| 事前に書式設定されたテキスト         | ✔ | ✔ |
| blockquote                | ✔ | ✔ |
| hyperlink                 | ✔ | ✔ |
| 画像リンク                | ✔ | ✖ |

## <a name="support-by-individual-platform"></a>個々のプラットフォームによるサポート

テキストの書式設定のサポートは、メッセージの種類やプラットフォームによって異なります。

### <a name="text-only-messages"></a>テキスト専用メッセージ

| Style                     | Desktop | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔ | ✔ | ✔ |
| italic                    | ✔ | ✔ | ✔ |
| ヘッダー (レベル 1 &ndash; 3) | ✖ | ✖ | ✖ |
| 取り消し線             | ✔ | ✔ | ✖ |
| 水平ルール           | ✖ | ✖ | ✖ |
| 順序なしリスト            | ✔ | ✖ | ✖ |
| 順序付きリスト              | ✔ | ✖ | ✖ |
| 事前に書式設定されたテキスト         | ✔ | ✔ | ✔ |
| blockquote                | ✔ | ✔ | ✔ |
| hyperlink                 | ✔ | ✔ | ✔ |
| 画像リンク                | ✔ | ✔ | ✔ |

### <a name="cards"></a>カード

カードの [サポートについては、「カードの書式設定](~/task-modules-and-cards/cards/cards-format.md) 」を参照してください。
