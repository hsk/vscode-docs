---
Order: 28
TOCTitle: Build 2017 Demo
PageTitle: Build 2017 Demo
MetaDescription: Build 2017 Demo Visual Studio Code - Conquering the Cloud with an editor and a CLI
Date: 2017-05-10
ShortDescription: Build 2017 Demo Visual Studio Code - Conquering the Cloud with an editor and a CLI
Author: Chris Dias
---
# Build 2017 デモ

2017年5月10日 Chris Dias、 [@chrisdias](https://twitter.com/chrisdias)

## ビデオ​​を見る！

[Visual Studioコード:エディタとCLIを使用してクラウドを征服する](https://channel9.msdn.com/Events/Build/2017/B8094)

以下は、 Build 2017 VS Code のトークで示されたサンプル、 ツール、 拡張機能へのリンクです。

## 役に立つリンク

* [設定レシピのデバッグ](https://github.com/weinand/vscode-recipes)
* [Dockerマルチステージビルド](https://codefresh.io/blog/node_docker_multistage/)

## 拡張機能

### ツール

* [NPM(ノードパッケージマネージャ)サポート](https://marketplace.visualstudio.com/items?itemName=eg2.vscode-npm-script) は、 VS Code 内からの npm install および npm uninstall コマンドの実行をサポートしています。

* [HTMLタグの自動クローズ](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag) は、 HTML と XML の終了タグを自動的に追加します。

* [CSS IntelliSense(Completions)](https://marketplace.visualstudio.com/items?itemName=Zignd.html-css-class-completion) は、 HTML クラス属性の CSS クラス名補完を提供します。 ワークスペース、 React の `className` アトリビュートがあります。

### Angular

* [Angular Language Service](https://marketplace.visualstudio.com/items?itemName=Angular.ng-template) は、 コンプリートリスト、 AOT 診断メッセージ、 迅速なインラインテンプレートと外部テンプレートの両方を含む、 Angular テンプレートの豊富な編集エクスペリエンスを提供します情報、 さらには定義に移動することもできます。

### デバッグ

* [Chrome Debugger](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) では、 Google Chrome ブラウザや Chrome デバッギングプロトコルをサポートする他のターゲットで実行されている JavaScript コードをデバッグできます。

### Linter

* [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint) は、TypeScript 言語用の [tslint](https://github.com/palantir/tslint) linter を VS Code に統合します。

* [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) には、 [ESLint](http://eslint.org/) (JavaScript および JavaScript React のプラグイン可能なユーティリティー JSX) を VS Code に変換します。

### NoSQL MongoDB

* [MongoDB Extension](https://code.visualstudio.com/demo/vscode-mongodb-0.0.1.vsix) **プレビュー** この拡張機能は非常に早期のプレビューであり、 VS Code で提案されている API を利用していますが、まだリリースされていせん。 その結果、この拡張機能は [Insiders](https://code.visualstudio.com/insiders) ビルドでのみ実行され、 コマンドラインから有効にする必要があります。 インストールするには:

  * 拡張機能をインストールする:
  
  ``` bash
  code-insiders --install-extension vscode-mongodb-0.0.1.vsix
  ```
  * 提案された API を使用する拡張機能を有効にして code-insiders をロードする:
  
  ``` bash
  code-insiders --enable-proposed-api ms-vscode.vscode-mongodb
  ```

### マイクロサービス

* [Docker Tools for VS Code](https://marketplace.visualstudio.com/items?itemName=PeterJausovec.vscode-docker) は、 Docker コンテナを使用したコンテナ化されたマイクロサービスベースのアプリケーションの開発と展開を容易にします。

### Azure拡張

**注:** あなたが Azure のサブスクリプションをお持ちでない場合、 30日間 **無料** で [登録](https://azure.microsoft.com/en-us/free/?b=16.48) して、 Azure サービスの任意の組み合わせを試用するには、 Azure クレジットで **$ 200** を取得してください。

* [Azure CLI](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azurecli) は、 VS Code 内で [Azure CLI 2.0](https://aka.ms/GetTheAzureCLI)を豊富な編集エクスペリエンスでラップします。
