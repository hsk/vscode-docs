---
Order: 9
Area: extensions
TOCTitle: Running and Debugging Extensions
ContentId: 44569A0C-7196-48E6-A5EE-FC5AAAAD32F3
PageTitle: Running and Debugging your Visual Studio Code Extension
DateApproved: 5/4/2017
MetaDescription: It is easy to debug and test your Visual Studio Code extension (plug-in).  The Yo Code extension generator scaffolds the necessary settings to run and debug your extension directly in Visual Studio Code.
---

# 1 エクステンションの実行とデバッグ

  VS Code を使用して VS Code の拡張機能を開発することができ、 VS Code は拡張機能開発を簡素化するいくつかのツールを提供します。

  * 拡張を scaffold する Yeoman ジェネレータ
  * 拡張APIの IntelliSense、ホバー、コードナビゲーション
  * TypeScript のコンパイル (TypeScriptで拡張を実装する場合)
  * 拡張機能の実行とデバッグ
  * エクステンションの公開

## 2 エクステンションの作成

  基本ファイルを scaffold で作成して拡張機能の開発を始めることをお勧めします。 `yo code` Yeoman ジェネレータを使ってこの捜査ができ、 私たちは [拡張ジェネレータ](/docs/extensions/yocode.md) トピックの詳細をカバーします。 ジェネレータはすべてがセットアップされていることを保証し、開発経験が豊富です。

## 3 エクステンションの実行とデバッグ

`F5` を押すと、デバッガの下でエクステンションを簡単に実行することができます。 拡張機能がロードされた新しい VS Code ウィンドウが開きます。 拡張モジュールの出力は `Debug Console` に表示されます。 ブレークポイントを設定し、コードをステップ実行し、 `Debug` ビューまたは `Debug Console` で変数を検査することができます。

![Debugging extensions](images/debugging-extensions/debug.png)

舞台裏で何が起こっているのかを見てみましょう。 TypeScript に拡張機能を書く場合は、コードを JavaScript にコンパイルする必要があります。

## 4 TypeScript をコンパイルする

TypeScript のコンパイルは、生成された拡張で次のように設定されます。

* `tsconfig.json` は、 TypeScript コンパイラのコンパイルオプションを定義します。 詳細については、[TypeScript wiki](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html) または [TypeScript言語セクション](/docs/languages/typescript.md#tsconfigjson)。
* 適切なバージョンの TypeScript コンパイラが node_modules フォルダ内に含まれています。
* API 定義は `node_modules/vscode` に含まれています。

拡張機能を実行する前に TypeScript のコンパイルがトリガーされます。 これは `preLaunchTask` 属性で定義されています。
デバッグセッションを開始する前に実行するタスクを宣言する `.vscode/launch.json` ファイルです。 タスクは `.vscode/ tasks.json` ファイルの中で定義されます。

> **注:** TypeScript コンパイラは時計モードで起動されるため、変更を加えるとファイルがコンパイルされます。

## 5 エクステンションを起動する

あなたの拡張機能は、 `Extension Development Host` というタイトルの新しいウィンドウで起動されます。 このウィンドウは、 VS Code を実行するか、より正確には拡張機能を使用して開発中の拡張ホストを実行します。

`extensionDevelopmentPath` オプションを使用してコマンドラインからも同じことができます。 このオプションは VS Code に
拡張子を探すべき他の場所、例えば、

>`code --extensionDevelopmentPath=_my_extension_folder`.

エクステンションホストが起動すると、 VS Code はデバッガをアタッチしてデバッグセッションを開始します。

これは `F5` を押すと起こります：

  1. `.vscode/launch.json` は `npm` という名前のタスクを最初に実行するよう指示します。
  2. `.vscode/tasks.json` はタスク `npm` を `npm run compile` のシェルコマンドとして定義します。
  3. `package.json` はスクリプト `compile` を `tsc -watch -p ./` として定義します。
  これにより、最終的に node_modules に含まれる TypeScript コンパイラが呼び出され、 `out/src/extension.js` と ` out/src/extension.js.map` が生成されます。
  5. TypeScriptのコンパイルタスクが終了すると、 `code --extensionDevelopmentPath=${workspaceRoot}` プロセスが生成されます。
  6. VSコードの2番目のインスタンスは特殊モードで起動され、 `${workspaceRoot}` で拡張子を検索します。

## 6 エクステンションの変更と再読み込み

TypeScript コンパイラは watch モードで実行されるため、変更を加えると TypeScript ファイルが自動的にコンパイルされます。
コンパイルの進捗状況は、VS Code のステータスバーの左側で確認できます。
ステータスバーには、コンパイルのエラー数と警告数も表示されます。
コンパイルがエラーなしで完了したら、 `Extension Development Host` を再ロードして、変更が反映されるようにする必要があります。
これを行うには2つの選択肢があります：

* debug restart アクションをクリックして、拡張開発ホストウィンドウを再起動します。
* 拡張開発ホストウィンドウで `kbstyle(Ctrl+R)` (Mac: `kbstyle(Cmd+R)`) を押します。

## 7 次のステップ

* [拡張機能のテスト](/docs/extensions/testing-extensions.md) - 拡張機能のユニットテストと統合テストの作成方法を学ぶ
* [公開ツール](/docs/extensions/publish-extension.md) - vsce コマンドラインツールで拡張機能を公開します。
* [拡張マニフェストファイル](/docs/extensionAPI/extension-manifest.md) - VS Code 拡張マニフェストファイルリファレンス
* [Extension API](/docs/extensionAPI/overview.md) - VS Code 拡張 API の詳細

## 8 よくある質問

**Q: VS Code の新しいリリースで導入された拡張機能から API を使用するにはどうしたらいいですか？**

**A:** エクステンションがVSコードの新しいリリースで導入された API を使用している場合は、この依存関係をエクステンションの `package.json` ファイルの `engines` フィールドに宣言する必要があります。

手順は次のとおりです:

* あなたの拡張モジュールが `package.json` の `engine` フィールドに必要とする VS Code の最小バージョンを設定します。
* `vscode` モジュールの devDependency が少なくとも `0.11.0` であることを確認してください。
* `postinstall` スクリプトを `package.json` に以下のように追加してください:

```json
"scripts": {
    "postinstall": "node ./node_modules/vscode/bin/install"
}
```

* あなたの拡張機能のルートから `npm install` と入力してください。
* `vscode` モジュールはあなたが宣言した `engine` フィールドに基づいて `vscode.d.ts` の適切なバージョンをダウンロードします。
* VS Code に戻って、選択した特定のバージョンの API が IntelliSense と検証にどのように表示されるかを確認してください。

