---
Order: 3
Area: nodejs
TOCTitle: React Tutorial
ContentId: 2dd2eeff-2eb3-4a0c-a59d-ea9a0b10c468
PageTitle: React JavaScript Tutorial in VS Code
DateApproved: 6/2/2017
MetaDescription: React JavaScript tutorial showing IntelliSense, debugging, and code navigation support in Visual Studio Code.
MetaSocialImage: nodejs_javascript_vscode.png
---
# VS Code で React チュートリアル
# React Tutorial in VS Code

[React](https://facebook.github.io/react/).js は、 Facebook によって開発された Web アプリケーションのユーザーインターフェイスを構築するための人気のある JavaScript ライブラリです。
VS Code は React.js IntelliSense と box 外のコードナビゲーションをサポートしています。

![welcome to react](images/reactjs/welcome-to-react.png)

## Welcome to React

このチュートリアルでは、 `create-react-app` [generator](https://facebook.github.io/react/docs/installation.html#creating-a-new-application) を使用します。 React アプリケーションサーバーを実行するだけでなくジェネレータをインストールして使用するには、[Node.js](https://nodejs.org/) JavaScriptランタイムと [npm](https://www.npm.js.com/) (Node.js パッケージマネージャ) がインストールされていることが必要です。 npm は Node.js に含まれており [here]（https://nodejs.org/en/download/）からインストールできます。

> **ヒント**: Node.js と npm がマシンに正しくインストールされていることをテストするには、 `node --version` と ` npm --version` と入力します。

`create-react-app` ジェネレータをインストールするには、端末またはコマンドプロンプトで次のように入力します。

```bash
npm install -g create-react-app
```

インストールには数分かかることがあります。次のように入力して、新しい React アプリケーションを作成できるようになりました:

```bash
create-react-app my-app
```

ここで `my-app` はアプリケーションのフォルダ名です。Reactアプリケーションを作成して依存関係をインストールするには、数分かかることがあります。

新しいフォルダに移動し、 `npm start` と入力して Web サーバを起動し、ブラウザでアプリケーションを開くことで React アプリケーションをすぐに実行しましょう:

```bash
cd my-app
npm start
```

ブラウザーの `http://localhost:3000`に "Welcome to React" と表示されるはずです。 私たちは VS Code でアプリケーションを見ている間、Webサーバーを実行したままにしておきます。

React アプリケーションをVSコードで開くには、別のターミナル (またはコマンドプロンプト) を開き、 `my-app` フォルダに移動して `code .` と打ちます:

```bash
cd my-app
code .
```

### マークダウンプレビュー
### Markdown Preview

ファイルエクスプローラには、アプリケーションの `README.md` の Markdown ファイルが表示されます。 これには、アプリケーションと React に関する一般的な情報がたくさんあります。 README を確認するには、VS Code [Markdown Preview](/docs/languages/markdown.md#markdown-preview) を使用します。 現在のエディタグループ (**Markdown: 開くプレビュー** `kb(markdown.showPreview)`) または新しいエディタグループ (**Markdown: サイドにプレビューを開く** `kb(markdown.showPreviewToSide)`) でプレビューを開くことができます。 ヘッダーへのハイパーリンクのナビゲーションや、コードブロック内の構文のハイライト表示が得られます。

![README markdown preview](images/reactjs/markdown-preview.png)

### シンタックスハイライトとブラケットマッチング
### Syntax highlighting and bracket matching

`src` フォルダを開き、`index.js` ファイルを選択します。 VS Code にはさまざまなソースコード要素の構文が強調表示されていますが、カーソルをかっこに置くと、一致する括弧も選択されます。

![react bracket matching](images/reactjs/bracket-matching.png)

### IntelliSense

`index.js` で入力を開始すると、スマートな提案や補完が表示されます。

![react suggestions](images/reactjs/suggestions.png)

提案を選択して `.`と入力すると、 [IntelliSense](/docs/editor/intellisense.md) を介してオブジェクトの種類とメソッドが表示されます。

![react intellisense](images/reactjs/intellisense.png)

VS Code は、 JavaScript コードインテリジェンスのために TypeScript 言語サービスを使用し、 この機能は [自動タイプ取得](/docs/languages/javascript.md#automatic-type-acquisition) (ATA) という npm 型定義ファイル `package.json` で参照されている npm モジュールの (`*.d.ts`) をプルダウンする機能です。

メソッドを選択すると、パラメータヘルプも表示されます:

![react parameter help](images/reactjs/parameter-help.png)

### 定義へ移動、定義を抽出

TypeScript 言語サービスを介して、 VS Code は **定義へ移動** (`kb(editor.action.gotodeclaration)`) または **Peek Defintion** (`kb(editor.action.peekImplementation)`)。 `App` の上にカーソルを置き、右クリックして **Peek Definition** を選択します。 [Peek window](/docs/editor/editingevolved.md#peek) が開き、 `App.js` の `App` 定義が表示されます。

![react peek definition](images/reactjs/peek-definition.png)

`kbstyle(Escape)` を押すと、 Peekウィンドウが閉じます。

## Hello World!

サンプルアプリケーションを "Hello World!" に更新しましょう。 リンクを追加して新しいH1ヘッダを宣言し、 `ReactDOM.render` の `<App />` タグを `element` に置き換えてください。
```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import './index.css';

var element = React.createElement('h1', { className: 'greeting' }, 'Hello, world!');
ReactDOM.render(element, document.getElementById('root'));
registerServiceWorker();
```

`index.js` を保存すると、サーバの実行中のインスタンスがWebページを更新し、 "Hello World!" が表示されます。

> **ヒント**: VS Code は自動保存機能をサポートしています。デフォルトでは、ファイルは遅れて保存されます。 **ファイル** > **自動保存** をチェックして自動保存を有効にするか、 直接 `files.autoSave` ユーザ[設定](/docs/getstarted/settings.md) を設定してください。

![hello world](images/reactjs/hello-world.png)

## React のデバッグ
## Debugging React

クライアント側の React コードをデバッグするには、[Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) 拡張機能をインストールする必要があります。

>注意: このチュートリアルでは、Chromeブラウザがインストールされていることを前提としています。 Debugger for Chrome拡張機能のビルダーには、[Safari on iOS](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-ios-web) および [Edge](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-edge)ブラウザ用のバージョンも用意されています。

Open the Extensions view (`kb(workbench.view.extensions)`) and type 'chrome` in the search box. You'll see several extension which reference Chrome.

![debugger for chrome](images/reactjs/debugger-for-chrome.png)

**Debug for Chrome** の **Install** ボタンを押してください。 ボタンが **インストール中** に変わり、インストールが完了すると **再読み込み** に変わります。 **再読み込み** を押して VS Code を再起動し、拡張機能を有効にします。

### ブレークポイントを設定する
### Set a breakpoint
---
Order: 3
Area: nodejs
TOCTitle: React Tutorial
ContentId: 2dd2eeff-2eb3-4a0c-a59d-ea9a0b10c468
PageTitle: React JavaScript Tutorial in VS Code
DateApproved: 6/2/2017
MetaDescription: React JavaScript tutorial showing IntelliSense, debugging, and code navigation support in Visual Studio Code.
MetaSocialImage: nodejs_javascript_vscode.png
---
# VS Code で React チュートリアル
# React Tutorial in VS Code

[React](https://facebook.github.io/react/).js は、 Facebook によって開発された Web アプリケーションのユーザーインターフェイスを構築するための人気のある JavaScript ライブラリです。
VS Code は React.js IntelliSense と box 外のコードナビゲーションをサポートしています。

![welcome to react](images/reactjs/welcome-to-react.png)

## Welcome to React

このチュートリアルでは、 `create-react-app` [generator](https://facebook.github.io/react/docs/installation.html#creating-a-new-application) を使用します。 React アプリケーションサーバーを実行するだけでなくジェネレータをインストールして使用するには、[Node.js](https://nodejs.org/) JavaScriptランタイムと [npm](https://www.npm.js.com/) (Node.js パッケージマネージャ) がインストールされていることが必要です。 npm は Node.js に含まれており [here]（https://nodejs.org/en/download/）からインストールできます。

> **ヒント**: Node.js と npm がマシンに正しくインストールされていることをテストするには、 `node --version` と ` npm --version` と入力します。

`create-react-app` ジェネレータをインストールするには、端末またはコマンドプロンプトで次のように入力します。

```bash
npm install -g create-react-app
```

インストールには数分かかることがあります。次のように入力して、新しい React アプリケーションを作成できるようになりました:

```bash
create-react-app my-app
```

ここで `my-app` はアプリケーションのフォルダ名です。Reactアプリケーションを作成して依存関係をインストールするには、数分かかることがあります。

新しいフォルダに移動し、 `npm start` と入力して Web サーバを起動し、ブラウザでアプリケーションを開くことで React アプリケーションをすぐに実行しましょう:

```bash
cd my-app
npm start
```

ブラウザーの `http://localhost:3000`に "Welcome to React" と表示されるはずです。 私たちは VS Code でアプリケーションを見ている間、Webサーバーを実行したままにしておきます。

React アプリケーションをVSコードで開くには、別のターミナル (またはコマンドプロンプト) を開き、 `my-app` フォルダに移動して `code .` と打ちます:

```bash
cd my-app
code .
```

### マークダウンプレビュー
### Markdown Preview

ファイルエクスプローラには、アプリケーションの `README.md` の Markdown ファイルが表示されます。 これには、アプリケーションと React に関する一般的な情報がたくさんあります。 README を確認するには、VS Code [Markdown Preview](/docs/languages/markdown.md#markdown-preview) を使用します。 現在のエディタグループ (**Markdown: 開くプレビュー** `kb(markdown.showPreview)`) または新しいエディタグループ (**Markdown: サイドにプレビューを開く** `kb(markdown.showPreviewToSide)`) でプレビューを開くことができます。 ヘッダーへのハイパーリンクのナビゲーションや、コードブロック内の構文のハイライト表示が得られます。

![README markdown preview](images/reactjs/markdown-preview.png)

### シンタックスハイライトとブラケットマッチング
### Syntax highlighting and bracket matching

`src` フォルダを開き、`index.js` ファイルを選択します。 VS Code にはさまざまなソースコード要素の構文が強調表示されていますが、カーソルをかっこに置くと、一致する括弧も選択されます。

![react bracket matching](images/reactjs/bracket-matching.png)

### IntelliSense

`index.js` で入力を開始すると、スマートな提案や補完が表示されます。

![react suggestions](images/reactjs/suggestions.png)

提案を選択して `.`と入力すると、 [IntelliSense](/docs/editor/intellisense.md) を介してオブジェクトの種類とメソッドが表示されます。

![react intellisense](images/reactjs/intellisense.png)

VS Code は、 JavaScript コードインテリジェンスのために TypeScript 言語サービスを使用し、 この機能は [自動タイプ取得](/docs/languages/javascript.md#automatic-type-acquisition) (ATA) という npm 型定義ファイル `package.json` で参照されている npm モジュールの (`*.d.ts`) をプルダウンする機能です。

メソッドを選択すると、パラメータヘルプも表示されます:

![react parameter help](images/reactjs/parameter-help.png)

### 定義へ移動、定義を抽出

TypeScript 言語サービスを介して、 VS Code は **定義へ移動** (`kb(editor.action.gotodeclaration)`) または **Peek Defintion** (`kb(editor.action.peekImplementation)`)。 `App` の上にカーソルを置き、右クリックして **Peek Definition** を選択します。 [Peek window](/docs/editor/editingevolved.md#peek) が開き、 `App.js` の `App` 定義が表示されます。

![react peek definition](images/reactjs/peek-definition.png)

`kbstyle(Escape)` を押すと、 Peekウィンドウが閉じます。

## Hello World!

サンプルアプリケーションを "Hello World!" に更新しましょう。 リンクを追加して新しいH1ヘッダを宣言し、 `ReactDOM.render` の `<App />` タグを `element` に置き換えてください。
```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import './index.css';

var element = React.createElement('h1', { className: 'greeting' }, 'Hello, world!');
ReactDOM.render(element, document.getElementById('root'));
registerServiceWorker();
```

`index.js` を保存すると、サーバの実行中のインスタンスがWebページを更新し、 "Hello World!" が表示されます。

> **ヒント**: VS Code は自動保存機能をサポートしています。デフォルトでは、ファイルは遅れて保存されます。 **ファイル** > **自動保存** をチェックして自動保存を有効にするか、 直接 `files.autoSave` ユーザ[設定](/docs/getstarted/settings.md) を設定してください。

![hello world](images/reactjs/hello-world.png)

## React のデバッグ
## Debugging React

クライアント側の React コードをデバッグするには、[Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) 拡張機能をインストールする必要があります。

>注意: このチュートリアルでは、Chromeブラウザがインストールされていることを前提としています。 Debugger for Chrome拡張機能のビルダーには、[Safari on iOS](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-ios-web) および [Edge](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-edge)ブラウザ用のバージョンも用意されています。

Open the Extensions view (`kb(workbench.view.extensions)`) and type 'chrome` in the search box. You'll see several extension which reference Chrome.

![debugger for chrome](images/reactjs/debugger-for-chrome.png)

**Debug for Chrome** の **Install** ボタンを押してください。 ボタンが **インストール中** に変わり、インストールが完了すると **再読み込み** に変わります。 **再読み込み** を押して VS Code を再起動し、拡張機能を有効にします。

### ブレークポイントを設定する
### Set a breakpoint

`index.js` にブレークポイントを設定するには、行番号の左側にあるガターをクリックします。これにより、赤い円として表示されるブレークポイントが設定されます。

![set a breakpoint](images/reactjs/breakpoint.png)

### Chrome デバッガを設定する
### Configure the Chrome debugger

最初に [デバッガ](/docs/editor/debugging.md) を設定する必要があります。 これを行うには、デバッグビュー (`kb(workbench.view.debug)`) に行き、歯車ボタンをクリックして `launch.json` デバッガ設定ファイルを作成します。 **環境の選択** ドロップダウンから **Chrome** を選択します。 プロジェクトの新しい `.vscode` フォルダに `launch.json` ファイルが作成されます。これには、ウェブサイトを起動するか、実行中のインスタンスにアタッチするための設定が含まれています。

我々の例では、ポートを `8080` から `3000` に変更するために1つの変更を加える必要があります。 `launch.json` は次のようになります:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "chrome",
            "request": "launch",
            "name": "Launch Chrome against localhost",
            "url": "http://localhost:3000",
            "webRoot": "${workspaceRoot}"
        },
        {
            "type": "chrome",
            "request": "attach",
            "name": "Attach to Chrome",
            "port": 9222,
            "webRoot": "${workspaceRoot}"
        }
    ]
}
```

`kb(workbench.action.debug.start)` または緑の矢印を押してデバッガを起動し、新しいブラウザインスタンスを開きます。 ブレークポイントが設定されているソースコードは、デバッガがアタッチされる前に起動時に実行されるため、Webページを更新するまでブレークポイントにヒットしません。 ページを更新すると、ブレークポイントに当たるはずです。

![hit breakpoint](images/reactjs/hit-breakpoint.png)

ソースコード (`kb(workbench.action.debug.stepOver)`) を実行し、 `element`などの変数を検査し、クライアント側のReactアプリケーションの呼び出しスタックを見ることができます。

![debug variable](images/reactjs/debug-variable.png)

**Debugger for Chrome** 拡張 README には、他の設定、ソースマップの操作、トラブルシューティングに関する多くの情報があります。また、**Extensions** ビューからVSコード内で直接確認することもできます。 **詳細** 表示。

## Linting

Lintersはあなたのソースコードを分析し、アプリケーションを実行する前に潜在的な問題について警告することができます。 VSコード組み込みJavaScript言語サービスには、デフォルトで[**問題**]パネル（**表示** > **問題** `kb(workbench.actions.view.problems)`)。

あなたの React のソースコードに小さな誤りを入れてみると、**Problems** パネルに緑色のちらつきと警告が表示されます。

![javascript error](images/reactjs/js-error.png)

リンターは、より洗練された分析、コーディング規則の実施、アンチパターンの検出を提供することができます。よく使われるJavaScriptリンターは[ESLint](http://eslint.org/) です。 ESLint VS Code [extension](https://marketplace.visualstudio.com/items/dbaeumer.vscode-eslint) と組み合わされた ESLint は、優れた製品内の糸くず処理経験を提供します。

最初に ESLint コマンドラインツールをインストールします。

```bash
npm install -g eslint
```

次に、**Extensions** ビューに行き、 'eslint' と入力して ESLint 拡張機能をインストールします。

![ESLint extension](images/reactjs/eslint-extension.png)

ESLint拡張機能がインストールされ、VSコードがリロードされたら、ESLint設定ファイル `eslintrc.json` を作成します。**コマンドパレット** (`kb(workbench.action.showCommands)`) から拡張機能の **ESLint: Create 'eslintrc.json' File** コマンドを使って作成することができます。

![create eslintrc](images/reactjs/create-eslintrc.png)

このコマンドはプロジェクトルートに `.eslintrc.json` ファイルを作成します:

```json
{
    "env": {
        "browser": true,
        "commonjs": true,
        "es6": true,
        "node": true
    },
    "parserOptions": {
        "ecmaFeatures": {
            "jsx": true
        },
        "sourceType": "module"
    },
    "rules": {
        "no-const-assign": "warn",
        "no-this-before-super": "warn",
        "no-undef": "warn",
        "no-unreachable": "warn",
        "no-unused-vars": "warn",
        "constructor-super": "warn",
        "valid-typeof": "warn"
    }
}
```

ESLintは開いているファイルを解析し、 'App'が定義されているが使用されていないことを警告する `index.js` を表示します。

 ![App is unused](images/reactjs/app-is-unused.png)

ESLint [rules](http://eslint.org/docs/rules/) を変更することができ、 ESLint 拡張機能は `eslintrc.json` に IntelliSense を提供します。

![eslintrc IntelliSense](images/reactjs/eslintrc-intellisense.png)

余分なセミコロンのエラールールを追加しましょう：

```json
 "rules": {
        "no-const-assign": "warn",
        "no-this-before-super": "warn",
        "no-undef": "warn",
        "no-unreachable": "warn",
        "no-unused-vars": "warn",
        "constructor-super": "warn",
        "valid-typeof": "warn",
        "no-extra-semi":"error"
    }
```

行に複数のセミコロンが間違っていると、エディタにエラー（赤いちらつき）が表示され、**問題**パネルにエラーが表示されます。

![extra semicolon error](images/reactjs/extra-semi-error.png)

## 人気スターターキット

このチュートリアルでは、単純な React アプリケーションを作成するために `create-react-app` ジェネレータを使用しました。あなたの最初の React アプリケーションを構築するのに役立つ素晴らしいサンプルとスターターキットがたくさんあります。

### VS Code React Sample

これは、[demo](https://channel9.msdn.com/events/Build/2017/T6078) に使用されている [sample](https://github.com/Microsoft/vscode-react-sample) Reactアプリケーションです。今年のビルドカンファレンスで。このサンプルでは簡単なTODOアプリケーションが作成され、Node.js [Express](https://expressjs.com/) サーバーのソースコードが含まれています。また、[Babel](https://babeljs.io) ES6 トランスペレーターを使用し、 [webpack](https://webpack.js.org/) を使用してサイト資産をバンドルする方法も示しています。

### MERN スターター

完全なMERN(MongoDB、Express、React、Node.js) スタックの例を見たい場合は、[MERN Starter](http://mern.io/) を見てください。 [MongoDB](https://docs.mongodb.com/v3.0/installation/) をインストールして起動する必要がありますが、すぐに MERN アプリケーションが実行されます。 [vscode-recipes](https://github.com/weinand/vscode-recipes/tree/master/MERN-Starter) には、 Node.js サーバーのデバッグの設定に関する詳細なVSコード固有のドキュメントがあります。

### TypeScript React

If you're curious about TypeScript and React, you can also create a TypeScript version of the `create-react-app` application. See the details at [TypeScript-React-Starter](https://github.com/Microsoft/TypeScript-React-Starter) on the [TypeScript Quick Start](http://www.typescriptlang.org/samples/index.html) site.
`index.js` にブレークポイントを設定するには、行番号の左側にあるガターをクリックします。これにより、赤い円として表示されるブレークポイントが設定されます。

![set a breakpoint](images/reactjs/breakpoint.png)

### Chrome デバッガを設定する
### Configure the Chrome debugger

最初に [デバッガ](/docs/editor/debugging.md) を設定する必要があります。 これを行うには、デバッグビュー (`kb(workbench.view.debug)`) に行き、歯車ボタンをクリックして `launch.json` デバッガ設定ファイルを作成します。 **環境の選択** ドロップダウンから **Chrome** を選択します。 プロジェクトの新しい `.vscode` フォルダに `launch.json` ファイルが作成されます。これには、ウェブサイトを起動するか、実行中のインスタンスにアタッチするための設定が含まれています。

我々の例では、ポートを `8080` から `3000` に変更するために1つの変更を加える必要があります。 `launch.json` は次のようになります:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "chrome",
            "request": "launch",
            "name": "Launch Chrome against localhost",
            "url": "http://localhost:3000",
            "webRoot": "${workspaceRoot}"
        },
        {
            "type": "chrome",
            "request": "attach",
            "name": "Attach to Chrome",
            "port": 9222,
            "webRoot": "${workspaceRoot}"
        }
    ]
}
```

`kb(workbench.action.debug.start)` または緑の矢印を押してデバッガを起動し、新しいブラウザインスタンスを開きます。 ブレークポイントが設定されているソースコードは、デバッガがアタッチされる前に起動時に実行されるため、Webページを更新するまでブレークポイントにヒットしません。 ページを更新すると、ブレークポイントに当たるはずです。

![hit breakpoint](images/reactjs/hit-breakpoint.png)

ソースコード (`kb(workbench.action.debug.stepOver)`) を実行し、 `element`などの変数を検査し、クライアント側のReactアプリケーションの呼び出しスタックを見ることができます。

![debug variable](images/reactjs/debug-variable.png)

**Debugger for Chrome** 拡張 README には、他の設定、ソースマップの操作、トラブルシューティングに関する多くの情報があります。また、**Extensions** ビューからVSコード内で直接確認することもできます。 **詳細** 表示。

## Linting

Lintersはあなたのソースコードを分析し、アプリケーションを実行する前に潜在的な問題について警告することができます。 VSコード組み込みJavaScript言語サービスには、デフォルトで[**問題**]パネル（**表示** > **問題** `kb(workbench.actions.view.problems)`)。

あなたの React のソースコードに小さな誤りを入れてみると、**Problems** パネルに緑色のちらつきと警告が表示されます。

![javascript error](images/reactjs/js-error.png)

リンターは、より洗練された分析、コーディング規則の実施、アンチパターンの検出を提供することができます。よく使われるJavaScriptリンターは[ESLint](http://eslint.org/) です。 ESLint VS Code [extension](https://marketplace.visualstudio.com/items/dbaeumer.vscode-eslint) と組み合わされた ESLint は、優れた製品内の糸くず処理経験を提供します。

最初に ESLint コマンドラインツールをインストールします。

```bash
npm install -g eslint
```

次に、**Extensions** ビューに行き、 'eslint' と入力して ESLint 拡張機能をインストールします。

![ESLint extension](images/reactjs/eslint-extension.png)

ESLint拡張機能がインストールされ、VSコードがリロードされたら、ESLint設定ファイル `eslintrc.json` を作成します。**コマンドパレット** (`kb(workbench.action.showCommands)`) から拡張機能の **ESLint: Create 'eslintrc.json' File** コマンドを使って作成することができます。

![create eslintrc](images/reactjs/create-eslintrc.png)

このコマンドはプロジェクトルートに `.eslintrc.json` ファイルを作成します:

```json
{
    "env": {
        "browser": true,
        "commonjs": true,
        "es6": true,
        "node": true
    },
    "parserOptions": {
        "ecmaFeatures": {
            "jsx": true
        },
        "sourceType": "module"
    },
    "rules": {
        "no-const-assign": "warn",
        "no-this-before-super": "warn",
        "no-undef": "warn",
        "no-unreachable": "warn",
        "no-unused-vars": "warn",
        "constructor-super": "warn",
        "valid-typeof": "warn"
    }
}
```

ESLintは開いているファイルを解析し、 'App'が定義されているが使用されていないことを警告する `index.js` を表示します。

 ![App is unused](images/reactjs/app-is-unused.png)

ESLint [rules](http://eslint.org/docs/rules/) を変更することができ、 ESLint 拡張機能は `eslintrc.json` に IntelliSense を提供します。

![eslintrc IntelliSense](images/reactjs/eslintrc-intellisense.png)

余分なセミコロンのエラールールを追加しましょう：

```json
 "rules": {
        "no-const-assign": "warn",
        "no-this-before-super": "warn",
        "no-undef": "warn",
        "no-unreachable": "warn",
        "no-unused-vars": "warn",
        "constructor-super": "warn",
        "valid-typeof": "warn",
        "no-extra-semi":"error"
    }
```

行に複数のセミコロンが間違っていると、エディタにエラー（赤いちらつき）が表示され、**問題**パネルにエラーが表示されます。

![extra semicolon error](images/reactjs/extra-semi-error.png)

## 人気スターターキット

このチュートリアルでは、単純な React アプリケーションを作成するために `create-react-app` ジェネレータを使用しました。あなたの最初の React アプリケーションを構築するのに役立つ素晴らしいサンプルとスターターキットがたくさんあります。

### VS Code React Sample

これは、[demo](https://channel9.msdn.com/events/Build/2017/T6078) に使用されている [sample](https://github.com/Microsoft/vscode-react-sample) Reactアプリケーションです。今年のビルドカンファレンスで。このサンプルでは簡単なTODOアプリケーションが作成され、Node.js [Express](https://expressjs.com/) サーバーのソースコードが含まれています。また、[Babel](https://babeljs.io) ES6 トランスペレーターを使用し、 [webpack](https://webpack.js.org/) を使用してサイト資産をバンドルする方法も示しています。

### MERN スターター

完全なMERN(MongoDB、Express、React、Node.js) スタックの例を見たい場合は、[MERN Starter](http://mern.io/) を見てください。 [MongoDB](https://docs.mongodb.com/v3.0/installation/) をインストールして起動する必要がありますが、すぐに MERN アプリケーションが実行されます。 [vscode-recipes](https://github.com/weinand/vscode-recipes/tree/master/MERN-Starter) には、 Node.js サーバーのデバッグの設定に関する詳細なVSコード固有のドキュメントがあります。

### TypeScript React

If you're curious about TypeScript and React, you can also create a TypeScript version of the `create-react-app` application. See the details at [TypeScript-React-Starter](https://github.com/Microsoft/TypeScript-React-Starter) on the [TypeScript Quick Start](http://www.typescriptlang.org/samples/index.html) site.