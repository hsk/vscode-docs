---
Order: 5
Area: extensions
TOCTitle: Example-Language Server
ContentId: A8CBE8D6-1FEE-47BF-B81E-D79FA0DB5D03
PageTitle: Creating Language Servers for Visual Studio Code
DateApproved: 5/4/2017
MetaDescription: Learn how to create Language Servers for Visual Studio Code.  These can be used to easily integrate existing Linters into VS Code.
---

# 例 - 言語サーバー

  言語サーバーを使用すると、VSコードで開いているファイルに独自の検証ロジックを追加できます。通常、プログラミング言語を検証するだけです。しかし、他のファイルタイプを検証することも有効です。例えば、言語サーバは、不適切な言語のファイルをチェックすることができる。

  一般に、プログラミング言語の検証は高価になる可能性があります。特に検証では複数のファイルを解析し、抽象構文木を構築する必要があります。パフォーマンスコストを避けるために、VSコードの言語サーバーは別のプロセスで実行されます。このアーキテクチャは、言語サーバが TypeScript/JavaScript 以外の言語で書かれ、コード補完や `Find All References` のような高価な追加言語機能をサポートすることも可能にします。

  残りの文書は、VSコードの通常の [拡張開発](/docs/extensions/overview.md) に精通していることを前提としています。

## 1 独自の言語サーバーを実装する

  言語サーバーはどの言語でも実装でき、 [言語サーバープロトコル](https://github.com/Microsoft/language-server-protocol) に従います。しかし、現在 VS Code は Node.js 用のライブラリしか提供していません。将来、追加のライブラリが続くでしょう。 Node.js の言語サーバ実装の出発点は、サンプルリポジトリ [言語サーバノードの例](https://github.com/Microsoft/vscode-languageserver-node-example.git) です。

  リポジトリをクローンし、次に実行します。

  ```bash
  > cd client
  > npm install
  > code .
  > cd ../server
  > npm install
  > code .
  ```
  上記はすべての依存関係をインストールし、2つの VS Code インスタンスを開きます: 1つはサーバーコード用、もう1つはクライアントコード用です。

## 2 'クライアント' の説明

  クライアントは実際には通常のVSコード拡張です。 これには、workspaceフォルダのルートに `package.json`ファイルが含まれています。 そのファイルには3つの興味深いセクションがあります。

  最初に `activationEvents` を見てください:

  ```json
  "activationEvents": [
      "onLanguage:plaintext"
  ]
  ```

  このセクションでは、プレーンテキストファイルを開くとすぐに拡張子をアクティブにするよう VS Code に指示します（拡張子が `.txt` のファイルなど）。

  次の `configuration` セクションを見てください：

  ```json
  "configuration": {
      "type": "object",
      "title": "Example configuration",
      "properties": {
          "languageServerExample.maxNumberOfProblems": {
              "type": "number",
              "default": 100,
              "description": "Controls the maximum number of problems produced by the server."
          }
      }
  }
  ```

  このセクションはVSコードへの `configuration` 設定に寄与します。 この例では、これらの設定が起動時および設定の変更時に言語サーバーに送信される方法について説明します。

  最後の部分は `vscode-languageclient` ライブラリに依存関係を追加します:

  ```json
  "dependencies": {
      "vscode-languageclient": "^2.6.3"
  }
  ```

  前述のように、クライアントは通常のVSコード拡張として実装されています。

  以下は対応する extension.ts ファイルの内容です:

  ```typescript
  /* --------------------------------------------------------------------------------------------
   * Copyright (c) Microsoft Corporation. All rights reserved.
   * Licensed under the MIT License. See License.txt in the project root for license information.
   * ------------------------------------------------------------------------------------------ */
  'use strict';

  import * as path from 'path';

  import { workspace, Disposable, ExtensionContext } from 'vscode';
  import { LanguageClient, LanguageClientOptions, SettingMonitor, ServerOptions, TransportKind } from 'vscode-languageclient';

  export function activate(context: ExtensionContext) {

	  // The server is implemented in node
	  let serverModule = context.asAbsolutePath(path.join('server', 'server.js'));
	  // The debug options for the server
	  let debugOptions = { execArgv: ["--nolazy", "--debug=6004"] };
	
	  // If the extension is launched in debug mode then the debug server options are used
	  // Otherwise the run options are used
	  let serverOptions: ServerOptions = {
		  run : { module: serverModule, transport: TransportKind.ipc },
		  debug: { module: serverModule, transport: TransportKind.ipc, options: debugOptions }
	  }
	
	  // Options to control the language client
	  let clientOptions: LanguageClientOptions = {
		  // Register the server for plain text documents
		  documentSelector: ['plaintext'],
		  synchronize: {
			  // Synchronize the setting section 'languageServerExample' to the server
			  configurationSection: 'languageServerExample',
			  // Notify the server about file changes to '.clientrc files contain in the workspace
			  fileEvents: workspace.createFileSystemWatcher('**/.clientrc')
		  }
	  }
	
	  // Create the language client and start the client.
	  let disposable = new LanguageClient('languageServerExample', 'Language Server Example', serverOptions, clientOptions).start();
	
	  // Push the disposable to the context's subscriptions so that the 
	  // client can be deactivated on extension deactivation
	  context.subscriptions.push(disposable);
  }
  ```

## 3 'Server' を説明します

  > **注:** GitHub リポジトリからクローン化された 'Server' 実装は、最後のウォークスルー実装を備えています。 ウォークスルーに従うために、新しい `server.ts` を作成するか、複製されたバージョンの内容を変更することができます。

  この例では、サーバーは TypeScript で実装され、 Node.js を使用して実行されます。 VS Code には Node.js ランタイムが付属しているため、ランタイムに固有の要件がない限り、独自に提供する必要はありません。

  サーバの `package.json` ファイルの興味深いセクションは次のとおりです：

  ```json
  "dependencies": {
      "vscode-languageserver": "^2.6.2"
  }
  ```

  これにより、 vscode-languageserver ライブラリが取得されます。

  以下は、提供されているシンプルテキストドキュメントマネージャを使用してサーバーの実装です。このドキュメントマネージャは、VSコードからサーバーにファイルのフルコンテンツを常に送信することによってテキストドキュメントを同期します。

  ```typescript
  /* --------------------------------------------------------------------------------------------
   * Copyright (c) Microsoft Corporation. All rights reserved.
   * Licensed under the MIT License. See License.txt in the project root for license information.
   * ------------------------------------------------------------------------------------------ */
  'use strict';

  import {
      IPCMessageReader, IPCMessageWriter,
	  createConnection, IConnection,
	  TextDocuments, TextDocument, Diagnostic, DiagnosticSeverity, 
	  InitializeParams, InitializeResult
  } from 'vscode-languageserver';

  // Create a connection for the server. The connection uses Node's IPC as a transport
  let connection: IConnection = createConnection(new IPCMessageReader(process), new IPCMessageWriter(process));

  // Create a simple text document manager. The text document manager
  // supports full document sync only
  let documents: TextDocuments = new TextDocuments();
  // Make the text document manager listen on the connection
  // for open, change and close text document events
  documents.listen(connection);

  // After the server has started the client sends an initialize request. The server receives
  // in the passed params the rootPath of the workspace plus the client capabilities. 
  let workspaceRoot: string;
  connection.onInitialize((params): InitializeResult => {
	  workspaceRoot = params.rootPath;
	  return {
		  capabilities: {
			  // Tell the client that the server works in FULL text document sync mode
			  textDocumentSync: documents.syncKind
			  }
		  }
  });

  // Listen on the connection
  connection.listen();
  ```

## 4 単純なバリデーションを追加する

  ドキュメントの検証をサーバーに追加するために、テキストドキュメントの内容が変更されたときに呼び出されるリスナをテキストドキュメントマネージャに追加します。 次に、サーバーが最適な時刻に文書を検証する時期を決定するのは、サーバーの責任です。 この実装例では、サーバはプレーンテキスト文書を検証し、 `typescript` のすべての出現にフラグを立てるメッセージを `TypeScript` にフラグを立てます。 対応するコードスニペットは次のようになります。

  ```typescript
  // The content of a text document has changed. This event is emitted
  // when the text document first opened or when its content has changed.
  documents.onDidChangeContent((change) => {
      let diagnostics: Diagnostic[] = [];
      let lines = change.document.getText().split(/\r?\n/g);
      lines.forEach((line, i) => {
          let index = line.indexOf('typescript');
          if (index >= 0) {
              diagnostics.push({
                  severity: DiagnosticSeverity.Warning,
                  range: {
                      start: { line: i, character: index},
                      end: { line: i, character: index + 10 }
                  },
                  message: `${line.substr(index, 10)} should be spelled TypeScript`,
                  source: 'ex'
              });
          }
      })
      // Send the computed diagnostics to VS Code.
      connection.sendDiagnostics({ uri: change.document.uri, diagnostics });
  });
  ```

### 4.1 診断のヒントとテクニック！

  * 開始位置と終了位置が同じ場合、 VS Code はその位置で単語を揺らします。
  * 行末まで揺らぎたい場合は、終了位置の文字を Number.MAX_VALUE に設定します。


  言語サーバーをテストするには、次の手順を実行します。

  * サーバコード（上記参照）を含むVSコードインスタンスに移動し、 `kb(workbench.action.tasks.build)` を押してビルドタスクを開始します。 タスクは、サーバコードをコンパイルし、それを拡張フォルダにインストールする（例えば、コピーする）。
  * 拡張子 (client) を持つVSコードインスタンスに戻り、拡張コードを実行するVSコードの追加拡張開発ホストインスタンスを起動するために `kb(workbench.action.debug.start)` を押します。
  * ルートフォルダに test.txt ファイルを作成し、次の内容を貼り付けます。


  ```txt
  typescript lets you write JavaScript the way you really want to.
  typescript is a typed superset of JavaScript that compiles to plain JavaScript.
  Any browser. Any host. Any OS. Open Source.
  ```

  `Extension Development Host` インスタンスは次のようになります:

  ![Validating a text file](images/example-language-server/validation.png)

## 5 クライアントとサーバーの両方のデバッグ

  クライアントコードのデバッグは、通常の拡張機能をデバッグするのと同じくらい簡単です。クライアントコードを含む VS Code インスタンスにブレークポイントを設定し、 `kb(workbench.action.debug.start)` を押して拡張機能をデバッグします。拡張機能の起動とデバッグの詳細については、 [拡張機能の実行とデバッグ](/docs/extensions/debugging-extensions.md) を参照してください。

  ![Debugging the client](images/example-language-server/debugging-client.png)

  サーバは拡張機能(クライアント)で動作する `LanguageClient` によって起動されるので、実行中のサーバにデバッガを接続する必要があります。これを行うには、サーバコードを含む VS Code インスタンスに切り替え、 `kb(workbench.action.debug.start)` を押します。 これにより、デバッガがサーバに接続されます。実行中のサーバーと対話するには、通常のデバッグビューを使用します。

  ![Debugging the server](images/example-language-server/debugging-server.png)

## 6 サーバの設定を使う

  拡張機能のクライアント部分を記述する際には、すでに報告されている問題の最大数を制御する設定を定義しています。 `LanguageClient` が `LanguageClientOptions` の同期設定を使ってこれらの設定をサーバに同期するように指示しました：

  ```typescript
  synchronize: {
      // Synchronize the setting section 'languageClientExample' to the server
      configurationSection: 'languageServerExample',
      // Notify the server about file changes to '.clientrc files contain in the workspace
      fileEvents: workspace.createFileSystemWatcher('**/.clientrc')
  }
  ```

  私たちが今必要とするのは、サーバー側で構成の変更を聞くことだけです。設定が変更された場合、開いているテキスト文書を再検証してください。 ドキュメント変更イベント処理の検証ロジックを再利用できるようにするために、コードを `validateTextDocument` 関数に抽出し、 `maxNumberOfProblems` 変数を尊重するようにコードを修正します：

  ```typescript
  function validateTextDocument(textDocument: TextDocument): void {
      let diagnostics: Diagnostic[] = [];
      let lines = textDocument.getText().split(/\r?\n/g);
      let problems = 0;
      for (var i = 0; i < lines.length && problems < maxNumberOfProblems; i++) {
          let line = lines[i];
          let index = line.indexOf('typescript');
          if (index >= 0) {
              problems++;
              diagnostics.push({
                  severity: DiagnosticSeverity.Warning,
                  range: {
                      start: { line: i, character: index},
                      end: { line: i, character: index + 10 }
                  },
                  message: `${line.substr(index, 10)} should be spelled TypeScript`,
                  source: 'ex'
              });
          }
      }
      // Send the computed diagnostics to VS Code.
      connection.sendDiagnostics({ uri: textDocument.uri, diagnostics });
  }
  ```

  構成変更の処理は、構成変更の通知ハンドラーを接続に追加することによって行われます。 対応するコードは次のようになります。

  ```typescript
  // The settings interface describe the server relevant settings part
  interface Settings {
      languageServerExample: ExampleSettings;
  }

  // These are the example settings we defined in the client's package.json
  // file
  interface ExampleSettings {
      maxNumberOfProblems: number;
  }

  // hold the maxNumberOfProblems setting
  let maxNumberOfProblems: number;
  // The settings have changed. Is send on server activation
  // as well.
  connection.onDidChangeConfiguration((change) => {
      let settings = <Settings>change.settings;
      maxNumberOfProblems = settings.languageServerExample.maxNumberOfProblems || 100;
      // Revalidate any open text documents
      documents.all().forEach(validateTextDocument);
  });
  ```

  クライアントを再起動し、設定を最大レポート1に変更すると、次の検証が行われます。

  ![Maximum One Problem](images/example-language-server/validationOneProblem.png)

## 7 その他の言語機能を追加する

  言語サーバーが通常実装する最初の興味深い機能は、ドキュメントの検証です。 その意味では、リンターは言語サーバーとしてカウントされ、 VS Code では通常、言語サーバーとして実装されます ([eslint](https://github.com/Microsoft/vscode-eslint) および [jshint](https://github.com/Microsoft/vscode-jshint) を参照してください)。 しかし、言語サーバーには多くのものがあります。 コードの完成、すべての参照の検索、または定義への移動が可能です。 以下のサンプルコードは、コード補完をサーバーに追加します。 'TypeScript' と 'JavaScript' という2つの単語を提案します。

  ```typescript
  // This handler provides the initial list of the completion items.
  connection.onCompletion((textDocumentPosition: TextDocumentPositionParams): CompletionItem[] => {
      // The pass parameter contains the position of the text document in 
      // which code complete got requested. For the example we ignore this
      // info and always provide the same completion items.
      return [
          {
              label: 'TypeScript',
              kind: CompletionItemKind.Text,
              data: 1
          },
          {
              label: 'JavaScript',
              kind: CompletionItemKind.Text,
              data: 2
          }
      ]
  });

  // This handler resolve additional information for the item selected in
  // the completion list.
  connection.onCompletionResolve((item: CompletionItem): CompletionItem => {
      if (item.data === 1) {
          item.detail = 'TypeScript details',
          item.documentation = 'TypeScript documentation'
      } else if (item.data === 2) {
          item.detail = 'JavaScript details',
          item.documentation = 'JavaScript documentation'
      }
      return item;
  });
  ```

  `data` フィールドは、解決ハンドラ内の完了項目を一意的に識別するために使用される。 data プロパティは、プロトコルに対して透過的です。 基本的なメッセージパッシングプロトコルは JSON ベースであるため、データフィールドは JSON との間でシリアル化可能なデータだけを保持する必要があります。

  行方不明のものは、サーバーがコード補完要求をサポートしていることをVSコードに伝えることです。 これを行うには、 initialize ハンドラの対応する機能にフラグを立てます。

  ```typescript
  connection.onInitialize((params): InitializeResult => {
      ...
      return {
          capabilities: {
              ...
              // Tell the client that the server support code complete
              completionProvider: {
                  resolveProvider: true
              }
          }
      }
  });
  ```

  以下のスクリーンショットは、プレーンテキストファイルで実行されている完成したコードを示しています。

  ![Code Complete](images/example-language-server/codeComplete.png)

## 8 その他の言語サーバーの機能

  現在、言語補完機能とともに、言語サーバーでサポートされている言語機能は次のとおりです:

  * _ドキュメントハイライト_: テキストドキュメント内のすべての「等しい」シンボルを強調表示します。
  * _Hover_: テキストドキュメントで選択されたシンボルのホバー情報を提供します。
  * _Signature Help_: テキスト文書で選択された記号の署名ヘルプを提供します。
  * _Goto Definition_: テキスト文書で選択されたシンボルの定義をサポートします。
  * _Find References_: テキスト文書で選択されたシンボルのプロジェクト全体の参照をすべて検索します。
  * _ListドキュメントSymbols_: テキストドキュメントに定義されているすべてのシンボルをリストします。
  * _ListワークスペースSymbols_: プロジェクト全体のシンボルをすべて一覧表示します。
  * _Code Actions_: 指定されたテキスト文書と範囲のコマンドを計算します。
  * _CodeLens_: 指定されたテキストドキュメントの CodeLens 統計を計算します。
  * _Document Formatting_: これは、ドキュメント全体の書式設定、ドキュメント範囲、および書式設定を含みます。
  * _Rename_: プロジェクト全体のシンボルの名前変更。
  * _Document Links_: ドキュメント内のリンクを計算して解決します。


  [言語拡張ガイドライン](/docs/extensionAPI/language-support.md) トピックでは、上記の各言語機能について説明し、言語サーバープロトコルまたは拡張機能から直接拡張 API を使用して実装する方法のガイダンスを提供しています。

## 9 インクリメンタルテキスト文書の同期

  この例では、 `vscode-languageserver` モジュールによって提供される単純なテキストドキュメントマネージャを使用して、 VS Code と言語サーバ間でドキュメントを同期します。

  これには2つの欠点があります。

  * テキスト文書の全内容がサーバーに繰り返し送信されるため、多くのデータ転送が可能です。
  * 既存の言語ライブラリが使用されている場合、そのようなライブラリは通常、不必要な解析と抽象構文ツリーの作成を避けるために増分ドキュメントの更新をサポートします。


  したがって、プロトコルは増分文書同期もサポートしています。

  インクリメンタルなドキュメント同期を利用するには、サーバーで3つの通知ハンドラをインストールする必要があります。

  * _onDidOpenTextDocument_: テキスト文書をVSコードで開くと呼び出されます。
  * _onDidChangeTextDocument_: テキスト文書の内容がVSコードで変更されたときに呼び出されます。
  * _onDidCloseTextDocument_: テキスト文書がVSコードで閉じられたときに呼び出されます。


  接続上でこれらの通知ハンドラをフックする方法と、初期化時に正しい機能を返す方法を示すコードスニペットの下に:

  ```typescript
  connection.onInitialize((params): InitializeResult => {
      ...
      return {
          capabilities: {
              // Enable incremental document sync
              textDocumentSync: TextDocumentSyncKind.Incremental,
              ...
          }
      }
  });

  connection.onDidOpenTextDocument((params) => {
      // A text document got opened in VS Code.
      // params.uri uniquely identifies the document. For documents store on disk this is a file URI.
      // params.text the initial full content of the document.
  });

  connection.onDidChangeTextDocument((params) => {
      // The content of a text document did change in VS Code.
      // params.uri uniquely identifies the document.
      // params.contentChanges describe the content changes to the document.
  });

  connection.onDidCloseTextDocument((params) => {
      // A text document got closed in VS Code.
      // params.uri uniquely identifies the document.
  });
  ```

## 10 次のステップ

  VS Code の拡張性モデルの詳細については、次のトピックを参照してください:

  * [vscode APIリファレンス](/docs/extensionAPI/vscode-api.md) - VSコード言語サービスとの深い言語統合について学びます。
  * [言語拡張ガイドライン](/docs/extensionAPI/language-support.md) - VSコードの豊富な言語機能を実装するためのガイドです。
  * [その他の拡張の例](/docs/extensions/samples.md) - 拡張プロジェクトの例をご覧ください。

## 11 よくある質問

  **Q: サーバーに接続しようとすると、 "実行時プロセスに接続できません (5000ms後にタイムアウト)"？**

  **A:** デバッガを接続しようとしたときにサーバが動作していない場合、このタイムアウトエラーが表示されます。 クライアントは言語サーバーを起動するので、実行中のサーバーを持つためにクライアントを起動していることを確認してください。 また、サーバーの起動を妨げるクライアントブレークポイントを無効にする必要があります。


