---
title: 会話でサポートされるテキストの書式設定
description: ボットの会話でのテキストの書式設定のサポートについて説明します。
keywords: ボットの会話メッセージング
ms.topic: how-to
localization_priority: Normal
ms.date: 03/29/2018
ms.openlocfilehash: dfb91e18a2ad895ae5b48c905046a22449304fc6
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566748"
---
# <a name="formatting-bot-messages"></a>ボット メッセージの書式設定

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

省略可能なプロパティを設定して、メッセージのテキスト コンテンツのレンダリング方法 [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) を制御できます。

Microsoft Teamsは、次の書式設定オプションをサポートしています。

| TextFormat 値 | 説明 |
| --- | --- |
| プレーン | テキストは、書式が適用されずに生テキストとして扱われる必要があります。 |
| markdown | テキストは Markdown 書式設定として扱い、必要に応じてチャネルにレンダリングする必要があります。「サポート [されているスタイルのテキスト コンテンツ](#formatting-text-content) を書式設定する」を参照してください。 |
| xml | テキストは単純な XML マークアップです。「サポート [されているスタイルのテキスト コンテンツ](#formatting-text-content) を書式設定する」を参照してください。 |

## <a name="formatting-text-content"></a>テキスト コンテンツの書式設定

Microsoft Teamsは、Markdown および XML (HTML) 書式タグのサブセットをサポートします。

現時点では、次の制限が適用されます。

* テキスト専用メッセージはテーブルの書式設定をサポートしません

カードの書式設定の詳細については[、「Teams」を参照してください](~/task-modules-and-cards/cards/cards-reference.md)。

### <a name="cross-platform-support"></a>クロスプラットフォームのサポート

Microsoft Teams でサポートされているすべてのプラットフォームで書式設定が機能するには、一部のスタイルが現在すべてのプラットフォームでサポートされていない点に注意してください。

| Style                     | テキスト専用メッセージ | カード (XML のみ) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| ヘッダー (レベル 1 &ndash; 3) | ✖                  | ✔                |
| 取り消し線             | ✖                  | ✔                |
| 水平ルール           | ✖                  | ✖                |
| 順序なしリスト            | ✖                  | ✔                |
| 順序付きリスト              | ✖                  | ✔                |
| 事前に書式設定されたテキスト         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| hyperlink                 | ✔                  | ✔                |
| 画像リンク                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>個々のプラットフォームによるサポート

テキストの書式設定のサポートは、メッセージの種類やプラットフォームによって異なります。

#### <a name="text-only-messages"></a>テキスト専用メッセージ

| Style                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| ヘッダー (レベル 1 &ndash; 3) | ✖       | ✖   | ✖       |
| 取り消し線             | ✔       | ✔   | ✖       |
| 水平ルール           | ✖       | ✖   | ✖       |
| 順序なしリスト            | ✔       | ✖   | ✖       |
| 順序付きリスト              | ✔       | ✖   | ✖       |
| 事前に書式設定されたテキスト         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| hyperlink                 | ✔       | ✔   | ✔       |
| 画像リンク                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>テキストの書式設定の例

| Style | 例 | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| ヘッダー (レベル 1 &ndash; 3) | **Text** | `### Text` | `<h3>Text</h3>` |
| 取り消し線 | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| 順序なしリスト | <ul><li>テキスト</li><li>テキスト</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| 順序付きリスト | <ol><li>テキスト</li><li>テキスト</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| 事前に書式設定されたテキスト | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>テキスト</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
