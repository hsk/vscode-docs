
---
Order: 7
Area: extensionapi
TOCTitle: Complex Commands
ContentId: A010AEDF-EF37-406E-96F5-E129408FFDE1
PageTitle: Visual Studio Code Complex Commands Reference
DateApproved: 5/4/2017
MetaDescription: Visual Studio Code extensions (plug-ins) complex commands Reference.
---
# 複合コマンド

このドキュメントでは、 Visual Studio Code の複雑なコマンドのセットについて説明します。それらはパラメータを必要とし、しばしば値を返すため複雑なコマンドと呼ばれます。これらのコマンドは、 `executeCommand` API と組み合わせて使用​​できます。

HTML 文書をプレビューする方法の例を次に示します。

```javascript
let uri = Uri.parse('file:///some/path/to/file.html');
let success = await commands.executeCommand('vscode.previewHtml', uri);
```

## コマンド

`vscode.executeWorkspaceSymbolProvider` - すべてのワークスペースシンボルプロバイダを実行します。

* _query_ 検索文字列
* _(returns)_ SymbolInformation-instances の配列に解決される promise。


`vscode.executeDefinitionProvider` - すべての定義プロバイダを実行します。

* _uri_ テキスト文書の Uri
* _position_ シンボルの位置
* _(returns)_ Location インスタンスの配列に解決する promise。

`vscode.executeImplementationProvider` - すべての実装プロバイダを実行します。

* _uri_ テキスト文書の Uri
* _position_ シンボルの位置
* _(returns)_ Location-instance の配列に解決される promise。


`vscode.executeHoverProvider` - すべてのホバープロバイダを実行します。

* _uri_テキスト文書の Uri
* _position_ シンボルの位置
* _(returns)_ ホバーインスタンスの配列に解決される約束。


`vscode.executeDocumentHighlights` - ドキュメントハイライトプロバイダを実行します。

* _uri_ テキスト文書の Uri
* _position_ テキスト文書内の位置
* _(returns)_ DocumentHighlightインスタンスの配列に解決する promise。


`vscode.executeReferenceProvider` - 参照プロバイダを実行します。

* _uri_ テキスト文書の Uri
* _position_ テキスト文書内の位置
* _(returns)_ Locationインスタンスの配列に解決する promise。


`vscode.executeDocumentRenameProvider` - 名前変更プロバイダを実行します。

* _uri_ テキスト文書の Uri
* _position_ テキスト文書内の位置
* _newName_ 新しいシンボル名
* _(returns)_ WorkspaceEditに解決する promise。


`vscode.executeSignatureHelpProvider` - 署名ヘルププロバイダを実行します。

* _uri_ テキスト文書の Uri
* _position_ テキスト文書内の位置
* _triggerCharacter_ (オプション）ユーザーが文字を入力すると、トリガー署名のヘルプ( `、`、 `
* _(returns)_ SignatureHelpに解決する promise。


`vscode.executeDocumentSymbolProvider` - ドキュメントシンボルプロバイダを実行します。

* _uri_ テキスト文書の Uri
* _(returns)_ SymbolInformation-instancesの配列に解決される約束。


`vscode.executeCompletionItemProvider` - 補完項目プロバイダを実行します。

* _uri_ テキスト文書の Uri
* _position_ テキスト文書内の位置
* _triggerCharacter_ (オプション）ユーザーが `、`、 `(`
* _(returns)_ CompletionListインスタンスに解決する promise。


`vscode.executeCodeActionProvider` - コードアクションプロバイダを実行します。

* _uri_ テキスト文書の Uri
* _range_ テキスト文書の範囲
* _(returns)_ コマンドインスタンスの配列に解決する promise。


`vscode.executeCodeLensProvider` - CodeLensプロバイダを実行します。

* _uri_ テキスト文書の Uri
* _(returns)_ CodeLensインスタンスの配列に解決する promise。


`vscode.executeFormatDocumentProvider` - ドキュメントフォーマットプロバイダを実行します。

* _uri_ テキスト文書の Uri
* _options_書式設定オプション
* _(returns)_ TextEdits の配列に解決する promise です。


`vscode.executeFormatRangeProvider` - 実行範囲フォーマットプロバイダ。

* _uri_ テキスト文書の Uri
* _range_テキスト文書の範囲
* _options_書式設定オプション
* _(returns)_ TextEdits の配列に解決する promise です。


`vscode.executeFormatOnTypeProvider` - ドキュメントフォーマットプロバイダを実行します。

* _uri_ テキスト文書の Uri
* _position_ テキスト文書内の位置
* _ch_入力された文字
* _options_書式設定オプション
* _(returns)_ TextEdits の配列に解決する promise です。


`vscode.executeLinkProvider` - ドキュメントリンクプロバイダを実行します。

* _uri_ テキスト文書の Uri
* _(returns)_ DocumentLinkインスタンスの配列に解決する promise。


`vscode.previewHtml` - エディタビューでリソースのHTMLをレンダリングします。

* _uri_ Uriはプレビューするリソースです。
* _column_ (オプション）プレビューする列。
* _label_ (オプション）プレビューのタイトルとして使用される人間が読める文字列です。

HTMLプレビューとエディタの統合、および拡張機能の作成者のベストプラクティスの詳細については、[HTMLプレビューの操作](/docs/extensionAPI/vscode-api-commands.md＃working-with-the-htmlプレビュー）を参照してください。


`vscode.openFolder` - newWindow引数に応じて、現在のウィンドウまたは新しいウィンドウでフォルダを開きます。 newWindowパラメータがtrueに設定されていない限り、同じウィンドウで開くと現在の拡張ホストプロセスがシャットダウンされ、指定されたフォルダで新しいプロセスが開始されます。

* _uri_(オプション)開くフォルダのUri。提供されていない場合、ネイティブダイアログがユーザにフォルダを尋ねます
* _newWindow_(オプション)新しいウィンドウでフォルダを開くか、同じフォルダで開くか。既定では、同じウィンドウで開くように設定されています。


`vscode.startDebug` - デバッグセッションを開始します。

* _configuration_(オプション)使用する 'launch.json'のデバッグ構成の名前。または、使用するコンフィグレーションjsonオブジェクト。


`vscode.diff` - 提供されたリソースをdiffエディタで開き、内容を比較します。

* _left_ diffエディタの左側のリソース
* _right_ diffエディタの右側のリソース
* _title_ (オプション)diffエディタの人間が読めるタイトル


`vscode.open` - 提供されたリソースをエディタで開きます。テキストファイルまたはバイナリファイル、またはhttp(s)のURLにすることができます。

* _resource_ オープンするリソース
* _column_ (オプション)開く列


`cursorMove` - カーソルをビュー内の論理位置に移動する

* _カーソル移動引数object_

  この引数を渡すことができるプロパティ値ペア：

  * 'to'：カーソルをどこに移動するかを指定する必須の論理位置値。
    ```
    'left', 'right', 'up', 'down'
    'wrappedLineStart', 'wrappedLineEnd', 'wrappedLineColumnCenter'
    'wrappedLineFirstNonWhitespaceCharacter', 'wrappedLineLastNonWhitespaceCharacter'
    'viewPortTop', 'viewPortCenter', 'viewPortBottom', 'viewPortIfOutside'
    ```
  * 'by'：移動する単位。デフォルトは 'to'値に基づいて計算されます。
    ```
    'line', 'wrappedLine', 'character', 'halfLine'
    ```
  * 'value'：移動するユニットの数。デフォルトは '1'です。
  * 'select'： 'true'なら選択を行います。デフォルトは 'false'です。


`editorScroll` - 指定された方向にエディタをスクロールします。

* _Editorスクロール引数object_

  この引数を渡すことができるプロパティ値ペア：

  * 'to'：必須の方向値。
    ```
    'up', 'down'
    ```
  * 'by'：移動する単位。デフォルトは 'to'値に基づいて計算されます。
    ```
    'line', 'wrappedLine', 'page', 'halfPage'
    ```
  * 'value': 移動するユニットの数。デフォルトは '1' です。
  * 'revealCursor': 'true'の場合、カーソルがビューポートの外にある場合に表示されます。


`revealLine` - 指定された論理位置に与えられた行を表示する

* _リバースライン引数object_

  この引数を渡すことができるプロパティ値ペア:

  * 'lineNumber'：行番号の必須値。
  * 'at'：線が現れるべき論理位置。
    ```
    'top', 'center', 'bottom'
    ```


`editor.unfold` - エディタでコンテンツを展開する

* _Unfoldエディタ引数_

  この引数を渡すことができるプロパティ値ペア：

  * 'level': 展開するレベルの数


`editor.fold` - エディタでのコンテンツの折り畳み

* _Foldエディタ引数_

  この引数を渡すことができるプロパティ値ペア：

  * 'levels': 折りたたむレベルの数
  * 'up': 'true' の場合、与えられた数のレベルを折りたたむ


`editor.action.showReferences` - ファイル内のある位置に参照を表示する

* _uri_ 参照を表示するテキスト文書
* _position_ 表示する位置
* _locations_ 場所の配列。


`moveActiveEditor` - アクティブなエディタをタブまたはグループで移動します

* _アクティブなエディタ移動引数_

  引数のプロパティ:

  * 'to': どこに移動するかを指定する文字列値。
  * 'by': 移動の単位を提供する文字列値。タブ別またはグループ別。
  * 'value': 移動する位置または絶対位置の数を指定する数値です。

## HTMLプレビューを操作する

### スタイリング

`vscode-light`、`vscode-dark`、または `vscode-high`、 または `vscode-high` の現在のカラーテーマVSコードを伝えるために、表示されたHTMLのbody要素には、コントラスト。

### リンク

ドキュメントに含まれるリンクはVSコードで処理され、 `file` リソースと [virtual](https://github.com/Microsoft/vscode/blob/master/src/vs/vscode.d.ts#L3295) をサポートします。 リソースのほか、 `command` スキームを使ってコマンドをトリガーします。 JSONでエンコードされた引数を渡すには、 command-uri のクエリ部分を使用します。 URL エンコーディングを適用する必要があることに注意してください。

以下のスニペットは、 _previewHtml_ コマンドを呼び出して URI を渡すコマンドリンクを定義しています。

```javascript
  let href = encodeURI('command:vscode.previewHtml?' + JSON.stringify(someUri));
  let html = '<a href="' + href + '">Show Resource...</a>.';
```

### セキュリティのヒント

拡張プレゼンターとして、HTMLプレビューを使用する場合は、ユーザーを潜在的に悪質なコンテンツから保護する責任があります。主な危険性は、攻撃者がHTMLプレビューを使用してスクリプトを実行したり、その他の安全でない動作を実行する悪意のあるワークスペースを作成する可能性があることです。通常のWebセキュリティのベストプラクティスに加えて、ユーザーを保護するためのヒントとヒントをいくつか紹介します。

### サニタイズコンテンツ

最初の防衛線として、プレビュー用のHTML文書を作成するときは、ワークスペース設定やユーザーのシステム上のファイルからのすべての入力を適切にサニタイズするようにしてください。 HTMLコンテンツの場合は、安全なタグと属性のホワイトリストを使用することを検討してください。 [sanitize-html](https://www.npmjs.com/package/sanitize-html）のようなライブラリがこれを助けることができます。

### スクリプトを無効にする

プレビューでJavaScriptを実行する必要がない場合は、スクリプトの実行を完全に無効にすることで、セキュリティをさらに強化できます。これを達成する1つの方法は、信頼できないコンテンツを `iframe`の中に` sandbox`属性を設定して読み込むことです。この場合、コンテンツは `srcdoc`属性を使って読み込まれます：

```html
<iframe sandbox srcdoc="<!DOCTYPE html>..."></iframe>
```

プレビューで画像などのローカルリソースを読み込む必要がある場合は、代わりに `sandbox =" allow-same-origin "を使ってみてください：

```html
<iframe sandbox="allow-same-origin" srcdoc="<!DOCTYPE html>..."></iframe>
```

`sandbox = "allow-same-origin" は `iframe` 内でスクリプトの実行を無効にしますが、スタイルシートや画像などのユーザのシステムからリソースを読み込むことができます。一般に、プレビューが絶対に必要としない限り、ローカルリソースへのアクセスを無効にすることが最善です。

### コンテンツセキュリティポリシーの使用

プレビューの機能がスクリプトに依存する場合は、 [コンテンツセキュリティポリシー](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) を使用して、信頼できないユーザーコンテンツからのスクリプトを無効にすることを検討してください。コンテンツセキュリティポリシーにより、どのリソースがロードされるかを細かく制御できます。

たとえば、どこからでもイメージを作成し、ユーザーのローカルシステムからスタイルシートを作成し、すべてのスクリプトを無効にするコンテンツセキュリティポリシーを次に示します。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Security-Policy" content="default-src 'none'; img-src *; style-src 'self'; script-src 'none';">
  <title>...</title>
</head>
<body>
  Content
</body>
</html>
```

スクリプトを選択的に有効にするには、動的に生成された [nonce](https://developers.google.com/web/fundamentals/security/csp/) を使用して、特定の信頼できるスクリプトをホワイトリストに登録するのが最適です。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="Content-Security-Policy" content="default-src 'none'; img-src *; style-src 'self'; script-src 'nonce-123456';">
  <title>...</title>
</head>
<body>
  Content
  <script nonce="123456" src="file:///path/to/extension/my_trusted_script.js"></script>
</body>
</html>
```
