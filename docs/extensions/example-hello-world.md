---
Order: 3
Area: extensions
TOCTitle: Example-Hello World
ContentId: DC915D6C-13D4-4022-9101-57C4A4118B07
PageTitle: Your First Visual Studio Code Extension - Hello World
DateApproved: 5/4/2017
MetaDescription: Create your first Visual Studio extension (plug-in) with a simple Hello Word example.  This walkthrough will take you through the basics of VS Code extensibility.
---

# 例 - Hello World

## 1. 初めてのエクステンション

  このドキュメントでは、最初の VS Code 拡張 ("Hello World") を作成し、基本的な VS Code の拡張性の概念について説明します。

  このチュートリアルでは、簡単な "Hello World" メッセージを表示する VS Code に新しいコマンドを追加します。
  ウォークスルーの後半では、 VS Code エディタとやり取りして、現在選択されているユーザーのテキストをクエリします。

## 2. 前提条件

  `$PATH` には [Node.js](https:// nodejs.org/ja/) がインストールされていなければなりません。

## 3. 新しい拡張の生成

  VS Code に独自の機能を追加する最も簡単な方法は、 コマンドを追加することです。
  コマンドは、 **Command Palette** から呼び出すことができるコールバック関数を登録するか、 またはキーバインドで登録します。

  Yeoman ジェネレータを叩いて、 開始するのに役立てます。
  Yeoman と [Yeoman VS Code Extension generator](/docs/extensions/yocode.md) をインストールし、新しい拡張を scaffold してください:

  ```sh
  npm install -g yo generator-code
  yo code
  ```

  hello world 拡張の場合は、 **TypeScript** 拡張または **JavaScript** 拡張のいずれかを作成できます。
  この例では、 **TypeScript** 拡張を選択します。

  ![The command generator](images/example-hello-world/generator.png)

## 4. エクステンションを実行する

  * VS Code を起動し、 `File` > `Open Folder` を選択し、生成したフォルダを選択します。
  * `kb(workbench.action.debug.start)` を押すか、 `Debug` アイコンをクリックして `Start` をクリックしてください。
  * VS Code の新しいインスタンスは特殊モード(拡張開発ホスト) で起動し、 **この新しいインスタンスはあなたの拡張機能を認識しています**。
  * `kb(workbench.action.showCommands)` を押し、 `Hello World` というコマンドを実行します。
  * おめでとう！ 最初の VS Code コマンドを作成して実行しました！

  ![Running VS Code with an extension](images/example-hello-world/running.png)

## 5. エクステンションの構造

  実行後、 生成された拡張は次の構造を持つ必要があります。

  ```
  .
  ├── .gitignore
  ├── .vscode                     // VS Code インテグレーション
  │   ├── launch.json
  │   ├── settings.json
  │   └── tasks.json
  ├── .vscodeignore
  ├── README.md
  ├── src                         // ソース
  │   └── extension.ts            // JavaScript 拡張の場合は extension.js
  ├── test                        // テストフォルダ
  │   ├── extension.test.ts       // JavaScript 拡張の場合はextension.test.js
  │   └── index.ts                // JavaScript 拡張の場合は index.js
  ├── node_modules
  │   ├── vscode                  // 言語サービス
  │   └── typescript              // typescriptコンパイラ (TypeScript のみ)
  ├── out                         // コンパイル出力 (TypeScript のみ)
  │   ├── src
  │   |   ├── extension.js
  │   |   └── extension.js.map
  │   └── test
  │       ├── extension.test.js
  │       ├── extension.test.js.map
  │       ├── index.js
  │       └── index.js.map
  ├── package.json                // 拡張のマニフェスト
  ├── tsconfig.json               // JavaScript 拡張の場合は jsconfig.json
  └── vsc-extension-quickstart.md // 拡張開発クイックスタート
  ```

  これらすべてのファイルの目的を理解し、その内容を説明しましょう:

 ### 5.1 拡張マニフェスト：:

  * [`package.json` 拡張マニフェストのリファレンス](/docs/extensionAPI/extension-manifest.md) をお読みください
  * [`package.json` コントリビューションポイント](/docs/extensionAPI/extension-points.md) に関する詳細情報
  * 各VS Code 拡張には、その機能を記述する `package.json` ファイルが必要です。
  * VS Code は起動時にこのファイルを読み込み、すぐに各 `contributes` セクションに反応します。

 #### 5.1.1 TypeScript拡張マニフェストの例

  ```json
  {
      "name": "myFirstExtension",
      "description": "",
      "version": "0.0.1",
      "publisher": "",
      "engines": {
          "vscode": "^1.5.0"
      },
      "categories": [
          "Other"
      ],
      "activationEvents": [
          "onCommand:extension.sayHello"
      ],
      "main": "./out/src/extension",
      "contributes": {
          "commands": [{
              "command": "extension.sayHello",
              "title": "Hello World"
          }]
      },
      "scripts": {
          "vscode:prepublish": "tsc -p ./",
          "compile": "tsc -watch -p ./",
          "postinstall": "node ./node_modules/vscode/bin/install",
          "test": "node ./node_modules/vscode/bin/test"
      },
      "devDependencies": {
        "typescript": "^2.0.3",
          "vscode": "^1.5.0",
          "mocha": "^2.3.3",
          "@types/node": "^6.0.40",
          "@types/mocha": "^2.2.32"
    }
  }
  ```

  > **注意:** VS Code は、起動時に拡張機能のコードを熱心にロード**しません**。
  拡張機能は、どのような条件の下で [`activateEvents`](/docs/extensionAPI/activation-events.md) プロパティを使用してアクティブ化(ロード)するべきかを記述する必要があります。

 ### 5.2 生成されたコード

  生成された拡張モジュールのコードは  `extension.ts` (または JavaScript 拡張の場合は `extension.js`) にあります:

  ```javascript
  // The module 'vscode' contains the VS Code extensibility API
  // Import the module and reference it with the alias vscode in your code below
  import * as vscode from 'vscode';

  // this method is called when your extension is activated
  // your extension is activated the very first time the command is executed
  export function activate(context: vscode.ExtensionContext) {

      // Use the console to output diagnostic information (console.log) and errors (console.error)
      // This line of code will only be executed once when your extension is activated
      console.log('Congratulations, your extension "my-first-extension" is now active!');

      // The command has been defined in the package.json file
      // Now provide the implementation of the command with  registerCommand
      // The commandId parameter must match the command field in package.json
      var disposable = vscode.commands.registerCommand('extension.sayHello', () => {
          // The code you place here will be executed every time your command is executed

          // Display a message box to the user
          vscode.window.showInformationMessage('Hello World!');
      });

      context.subscriptions.push(disposable);
  }
  ```

  * それぞれの拡張モジュールは `activate()` という名前の関数をメインファイルからエクスポートする必要があり、
    どの VS Code でも、 `package.json` ファイルに記述されている `activationEvents` のどれかが出現したときに **一度だけ** 起動します。

  * 拡張機能がOSリソース(例えばプロセスを生成する)を利用する場合、拡張機能はメインファイルから `deactivate()`関数をエクスポートして、クリーンアップ作業を行い、 VS Code がシャットダウン時にその関数を呼び出すことができます。

  * この特定の拡張機能は、 `vscode` APIをインポートしてから、` `extension.sayHello" `コマンドが呼び出されるときに呼び出される関数を関連付けるコマンドを登録します。 コマンドの実装では、V Sコ Code に「Hello world」というメッセージが表示されます。

  > **注意：** `package.json` の `contributes` セクションは、コマンドパレットにエントリを追加します。 extension.ts/.jsのコードは `"extension.sayHello"` の実装を定義します。

  > **注：** TypeScript拡張の場合、生成されたファイル `out/src/extension.js` は実行時に読み込まれ、 VS Code で実行されます。

  > **Note:** The `contributes` section of the `package.json` adds an entry to the Command Palette.  The code in extension.ts/.js defines the implementation of `"extension.sayHello"`.

  > **Note:** For TypeScript extensions, the generated file `out/src/extension.js` will be loaded at runtime and executed by VS Code.

 ### 5.3 その他のファイル

  * `.vscode/launch.json`は、エクステンション開発モードで VS Code を起動することを定義します。 また、 `PreLaunchTask`はTypeScriptコンパイラを実行する` .vscode/tasks.json`で定義されたタスクを指しています。
  * `.vscode/settings.json`はデフォルトで` out`フォルダを除外します。 隠すファイルタイプを変更することができます。
  * `.gitignore` - どのパターンを無視するかをGitに指示します。
  * [`.vscodeignore`](/docs/extensions/publish-extension.md＃advanced-usage) - 拡張機能を公開する際に無視するファイルをパッケージツールに指示します。
  * `README.md` -  VS Code ユーザー用の拡張機能を説明するREADMEファイル。
  * `vsc-extension-quickstart.md` - クイックスタートガイドです。
  * `test/extension.test.ts` - あなたの拡張ユニットテストをここに入れ、 VS Code APIに対してテストを実行することができます([拡張機能のテスト](/docs/extensions/testing-extensions.mdを参照)

  * `.vscode/launch.json` defines launching VS Code in the Extension Development mode. It also points with `preLaunchTask` to a task defined in `.vscode/tasks.json` that runs the TypeScript compiler.
  * `.vscode/settings.json` by default excludes the `out` folder.  You can modify which file types you want to hide.
  * `.gitignore` - Tells Git version control which patterns to ignore.
  * [`.vscodeignore`](/docs/extensions/publish-extension.md#advanced-usage) - Tells the packaging tool which files to ignore when publishing the extension.
  * `README.md` - README file describing your extension for VS Code users.
  * `vsc-extension-quickstart.md` - A Quick Start guide for you.
  * `test/extension.test.ts` - you can put your extension unit tests in here and run your tests against the VS Code API (see [Testing Your Extension](/docs/extensions/testing-extensions.md))

## 6 拡張アクティベーション

  拡張機能に含まれるファイルの役割が明確になったので、 拡張機能をどのようにアクティブにするかを以下に示します。

  Now that the roles of the files included in the extension are clarified, here is how your extension gets activated:

  * 拡張開発インスタンスは、拡張を検出し、その `package.json`ファイルを読み込みます。
  * 後で `kb(workbench.action.showCommands）`を押すと：
   * 登録されたコマンドは、コマンドパレットに表示されます。
   * このリストには、 `"Hello world"` というエントリがあり、これは `package.json` で定義されています。
  * `"Hello world"` コマンドを選択するとき：
   * コマンド "extension.sayHello" が呼び出されます：
     * 起動イベント `"onCommand：extension.sayHello"` が生成されます。
     * このactivationイベントを `activateEvents`にリストしたすべての拡張機能が有効になります。
       * `。/out/src/extension.js`のファイルがJavaScript VMにロードされます。
       *  VS Code は、エクスポートされた関数 `activate`を探して呼び出します。
       * コマンド "extension.sayHello"が登録され、その実装が定義されました。
   * コマンド "extension.sayHello"の実装関数が呼び出されます。
   * コマンドの実装では、「Hello World」というメッセージが表示されます。


  * The extension development instance discovers the extension and reads its `package.json` file.
  * Later when you press `kb(workbench.action.showCommands)`:
  * The registered commands are displayed in the Command Palette.
  * In this list there is now an entry `"Hello world"` that is defined in the `package.json`.
  * When selecting the `"Hello world"` command:
  * The command `"extension.sayHello"` is invoked:
    * An activation event `"onCommand:extension.sayHello"` is created.
    * All extensions listing this activation event in their `activationEvents` are activated.
      * The file at `./out/src/extension.js` gets loaded in the JavaScript VM.
      * VS Code looks for an exported function `activate` and calls it.
      * The command `"extension.sayHello"` is registered and its implementation is now defined.
  * The command `"extension.sayHello"` implementation function is invoked.
  * The command implementation displays the "Hello World" message.

## 7 拡張機能のデバッグ

  Set a breakpoint, for example inside the registered command, and run the `"Hello world"` command in the Extension Development VS Code instance.

  ![Debugging the extension](images/example-hello-world/hitbp.png)

  > **Note:** For TypeScript extensions, even though VS Code loads and executes `out/src/extension.js`, you are actually able to debug the original TypeScript code due to the generated source map `out/src/extension.js.map` and VS Code's debugger support for source maps.

  > **Tip:** The Debug Console will show all the messages you log to the console.

  To learn more about the extension [development environment](/docs/extensions/debugging-extensions.md).


  たとえば、登録されたコマンドの中にブレークポイントを設定し、Extension Development VS Codeインスタンスで `` Hello world "`コマンドを実行します。

  ！[拡張機能のデバッグ](images/example-hello-world/hitbp.png）

  > **注意：** TypeScript拡張の場合、 VS Code が `out/src/extension.js`をロードして実行しても、実際に生成されたソースマップ` out/src/extensionによって元のTypeScriptコードをデバッグすることができます .js.map`とソースコードのVS Codeのデバッガサポートが含まれています。

  > **ヒント：**デバッグコンソールには、コンソールにログするすべてのメッセージが表示されます。

  拡張機能[開発環境](/docs/extensions/debugging-extensions.md）の詳細については、こちらをご覧ください。

## 8 単純な変更

  `extension.ts`(またはJavaScript拡張モジュールの`extension.js`）では、エディタで選択された文字数を表示するために `extension.sayHello`コマンド実装を置き換えてみてください：

  ```javascript
  var editor = vscode.window.activeTextEditor;
  if (!editor) {
      return; // No open text editor
  }

  var selection = editor.selection;
  var text = editor.document.getText(selection);

  // Display a message box to the user
  vscode.window.showInformationMessage('Selected characters: ' + text.length);
  ```

  > **ヒント：** 拡張ソースコードを変更したら、VSコードの拡張開発インスタンスを再起動する必要があります。
  2番目のインスタンスで `kbstyle(Ctrl + R）`(Mac： `kbstyle(Cmd + R）`）を使用するか、プライマリ VS Code インスタンスの一番上にあるRestartボタンをクリックしてください。

  ![Running the modified extension](images/example-hello-world/selection-length.png)

## 9 ローカルに作成した拡張をインストールする

  これまでに書いた拡張機能は、Extension DevelopmentのインスタンスであるVSコードの特別なインスタンスでのみ実行されます。 エクステンションをVSコードのすべてのインスタンスで実行するには、ローカルエクステンションフォルダの下の新しいフォルダにコピーする必要があります。

  * Windows： `％USERPROFILE％\。vscode \ extensions`
  * Mac/Linux： `$ HOME/.vscode/extensions`

## 10 エクステンションを公開する

  [拡張機能を共有する](/docs/extensions/publish-extension.md) 方法をお読みください。


## 11 次のステップ

  このチュートリアルでは、非常に単純な拡張を見てきました。より詳細な例については、特定の言語(Markdown）をターゲットにしてエディタのドキュメント変更イベントを聞く方法を示す[ワード数の例](/docs/extensions/example-word-count.md）を参照してください。

  より一般的な拡張APIについては、次のトピックを参照してください。

  * [Extension API Overview](/docs/extensionAPI/overview.md) - 完全なVSコード拡張性モデルについて学びます。
  * [APIの原則とパターン](/docs/extensionAPI/patterns-and-principles.md) - VSコードの拡張性は、いくつかの基本原則とパターンに基づいています。
  * [Contribution Points](/docs/extensionAPI/extension-points.md) - さまざまなVSコードの寄付ポイントの詳細。
  * [アクティベーションイベント](/docs/extensionAPI/activation-events.md) - VSコードアクティベーションイベントリファレンス
  * [その他の拡張の例](/docs/extensions/samples.md) - サンプルの拡張プロジェクトの一覧を見てください。
