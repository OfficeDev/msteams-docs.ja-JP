---
title: Bot メッセージ形式
description: Bot メッセージの書式設定の詳細について説明します。
keywords: teams のシナリオチャネルの会話メッセージ
ms.date: 05/20/2019
ms.openlocfilehash: eb0d0303d2b414ff84beab73055be5f057fff11c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675106"
---
# <a name="message-formatting-for-bots"></a>Bot のメッセージ形式

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

オプション[`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message)のプロパティを設定して、メッセージのテキストコンテンツの表示方法を制御することができます。

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
* リッチカードは、title または副題のプロパティではなく、text プロパティのみをサポートしています。
* リッチカードでは、Markdown または表の書式設定はサポートされていません。

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
