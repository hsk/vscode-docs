---
Order: 8
Area: extensions
TOCTitle: Additional Examples
ContentId: B32601A8-27ED-4D97-BA83-F1C8C945C635
PageTitle: Visual Studio Code Extension Examples
DateApproved: 5/4/2017
MetaDescription: Learn from existing Visual Studio Code extension examples.
---
# VS Code 拡張の例

## 拡張の基礎

コアコンセプトの多くをカバーする2つのウォークスルーがあります:

* **[最初の拡張](/docs/extensions/example-hello-world.md)** - ウォークスルーでコアの拡張の概念を説明します。
* **[Word Count 拡張](/docs/extensions/example-word-count.md)** - 最後の別のウォークスルービルド。

## サンプル拡張

サンプル|説明|タイプ| Marketplace
------|-----------|----|---------
**[Word Count](https://github.com/Microsoft/vscode-wordcount)**|編集イベントで更新されるマークダウンファイルのステータスバーに単語数を追加します。 [これがどのように作成されたかについてのウォークスルー](/docs/extensions/example-word-count.md) があります。 | [拡張](/docs/extensions/example-hello-world.md)|Y
**[MDTools](https://github.com/Microsoft/vscode-MDTools)**|一般的なテキスト処理に基づいて選択や更新を行います。 ToUpper、HTMLEncode、...|[拡張](/docs/extensions/example-hello-world.md)|Y
**[Decorator](https://github.com/Microsoft/vscode-extension-samples/tree/master/decorator-sample)**|境界線、色、およびカスタムカーソルを使用してエディタテキストを飾る方法を示します。|[拡張](/docs/extensions/example-hello-world.md)|N
**[Preview Html](https://github.com/Microsoft/vscode-extension-samples/tree/master/previewhtml-sample)**| `vscode.previewHtml` [コマンドと一緒に仮想ドキュメントを作成する方法を示します](/docs/extensionAPI/vscode-api-commands.md#commands)。|[拡張](/docs/extensions/example-hello-world.md)|Y
**[ドキュメントコンテンツプロバイダ](https://github.com/Microsoft/vscode-extension-samples/tree/master/contentprovider-sample)**|APIコマンドの使用方法と、 `TextDocumentContentProvider`-API を使用して _virtual_ ドキュメントを作成する方法を示します。|[拡張](/docs/extensions/example-hello-world.md)|Y
**[TSLint](https://github.com/Microsoft/vscode-tslint)**|TSLint  に基づいて TypeScript ファイルをリントします。|[Language Server](/docs/extensions/example-language-server.md)|Y
**[スペルチェックと文章校正](https://github.com/Microsoft/vscode-spell-check)**|設定可能なマークダウンのスペルチェックと文章校正。チェックのために外部Webサービスを呼び出し、アクティベーションをサポートし、ディクショナリに追加し、エラーマッピングを行います。設定ファイルの変更をリアルタイムで監視する|[拡張](/docs/extensions/example-hello-world.md)|Y
**[モックデバッガ](https://github.com/Microsoft/vscode-mock-debug)**|デバッガをビルドしてテストするのに役立ちます。 |[デバッガ](/docs/extensions/example-debuggers.md)|Y
**[Go言語サポート](https://github.com/microsoft/vscode-go)**| [Go Lang](https://golang.org/) の豊富な言語サポート - IntelliSense、 Debug、 Peek、 名前の変更、 構文、 ...|[拡張](/docs/extensionAPI/vscode-api.md#languages)|Y

## 拡張を構築するためのツール

ツール|目的
----|-------
**[Extension Generator](/docs/extensions/yocode.md)**|拡張機能を実装するのを手助けするため、 [Yeoman](http://yeoman.io/) ジェネレータがあります。 これにより、開発環境がうまく動作するために必要なすべての初期設定が作成され、 API タイピングファイルと関連モジュールが含まれます。 ジェネレータのソースコードは [こちら](https://github.com/Microsoft/vscode-generator-code) にあります。
**[Debugging Extensions](/docs/extensions/debugging-extensions.md)**|私たちは、拡張機能の開発、デバッグ、ローカルテストを簡単に行うために努力しました。
**[Publishing Tool](/docs/extensions/publish-extension.md)**|有効な拡張機能があれば、それを [拡張機能 Marketplace](/docs/editor/extension-gallery.md) で共有しましょう。 このための簡単なコマンドラインツールがあります。

## チュートリアルのサンプル

チュートリアル|説明 
--------|-----------
**[Node.js](https://github.com/Microsoft/vscode-samples)**|Node.js Expressの [tutorial](/docs/nodejs/nodejs-tutorial.md) の最終結果

## 次のステップ

* [拡張機能 Marketplace](/docs/editor/extension-gallery.md) -  公開されている VS Code 拡張機能 Marketplace の詳細をご覧ください。
