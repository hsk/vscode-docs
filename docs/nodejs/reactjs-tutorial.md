---
Order: 
Area: nodejs
TOCTitle: React Tutorial
ContentId: 2dd2eeff-2eb3-4a0c-a59d-ea9a0b10c468
PageTitle: React JavaScript Tutorial in VS Code
DateApproved: 3/10/2017
MetaDescription: React JavaScript tutorial showing IntelliSense, debugging, and code navigation support in Visual Studio Code.
MetaSocialImage: nodejs_javascript_vscode.png
---
# VS Code で React チュートリアル
# React Tutorial in VS Code

[React](https://facebook.github.io/react/).js は、 Facebook によって開発された Web アプリケーションのユーザーインターフェイスを構築するための人気のある JavaScript ライブラリです。
VS Code は React.js IntelliSense と box 外のコードナビゲーションをサポートしています。

## Hello World

このチュートリアルでは、 `create-react-app` [generator](https://facebook.github.io/react/docs/installation.html#creating-a-new-application) を使用します。 React アプリケーションサーバーを実行するだけでなくジェネレータをインストールして使用するには、[Node.js](https://nodejs.org/) JavaScriptランタイムと [npm](https://www.npm.js.com/) (Node.js パッケージマネージャ) がインストールされていることが必要です。 Node.js は [here]（https://nodejs.org/en/download/）からインストールでき、 npm も含まれています。

> **ヒント**: Node.js と npm がマシンに正しくインストールされていることをテストするには、 `node --version` と ` npm --version` と入力します。

`create-react-app` ジェネレータをインストールするには、端末またはコマンドプロンプトで次のように入力します。

```bash
npm install -g create-react-app
```

インストールには数分かかることがあります。次のように入力して、新しい React アプリケーションを作成できるようになりました:

```bash
create-react-app my-app
```

ここで `my-app` はアプリケーションのフォルダ名です。 React アプリケーションを作成して依存関係をインストールするには、これも数分かかることがあります。

新しいフォルダに移動し、 `npm start` と入力して Web サーバを起動し、ブラウザでアプリケーションを開くことで React アプリケーションをすぐに実行しましょう:

```bash
cd my-app
npm start
```

ブラウザーの `http://localhost:3000` に "Welcome to React" と表示されるはずです。 私たちは VS Code でアプリケーションを見ている間、Webサーバーを実行したままにしておきます。

![welcome to react](images/reactjs/welcome-to-react.png)

React アプリケーションを VS Code で開くには、別のターミナル（またはコマンドプロンプト）を開き、 `my-app` フォルダに移動して `code .` をタイプします:

```bash
cd my-app
code .
```

### マークダウンプレビュー
### Markdown Preview

ファイルエクスプローラのファイルには、 `README.md` というアプリケーションがあります。これには、アプリケーションと React に関する一般的な情報がたくさんあります。 README を確認するには、 VS Code Markdown Preview を使用する方法があります。 現在のエディタグループ（**Markdown: 開くプレビュー** `kb(markdown.showPreview)`) または新しいエディタグループ（**Markdown: サイドにプレビューを開く** `kb(markdown.showPreviewToSide)`) でプレビューを開くことができます 。ヘッダーへのハイパーリンクのナビゲーションや、コードブロック内の構文のハイライト表示が得られます。

![README markdown preview](images/reactjs/markdown-preview.png)

### シンタックスハイライトとブラケットマッチング
### Syntax highlighting and bracket matching

Now open the `src` folder and select the `index.js` file. You'll notice that VS Code has syntax highlighting of the various source code elements and if you put the cursor on a parentheses, the matching bracket is also selected.

![react bracket matching](images/reactjs/bracket-matching.png)

### IntelliSense

As you start typing in `index.js`, you'll see smart suggestions or completions.

![react suggestions](images/reactjs/suggestions.png)

After you select a suggestion and type `.`, you see the types and methods on the object through IntelliSense.

![react intellisense](images/reactjs/intellisense.png)

VS Code uses the TypeScript language service for it's JavaScript code intelligence and it has a feature called Automatic Type Acquisition (ATA) which pulls down the npm Type Definition files (`*.d.ts`) for the npm modules referenced in the `package.json`.

If you select a method, you'll also get parameter help:

![react parameter help](images/reactjs/parameter-help.png)

### Go to Definition, Peek definition

Through the TypeScript language service, VS Code can also provide type definition information in the editor through **Go to Definition** (`kb(editor.action.gotodeclaration)`) or ** and **Peek Defintion** (`kb(editor.action.peekImplementation)`). Put the cursor over the `App`, right click and select **Peek Definition**. A Peek window with open showing the `App` definition from `App.js`.

![react peek definition](images/reactjs/peek-definition.png)

Press `kbstyle(Escape)` to close the Peek window.

### Hello World!

Let's update the sample application to "Hello World!". Add the link to declare a new H1 header and replace the `<App />` tag in `ReactDOM.render` with `element'.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import './index.css';

var element = React.createElement('h1', {className: 'greeting'}, 'Hello, world!');
ReactDOM.render(element, document.getElementById('root'));
registerServiceWorker();
```

Once you save the `index.js`, the running instance of the server will update the web page and you'll see "Hello World!".

![hello world](images/reactjs/hello-world.png)

## Hello World をデバッグする
## Debug Hello World

To debug the client side React code, we'll need to install the [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) extension.

>Note: This tutorial assumes you have the Chrome browser installed. The builders of the Debugger for Chrome extension also have versions for the [Safari on iOS(https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-ios-web) and [Edge](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-edge) browsers.

Open the Extensions view (`kb(workbench.view.showExtensions)`) and type 'chrome` in the search box. You'll see several extension which reference Chrome. 

![debugger for chrome](images/reactjs/debugger-for-chrome.png)

Press the **Install** button for **Debugger for Chrome**. The button will change to **Installing** then **Reload**. Press **Reload** to restart VS Code and activate the extension.

### Set a breakpoint

To set a breakpoint in `index.js`, click on the gutter to the left of the line numbers. This will set a breakpoint which will be visible as a red circle.

![set a breakpoint](images/reactjs/breakpoint.png)

## Configure the Chrome debugger

We need to initially configure the debugger. To do so, go to the Debug view (`kb(workbench.view.debug)`)

Configuration

shutdown localhost:3000, F5, refresh

## Linting

デフォルトで js エラーを取得する

```bash
npm install -g eslint
```

## [Popular Starter Kit]
## [人気スターターキット]
