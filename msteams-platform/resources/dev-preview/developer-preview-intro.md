---
title: Developer Preview
description: Microsoft Teams のパブリック アプリケーションのDeveloper Previewについて説明します。
ms.topic: conceptual
keywords: Teams プレビュー開発者向け機能
ms.openlocfilehash: b8e8847d71ec3a571d434f952c79f3dd6a8f5bf1
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014076"
---
# <a name="public-developer-preview-for-microsoft-teams"></a>Microsoft Teams のパブリック開発者プレビュー

>[!NOTE]
>プレビューに含まれる機能は完全ではなく、一般リリースで利用可能になる前に変更される可能性があります。 これらは、テストおよび調査のみを目的として提供されます。 これらは、実稼働アプリケーションでは使用できません。

Developer Previewは、Microsoft Teams で未公開の機能に早期にアクセスできる開発者向けのパブリック プログラムです。 これにより、Microsoft Teams アプリに組み込まれる可能性がある機能について、今後の機能を確認してテストできます。 開発者プレビューの [機能](~/feedback.md) に関するフィードバックも歓迎します。 開発者プレビューは Microsoft Teams クライアントごとに有効になっているので、組織全体に影響を与える心配はありません。

## <a name="developer-preview-app-manifest"></a>開発者プレビュー アプリ マニフェスト

開発者プレビューで有効になっている多くの機能では、アプリ マニフェストの JSON ファイルを変更する必要があります。 これを行うには、開発者プレビュー マニフェスト スキーマ[](~/resources/schema/manifest-schema-dev-preview.md)を使用する必要があります。このスキーマを使用する場合[、App Studio](~/concepts/build-and-test/app-studio-overview.md)を使用してこれらの変更を加え、テスト用にアプリをアップロードすることはできません。 アプリをアップロードするには、アプリ バーのアイコンをクリックし、 `More apps` `Upload a custom app link` この方法では、zip 形式のアプリ パッケージのみをアップロードできます。

App Studio を使用してアプリ パッケージの開発者以外のプレビュー部分を作成し、そのパッケージをエクスポートし、ファイルを手動で編集して、使用する開発者プレビュー機能を追加すると便利な場合があります。 `manifest.json` ファイルに開発者向けのプレビュー機能を追加すると、パッケージを App Studio に再 `manifest.json` インポートできます。

## <a name="enable-developer-preview"></a>開発者プレビューを有効にする

開発者プレビューはクライアントごとに有効になりますが、開発者プレビューを有効にするオプションは組織レベルで制御されます。 個人の開発者プレビューを有効にするオプションを有効にするには、カスタム アプリをアップロードする機能をユーザーが持っている必要があります。 詳細 [については、テナントの設定](~/concepts/build-and-test/prepare-your-o365-tenant.md) を参照してください。

開発者プレビュー機能を含むアプリを使用すると、開発者プレビューを有効にしていないクライアントが予期せず動作する可能性があります。 開発者プレビューのエントリが表示されない場合、組織がアプリのアップロード用に構成されていない可能性が最も高い理由です。

### <a name="on-a-desktop-or-web-client"></a>デスクトップまたは Web クライアント上

デスクトップまたは Web クライアントでパブリック開発者プレビューを有効にするには、次の手順を実行する必要があります。

1. ここで説明するように、テナントの管理コンソールでアプリのアップロードを有効 [にします](~/concepts/build-and-test/prepare-your-o365-tenant.md)。
1. 自分のプロファイル (Teams インターフェイスの右上または左下) をクリックして、Teams メニューを表示します。
1. [開発者向けプレビュー→について] を選択します。
1. [開発者 **向けプレビューに切り替える] を選択します**。

### <a name="on-a-mobile-client"></a>モバイル クライアントの場合

モバイル クライアントでパブリック開発者プレビューを有効にするには、次の手順を実行する必要があります。

1. ここで説明するように、テナントの管理コンソールでアプリのアップロードを有効 [にします](~/concepts/build-and-test/prepare-your-o365-tenant.md)。
1. 左上のハンバーガー メニューを開き、[設定] を選択 **します**。
1. Select **About**.
1. [開発者向けプレビュー] トグルをクリックします。

## <a name="disable-developer-preview"></a>開発者プレビューを無効にする

[開発者向けプレビューについて] で同じメニュー→クリックしてオフにします。

## <a name="features-available-in-developer-preview"></a>開発者プレビューで利用可能な機能

開発者プレビューで現在有効になっている機能の完全な一覧については、「パブリック開発者プレビューの [機能」を参照してください](../../resources/dev-preview/developer-preview-features.md)。
