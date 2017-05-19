---
Order: 4
Area: extensions
TOCTitle: Example-Word Count
ContentId: 4D9132DC-CDDB-4E07-B2DD-9A7E168BE384
PageTitle: Visual Studio Code Example - Word Count Extension
DateApproved: 5/4/2017
MetaDescription: The Word Count extension (plug-in) example takes you deeper into the Visual Studio Code extensibility model, showing how to interact with the editor and manage extension and VS Code resources.
---

# 例 - Word Count

このドキュメントでは、 VS Code の拡張性の基礎を説明する [初めてのエクステンション](/docs/extensions/example-hello-world.md) を読んだことを前提としています。

Word Count は、 エンド・トゥ・エンドのチュートリアルで、 Markdown のオーサリングを補助する拡張子を作成する方法を示しています。 どのように動作するのかを理解する前に、 構築するコア機能を簡単にデモして、 何を期待するのかを理解しておきましょう。

`Markdown` ファイルが編集されるたびに、ステータスバーメッセージが追加されます。 このメッセージには、現在の単語数と入力時の更新がファイルからファイルに移動します。

![Word Count on Status Bar](images/example-word-count/wordcountevent2.gif)

> **ヒント:** 完成したサンプルの必要があれば、 [このGitHubリポジトリ](https://github.com/microsoft/vscode-wordcount) から入手できます。


## 概要

この例は、3つのセクションから構成され、一連の関連概念を説明します。

1. [ステータスバーの更新](/docs/extensions/example-word-count.md#update-the-status-bar) - VS Code の `ステータスバー` にカスタムテキストを表示します
2. [イベントの購読](/docs/extensions/example-word-count.md#subscribing-to-events) - エディタイベントに基づいて `ステータスバー` を更新します
3. [拡張リソースの廃棄](/docs/extensions/example-word-count.md#disposing-extension-resources) - イベント購読やUIハンドルなどのリソースを解放します

まず、最新の VS Code 拡張ジェネレータがインストールされていることを確認してから実行してください。

```bash
npm install -g yo generator-code
yo code
```

拡張ジェネレータが開きます。この例は TypeScript の `New Extension` オプションに基づいています。今のところ、下の画像で完成したのと同じ方法でフィールドに記入してください(拡張名として 'WordCount'、publisher として自分の名前を使用)。

![Yo Code Word Count Example Output](images/example-word-count/yo1.png)

これでジェネレータの出力に記載されているように、 VS Code を開くことができます:

```bash
cd WordCount
code .
```

## エクステンションを実行する

作業を始める前に、拡張機能を実行して、 `kb(workbench.action.debug.start)` を押してすべてが期待どおりに動作することを確認します。以前の "Hello World" ウォークスルーで見たように、 VS Code は拡張機能がロードされる別のウィンドウ(**[拡張開発ホスト]**ウィンドウ)を開きます。 コマンドパレット ("kb(workbench.action.showCommands)"を押す) で "Hello World" コマンドを見つけて、それを選択すると、ウィンドウの上部に "Hello World" という情報ボックスが表示されます。

拡張機能が適切に動作していることを確認したので、必要に応じて拡張機能の開発ウィンドウを開いたままにしておくことができます。あなたのエクステンションに加えた変更をテストするには、開発ウィンドウで `kb(workbench.action.debug.continue)` をもう一度押すか、 `kbstyle(Ctrl+R)` (Mac: `kbstyle(Cmd+R)`) を押してエクステンション開発ウィンドウをリロードしてください。

## ステータスバーを更新する

生成された `extension.ts` ファイルの内容を以下のコードに置き換えてください。 これは、単語をカウントして VS Code ステータスバーに表示することができる `WordCounter` クラスを宣言し、インスタンス化します。 呼び出されると、 "Hello Word" コマンドは `updateWordCount` を呼び出します。

```javascript
// モジュール 'vscode' には VS Code 拡張 API が含まれています
// 下のコードで使用するために必要な拡張性タイプをインポートする
import {window, commands, Disposable, ExtensionContext, StatusBarAlignment, StatusBarItem, TextDocument} from 'vscode';

// このメソッドは、拡張機能がアクティブになったときに呼び出されます。有効化は
// package.json で定義されているアクティベーションイベントによって制御されます。
export function activate(context: ExtensionContext) {

    // コンソールを使用して診断情報(console.log)とエラー(console.error)を出力します。
    // このコード行は、拡張機能がアクティブになったときに一度だけ実行されます。
    console.log('Congratulations, your extension "WordCount" is now active!');

    // 新しい単語カウンターを作成する
    let wordCounter = new WordCounter();

    var disposable = commands.registerCommand('extension.sayHello', () => {
        wordCounter.updateWordCount();
    });

    // この拡張機能が無効になったときに処理されるディスポーザブルのリストに追加します。
    context.subscriptions.push(wordCounter);
    context.subscriptions.push(disposable);
}

class WordCounter {

    private _statusBarItem: StatusBarItem;

    public updateWordCount() {

        // 必要に応じて作成する
        if (!this._statusBarItem) {
            this._statusBarItem = window.createStatusBarItem(StatusBarAlignment.Left);
        }

        // 現在のテキストエディタを取得する
        let editor = window.activeTextEditor;
        if (!editor) {
            this._statusBarItem.hide();
            return;
        }

        let doc = editor.document;

        // Markdownファイルがあればステータスを更新する
        if (doc.languageId === "markdown") {
            let wordCount = this._getWordCount(doc);

            // ステータスバーを更新する
            this._statusBarItem.text = wordCount !== 1 ? `${wordCount} Words` : '1 Word';
            this._statusBarItem.show();
        } else { 
            this._statusBarItem.hide();
        }
    }

    public _getWordCount(doc: TextDocument): number {

        let docContent = doc.getText();

        // 分割が正確になるように不要な空白を解析する
        docContent = docContent.replace(/(< ([^>]+)<)/g, '').replace(/\s+/g, ' ');
        docContent = docContent.replace(/^\s\s*/, '').replace(/\s\s*$/, '');
        let wordCount = 0;
        if (docContent != "") {
            wordCount = docContent.split(" ").length;
        }

        return wordCount;
    }

    dispose() {
        this._statusBarItem.dispose();
    }
}
```

次に、拡張機能のアップデートを試してみましょう。

TypeScript ファイルのコンパイルを watch (拡張の .vscode\tasks.jsonファイル) に設定しているので、再ビルドする必要はありません。 あなたのコードが実行されている **[拡張機能開発ホスト]** ウィンドウで `kbstyle(Ctrl+R)` を押すと、拡張機能がリロードされます (プライマリ開発ウィンドウから `kb(workbench.action.debug.start)` を実行することもできます)。 "Hello World" コマンドを使用して、前と同じ方法でコードをアクティブ化する必要があります。あなたが Markdown ファイル内にいると仮定すると、あなたのステータスバーは単語数を表示します。

![Working Word Count](images/example-word-count/wordcount2.png)

これは良いスタートですが、ファイルが変更されたときにカウントが更新されると、よりクールになります。

## イベントを購読 (Subscribing) する

あなたのヘルパークラスを一連のイベントに接続しましょう。

* `onDidChangeTextEditorSelection` - カーソルの位置が変化するとイベントが発生します
* `onDidChangeActiveTextEditor` - アクティブなエディタが変更されるとイベントが発生します。

これを行うために、新しいクラスを `extension.ts` ファイルに追加します。これらのイベントの購読を設定し、ワードカウントを更新するように `WordCounter` に依頼します。また、このクラスが Disposables としてサブスクリプションを管理する方法と、それ自体が廃棄されるときにリストを停止する方法にも注意してください。

`extension.ts` ファイルの一番下に下記のような `WordCounterController` を追加してください。

```javascript
class WordCounterController {

    private _wordCounter: WordCounter;
    private _disposable: Disposable;

    constructor(wordCounter: WordCounter) {
        this._wordCounter = wordCounter;
        this._wordCounter.updateWordCount();

        // 選択の変更とエディタの起動イベントに登録する
        let subscriptions: Disposable[] = [];
        window.onDidChangeTextEditorSelection(this._onEvent, this, subscriptions);
        window.onDidChangeActiveTextEditor(this._onEvent, this, subscriptions);

        // 現在のファイルのカウンタを更新する
        this._wordCounter.updateWordCount();

        // 両方のイベントサブスクリプションから組み合わせたディスポーザブルを作成する
        this._disposable = Disposable.from(...subscriptions);
    }

    dispose() {
        this._disposable.dispose();
    }

    private _onEvent() {
        this._wordCounter.updateWordCount();
    }
}
```

コマンドが呼び出されたときに Word Count 拡張が読み込まれるのではなく、各 *Markdown* ファイルで使用できるようにしました。

まず、 `activate` 関数の本体を次のように置き換えます。

```javascript
// コンソールを使用して診断情報 (console.log) とエラー (console.error) を出力します。
// このコード行は、拡張機能がアクティブになったときに一度だけ実行されます。
console.log('Congratulations, your extension "WordCount" is now active!');

// 新しい単語カウンターを作成する
let wordCounter = new WordCounter();
let controller = new WordCounterController(wordCounter);

// この拡張機能が無効になったときに処理されるディスポーザブルのリストに追加します。
context.subscriptions.push(controller);
context.subscriptions.push(wordCounter);
```

次に、 `Markdown` ファイルのオープン時に拡張機能が有効になっていることを確認する必要があります。 これを行うには、 `package.json` ファイルを変更する必要があります。 以前は、拡張機能は `extension.sayHello` コマンドで有効になっていました。このコマンドは `package.json` から `contributes` 属性全体を削除できます：

```json
    "contributes": {
        "commands":
            [{
                "command": "extension.sayHello",
                "title": "Hello World"
            }
        ]
    },
```

`activateEvents` 属性をこれに更新することによって、 *Markdown* ファイルのオープン時にアクティブになるように、あなたの拡張子を変更してください：

```json
    "activationEvents": [
        "onLanguage:markdown"
    ]
```

The  [`onLanguage:${language}`](/docs/extensionAPI/activation-events.md#activationeventsonlanguage) イベントは言語ID(この場合は "markdown")をとり、その言語のファイルが開かれるたびに呼び出されます。

ウィンドウリロード `kbstyle(Ctrl+R)` または `kb(workbench.action.debug.start)` を実行して拡張機能を実行し、 Markdown ファイルの編集を開始します。 これで、 Word Count をライブアップデート出来るようになりました。

![Word Count Updating on Events](images/example-word-count/wordcountevent2.gif)

`activate` 関数にブレークポイントを設定すると、最初の Markdown ファイルが開かれたときに一度だけ呼び出されることに気づくでしょう。 `WordCountController` コンストラクタが実行され、エディタイベントに登録されるので、 Markdown ファイルが開かれ、そのテキストが変更されるときに `updateWordCount` 関数が呼び出されます。

## ステータスバーのカスタマイズ

ステータスバーに書式設定されたテキストを表示する方法を見てきました。  VS Code を使用すると、ステータスバーの追加を色、アイコン、ツールチップなどでさらにカスタマイズできます。 IntelliSenseを使用すると、さまざまな `StatusBarItem`フィールドを見ることができます。  VS Code 拡張APIについて学ぶためのもう1つの素晴らしいリソースは、生成された拡張プロジェクトに含まれる `vscode.d.ts`型宣言ファイルです。エディタで `node_modules \ vscode \ vscode.d.ts`を開くと、コメントを含む完全な VS Code 拡張APIが表示されます。

![vscode-d-ts file](images/example-word-count/vscode-d-ts.png)

StatusBarItem更新コードを次のように置き換えます。

```javascript
    // ステータスバーを更新する
    this._statusBarItem.text = wordCount !== 1 ? `$(pencil) ${wordCount} Words` : '$(pencil) 1 Word';
    this._statusBarItem.show();
```

計算された単語数の左に [GitHub Octicon](https://octicons.github.com) の `鉛筆` アイコンが表示されます。

![Word Count with pencil icon](images/example-word-count/wordcount-pencil.png)

## 拡張リソースの廃棄

次に、 [Disposables](/docs/extensionAPI/patterns-and-principles.md#disposables) を使って、拡張機能が VS Code リソースをどのように処理するかを詳しく見ていきます。

拡張機能が有効化されると、Disposablesの `subscription` コレクションを持つ `ExtensionContext` オブジェクトが渡されます。エクステンションは Disposable オブジェクトをこのコレクションに追加することができ、 VS Code はエクステンションが無効化されたときにそれらのオブジェクトを破棄します。

ワークスペースやUIオブジェクト(例： `registerCommand`)を作成する多くの VS Code APIはDisposableを返し、disposeメソッドを直接呼び出して VS Code からこれらの要素を削除することができます。

イベントは `onDid*` イベントサブスクライバメソッドが Disposable を返す別の例です。エクステンションは、イベントの Disposable を廃棄することにより、イベントを退会します。この例では、 `WordCountController` は、イベントサブスクリプションDisposablesを、非アクティブ化時にクリーンアップする独自の Disposable コレクションを保持することによって直接処理します。

```javascript
    // 選択の変更とエディタの起動イベントに登録する
    let subscriptions: Disposable[] = [];
    window.onDidChangeTextEditorSelection(this._onEvent, this, subscriptions);
    window.onDidChangeActiveTextEditor(this._onEvent, this, subscriptions);

    // 両方のイベントサブスクリプションから組み合わせたディスポーザブルを作成する
    this._disposable = Disposable.from(...subscriptions);
```

## あなたの機能拡張をローカルにインストールする

これまでに書いたエクステンションは、エクステンション開発ホストのインスタンスである VS Code の特別なインスタンスでのみ実行されます。拡張機能をすべての VS Code インスタンスで使用できるようにするには、拡張フォルダの内容を [.vscode/extensions`フォルダ](/docs/extensions/yocode.md#your-extensions-folder) の下の新しいフォルダにコピーします。

## エクステンションを公開する

[エクステンションを共有する](/docs/extensions/publish-extension.md)の方法をお読みください。

## 次のステップ

詳しくは、次を参照してください。

* [Extension Generator](/docs/extensions/yocode.md) - Yoコード拡張ジェネレータのその他のオプションについて学びます。
* [Extension API](/docs/extensionAPI/overview.md) - Extension API の概要を取得します。
* [公開ツール](/docs/extensions/publish-extension.md) - 公開マーケットプレイスにエクステンションを公開する方法を学びます。
* [エディタAPI](/docs/extensionAPI/vscode-api.md#window) - テキストドキュメント、テキストエディタ、およびテキストの編集について学んでください。
* [その他の拡張の例](/docs/extensions/samples.md) - サンプルの拡張プロジェクトの一覧を見てください。


