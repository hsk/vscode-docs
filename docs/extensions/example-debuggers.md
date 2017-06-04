---
Order: 6
Area: extensions
TOCTitle: Example-Debuggers
ContentId: 49EF49AD-8BE6-4D46-ADC8-D678BDC04E85
PageTitle: Integrating Debuggers into Visual Studio Code
DateApproved: 5/4/2017
MetaDescription: Learn how to provide debug service extensions (plug-ins) for Visual Studio Code
---

# 例 - デバッガ

Visual Studio Code は一般的な （言語に依存しない） デバッグUIを実装しているため、 実際のデバッガと直接対話することはできませんが、代わりにデバッガまたはランタイム固有の機能を実装するためのデバッグ拡張機能に依存します。

これらのデバッグ拡張は、その実装が拡張ホストではなく、独立したスタンドアロンのプログラムとして、いわゆるデバッグアダプタとして実行されている点で、他の拡張とは異なります。
これらのプログラムは、 VS Code で使用される VS Code デバッグプロトコルに具体的なデバッガまたはランタイムのAPIまたはプロトコルを「適応」するため、これらのプログラムアダプタと呼ばれます。

![Debugger Architecture](images/example-debuggers/debug-arch.png)

デバッグ・アダプターをスタンドアロン・エキスパートとして実装する理由は2つあります。
第1に、アダプターを特定のデバッガーまたはランタイムに最も適した言語でインプリメントすることが可能になります。
第2に、スタンドアロンのプログラムは、基礎となるデバッガやランタイムで必要とされる場合に、より簡単に昇格モードで実行できます。

ローカルファイアウォールの問題を回避するために、VS Code は、より洗練されたメカニズム（ソケットなど）ではなく、 stdin/stdout を使用してアダプタと通信します。

すべてのデバッグ拡張機能は、 VS Code 起動設定から参照されるデバッグ `type` を定義します。
デバッグセッションが開始されると、 VS Code はデバッグタイプに基づいてデバッグエクステンションを検索し、エクステンションのデバッグアダプタ実行可能ファイルを別のプロセスとして起動します。
デバッグセッションが終了すると、アダプタは停止します。

Visual Studio Code には Node.js 用の2つのデバッグ拡張機能が付属しています。
`node-debug` はノードバージョン<6.3の（推奨されない）v8デバッガプロトコルを使用し、 `node-debug2` はノードバージョン> = 6.3でサポートされる Chrome デバッガプロトコル （CDP） を使用します。
[VS Code Marketplace](https://marketplace.visualstudio.com/vscode/Debuggers) からさらに多くのデバッガエクステンションを利用できます。
また、自分でデバッガエクステンションを作成することもできます。

このドキュメントの残りの部分では、デバッガ拡張を開発する方法を示します。

## 1. モックデバッグエクステンション

最初からデバッグアダプタを作成することはこのチュートリアルでは少し重いので、私たちは教育デバッグアダプタ 'スタータキット' として作成した簡単なデバッグアダプタから始めます。
それは実際のデバッガとは話しませんが、 モックデバッグと呼ばれるので、 Mock Debug と呼ばれています。
したがって、 Mock デバッグはデバッガをシミュレートし、 ステップ、 継続、 ブレークポイント、 例外、 および可変アクセスをサポートしますが、 実際のデバッガには接続されません。

モックデバッグの開発設定を掘り下げる前に、 まず VS Code マーケットプレイスから [事前構築されたバージョン](https://marketplace.visualstudio.com/items/andreweinand.mock-debug) をインストールして試してみましょう。

* 拡張機能のビューレットに切り替え、 'Mock' と入力して Mock デバッグ拡張機能を検索し、
* 拡張機能は「インストール」と「再ロード」します。

モックデバッグを試すには:

* 新しい空のフォルダ `mock test` を作成し、 VS Code で開きます。
* `readme.md` ファイルを作成し、複数行の任意のテキストを入力します。
* デバッグビューに切り替えて歯車アイコンを押します。
* VS Code を使用すると、デフォルトの起動設定を作成するために「環境」を選択できます。 「モックデバッグ」を選択します。
* 緑色の「スタート」ボタンを押し、次に「Enter」を押して、提案されたファイル 'readme.md' を確定します。

デバッグセッションが開始され、 readme ファイルの 「ステップ実行」、 ブレークポイントの設定とヒット、 例外への実行 （`exception` が行に出現する場合） が実行されます。

![Mock Debugger running](images/example-debuggers/mock-debug.gif)

あなた自身の開発の出発点として Mock Debug を使用する前に、 まずビルド前のバージョンをアンインストールすることをお勧めします:

* Extensionsビューレットに切り替え、 Mock Debug 拡張機能の歯車アイコンをクリックして、
* 'アンインストール' アクションを実行し、 ウィンドウを再読み込みします。

## 2. モックデバッグの開発セットアップ

さあ、 Mock Debug のソースを手に入れ、 VS Code 内で開発を始めましょう。

```
git clone https://github.com/Microsoft/vscode-mock-debug.git
cd vscode-mock-debug
npm install
```

VS Code でプロジェクトフォルダ `vscode-mock-debug` を開きます。

パッケージには何が入っていますか？

* `package.json` は mock-debug 拡張のマニフェストです:
    - mock-debug 拡張の提供を列挙し、
    - `compile` スクリプトと `watch` スクリプトを使用して、 TypeScript ソースを `out` フォルダーに移動し、その後のソース変更を監視し、
    - `vscode-debugprotocol`、 `vscode-debugadapter`、 および`vscode-debugadapter-testsupport` の依存関係は、ノードベースのデバッグアダプターの開発を簡素化する NPM モジュールです。
* 拡張モジュールのデバッグアダプタの実装は `src/mockDebug.ts` にあります。 ここでは、 VS Code デバッグプロトコルのさまざまな要求に対するハンドラを見つけることができます。
* デバッグ拡張モジュールの実装はデバッグアダプタ内に存在するので、拡張コードを全く必要としない（すなわち、拡張ホストプロセスで実行されるコード）。 しかし、 Mock デバッグは、 デバッグ拡張の拡張コードで何ができるかを示しているので、小さな `src/extension.ts` を持っています。

`Extension` の起動設定を選択し、 `F5` を押して、 Mock Debug 拡張機能をビルドして起動します。
最初は、 TypeScript ソースを `out` フォルダーに完全に展開します。
フルビルドの後、 あなたが行ったすべての変更を反映する 「ウォッチャータスク」 が開始されます。

ソースを翻訳した後、デバッグモードで実行されている Mock デバッグ拡張機能とともに新しい VS Code ウィンドウ （[拡張開発ホスト]） が表示されます。
そのウィンドウから、 `readme.md` ファイルを使って `mock test` プロジェクトを開き、 'F5' でデバッグセッションを開始してから、 それを実行します。

![Debugging Extension and Server](images/example-debuggers/debug-mock-session.png)

拡張機能をデバッグモードで実行しているので、 `src/extension.ts` にブレークポイントを設定して打つことができますが、上記のように、拡張機能では面白いコードは実行されません。
興味深いコードは別のプロセスであるデバッグアダプタで実行されます。

デバッグアダプタ自体をデバッグするには、デバッグモードで実行する必要があります。
これは、 「サーバモード」 でデバッグアダプタを実行し、 VS Code を接続するように設定することで最も簡単に実現します。
あなたの VS Code vscode-mock-debug プロジェクトで、 ドロップダウンメニューから起動設定 'server' を選択し、 緑色の 「開始」 ボタンを押します。

拡張機能のアクティブなデバッグセッションが既に存在しているので、 VS Code デバッガ UI は 「マルチセッション」 モードに入り、 CALL STACK ビューに表示される2つのデバッグセッション **Extension** と **Server** の名前を表示することで示されます。

![Debugging Extension and Server](images/example-debuggers/debug-extension-server.png)

これで、拡張アダプタとデバッグアダプタの両方を同時にデバッグできるようになりました。
ここに到達するより速い方法は、両方のセッションを自動的に起動する **Extension + Server** 起動設定を使用することです。

ファイル `src/mockDebug.ts` のメソッド `launchRequest（...）` の先頭にブレークポイントを設定し、 最後のステップとして、モックテストの launch config に `debugServer` 属性にポート `4711` を追加して、モックデバッガをデバッグアダプタサーバに接続するように設定します：

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "mock",
            "request": "launch",
            "name": "mock test",
            "program": "${workspaceRoot}/readme.md",
            "stopOnEntry": true,
            "debugServer": 4711
        }
    ]
}
```

このデバッグ設定を起動すると、 VS Code はモックデバッグアダプタを別のプロセスとして起動するのではなく、 すでに実行中のサーバのローカルポート4711に直接接続し、 `launchRequest` のブレークポイントにヒットする必要があります。

この設定では、Mockデバッグを簡単に編集、簡略化、デバッグできるようになりました。

しかし、 実際の作業が始まりました。あなたは、デバッガまたはランタイムと通信するいくつかの「実際の」コードによって、 `src/mockDebug.ts` 内のデバッグアダプタの「モック」実装を置き換える必要があります。 これには、 VS Code デバッグプロトコルの理解と実装が含まれます。 詳細は [こちら](https://code.visualstudio.com/docs/extensionAPI/api-debugging) をご覧ください。

## 3. Debug Extension の package.json の構造

デバッガアダプタのデバッガ固有の実装を提供することに加えて、 デバッガ拡張には、さまざまなデバッグ関連の提供ポイントに提供する `package.json` が必要です。

では、 Mock Debugの `package.json` を詳しく見てみましょう。

すべてのVS Code 拡張と同様に、 `package.json` は基本プロパティの **name**、 **publisher**、 および拡張の **version** を宣言します。 **categories** フィールドを使用すると、 VS Code 拡張機能 Marketplace で拡張機能を簡単に見つけることができます。

```json
{
    "name": "mock-debug",
    "version": "0.17.0",
    "publisher": "andreweinand",
    "description": "Starter extension for developing debug adapters for VS Code.",
    "engines": {
        "vscode": "^1.1.0",
        "node": "^6.5.0"
    },
    "categories": [ "Debuggers" ],

    "activationEvents": [
        "onCommand:extension.mock-debug.getProgramName",
        "onCommand:extension.mock-debug.provideInitialConfigurations"
    ],

    "contributes": {
        "breakpoints": [
            {
                "language": "markdown"
            }
        ],
        "debuggers": [{
            "type": "mock",
            "label": "Mock Debug",

            "program": "./out/mockDebug.js",
            "runtime": "node",

            "configurationAttributes": {
                "launch": {
                    "required": ["program"],
                    "properties": {
                        "program": {
                            "type": "string",
                            "description": "Absolute path to a text file.",
                            "default": "${workspaceRoot}/readme.md"
                        },
                        "stopOnEntry": {
                            "type": "boolean",
                            "description": "Automatically stop after launch.",
                            "default": true
                        }
                    }
                }
            },

            "initialConfigurations": [
                {
                    "type": "mock",
                    "name": "Mock Debug",
                    "request": "launch",
                    "program": "readme.md",
                    "stopOnEntry": true
                }
            ],

            "configurationSnippets": [
                {
                    "label": "Mock Debug: Launch",
                    "description": "A new configuration for launching a mock debug program",
                    "body": {
                        "type": "mock",
                        "request": "launch",
                        "name": "${2:Launch Program}",
                        "program": "^\"\\${workspaceRoot}/${1:Program}\""
                    }
                }
            ],

            "variables": {
                "AskForProgramName": "extension.mock-debug.getProgramName"
            }
        }]
    }
}
```

ここで、デバッグ拡張に固有の contribute を含む **contributes** セクションを見てみましょう。

最初に、 **breakpoints** の contributes を使用して、ブレークポイントの設定を有効にする言語をリストします。

次は **debuggers** のセクションです。ここでは、 （一意の） デバッグ **type** `mock` の下に1つのデバッガが導入されています。
ユーザーは、 起動設定でこの type を参照できます。 オプションの属性 **label** を使用して、 UI に表示するときにデバッグタイプをより良い名前にすることができます。

デバッグ拡張機能はデバッグアダプタを使用するため、これに対する相対パスは **program** 属性として与えられます。
エクステンションを自己完結型にするには、アプリケーションがエクステンションフォルダ内に存在していなければなりません。
規約上、このアプリケーションは `out` または `bin` という名前のフォルダ内にありますが、別の名前を自由に使用できます。

VS Code はさまざまなプラットフォームで動作するため、デバッグアダプタプログラムが異なるプラットフォームをサポートしていることを確認する必要があります。
これには次のオプションがあります:

1. プログラムがプラットフォームに依存しない方法で実装されている場合 （例:サポートされているすべてのプラットフォームで使用可能なランタイムで実行されるプログラムとして、ランタイム属性を使用してこのランタイムを指定できます。
   今日の VS コードは、 `node` ランタイムと `mono` ランタイムをサポートしています。
   上の Mock Debug アダプタは、このアプローチを使用しています。

2. デバッグアダプタの実装が異なるプラットフォーム上で異なる実行可能ファイルを必要とする場合、 **program** 属性は次のような特定のプラットフォームで修飾できます。

    ```json
    "debuggers": [{
        "type": "gdb",
        "windows": {
            "program": "./bin/gdbDebug.exe",
        },
        "osx": {
            "program": "./bin/gdbDebug.sh",
        },
        "linux": {
            "program": "./bin/gdbDebug.sh",
        }
    }]
    ```

3. 両方のアプローチの組み合わせも可能です。 次の例は Mono Debug アダプタからのもので、 OS X および Linux ではランタイムが必要で Windows では実行されないモノラルアプリケーションとして実装されています:

    ```json
    "debuggers": [{
        "type": "mono",
        "program": "./bin/monoDebug.exe",
        "osx": {
            "runtime": "mono"
        },
        "linux": {
            "runtime": "mono"
        }
    }]
    ```

**configurationAttributes** は、このデバッガーで使用可能な `launch.json` 属性のスキーマを表します。
このスキーマは、 `launch.json` を検証し、 起動設定を編集するときに IntelliSense とホバーヘルプをサポートするために使用されます。

**initialConfigurations** は、このデバッガのデフォルト `launch.json` の初期内容を定義します。
この情報は、プロジェクトに `launch.json` がなく、ユーザーがデバッグセッションを開始したとき、またはデバッグビューレットの歯車アイコンをクリックしたときに使用されます。
この場合、VS Code を使用すると、 すべてのデバッガのリストからデバッガを選択し、対応する `launch.json` を作成できます:

![Debugger Quickpick](images/example-debuggers/debug-init-config.png)

`package.json` 内に `launch.json` の初期コンテンツを静的に定義する代わりに、拡張で実装されているコマンドで初期コンテンツを '計算' することができます。

この場合、 `initialConfigurations` 属性の値をコマンドIDに設定する必要があります。

```json
// ...
"initialConfigurations": "extension.mock-debug.provideInitialConfigurations",
// ...
```

また、このコマンドの実装は `src/extension.ts` にあり、 `launch.json` の内容を文字列として返します（これにより、コメントを含めることができ、フォーマットを正確に制御することができます）。

```ts
const initialConfigurations = {
    version: '0.2.0',
    configurations: [
        {
            type: 'mock',
            request: 'launch',
            name: 'Mock Debug',
            program: '${workspaceRoot}/readme.md',
            stopOnEntry: true
        }
    ]
};

vscode.commands.registerCommand('extension.mock-debug.provideInitialConfigurations', () => {
    return [
        '// Use IntelliSense to learn about possible Mock Debug attributes.',
        '// Hover to view descriptions of existing attributes.',
        JSON.stringify(initialConfigurations, null, '\t')
    ].join('\n');
});
```

**configurationSnippets** は、 `launch.json` を編集するときに IntelliSense に表示される起動設定スニペットを定義します。
スニペットの `label` 属性の先頭にはデバッガ名が付いており、 すべてのスニペットプロポーザルのリストに表示されたときに明確に識別されます。

**variables** contributes は '変数' を 'コマンド' に束縛します。
これらの変数は、 **${command.Xxxx}** 構文を使用した起動設定で使用でき、変数はデバッグセッションの開始時にバインドされたコマンドから返された値で置き換えられます。

コマンドの実装はエクステンション内に存在し、UIを持たない簡単な式から、拡張APIで利用できるUI機能に基づいた洗練された機能にまで及ぶ可能性があります。
Mock Debugは、変数 `AskForProgramName` をコマンド `extension.mock-debug.getProgramName` にバインドします。
`src/extension.ts` にこのコマンドを実装すると、 `showInputBox` が使用され、ユーザーはプログラム名を入力できます。
```ts
vscode.commands.registerCommand('extension.mock-debug.getProgramName', config => {
    return vscode.window.showInputBox({
        placeHolder: "Please enter the name of a markdown file in the workspace folder",
        value: "readme.md"
    });
});
```
この変数は、 **${command.AskForProgramName}** のような起動設定の任意の文字列型の値で使用できるようになりました。

## 4. デバッグアダプタの公開

デバッグアダプタを作成したら、 Marketplace に公開することができます:

* デバッグアダプタの名前と目的を反映するために `package.json` の属性を更新します。
* [拡張機能の共有](/docs/extensions/publish-extension.md) セクションに記載されているように Marketplace にアップロードしてください。
