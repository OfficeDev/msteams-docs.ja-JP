---
title: アプリの既定のインストール オプションを構成する
description: アプリの既定のインストール オプションを指定する方法について説明します。
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a4b70df70c7b9442e29953dae8a8c4e892cb72c1
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946491"
---
# <a name="add-a-default-install-scope-and-group-capability"></a>既定のインストール スコープとグループ機能を追加する

アプリが Teams で複数のシナリオをサポートする場合は一般的ですが、特定の範囲と機能を念頭に置いて設計した可能性があります。 たとえば、アプリが主にチームまたはチャネルを使用する場合は、ストアでユーザーに表示される最初のインストール オプションが [チームに追加] である必要 **があります**。

![アプリの追加](../../assets/images/compose-extensions/addanapp.png)

アプリの主な機能がボットである場合は、ユーザーがアプリをチームにインストールするときにボットを既定の機能にすることもできます。 

## <a name="configure-your-apps-default-install-scope"></a>アプリの既定のインストール スコープを構成する

アプリの既定のインストール スコープを構成します。 一度に設定できるスコープは 1 つのみです。

**アプリ マニフェストで既定のインストール スコープを構成するには**

1. アプリ マニフェストを開き、プロパティを追加 `defaultInstallScope` します。
2. 、、または `personal` (以下の `team` 例 `groupchat` を参照) `meetings` の値を設定します。

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> 詳細については、「アプリ マニフェスト スキーマ [」を参照してください](~/resources/schema/manifest-schema.md)。

## <a name="configure-the-default-capability-for-shared-scopes"></a>共有スコープの既定の機能を構成する

チーム、会議、またはチャット用にアプリがインストールされている場合は、既定の機能を構成します。

**アプリ マニフェストで詳細を構成するには**

1. アプリ マニフェストを開き、プロパティ `defaultGroupCapability` を追加します。
2. 更新プログラムを保存します。

    JSON の例を次に示します。

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```
> [!NOTE]
> 完全なスキーマの詳細については、「マニフェスト スキーマ [」を参照してください](~/resources/schema/manifest-schema.md)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アプリの配信方法を選ぶ](overview.md)
