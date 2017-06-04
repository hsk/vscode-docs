---
Order: 4
Area: extensionapi
TOCTitle: Extension Manifest
ContentId: C4F184A5-A804-4B0B-9EBA-AFE83B88EE49
PageTitle: Visual Studio Code Extension Manifest File - package.json
DateApproved: 5/4/2017
MetaDescription: At the core of Visual Studio Code's extensibility model is an extension (plug-in) manifest file where your extension declares its extension type(s), activation rules and runtime resources.
---
# 拡張マニフェストファイル - package.json

すべての Visual Studio コード拡張には、拡張ディレクトリ構造のルートにマニフェストファイル `package.json` が必要です。

## フィールド

名前|必須|タイプ|詳細
---- |:--------:| ---- | -------
`name`| Y | `string` | 拡張子の名前 - すべてスペースでスペースを入れずに小文字にする必要があります。
`version`| Y | `string` | [SemVer](http://semver.org/) 互換バージョン。
`publisher` | Y | `string` | [発行者名](/docs/extensions/publish-extension.md#publishers-and-personal-access-tokens)
`engines` | Y | `object` | オブジェクト拡張子が互換性のあるVSコードのバージョンと一致する少なくとも vscode キーを含むオブジェクト。 `*` にすることはできません。 例: `^0.10.5` は最小VSコードバージョンの `0.10.5` との互換性を示します。
`license` | | `string` | [npmのドキュメント](https://docs.npmjs.com/files/package.json#license) を参照してください。あなたの拡張のルートに `LICENSE` ファイルがある場合、`license` の値は `"SEE LICENSE IN <filename>"` でなければなりません。
`displayName` | | `string`| マーケットプレイスで使用される拡張機能の表示名。
`description` | | `string` | あなたの拡張機能が何であるかについての短い説明。
`categories` | | `string[]` | `[Languages, Snippets, Linters, Themes, Debuggers, Formatters, Keymaps, Other, Extension Packs]`
`keywords` | | `array` | 拡張機能を簡単に見つけるための**キーワード**または**タグ**の配列。
`galleryBanner` | | `object` |オブジェクトMarketplaceヘッダーのフォーマットをあなたのアイコンに合わせるのに役立ちます。以下の詳細を参照してください。
`preview` | | `boolean` | マーケットプレースのプレビューとしてフラグを立てるように設定します。
`main` | | `string` | あなたの内線番号のエントリポイント。
[`contributes`](/​​docs/extensionAPI/extension-points.md) | | `object` |オブジェクト拡張機能の [contributions](/docs/extensionAPI/extension-points.md) を記述するオブジェクト。
[`activationEvents`](/docs/extensionAPI/activation-events.md) | | `array` | この拡張モジュールの [activation events](/docs/extensionAPI/activation-events.md) の配列。
`badges` | | | Marketplaceの拡張ページのサイドバーに表示するバッジの配列。各バッジは、バッジの画像URLを表す「url」、バッジをクリックしたときに表示されるリンクの「href」、「description」の3つのプロパティを含むオブジェクトです。
`markdown` | | `string` | Marketplaceで使用されるMarkdownレンダリングエンジンを制御します。 `github`（デフォルト）または` standard`です。
`dependencies` | | |オブジェクト拡張機能に必要な実行時Node.js依存関係。 [npmの `dependencies`]（https://docs.npmjs.com/files/package.json#dependencies）とまったく同じです。
`devDependencies` | | |オブジェクト拡張が必要とする開発Node.js依存関係。正確に[npmの `devDependencies`](https://docs.npmjs.com/files/package.json#devdependencies)と同じです。
`extensionDependencies` | | |この拡張が依存する拡張のIDを持つ配列。これらのその他の拡張機能は、プライマリ拡張機能のインストール時にインストールされます。拡張子のIDは常に `$ {publisher}。$ {name}`です。たとえば、 `vscode.csharp`です。
`scripts` | | |オブジェクト正確に[npmの `scripts`]（https://docs.npmjs.com/misc/scripts）と同じですが、[追加のVSコード固有のフィールド]（/ docs / extensions / publish-extension.md＃pre-publish-ステップ）。
`icon` | `string` | 128x128ピクセルのアイコンへのパス。

また、 [npm の `package.json`リファレンス](https://docs.npmjs.com/files/package.json) もチェックしてください。

## 例

ここには完全な `package.json` があります

```json
{
    "name": "spell",
    "displayName": "Spelling and Grammar Checker",
    "description": "Detect mistakes as you type and suggest fixes - great for Markdown.",
    "icon": "images/spellIcon.svg",
    "version": "0.0.19",
    "publisher": "seanmcbreen",
    "galleryBanner": {
        "color": "#0000FF",
        "theme": "dark"
    },
    "license": "SEE LICENSE IN LICENSE.md",
    "bugs": {
        "url": "https://github.com/Microsoft/vscode-spell-check/issues",
        "email": "smcbreen@microsoft.com"
    },
    "homepage": "https://github.com/Microsoft/vscode-spell-check/blob/master/README.md",
    "repository": {
        "type": "git",
        "url": "https://github.com/Microsoft/vscode-spell-check.git"
    },
    "categories": [
        "Linters", "Languages", "Other"
    ],
    "engines": {
        "vscode": "^1.0.0"
    },
    "main": "./out/extension",
    "activationEvents": [
        "onLanguage:markdown"
    ],
    "contributes": {
        "commands": [
            {
                "command": "Spell.suggestFix",
                "title": "Spell Checker Suggestions"
            }
        ],
        "keybindings": [
            {
                "command": "Spell.suggestFix",
                "key": "Alt+."
            }
        ]
    },
    "badges": [
        {
            "url": "https://david-dm.org/Microsoft/vscode-spell-check.svg",
            "href": "https://david-dm.org/Microsoft/vscode-spell-check",
            "description": "Dependency Status"
        }
    ],
    "scripts": {
        "vscode:prepublish": "tsc -p ./",
        "compile": "tsc -watch -p ./"
    },
    "dependencies": {
        "teacher": "^0.0.1"
    },
    "devDependencies": {
        "vscode": "^1.0.0"
    }
}
```

## 市場プレゼンテーションのヒント

[VSコードマーケットプレイス](https://marketplace.visualstudio.com/VSCode) に表示されると、拡張機能を見栄えよくするためのヒントと推奨事項があります。

常に最新の `vsce` を使用して、`npm install -g vsce` を使用してください。

あなたの拡張機能のルートフォルダに `README.md` マークダウンファイルを置き、その内容を (Marketplace上の) 拡張機能の本文に含めます。 `REAMDE.md` に相対パス画像リンクを提供することができます。

いくつかの例があります:

1. [スペルチェッカー](https://marketplace.visualstudio.com/items/seanmcbreen.Spell)
2. [MD Tools](https://marketplace.visualstudio.com/items/seanmcbreen.MDTools)


適切な表示名と説明を入力します。これはマーケットプレイスや製品のディスプレイで重要です。これらの文字列は、VSコードのテキスト検索にも使用され、関連するキーワードを使用すると多くの役に立ちます。

```json
    "displayName": "Spelling and Grammar Checker",
    "description": "Detect mistakes as you type and suggest fixes - great for Markdown.",
```

Marketplace ページのヘッダーには、アイコンと対照的なバナー色がよく見えます。 `theme` 属性は、バナーで使用されるフォント、`dark` または `light` を指します。

```json
    "icon": "images/spellIcon.svg",
    "galleryBanner": {
        "color": "#5c2d91",
        "theme": "dark"
    },
```

オプションのリンク (`bugs`、` homepage`、 `repository`) があり、これは Marketplace の **Resources** セクションの下に表示されます。

```json
    "license": "SEE LICENSE IN LICENSE.md",
    "bugs": {
        "url": "https://github.com/Microsoft/vscode-spell-check/issues"
    },
    "homepage": "https://github.com/Microsoft/vscode-spell-check/blob/master/README.md",
    "repository": {
        "type": "git",
        "url": "https://github.com/Microsoft/vscode-spell-check.git"
    }
```

マーケットプレースのリソースリンク | package.json 属性
----------------- | -----------------------
問題 | `bug:url`
リポジトリ  | `repository:url`
ホームページ | `homepage`
ライセンス | `license`

あなたの拡張のための `category` を設定してください。同じ `category` 内の拡張子は、フィルタリングと発見を改善するマーケットプレイスにまとめられています。

> **注:** あなたの拡張機能に合った値だけを使用してください - 許される値は `[Languages, Snippets, Linters, Themes, Debuggers, Formatters, Keymaps, Other, Extension Packs]` です。

```json
    "categories": [
        "Linters", "Languages", "Other"
    ],
```

> **ヒント：** [拡張マニフェストエディタ](https://marketplace.visualstudio.com/items?itemName=ms-devlabs.extension-manifest-editor) 拡張機能を使用すると、拡張子 `README.md` のプレビューが可能です。 `package.json` メタデータは Marketplace に公開されたときに表示されます。

## 拡張機能提供の結合

`yo code` ジェネレータを使うと、 TextMate のテーマ、色分け、スニペットを簡単にパッケージ化し、新しい拡張機能を作成することができます。ジェネレータが実行されると、オプションごとに完全なスタンドアロンの拡張パッケージが作成されます。しかし、複数の貢献を組み合わせた単一の拡張を持つ方がしばしば便利です。たとえば、新しい言語のサポートを追加する場合は、ユーザーに色付けとスニペット、さらにはデバッグサポートの両方の言語定義を提供したいと考えています。

拡張貢献を組み合わせるには、既存の拡張マニフェスト `package.json` を編集し、新しい貢献と関連ファイルを追加します。

以下は、 LaTex 言語定義 (言語識別子とファイル拡張子)、カラー化（`grammar`）、スニペットを含む拡張マニフェストです。

```json
{
    "name": "language-latex",
    "description": "LaTex Language Support",
    "version": "0.0.1",
    "publisher": "someone",
    "engines": {
        "vscode": "0.10.x"
    },
    "categories": [
        "Languages",
        "Snippets"
    ],
    "contributes": {
        "languages": [{
            "id": "latex",
            "aliases": ["LaTeX", "latex"],
            "extensions": [".tex"]
        }],
        "grammars": [{
            "language": "latex",
            "scopeName": "text.tex.latex",
            "path": "./syntaxes/latex.tmLanguage"
        }],
        "snippets": [{
            "language": "latex",
            "path": "./snippets/snippets.json"
        }]
    }
}
```

拡張マニフェストの `categories` 属性は Marketplace 上の簡単な発見とフィルタリングのために `Languages` と `Snippets` の両方を含んでいることに注目してください。

> **ヒント:** あなたのマージされた貢献が同じ識別子を使用していることを確認してください。 上記の例では、3つすべての寄稿は言語識別子として "latex" を使用しています。 これにより、VS Code は、Colorizer (`grammar`) とスニペットが LaTeX 言語用であり、 LaTeX ファイルを編集するときにアクティブになることを知ることができます。

##エクステンションパック

別々のエクステンションを「エクステンションパック」にまとめてバンドルすることもできます。拡張パックは、一緒にインストールできる拡張機能のセットです。これにより、お気に入りのエクステンションを他のユーザと簡単に共有したり、PHP開発のような特定のシナリオ用の拡張セットを作成して、PHP開発者がVSコードをすばやく使い始める手助けをすることができます。

エクステンションパックには他の投稿を含めることができます。 この依存関係は `package.json` ファイル内の `extensionDependencies` 属性を使って表現されます。

たとえば、PHP用のExtension Packには、デバッガ、言語サービス、およびフォーマッタが含まれています。

```json
  "extensionDependencies": [
      "felixfbecker.php-debug",
      "felixfbecker.php-intellisense",
      "Kasik96.format-php"
  ]
```

Extension Pack をインストールすると、 VS Code はその拡張機能の依存関係もインストールされるようになりました。

エクステンションパックは、 `Extension Packs` マーケットカテゴリに分類する必要があります。

```json
  "categories": [
      "Extension Packs"
  ],
```

拡張パックを作成するには、 `yo code` Yeoman ジェネレータを使用します。オプションで、 VS Code インスタンスに現在インストールされている拡張機能のセットをパックにシードすることもできます。このようにして、お気に入りの拡張機能で Extension Pack を簡単に作成し、 Marketplace に公開し、他のユーザーと共有することができます。

##有用なノードモジュール

npmj にはいくつかの Node.js モジュールがあり、 VSCode 拡張機能の作成に役立ちます。拡張機能の `dependencies` セクションにこれらを含めることができます。

* [vscode-nls](https://www.npmjs.com/package/vscode-nls) - 外部化とローカリゼーションのサポート。
* [vscode-uri](https://www.npmjs.com/package/vscode-uri) - VSコードとその拡張機能で使用される URI の実装。
* [jsonc-parser](https://www.npmjs.com/package/jsonc-parser) - コメントの有無に関わらず JSON を処理するためのスキャナとフォールトトレラントなパーサー。
* [request-light](https://www.npmjs.com/package/request-light) - 軽量 Node.js リクエストライブラリ（プロキシサポートあり）
* [vscode-extension-telemetry](https://www.npmjs.com/package/vscode-extension-telemetry) - VSコード拡張の一貫したテレメトリレポート。
* [vscode-languageclient](https://www.npmjs.com/package/vscode-languageclient) - [言語サーバープロトコル](https://github.com/Microsoft/language-server) に準拠した言語サーバーを簡単に統合する-プロトコル)。

## 次のステップ

VS Code の拡張性モデルの詳細については、 次のトピックを参照してください。

* [提供ポイント](/docs/extensionAPI/extension-points.md) - VS Code 提供ポイントリファレンス
* [Activation Events](/docs/extensionAPI/activation-events.md) - VS Code アクティベーションイベントリファレンス
* [Extension Marketplace](/docs/editor/extension-gallery.md) - VS Code 拡張マーケットプレイスの詳細
