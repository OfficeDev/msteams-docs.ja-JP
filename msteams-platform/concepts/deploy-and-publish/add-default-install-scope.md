---
title: アプリの既定のインストール オプションを構成する
description: アプリの既定のインストール オプションを指定する方法について説明します。
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 0afcce50a4779421016c23c4ec4e3d25cc3401d1
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058615"
---
# <a name="add-a-default-install-scope-and-group-capability"></a>既定のインストール スコープとグループ機能を追加する

アプリが Teams で複数のシナリオをサポートする場合は一般的ですが、特定の範囲と機能を念頭に置いて設計した可能性があります。 たとえば、アプリが主にチームまたはチャネルを使用する場合は、ストアでユーザーに表示される最初のインストール オプションが [チームに追加] である必要 **があります**。

![アプリの追加](../../assets/images/compose-extensions/addanapp.png)

アプリの主な機能がボットである場合は、ユーザーがアプリをチームにインストールするときにボットを既定の機能にすることもできます。

## <a name="configure-your-apps-default-install-scope"></a>アプリの既定のインストール スコープを構成する

アプリの既定のインストール スコープを構成します。 一度に設定できるスコープは 1 つのみです。

**アプリ マニフェストで既定のインストール スコープを構成するには**

1. アプリ マニフェストを開き、プロパティを追加 `defaultInstallScope` します。
2. 既定のインストール スコープの値を 、のいずれか `personal` `team` `groupchat` として設定します `meetings` 。

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> 詳細については、「アプリ マニフェスト スキーマ [」を参照してください](~/resources/schema/manifest-schema.md)。

## <a name="configure-the-default-capability-for-shared-scopes"></a>共有スコープの既定の機能を構成する

チーム、会議、またはグループチャット用にアプリがインストールされている場合は、既定の機能を構成します。

> [!NOTE]
> `defaultGroupCapability` は、チーム、グループチャット、または会議に追加される既定の機能を提供します。 アプリの既定の機能としてタブ、ボット、またはコネクタを選択しますが、アプリ定義で選択した機能が提供されている必要があります。

**アプリ マニフェストで詳細を構成するには**

1. アプリ マニフェストを開き、プロパティ `defaultGroupCapability` を追加します。
2. 、または `team` の値 `groupchat` を設定します `meetings` 。
3. 選択したグループ機能の場合、使用可能なグループ機能は `bot` `tab` 、、またはです `connector` 。 

    > [!NOTE]
    > 既定の機能 、、または選択したグループ機能の `bot` `tab` `connector` 1 つのみ選択できます。

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> 詳細については、「アプリ マニフェスト スキーマ [」を参照してください](~/resources/schema/manifest-schema.md)。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [アプリの配信方法を選ぶ](overview.md)
