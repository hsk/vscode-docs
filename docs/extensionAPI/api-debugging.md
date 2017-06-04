---
Order: 8
Area: extensionapi
TOCTitle: Debugging API
ContentId: 9C4B10A2-44BE-4ABD-8FF4-F1A8683A90AD
PageTitle: Visual Studio Code Debugging API
DateApproved: 5/4/2017
MetaDescription: Visual Studio Code extensions (plug-ins) Debugging API.
---

# VS Code デバッグプロトコル

  Visual Studio Code は言語に依存しないデバッグUIを実装しているため、実際のデバッガと直接通信することはありません
  代わりに、 抽象的なワイヤプロトコルである *VS Code Debug Protocol* を介して、 いわゆる *デバッグアダプタ* と通信します。

  ![Debugger Architecture](images/api-debugging/debug-arch.png)

  VS Code のデバッグコンポーネントの拡張性は、 現在、 新しいデバッグアダプタの追加に限られています。
  したがって、 (まだ) VS Code のエディタコンポーネントのような方法でデバッガの UI を拡張することはできません。

## 1 デバッグアダプタ

  デバッグアダプタは、実際のデバッガと通信し、VS Code デバッグプロトコルとデバッガの具体的なプロトコルとの間で変換するスタンドアロンの実行可能ファイルです。
  デバッグアダプタは、最適な言語または特定のデバッガまたはランタイムで実装できるため、ワイヤプロトコルは、そのプロトコルを実装する特定のクライアントライブラリのAPIより重要です。

  [`vscode-debugadapter-node`](https://github.com/Microsoft/vscode-debugadapter-node) リポジトリには、[JSONスキーマ](https://github.com/Microsoft/vscode-debugadapter-node/blob/master/debugProtocol.json) または（生成された） [TypeScript定義](https://github.com/Microsoft/vscode-debugadapter-node/blob/master/protocol/src/debugProtocol.ts) ファイルとして表現された VS Code デバッグプロトコル仕様があります。
  どちらのファイルも、個々のプロトコル要求、応答、およびイベントの詳細な構造を示しています。
  このプロトコルは、 NPM モジュール [`vscode-debugprotocol`](https://www.npmjs.com/package/vscode-debugprotocol) としても使用できます。

  TypeScript と C# の VS Code デバッグプロトコル用のクライアントライブラリを実装しましたが、 JavaScript/TypeScript クライアントライブラリのみがすでに NPM モジュールとして利用可能です [`vscode-debugadapter-node`](https://github.com/Microsoft/vscode-debugadapter-node)。 C# クライアントライブラリは、 [Mono Debug](https://github.com/Microsoft/vscode-mono-debug/blob/master/src/DebugSession.cs) リポジトリにあります。

  デバッグアダプタを実装する方法の例として、 次のデバッガ拡張プロジェクトを使用できます:

  GitHubプロジェクト|説明|実装言語
  --- | --- | ---
  [Node Debug](https://github.com/Microsoft/vscode-node-debug.git) | 組み込みのv8ベースの Node.js デバッガ | TypeScript/JavaScript
  [Node Debug2](https://github.com/Microsoft/vscode-node-debug2.git) | 組み込みのCDPベースの Node.js デバッガ | TypeScript/JavaScript
  [Mono Debug](https://github.com/Microsoft/vscode-mono-debug.git) | Mono 用のシンプルな C# デバッガ | C#
  [Mock Debug](https://github.com/Microsoft/vscode-mock-debug.git) | 'フェイク' デバッガ | TypeScript/JavaScript


## 2 簡単な VS Code デバッグプロトコル

  このセクションでは、 VS Code とデバッグアダプタ間の相互作用の概要を説明します。
  これは、 VS Code デバッグプロトコルに基づくデバッグアダプタの実装に役立ちます。

  デバッグセッションが開始されると、VS Code は実行可能なデバッグアダプタを起動し、 *stdin* および *stdout*を使用してデバッグアダプタと通信します。
  VS Code は、 **initialize** 要求を送信して、 パスフォーマット(ネイティブまたはURI) に関する情報と、行と列の値が0または1のどちらであるかをアダプタに設定します。
  あなたのアダプタがTypeScriptまたはC#のデフォルト実装 `DebugSession` から派生している場合は、自分で初期化要求を処理する必要はありません。

  ユーザーが作成した起動設定 (launch configuration) で使用されている 'request' 属性に応じて、 VS Code は *launch* または *attach* リクエストを送信します。
  **launch** の場合、 デバッグアダプタはデバッグできるようにランタイムまたはプログラムを起動する必要があります。
  プログラムが stdin/stdout を介してユーザーと対話できるのであれば、デバッグアダプターが対話型端末またはコンソールでプログラムを起動することが重要です。
  **attach** の場合、デバッグアダプタは既に実行中のプログラムに接続または接続する必要があります。

  両方の要求の引数は特定のデバッグアダプタの実装に大きく依存するため、 VS Code デバッグプロトコルは引数を指定しません。
  代わりに、 VS Code はユーザーの起動設定 (launch configuration) からのすべての引数を *launch* または *attach* 要求に渡します。
  IntelliSense のスキーマとこれらの属性の追加情報は、 デバッグアダプター拡張の `package.json` で提供されます。
  これは、起動構成 (launch configurations) を作成または編集するときにユーザーを誘導します。

  VS Code はデバッグアダプタの代わりにブレークポイントを保持しているため、セッションが開始されるとデバッグアダプタにブレークポイントを登録する必要があります。
  VS Code は、このためにいつ良いか分からないので、デバッグアダプターは **initialize** イベントを VS Code に送り、ブレークポイント設定要求を受け入れる準備ができたことをアナウンスします。

  VS Code は、これらのブレークポイント設定要求を呼び出すことによって、すべてのブレークポイントを送信します:

  * **setBreakpoints** ブレークポイントを持つすべてのソースファイルに対して、
  * **setFunctionBreakpoints** デバッグアダプタがファンクションブレークポイントをサポートしている場合、
  * **setExceptionBreakpoints** デバッグアダプタが例外オプションをサポートしている場合、
  * **configurationDoneRequest** は、設定シーケンスの終了を示します。

  ブレークポイントを受け入れる準備ができたら、 *initialize* イベントを送信することを忘れないでください。
  さもなければ、永続化されたブレークポイントは復元されません。

  *setBreakpoint* リクエストは、ファイルに存在するすべてのブレークポイントを設定します(インクリメンタルではありません) 。
  デバッグアダプタでのこのセマンティクスの簡単な実装は、ファイルのすべてのブレークポイントをクリアしてから、そのリクエストで指定されたブレークポイントを設定することです。
  *setBreakpoints* と *setFunctionBreakpoints* は、 '実際の'ブレークポイントを返すと予想され、ブレークポイントを要求された位置に設定できず、デバッガのバックエンドによって移動された場合、 VS Code はUIを動的に更新します。

  プログラムが(ブレークポイントがヒットした、例外が発生した、またはユーザーが実行を一時停止するように要求したなどの理由で)停止するたびに 
  デバッグアダプタは、適切な理由とスレッドIDを持つ **stopped** イベントを送信する必要があります。
  受領すると、VS Code は最初に **thread** (下記参照) を要求し、次に **stoppedtrace** (スタックフレームのリスト) を停止イベントで記述されたスレッドに対して要求します。
  ユーザーがスタックフレームをドリルダウンすると、VS Code は最初に **scopes** にスタックフレームを要求し、次に **variables** をスコープに要求します。
  変数自体が構造化されている場合、 VS Code は追加の *variables* 要求によってそのプロパティを要求します。
  これにより、次の階層が生成されます:

  ```
  Threads
    Stackframes
        Scopes
          Variables
              ...
                Variables
  ```

  VS Code のデバッグUIはマルチスレッドをサポートしています (ただし、 Node.js デバッガだけを使用している場合は、これを認識していない可能性があります)。
  VS Code が **stopped** イベントまたは **thread** イベントを受信するたびに、 VS Code はその時点に存在するすべての **thread** を要求し、複数のスレッドが存在する場合はそれらを表示します。
  1つのスレッドのみが検出された場合、 VS Code UI はシングルスレッドモードのままです。
  **Thread** イベントはオプションですが、デバッグアダプタはそれらを送信して、停止していない状態であってもスレッドコードを動的に更新するようにVS Code を強制します。

  **launch** または **attach** が成功した後に、 VS Code は **thread** 要求で現在の既存のスレッドのベースラインを要求し、 **thread** イベントをリッスンして新しいスレッドまたは終了したスレッドを検出します。
  デバッグアダプタが複数のスレッドをサポートしていない場合でも、 **thread** 要求を実装し、単一の (ダミー) スレッドを返す必要があります。
  このスレッドのIDは、スレッドIDが必要なすべての **stacktrace**、**pause**、**continue**、**next**、**stepIn**、**stepOut** 要求で使用する必要があります。

  VS Code は **disconnect** 要求でデバッグセッションを終了します。
  デバッグターゲットが 'launched' (起動された)場合、 *disconnect* はターゲットプログラムを終了することが期待されます(必要に応じて強制的に終了します) 。
  デバッグターゲットが最初に'attache'(接続されている)場合、 *disconnect* はターゲットから切り離さなければなりません(これにより、デバッグターゲットは引き続き実行されます) 。
  どちらの場合も、ターゲットが正常に終了した場合やクラッシュした場合、デバッグアダプタは **terminated** イベントを発生させる必要があります。
  *disconnect* 要求からの応答を受け取った後、 VS Code はデバッグアダプタを終了します。

## 3 次のステップ

  VS Code 拡張モデルの詳細については、次のトピックを参照してください:

  * [デバッガの例](/docs/extensions/example-debuggers.md) - 実際の 'mock' デバッガの例を参照
  * [拡張APIの概要](/docs/extensionAPI/overview.md) - 完全な VS Code 拡張モデルについて学びます。
  * [拡張マニフェストファイル](/docs/extensionAPI/extension-manifest.md) - VS Code package.json 拡張マニフェストファイルリファレンス
  * [提供ポイント](/docs/extensionAPI/extension-points.md) - VS Code 提供ポイントの参照
