---
title: リアルタイムのメディア コールと Microsoft Teams とのオンライン会議
description: リアルタイム メディア プラットフォームを使用して、ボットが Microsoft Teams の通話や会議と対話できるようにする方法について説明します。 調査、メディア セッション、フレームとフレーム レート、オーディオとビデオの形式、アクティブなスピーカー、ビデオ サブスクリプション。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 8eeb30d63c982ead3e990c0dea2a2bb04a820b97
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100918"
---
# <a name="real-time-media-calls-and-meetings-with-microsoft-teams"></a>Microsoft Teamsでのリアルタイムのメディア通話と会議

リアルタイム メディア プラットフォームを使用すると、ボットは、リアルタイムの音声、ビデオ、および画面共有を使用して、Microsoft Teams の通話や会議で対話できます。 リアルタイム メディア プラットフォームは、ボットが音声およびビデオ コンテンツをフレームごとに送受信できるようにする高度な機能です。 ボットは、音声、ビデオ、および画面共有メディア ストリームに生でアクセスできます。 すべてのメディア処理をリアルタイム メディア プラットフォームに依存する、よりシンプルなサービス ホスト型メディア ボットがあります。 メディア自体を処理するボットは、アプリケーション ホスト型メディア ボットと呼ばれます。

たとえば、ボットとの 1 対 1 の通話では、ユーザーが話すと、ボットは 1 秒あたり 50 のオーディオ フレームを受信します。 ボットは、20 ミリ秒 (ms) のオーディオの各フレームでオーディオ フレームを受信します。 アプリケーション ホスト型メディア ボットは、オーディオ フレームが受信されると、リアルタイムの音声認識を実行できます。 ユーザーが話すのをやめた後、録音を待つ必要はありません。 ボットは、ビデオベースの画面共有コンテンツを含む高解像度ビデオを送受信することもできます。

プラットフォームは、ボットがメディアを送受信するためのシンプルなソケットのような API を提供します。 オーディオまたはビデオ パケットのリアルタイムのエンコードとデコードを処理します。 オーディオには SILK や G.722、ビデオには H.264 などのコーデックを使用します。 プラットフォームは、すべてのメディア パケットの暗号化または復号化とパケット ネットワーク送信も処理します。 ボットは、実際のオーディオまたはビデオ コンテンツのみに関係します。 リアルタイム メディア ボットは、複数の参加者との 1 対 1 の通話や会議に参加します。

## <a name="media-session"></a>メディア セッション

リアルタイム メディア ボットは、サポートする必要のあるモダリティを宣言する必要があります。 リアルタイム メディア ボットは、着信に応答するとき、またはTeams 会議に参加するときに、サポートを宣言する必要があります。 サポートされているモダリティごとに、ボットはメディアを送受信できるか、受信のみ、または送信のみが可能かを宣言します。 たとえば、1 対 1 の Teams 通話を処理するように設計されたボットは、音声の送信と受信の両方を必要とします。 ただし、ボットは発信者のビデオを受信する必要がないため、ビデオを送信するだけで済みます。 ボットと Teams の発信者または会議の間で確立された一連のオーディオおよびビデオ モダリティは、メディア セッションと呼ばれます。

メイン ビデオとビデオベースの画面共有の 2 種類のビデオ モダリティがサポートされています。 メイン ビデオは、ユーザーの Web カメラからビデオを転送するために使用されます。 ビデオベースの画面共有により、ユーザーは画面を共有できます。 プラットフォームにより、ボットは両方のビデオの種類を送受信できます。

Teams 会議に参加すると、ボットはメディア セッションごとに最大 10 の複数のメイン ビデオ ストリームを同時に受信できます。 ボットは、会議の複数の参加者を見ることができます。

次のセクションでは、一連のフレームとしてメディアを送受信するボットについて詳しく説明します。

## <a name="frames-and-frame-rate"></a>フレームとフレーム レート

リアルタイム メディア ボットは、メディア セッションのオーディオおよびビデオ モダリティと直接対話します。 ボットは一連のフレームとしてメディアを送受信しており、各フレームはコンテンツ ユニットです。 1 秒のオーディオが 50 フレームのシーケンスとして送信されます。 各フレームには、音声コンテンツの 1/50 秒である 20 ミリ秒が含まれています。 1 秒のビデオは 30 枚の静止画像のシーケンスとして送信されます。 各画像は、次のビデオ フレームの 1/30 秒前のわずか 33.3 ミリ秒で表示されるようになっています。 1 秒あたりに送信またはレンダリングされるフレーム数は、フレーム レートと呼ばれます。

次のセクションでは、リアルタイムのメディア通話や会議で使用されるオーディオおよびビデオ形式について詳しく説明します。

## <a name="audio-and-video-format"></a>オーディオおよびビデオ形式

オーディオ形式では、オーディオ 1 秒あたり 16,000 サンプルとして表され、各サンプルには 16 ビットのデータが含まれています。 20 ミリ秒のオーディオ フレームには、640 バイトのデータである 320 のサンプルが含まれています。

ビデオ形式では、いくつかの形式がサポートされています。 ビデオ形式の 2 つの重要なプロパティは、フレーム サイズとカラー フォーマットです。 サポートされているフレーム サイズには、360 ピクセルである 640x360、720 ピクセルである 1280x720、および 1080 ピクセルである 1920x1080 が含まれます。 サポートされているカラー フォーマットには、ピクセルあたり 12 ビットの NV12 とピクセルあたり 24 ビットの RGB24 が含まれます。

720 p のビデオ形式には、720 の 1280 倍である 921,600 ピクセルが含まれています。 RGB24 カラー フォーマットでは、各ピクセルは 3 バイトとして表されます。これは、赤、緑、青の各色成分 1 バイトを含む 24 ビットです。 単一の 720 p RGB24 ビデオ フレームには、921,600 ピクセル× 3 バイト/ピクセルの 2,764,800 バイトのデータが必要です。 可変フレーム レートで、720 p RGB24 ビデオ フレームを送信することは、毎秒約 80 メガバイトのコンテンツを処理することを意味します。 80 メガバイトは、ネットワーク送信前に H.264 ビデオ コーデックによって大幅に圧縮されます。

プラットフォームの高度な機能により、ボットはエンコードされた H.264 フレームとしてビデオを送受信できます。 独自の H.264 エンコーダーまたはデコーダーを提供するボットがサポートされているか、生の RGB24 または NV12 ビットマップにデコードされたビデオ ストリームは必要ありません。

次のセクションでは、どの会議参加者が話しているか、つまりどの会議参加者がアクティブで支配的なスピーカーであるかについて詳しく説明します。

## <a name="active-and-dominant-speakers"></a>アクティブで支配的なスピーカー

複数の参加者で構成される Teams 会議に参加すると、ボットはどの会議参加者が現在話しているかを識別できます。 アクティブ スピーカーは、受信した各オーディオ フレームでどの参加者が聞こえているかを識別します。 支配的なスピーカーは、グループ会話で現在最もアクティブまたは支配的である参加者を識別しますが、すべてのオーディオ フレームで彼らの声が聞こえるわけではありません。 さまざまな参加者が交代で話すと、支配的なスピーカーのセットが変わる可能性があります。

次のセクションでは、ボットによって行われたビデオ サブスクリプション要求について詳しく説明します。

## <a name="video-subscription"></a>ビデオ サブスクリプション

1 対 1 の通話では、ボットがビデオの受信を有効にしている場合、ボットは発信者のビデオを自動的に受信します。 Teams 会議では、ボットはプラットフォームにどの参加者を表示するかを示す必要があります。 ビデオ サブスクリプションは、参加者のメイン ビデオまたは画面共有コンテンツを受信するためのボットによる要求です。 会議の参加者が会話を行うと、ボットは必要なビデオ サブスクリプションを変更します。 ボットは、支配的なスピーカー セットの更新、または現在画面共有している参加者を示す通知に基づいて、ビデオ サブスクリプションを変更します。

次のセクションでは、インストールする必要があるものと、アプリケーション ホスト型メディア ボットを開発するための要件について詳しく説明します。

## <a name="developer-resources"></a>開発者向けリソース

アプリケーション ホスト型メディア ボットを開発するには、Visual Studio プロジェクト内に [Microsoft.Graph.Calls.Media.NET ライブラリ](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/)の NuGet パッケージをインストールする必要があります。

アプリケーション ホスト型メディア ボットには、.NET または C# と Windows Server が必要です。 詳細については、[アプリケーション ホスト型メディア ボットの要件と考慮事項](requirements-considerations-application-hosted-media-bots.md#c-or-net-and-windows-server-for-development)を参照してください。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [通話ボットを登録する](~/bots/calls-and-meetings/registering-calling-bot.md)

## <a name="see-also"></a>関連項目

[ボットでサポートされているメディア形式](~/resources/media-formats.md)
