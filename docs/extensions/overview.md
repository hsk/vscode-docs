---
Order: 1
Area: extensions
TOCTitle: Overview
ContentId: AD26EFB1-FFC6-4284-BAB8-F3BCB8294728
PageTitle: Building extensions for VS Code
DateApproved: 5/4/2017
MetaDescription: Visual Studio Code has a rich extensibility model for interacting with and adding to the tool.  Learn how to create your own extensions (plug-ins) for Visual Studio Code.
---
# Visual Studio Code 拡張

  あなたが VS Code を拡張することに興味があるなら、あなたは正しい場所にいます。
  ここでは、 VS Code の拡張性に関するドキュメントの概要と、最初の VS Code 拡張を迅速に構築する方法について説明します。
  VS Code の拡張性に関する設計アプローチについて興味があれば、 [ここ](patterns-and-principles.md) で読むことができます。

  既存のエクステンションを使用したいだけの場合は、 [Extension Marketplace](/docs/editor/extension-gallery.md) のトピックを参照して、VS Code [Marketplace](https://marketplace.visualstudio.com/VSCode) からエクステンションを見つけてインストールする方法を見つけてください。

  すべての VS Code 拡張は、 contribution （登録）、 activation （ロード）、 および VS Code 拡張 API へのアクセスの共通モデルを共有します。
  しかし、 VS Code 拡張の2つの特別なフレーバー、 言語サーバーとデバッガーがあります。
  それらは独自の追加プロトコルを持ち、 ドキュメントの独自のセクションでカバーされています。

  1. [Extensions](/docs/extensions/overview.md#extensions) - 基本ビルディングブロック
  2. [Language Servers](/docs/extensions/overview.md#language-servers) - 高コストのIOまたはCPU集約的なタスク
  3. [Debuggers](/docs/extensions/overview.md#debug-adapter) - 外部デバッガを接続する

## 1 拡張機能

  すべての拡張機能は、共有拡張ホストプロセスで実行されます。
  拡張のためのこの別のプロセスは、 VS Code が完全な応答を維持することを保証します。

  拡張機能には以下のサポートが含まれます：

  * **Activation** - 特定のファイルタイプが検出されたとき、特定のファイルが存在するとき、またはコマンドパレットまたはキーの組み合わせでコマンドが選択されたときに拡張子を読み込む
  * **Editor** - エディタのコンテンツを操作します - テキストを読み込んで操作したり、選択を活用する等
  * **Workspace** - 開いているエディタ、ステータスバー、情報メッセージなどにアクセスできます
  * **Eventing** - open、 close、 change など、 エディタのライフサイクルイベントに接続します
  * **Evolved editing** - IntelliSense、Peek、Hover、Diagnosticsなどを含む豊富な言語サポートのプロバイダを作成します

  拡張機能の基本については、2つのエンドツーエンドのチュートリアルがあります。

  1. **[Hello World](/docs/extensions/example-hello-world.md)** - 基本的な拡張機能を生成し、拡張機能のフォルダ構造、拡張機能のマニフェストを理解し、起動の仕組みを学び、拡張機能を実行してデバッグしますそれをローカルにインストールします。
  2. **[Word Count](/docs/extensions/example-word-count.md)** - ファイルを移動するときに、特定のファイルタイプに基づいてアクティブ化し、ステータスバーを更新し、テキストエディタの変更に応答し、拡張子を破棄します。

  また、拡張性API全体で使用される共有プログラミングパターンについての説明 [拡張性の原則とパターン](patterns-and-principles.md) も役立ちます。

## 2 言語サーバー

  言語サーバーを使用すると、拡張機能の専用プロセスを作成できます。
  エクステンションが高コストのCPUまたはIOを集中的に実行して、他の拡張機能を遅くする可能性がある場合、これは拡張機能にとって便利な設計方法です。
  これは、ワークスペース内のすべてのファイルにわたって機能するリンターまたは静的分析スイートのようなタスクで共通です。

  さらなる情報は [言語サーバー](/docs/extensions/example-language-server.md) の詳細を確認してください。

## 3 デバッグアダプタ

  VS Code はジェネリックデバッガのUIを実装し、デバッガの拡張機能やいわゆる「デバッグアダプタ」に依存してデバッグUIを実際のデバッガやランタイムに接続します。
  デバッグアダプタは、 _VS Code デバッグプロトコル_ を通じて VS Code と通信する専用のプロセスであり、どの言語でも実装できます。

  [デバッガ拡張機能](/docs/extensions/example-debuggers.md) の作成の詳細を確認してください。

  ---

  VS Code の拡張機能が動作する最も簡単な方法は、 [Extension Marketplace](/docs/editor/extension-gallery.md) を使用する方法です。
  便利なエクステンションをブラウズしてインストールして試してみて、自分の開発シナリオで VS Code を拡張する方法を知ることができます。

## 4 言語拡張ガイドライン

  [言語拡張ガイドライン](language-support.md) トピックは、拡張機能でサポートしたい言語機能を決定するのに役立ちます。
  VS Code で使用できるさまざまな言語機能（コードの提案や操作、書式設定、名前の変更など）と、言語サーバープロトコルを使用して実装する方法、または拡張機能から直接拡張APIを使用する方法を示します。

## 5 テーマ、スニペット、および色付け

  構文ハイライト、便利なスニペット、よくデザインされたカラーテーマなどの簡単な操作で、プログラミング言語の優れた編集体験を得ることができます。
  TextMate のカスタマイズファイルはこのサポートを提供し、 VS Code を使用すると簡単にパッケージ化して再利用できるため、拡張子に `.tmTheme`、 `.tmSnippets`、 および `.tmLanguage` ファイルを直接使用できます。
  [テーマ、スニペット、色付け](/docs/extensions/themes-snippets-colorizers.md) トピックでは、 TextMate ファイルを含める方法と、独自のテーマ、スニペット、言語カラーライザーの作成方法に関するガイダンスを提供します。

## 6 エクステンションを書く

  Yeoman [extension generator](/docs/extensions/yocode.md) があるので、 簡単な拡張プロジェクトの作成はとても簡単です。
  これらは初心者向けに優れており、 既存の拡張機能 [examples](/docs/extensions/samples.md) もあります。

  拡張機能は、 TypeScript または JavaScript で記述できます。
  VS Code は、 VS Code 自体の中からすべての [開発、ビルド、実行、テスト、デバッグ](/docs/extensions/debugging-extensions.md) が可能なファーストクラスの拡張開発環境を提供します。

## 7.拡張機能のテスト

  また、拡張機能の[テストの作成と実行](/docs/extensions/testing-extensions.md)も完全にサポートしています。
  VS Code API を呼び出し、 実行中のVSコードインスタンスでコードをテストする統合テストを簡単に作成できます。

## 8 次のステップ

  * [Your First Extension](/docs/extensions/example-hello-world.md) - 単純なHello World拡張を作成してみてください。
  * [Extension API](overview.md) - VS Code 拡張APIについて学びます。
  * [拡張の例](/docs/extensions/samples.md) - あなたが見直してビルドできる拡張サンプルのリスト。
