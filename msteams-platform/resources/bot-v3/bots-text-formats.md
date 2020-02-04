---
title: 会話でサポートされているテキスト形式
description: Bot の会話でのテキストの書式設定のサポートについて説明します。
keywords: ボット会話メッセージング
ms.date: 03/29/2018
ms.openlocfilehash: cc6cba697a1f6907bfb13b94740e7bf9e92596da
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674655"
---
# <a name="formatting-bot-messages"></a>Bot メッセージの書式設定

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

オプション[`TextFormat`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message)のプロパティを設定して、メッセージのテキストコンテンツの表示方法を制御することができます。

Microsoft Teams では、次の書式設定オプションをサポートしています。

| TextFormat の値 | 説明 |
| --- | --- |
| 標準 | 書式をまったく適用せずに、テキストを raw テキストとして処理する必要があります。 |
| markdown | テキストは Markdown 書式設定として扱われ、必要に応じてチャネル上でレンダリングされます。サポートされているスタイルの[テキストコンテンツの書式設定](#formatting-text-content)を参照してください。 |
| xml-rpc | テキストは単純な XML マークアップです。サポートされているスタイルの[テキストコンテンツの書式設定](#formatting-text-content)を参照してください。 |

## <a name="formatting-text-content"></a>テキストコンテンツの書式設定

Microsoft Teams では、Markdown と XML (HTML) 書式設定タグのサブセットをサポートしています。

現時点では、次の制限が適用されます。

* テキストのみのメッセージが表の書式設定をサポートしていない

カードの書式設定の詳細については、 [Teams カードリファレンス](~/task-modules-and-cards/cards/cards-reference.md)を参照してください。

### <a name="cross-platform-support"></a>クロスプラットフォームのサポート

Microsoft Teams でサポートされているすべてのプラットフォームで書式設定が機能することを確認するために、一部のスタイルは現在すべてのプラットフォームでサポートされていないことに注意してください。

| Style                     | テキストのみのメッセージ | カード (XML のみ) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| ヘッダー (レベル 1&ndash;3) | ✖                  | ✔                |
| 打ち消し             | ✖                  | ✔                |
| 段落罫線           | ✖                  | ✖                |
| 順序なしリスト            | ✖                  | ✔                |
| 順序付きリスト              | ✖                  | ✔                |
| 書式設定済みのテキスト         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| hyperlink                 | ✔                  | ✔                |
| 画像リンク                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>個別のプラットフォームによるサポート

テキストの書式設定のサポートは、メッセージの種類およびプラットフォームによって異なります。

#### <a name="text-only-messages"></a>テキストのみのメッセージ

| Style                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| ヘッダー (レベル 1&ndash;3) | ✖       | ✖   | ✖       |
| 打ち消し             | ✔       | ✔   | ✖       |
| 段落罫線           | ✖       | ✖   | ✖       |
| 順序なしリスト            | ✔       | ✖   | ✖       |
| 順序付きリスト              | ✔       | ✖   | ✖       |
| 書式設定済みのテキスト         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| hyperlink                 | ✔       | ✔   | ✔       |
| 画像リンク                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>テキストの書式設定の例

| Style | 例 | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| ヘッダー (レベル 1&ndash;3) | **テキスト** | `### Text` | `<h3>Text</h3>` |
| 打ち消し | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| 順序なしリスト | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| 順序付きリスト | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| 書式設定済みのテキスト | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| hyperlink | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| 画像リンク | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
