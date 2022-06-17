---
title: 会話でサポートされているテキストの書式設定
description: このモジュールでは、ボットの会話におけるテキストの書式設定のサポートと、Microsoft Teamsのテキスト コンテンツの書式設定について説明します
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/29/2018
ms.openlocfilehash: 2bec542b678f371e20317d1ea7d11b4e97f52338
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142333"
---
# <a name="formatting-bot-messages"></a>ボット メッセージの書式設定

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

オプション [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) のプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法を制御できます。

Microsoft Teamsでは、次の書式設定オプションがサポートされています。

| TextFormat 値 | 説明 |
| --- | --- |
| プレーン | テキストは、書式設定がまったく適用されていない生のテキストとして扱う必要があります。 |
| markdown | テキストは Markdown 書式設定として扱い、必要に応じてチャネルにレンダリングする必要があります。サポートされているスタイルの [テキスト コンテンツの書式設定](#formatting-text-content) に関するページを参照してください。 |
| Xml | テキストは単純な XML マークアップです。サポートされているスタイルの [テキスト コンテンツの書式設定](#formatting-text-content) に関するページを参照してください。 |

## <a name="formatting-text-content"></a>テキスト コンテンツの書式設定

Microsoft Teamsでは、Markdown と XML (HTML) の書式設定タグのサブセットがサポートされています。

現時点では、次の制限事項が適用されます。
* テキストのみのメッセージでは、テーブルの書式設定はサポートされていません。

カードの書式設定の詳細については、「[Teams カード リファレンス」を参照してください](~/task-modules-and-cards/cards/cards-reference.md)。

### <a name="cross-platform-support"></a>クロスプラットフォームサポート

Microsoft Teamsでサポートされているすべてのプラットフォームで書式設定を確実に機能させるには、一部のスタイルが現在すべてのプラットフォームでサポートされていない点に注意してください。

| Style                     | テキストのみのメッセージ | カード (XML のみ) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| ヘッダー (レベル 1&ndash;3) | ✖                  | ✔                |
| 取り消し 線             | ✖                  | ✔                |
| 水平ルール           | ✖                  | ✖                |
| 順序付けられていないリスト            | ✖                  | ✔                |
| 順序付きリスト              | ✖                  | ✔                |
| プリフォームフォーマットされたテキスト         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| hyperlink                 | ✔                  | ✔                |
| image link                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>個々のプラットフォームによるサポート

テキストの書式設定のサポートは、メッセージの種類とプラットフォームによって異なります。

#### <a name="text-only-messages"></a>テキストのみのメッセージ

| Style                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| ヘッダー (レベル 1&ndash;3) | ✖       | ✖   | ✖       |
| 取り消し 線             | ✔       | ✔   | ✖       |
| 水平ルール           | ✖       | ✖   | ✖       |
| 順序付けられていないリスト            | ✔       | ✖   | ✖       |
| 順序付きリスト              | ✔       | ✖   | ✖       |
| プリフォームフォーマットされたテキスト         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| hyperlink                 | ✔       | ✔   | ✔       |
| image link                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>テキストの書式設定の例

| Style | 例 | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| ヘッダー (レベル 1&ndash;3) | **Text** | `### Text` | `<h3>Text</h3>` |
| 取り消し 線 | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| 順序付けられていないリスト | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| 順序付きリスト | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| プリフォームフォーマットされたテキスト | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>テキスト</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| image link | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
