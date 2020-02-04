---
title: Bot メッセージの書式設定
author: clearab
description: Bot メッセージにリッチ書式を追加する
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: a11d01233481371c66562e0fa27ab805b06e9391
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674769"
---
# <a name="format-your-bot-messages"></a>Bot メッセージの書式設定

オプション[`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message)のプロパティを設定して、メッセージのテキストコンテンツの表示方法を制御することができます。

Microsoft Teams では、次の書式設定オプションをサポートしています。

| TextFormat の値 | 説明 |
| --- | --- |
| 標準 | 書式を適用せずに、テキストを raw テキストとして扱う必要があります。|
| markdown | テキストは、Markdown 形式として扱われ、必要に応じてチャネルでレンダリングされます。 サポートされているスタイルについては、 *「* [テキストコンテンツの書式設定](#formatting-text-content)」を参照 |
| xml-rpc | テキストは単純な XML マークアップです。 サポートされているスタイルについては、 *「* [テキストコンテンツの書式設定](#formatting-text-content)」を参照 |

## <a name="formatting-text-content"></a>テキストコンテンツの書式設定

Microsoft Teams では、Markdown と XML (HTML) 書式設定タグのサブセットをサポートしています。

現時点では、次の制限が適用されます。

* テキストのみのメッセージは、表の書式設定をサポートしていません。
* リッチカードは、title または副題のプロパティではなく、text プロパティだけで書式設定をサポートしています。
* リッチカードは、Markdown または表の書式設定をサポートしていません。

## <a name="cross-platform-support"></a>クロスプラットフォームのサポート

Microsoft Teams でサポートされているすべてのプラットフォームで書式設定が機能することを確認するために、一部のスタイルは現在すべてのプラットフォームでサポートされていないことに注意してください。

| Style                     | テキストのみのメッセージ | リッチカード (XML のみ) |
| ---                       | :---: | :---: |
| bold                      | ✔ | ✖ |
| italic                    | ✔ | ✔ |
| ヘッダー (レベル 1&ndash;3) | ✖ | ✔ |
| 打ち消し             | ✖ | ✔ |
| 段落罫線           | ✖ | ✖ |
| 順序なしリスト            | ✖ | ✔ |
| 順序付きリスト              | ✖ | ✔ |
| 書式設定済みのテキスト         | ✔ | ✔ |
| blockquote                | ✔ | ✔ |
| hyperlink                 | ✔ | ✔ |
| 画像リンク                | ✔ | ✖ |

## <a name="support-by-individual-platform"></a>個別のプラットフォームによるサポート

テキストの書式設定のサポートは、メッセージの種類およびプラットフォームによって異なります。

### <a name="text-only-messages"></a>テキストのみのメッセージ

| Style                     | Desktop | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔ | ✔ | ✔ |
| italic                    | ✔ | ✔ | ✔ |
| ヘッダー (レベル 1&ndash;3) | ✖ | ✖ | ✖ |
| 打ち消し             | ✔ | ✔ | ✖ |
| 段落罫線           | ✖ | ✖ | ✖ |
| 順序なしリスト            | ✔ | ✖ | ✖ |
| 順序付きリスト              | ✔ | ✖ | ✖ |
| 書式設定済みのテキスト         | ✔ | ✔ | ✔ |
| blockquote                | ✔ | ✔ | ✔ |
| hyperlink                 | ✔ | ✔ | ✔ |
| 画像リンク                | ✔ | ✔ | ✔ |

### <a name="cards"></a>Lcc

カードのサポートについては、[カード形式](~/task-modules-and-cards/cards/cards-format.md)を参照してください。
