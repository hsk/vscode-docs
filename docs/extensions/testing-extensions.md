---
Order: 12
Area: extensions
TOCTitle: Testing Extensions
ContentId: 2447F8EB-15F1-4279-B621-126C7B8EBF4B
PageTitle: Testing Visual Studio Code Extensions
DateApproved: 5/4/2017
MetaDescription: It is easy to write tests for your Visual Studio Code extension (plug-in).  The Yo Code extension generator scaffolds the necessary settings to run and debug your extension tests directly in Visual Studio Code.
---
# エクステンションをテストする

VS Code は、 VS Code API を必要とする拡張機能の実行テストとデバッグテストをサポートします。これらのテストは、 VS Code の特別なインスタンスである「拡張開発ホスト」内で実行され、完全な API にアクセスできます。これらのテストは、 VS Code ウィンドウから分離して実行できる単体テストを超えているため、これらのテストは統合テストと呼ばれます。このドキュメントでは、 VS Code の統合テストに焦点を当てています。単体テストでは、 [Mocha](https://mochajs.org/) や [Jasmine](https://jasmine.github.io/) のような一般的なテストフレームワークを使用できます。

## Yoコードテスト足場

基本的な [yo code generator](/docs/extensions/yocode.md) 拡張プロジェクトには、サンプルテストとそれを実行するのに必要なインフラストラクチャが含まれています。

**注**: 以下のドキュメントでは、 TypeScript 拡張機能を作成したと仮定していますが、 JavaScript 拡張機能にも同じことが適用されます。ただし、一部のファイル名が異なる場合があります。

新しいエクステンションを作成して VS Code でプロジェクトを開いたら、デバッグビューの上部にあるドロップダウンから `Launch Tests` 設定を選択することができます。

![launch tests](images/testing-extensions/launch-tests.png)

この設定を選択すると、 `Debug：Start`(` kb(workbench.action.debug.start) `)を実行すると、 VS Code は` Extension Development Host`インスタンスであなたの拡張を起動し、テストを実行します。テスト出力はデバッグコンソールに送られ、テスト結果が表示されます。

![test output](images/testing-extensions/test-output.png)

生成されたテストでは、テストランナーとライブラリ用に [Mocha test framework](https://mochajs.org/) を使用します。

拡張プロジェクトには、 `test` フォルダがあります。このフォルダには、Mochaテストランナーの設定を定義する `index.ts` ファイルと、 `Something 1`テストの例を持つ `extension.test.ts` が含まれています。通常は `index.ts` をそのままにしておくことができますが、モカの設定を変更するために変更することができます。

```
├── test
│   ├── extension.test.ts
│   └── index.ts
```

`test` フォルダーの下に `test.ts` ファイルをさらに作成することができます。自動的に (out/testに) ビルドされ実行されます。テストランナーは `*.test.ts` という名前パターンと一致するファイルのみを考慮します。

## Launch Tests の設定

`Launch Tests` 設定は、プロジェクトの `.vscode\launch.json` ファイルで定義されています。コンパイルされたテストファイルを指す `--extensionTestsPath` 引数(これは TypeScript プロジェクトであると仮定します)を追加した `Launch Extension` の設定と似ています。

```json
{
    "name": "Launch Tests",
    "type": "extensionHost",
    "request": "launch",
    "runtimeExecutable": "${execPath}",
    "args": ["--extensionDevelopmentPath=${workspaceRoot}", "--extensionTestsPath=${workspaceRoot}/out/test" ],
    "stopOnEntry": false,
    "sourceMaps": true,
    "outFiles": ["${workspaceRoot}/out/test/**/*.js"],
    "preLaunchTask": "npm"
}
```

## Extension Development Host への引数の受け渡し

起動インスタンスの引数リストの先頭にパスを挿入して、テストインスタンスが開くファイルまたはフォルダを設定できます。

```json
"args": ["file or folder name", "--extensionDevelopmentPath=${workspaceRoot}", "--extensionTestsPath=${workspaceRoot}/out/test" ],
```

この方法で、予測可能なコンテンツとフォルダ構造でテストを実行できます。

## 拡張パッケージからのテストファイルの除外

あなたがあなたのエクステンションを共有することを決めた場合、エクステンションパッケージにテストを含めたくないかもしれません。 [`.vscodeignore`](/docs/extensions/publish-extension.md#advance-usage) ファイルを使用すると、[`vsce`公開ツール](/docs/extensions/publish-extension.md) を使って拡張機能をパッケージ化し公開する際にテストファイルを除外できます。デフォルトでは、 `yo code` 生成された拡張プロジェクトは `test` と `out/test` フォルダを除外します。

```
out/test/**
test/**
```

## Travis CI ビルドマシンで自動的にテストを実行する

[Travis CI](https://travis-ci.org) のようなビルドマシンで自動的に拡張テストを実行できます。

自動拡張テストを有効にするために、 `vscode` npm モジュールは以下のテストコマンドを提供します：

* VS Code をダウンロードして解凍する
* VS Code 内で拡張テストを開始する
* 結果をコンソールに出力し、テストの成功または失敗に応じて終了コードを返します

このテストコマンドを有効にするには、 `package.json` を開き、 `scripts` セクションに次のエントリを追加します:

```json
"test": "node ./node_modules/vscode/bin/test"
```

Travis CI を最上位の `.travis.yml` 設定で簡単に有効にすることができます:

```yml
sudo: false

os:
  - osx
  - linux

before_install:
  - if [ $TRAVIS_OS_NAME == "linux" ]; then
      export CXX="g++-4.9" CC="gcc-4.9" DISPLAY=:99.0;
      sh -e /etc/init.d/xvfb start;
      sleep 3;
    fi

install:
  - npm install
  - npm run vscode:prepublish

script:
  - npm test --silent
```

上記のスクリプトは、 Linux と Mac の両方でテストを実行します。 Linux でテストを実行するには、
前述の `before_install` 設定を使用して、 Linux がビルドから VS Code を開始できるようにします。

テストランナーを設定するためのいくつかのオプションの環境変数があります:

|名前|説明|
| ------------|-------------------|
| `CODE_VERSION`         | テストを実行するための VS Code のバージョン (例: `0.10.10`) |
| `CODE_DOWNLOAD_URL`    | テストを実行するために使用する VS Code ドロップの完全な URL |
| `CODE_TESTS_PATH`      | 実行するテストの場所 |
| `CODE_TESTS_WORKSPACE` | テストインスタンスのために開くワークスペースの場所 |

## AppVeyor で Windows 上でテストを実行する

[AppVeyor](https://www.appveyor.com/) でWindows上で拡張テストを実行することもできます。開始取得するには、 VS Code 統合テストAppVeyor [設定ファイル](https://github.com/Microsoft/vscode/blob/master/appveyor.yml) を確認することができます。

## 次のステップ

* [あなたの拡張デバッグ](/docs/extensions/debugging-extensions.md) - あなたの拡張機能を実行してデバッグする方法については、こちらをご覧ください
* [VSCE](/docs/extensions/publish-extension.md) - VSCEコマンドラインツールを使用して拡張機能を公開します。
* [拡張マニフェストファイル](/docs/extensionAPI/extension-manifest.md) - VS Code 拡張マニフェストファイル参照
* [Extension API](/docs/extensionAPI/overview.md) -  VS Code 拡張 API の詳細
