---
title: Microsoft Teams の開発者向けパブリック プレビュー
description: この記事では、Microsoft Teams および開発者プレビュー アプリ マニフェストのパブリック開発者プレビューに含まれる機能について説明します。
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 6efc0681ad15add36ddaf94d3ca89ef931e9f30e
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143985"
---
# <a name="public-developer-preview-for-microsoft-teams"></a>Microsoft Teams の開発者向けパブリック プレビュー

>[!NOTE]
>プレビューに含まれている機能は完全でないため、一般公開前に変更される場合があります。 これらは、テストと調査のみを目的としています。 実稼働アプリケーションでは使用しないでください。

開発者向けプレビューは、Microsoft Teams のリリース前の機能にいち早くアクセスできる開発者向けの公開プログラムです。 これにより、今後の機能を検索およびテストし、Microsoft Teams アプリに潜在的に含めることができます。 開発者向けプレビューのあらゆる機能に関する[フィードバック](~/feedback.md)をお待ちしております。 開発者向けプレビューは、Microsoft Teams クライアントごとに有効になっているので、組織全体への影響を心配する必要はありません。

## <a name="developer-preview-app-manifest"></a>開発者向けプレビューのアプリ マニフェスト

開発者向けプレビューで有効になっている多くの機能は、アプリ マニフェスト JSON ファイルを変更する必要があります。 そのためには、[開発者向けプレビュー マニフェスト スキーマ](~/resources/schema/manifest-schema-dev-preview.md)を使用する必要があります。 このスキーマを使用した場合、[アプリ スタジオ](~/concepts/build-and-test/app-studio-overview.md)を使用してこれらの変更を行うことも、テスト用のアプリをアップロードすることもできません。 アプリをアップロードするには、アプリ バーの `More apps` アイコンを選択して、`Upload a custom app link` を選択する必要があります。 この方法を使用する場合、アプリ パッケージを圧縮 (zip 形式) してアップロードすることのみ可能です。

アプリ スタジオを使用してアプリ パッケージの開発者向けプレビュー以外の部分を作成し、そのパッケージをエクスポートして `manifest.json` ファイルを手動で編集し、使用する開発者向けプレビュー機能を追加すると便利です。 `manifest.json` ファイルに開発者向けプレビュー機能を追加すると、パッケージをアプリ スタジオに再インポートできなくなります。

## <a name="enable-developer-preview"></a>開発者向けプレビューを有効にする

開発者向けプレビューはクライアントごとに有効ですが、開発者向けプレビューをオンにするオプションは組織レベルで制御されます。 開発者向けプレビューを有効にするオプションを個人向けに有効にするには、そのユーザーがカスタム アプリをアップロードする機能を持っている必要があります。 追加情報については、「[テナントの設定](~/concepts/build-and-test/prepare-your-o365-tenant.md)」を参照してください。

開発者向けプレビュー機能を含むアプリを使用すると、開発者向けプレビューを有効にしていないクライアントが予期しない動作をする場合があります。 開発者向けプレビューのエントリが表示されない場合は、組織がアプリのアップロード用に構成されていないことが原因である可能性が最も高いと考えられます。

### <a name="on-a-desktop-or-web-client"></a>デスクトップまたは Web クライアントで

デスクトップまたは Web クライアントで開発者向けパブリック プレビューを有効にするには、以下を実行します。

1. 開発者テナントのカスタム アプリのアップロードまたはサイドローディングを有効にします。 詳細については、「[カスタムの Teams アプリを有効にする](../../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)」を参照してください。
1. ユーザー プロファイルの横にある省略記号 (...) メニューを選択して、Teams メニューを表示します。
1. **[情報]** > **[開発者向けプレビュー]** を選択します。
1. **[開発者向けプレビューに切り替え]** を選択します。

### <a name="on-a-mobile-client"></a>モバイル クライアントで

モバイル クライアントで開発者向けパブリック プレビューを有効にするには、以下を実行します。

1. 開発者テナントのアプリのアップロードまたはサイドローディングを有効にします。 詳細については、「[カスタムの Teams アプリを有効にする](../../concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)」を参照してください。
1. 左上のハンバーガー メニューを開き、**[設定]** を選択します。
1. **[バージョン情報]** を選びます。
1. **[開発者向けプレビュー]** のトグルをオンにします。

## <a name="disable-developer-preview"></a>開発者向けプレビューを無効にする

[情報] → [開発者向けプレビュー] で同じメニュー アイテムを使用し、それを選択してオフにします。

## <a name="see-also"></a>関連項目

[Microsoft Teams アプリのテストとデバッグ](~/concepts/build-and-test/debug.md)
