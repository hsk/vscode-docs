---
Order: 1
Area: extensionapi
TOCTitle: Overview
ContentId: C99AC3B3-47BC-41E3-8C7B-6F24364C20D1
PageTitle: Visual Studio Code Extensibility Reference
DateApproved: 5/4/2017
MetaDescription: Learn the details of Visual Studio Code's rich extensibility (plug-in) model.  This documentation describes the various extension points, activation rules and specific feature APIs (e.g. working with documents and editors).
---

# 拡張性リファレンス

このドキュメントのこのセクションでは、 VS Code の拡張性のさまざまな機能について詳しく説明します。
[extensions](/docs/extensions/overview.md)の紹介を見直すだけでなく、 ['Hello World'](/docs/extensions/example-hello-world.md) の例を掘り下げて調べることも価値がありますあまりにも深くここに。

VS Code の拡張機能が動作する最も簡単な方法は、 [拡張機能 Marketplace](/docs/editor/extension-gallery.md) を使用する方法です。
最初の拡張機能をビルドしたら、 他の人がインストールできるように [公開](/docs/extensions/publish-extension.md) することができます。

## 拡張性リファレンスドキュメント

このドキュメントのこのセクションでは、 次のトピックについて説明します。

トピック | 説明
----- | -----------
**[package.json拡張マニフェスト](/docs/extensionAPI/extension-manifest.md)** | すべてのVisual Studio Code 拡張は、 拡張フォルダのルートにマニフェストファイル `package.json` を必要とします。 このドキュメントでは、 そのファイルの構造と必須フィールドの概要について説明します。
**[提供ポイント](/docs/extensionAPI/extension-points.md)**          | ベースの `package.json` に基づいて、あなたが提供できる追加の拡張ポイントがいくつかあります。コマンド、テーマ、デバッガ、...
**[アクティベーションイベント](/docs/extensionAPI/activation-events.md)**     | VS Code は、拡張機能を遅くアクティブにします。 このドキュメントは、 `package.json` でサポートされているアクティベーションオプションについて概説しています。 特定のファイルタイプがロードされたとき、 コマンドが起動されたときなど
**[API vscode名前空間](/docs/extensionAPI/vscode-api.md)**                 | 完全な vscode 名前空間 API リファレンスを確認します。
**[API複合コマンド](/docs/extensionAPI/vscode-api-commands.md)**            | VS Code 複合コマンド API リファレンスを参照してください。
**[デバッグAPI](/docs/extensionAPI/api-debugging.md)**                      | デバッガを VS Code に統合する方法の詳細を学びます。
**[APIサンプル](https://github.com/Microsoft/vscode-extension-samples)**    | VS Code 拡張APIを示すサンプルコード。

## 言語拡張ガイドライン

プログラミング言語サポートを実装している場合は、 VS Code で使用できるさまざまな言語機能(コードの提案や操作、書式設定など)を示す
[言語拡張ガイドライン](/docs/extensionAPI/language-support.md)名前の変更)、 それらの実装方法に関するガイダンスを提供します。
