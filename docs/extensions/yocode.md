---
Order: 2
Area: extensions
TOCTitle: Extension Generator
ContentId: C733425A-3F06-4DB9-90A0-472EF1DB58D3
PageTitle: The Yo Code Visual Studio Code Extension Generator
DateApproved: 5/4/2017
MetaDescription: Easily create Visual Studio Code extensions and customizations with the Yo Code generator.
---
# Yo Code - 拡張ジェネレータ

私たちは、 [Yeoman generator](https://github.com/Microsoft/vscode-generator-code) を書いて、あなたの手助けをしています。

## ジェネレータをインストールする

Yeoman と VS Code 拡張機能ジェネレータをコマンドプロンプトからインストールします。

```bash
npm install -g yo generator-code
```

## Yo Code を実行する

Yeoman ジェネレータは、必要な情報のカスタマイズまたは拡張プロンプトを作成するために必要な手順を順を追って説明します。

ジェネレータを起動するには、コマンドプロンプトで次のように入力します。

```bash
yo code
```

![yo code output](images/yocode/yocode.png)

## ジェネレータのオプション

ジェネレータは、新しい拡張機能用の拡張スケルトンを作成するか、既存の TextMate 定義ファイルに基づいて言語、テーマまたはスニペット用のすぐに使用できる拡張機能を作成することができます。

### 新しい拡張機能 (TypeScript)

'hello world' コマンドを実装する拡張スケルトンを作成します。あなた自身の拡張のための出発点としてこれを使用してください。

* 拡張識別子の入力を求め、現在のディレクトリにその名前のフォルダを作成します。
* ソースフォルダ、テストフォルダ、および出力フォルダを含むベースフォルダ構造を作成します。
* `package.json` ファイルと拡張メインファイルをテンプレート化します。
* `launch.json` と `tasks.json` を設定して、 F5 があなたの拡張機能をコンパイルして実行し、デバッガをアタッチするようにします。
* オプションで Git リポジトリを設定します。

作成したら、作成したフォルダで VS Code を開きます。このフォルダには、次の手順のクイックガイドとしてファイル `vsc-extension-quickstart.md` が含まれています。 拡張機能は、拡張 API 用に IntelliSense を入手できるようにセットアップされています。

### 新しい拡張機能 (JavaScript)

`新しい拡張機能(TypeScript)` と同じですが、 JavaScript 用です。 拡張機能は、拡張API用に IntelliSense を入手できるようにセットアップされています。

### 新しい色のテーマ

既存の TextMate カラーテーマに基づいて新しいカラーテーマを作成する拡張機能を作成します。

* 既存のTextMateカラーテーマ (.tmTheme) の場所 (URLまたはファイルパス) を要求します。 このファイルは新しい拡張機能にインポートされます。
* カラーテーマ名とカラーベースのテーマ (明るいまたは暗い) をプロンプトします。
* 拡張識別子の入力を求め、現在のディレクトリにその名前のフォルダを作成します。

作成したら、作成したフォルダで VS Code を開き、拡張機能を実行して新しいテーマをテストします。
`vsc-extension-quickstart.md` をチェックしてください。 それは次のステップでの簡単なガイドです。

### 新しい言語サポート

Colorizer に言語を提供する拡張機能を作成します。

* 既存の TextMate 言語ファイル (.tmLanguage、 .plist、 または .json) の場所 (URLまたはファイルパス) を入力するよう求められます。 このファイルは新しい拡張機能にインポートされます。 新しい文法を開始するには、空の名前を渡すことでこれをスキップできます。
* 拡張識別子の入力を求め、現在のディレクトリにその名前のフォルダを作成します。

作成したら、作成したフォルダで VS Code を開き、拡張を実行して色付けをテストします。 次の手順については、 `vsc-extension-quickstart.md` を参照してください。 作成された言語構成ファイルを見て、その言語がどのようなスタイルやコメントを使用するかなどの構成オプションを定義します。

### 新しいコードスニペット

新しいコードスニペットに貢献する拡張機能を作成します。

* TextMate スニペット (.tmSnippet) または Sublime スニペット (.sublime-snippet) を含むフォルダの場所を入力するように要求します。 これらのファイルは VS Code スニペットファイルに変換されます。
* これらのスニペットがアクティブになる言語を要求します。
* 拡張識別子の入力を求め、現在のディレクトリにその名前のフォルダを作成します。

作成したら、作成したフォルダで VS Code を開き、スニペットをテストするために拡張子を実行します。 次の手順については、 `vsc-extension-quickstart.md` を参照してください。

### 新しい拡張パック

お気に入りの拡張機能で新しい拡張パックを提供する拡張機能を作成します。

* インストールされている拡張機能を拡張パックに追加するかどうかを確認するメッセージが表示されます。
* 拡張識別子の入力を求め、現在のディレクトリにその名前のフォルダを作成します。

拡張パックを公開する前に、 `package.json` ファイルの `extensionDependencies` を見直してください。

作成したら、作成したフォルダで VS Code を開き、拡張機能を実行して拡張機能パックをテストします。 次の手順については、 `vsc-extension-quickstart.md` を参照してください。

## 拡張フォルダ

拡張機能を読み込むには、ファイルを VS Code 拡張フォルダ `.vscode/extensions` にコピーする必要があります。プラットフォームによっては、次のフォルダにあります:

* **Windows** `%USERPROFILE%\.vscode\extensions`
* **Mac** `~/.vscode/extensions`
* **Linux** `~/.vscode/extensions`

VS Code を実行するたびに拡張機能を読み込みたい場合は、プロジェクト ('side loading') を `.vscode/extensions` の下の新しいフォルダにコピーします。 たとえば、 `~/.vscode/extensions/myextension` です。

## 次のステップ

* [公開ツール](/docs/extensions/publish-extension.md) - VS Code Marketplace に拡張機能を公開する方法を学びます。
* [Hello World](/docs/extensions/example-hello-world.md) - 最初の拡張をビルドするための 'Hello World' チュートリアルを試してください。
* [その他の拡張の例](/docs/extensions/samples.md) - 拡張プロジェクトの例をご覧ください。

##よくある質問

**Q: Windows 9で、 `yo code` ジェネレータは矢印キーに反応しません。**

**A:** Yeoman ジェネレータを `yo` だけ起動し、 `Code` ジェネレータを選択してみてください。

![yo workaround](images/yocode/yo-workaround.png)
