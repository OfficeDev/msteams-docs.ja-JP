---
title: ボット メッセージの形式
description: このモジュールでは、ボット メッセージの書式設定の詳細について説明します
ms.topic: reference
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 9e331a17940ee482a0c2adcb81b57a17823ab668
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190163"
---
# <a name="message-formatting-for-bots"></a>ボットのメッセージの書式設定

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

オプション [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) のプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法を制御できます。

Microsoft Teamsでは、次の書式設定オプションがサポートされています。

| TextFormat 値 | 説明 |
| --- | --- |
| プレーン | テキストは、書式設定がまったく適用されていない生のテキストとして扱う必要があります。 |
| markdown | テキストは Markdown 書式設定として扱い、必要に応じてチャネルにレンダリングする必要があります。サポートされているスタイルの [テキスト コンテンツの書式設定](#formatting-text-content) に関するページを参照してください。 |
| Xml | テキストは単純な XML マークアップです。サポートされているスタイルの [テキスト コンテンツの書式設定](#formatting-text-content) に関するページを参照してください。 |

## <a name="formatting-text-content"></a>テキスト コンテンツの書式設定

Teamsでは、Markdown と XML (HTML) の書式設定タグのサブセットがサポートされています。

現時点では、次の制限事項が適用されます。

* テキストのみのメッセージでは、テーブルの書式設定はサポートされていません。
* リッチ カードでは、タイトルやサブタイトルのプロパティではなく、テキスト プロパティの書式設定のみがサポートされます。
* リッチ カードでは、Markdown またはテーブルの書式設定はサポートされていません。

## <a name="cross-platform-support"></a>クロスプラットフォームサポート

Teamsでサポートされているすべてのプラットフォームで書式設定を確実に機能させるには、一部のスタイルが現在すべてのプラットフォームでサポートされていない点に注意してください。

| Style                     | テキストのみのメッセージ | リッチ カード (XML のみ) |
| ---                       | :---: | :---: |
| bold                      | ✔️️ | ❌ |
| italic                    | ✔️ | ✔️ |
| ヘッダー (レベル 1&ndash;3) | ❌ | ✔️ |
| 取り消し 線             | ❌ | ✔️ |
| 水平ルール           | ❌ | ❌ |
| 順序付けられていないリスト            | ❌ | ✔️ |
| 順序付きリスト              | ❌ | ✔️ |
| プリフォームフォーマットされたテキスト         | ✔️ | ✔️ |
| blockquote                | ✔️ | ✔️ |
| hyperlink                 | ✔️ | ✔️ |
| image link                | ✔️ | ❌ |

## <a name="support-by-individual-platform"></a>個々のプラットフォームによるサポート

テキストの書式設定のサポートは、メッセージの種類とプラットフォームによって異なります。

### <a name="text-only-messages"></a>テキストのみのメッセージ

| Style                     | Desktop | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔️ | ✔️ | ✔️ |
| italic                    | ✔️ | ✔️ | ✔️ |
| ヘッダー (レベル 1&ndash;3) | ❌ | ❌ | ❌ |
| 取り消し 線             | ✔️ | ✔️ | ❌ |
| 水平ルール           | ❌ | ❌ | ❌ |
| 順序付けられていないリスト            | ✔️ | ❌ | ❌ |
| 順序付きリスト              | ✔️ | ❌ | ❌ |
| プリフォームフォーマットされたテキスト         | ✔️ | ✔️ | ✔️ |
| blockquote                | ✔️ | ✔️ | ✔️ |
| hyperlink                 | ✔️ | ✔️ | ✔️ |
| image link                | ✔️ | ✔️ | ✔️ |

### <a name="cards"></a>カード

詳細については、「カードでのサポートに関する [カードの書式設定」を](~/task-modules-and-cards/cards/cards-format.md) 参照してください。
