---
Order: 5
Area: extensionapi
TOCTitle: Contribution Points
ContentId: 2F27A240-8E36-4CC2-973C-9A1D8069F83F
PageTitle: Visual Studio Code Extension Contribution Points - package.json
DateApproved: 5/4/2017
MetaDescription: To extend Visual Studio Code, your extension (plug-in) declares which of the various contribution points it is using in its package.json extension manifest file.
---
# 提供ポイント - package.json

このドキュメントでは、 [`package.json`拡張マニフェスト](/docs/extensionAPI/extension-manifest.md) で定義されているさまざまな提供ポイントについて説明します。

* [`configuration`](/docs/extensionAPI/extension-points.md#contributesconfiguration)
* [`commands`](/docs/extensionAPI/extension-points.md#contributescommands)
* [`menus`](/docs/extensionAPI/extension-points.md#contributesmenus)
* [`keybindings`](/docs/extensionAPI/extension-points.md#contributeskeybindings)
* [`languages`](/docs/extensionAPI/extension-points.md#contributeslanguages)
* [`debuggers`](/docs/extensionAPI/extension-points.md#contributesdebuggers)
* [`breakpoints`](/docs/extensionAPI/extension-points.md#contributesbreakpoints)
* [`grammars`](/docs/extensionAPI/extension-points.md#contributesgrammars)
* [`themes`](/docs/extensionAPI/extension-points.md#contributesthemes)
* [`snippets`](/docs/extensionAPI/extension-points.md#contributessnippets)
* [`jsonValidation`](/docs/extensionAPI/extension-points.md#contributesjsonvalidation)

## contributes.configuration

ユーザーに公開される設定キーを提供します。 ユーザーは、ユーザー設定またはワークスペース設定からこれらの構成オプションを設定できます。

設定キーを提供すると、これらのキーを記述する JSON スキーマが実際に提供します。 これにより、 VS Code 設定ファイルを作成する際に、ユーザーが優れたツールをサポートできるようになります。

これらの値は、 `vscode.workspace.getConfiguration('myExtension')` を使って拡張機能から読み込むことができます。

### 例

```json
"contributes": {
    "configuration": {
        "type": "object",
        "title": "TypeScript configuration",
        "properties": {
            "typescript.useCodeSnippetsOnMethodSuggest": {
                "type": "boolean",
                "default": false,
                "description": "Complete functions with their parameter signature."
            },
            "typescript.tsdk": {
                "type": ["string", "null"],
                "default": null,
                "description": "Specifies the folder path containing the tsserver and lib*.d.ts files to use."
            }
        }
    }
}
```

![configuration extension point example](images/extension-points/configuration.png)

## contributes.configurationDefaults

既定の言語固有のエディター設定を提供します。 これにより、提供された言語のデフォルトのエディタ設定が上書きされます。

次の例は、 `markdown` 言語のデフォルトのエディタ設定に提供しています:

### 例

```json
contributes": {
    "configurationDefaults": {
        "[markdown]": {
            "editor.wordWrap": "on",
            "editor.quickSuggestions": false
        }
    }
}
```

## contributes.commands

コマンドパレット (`kb(workbench.action.showCommands)`) に呼び出すタイトルとコマンドからなるエントリを提供します。

> **注:** コマンドが呼び出されると (キーバインディングまたはコマンドパレットから)、 VS Code は activationEvent `onCommand:${command}` を発行します。

### 例

```json
"contributes": {
    "commands": [{
        "command": "extension.sayHello",
        "title": "Hello World"
    }]
}
```

![commands extension point example](images/extension-points/commands.png)

## contributes.menus

コマンドのメニュー項目をエディタまたはエクスプローラに提供します。メニュー項目の定義には、選択されたときに呼び出されるコマンドと、その項目が表示される条件が含まれています。
後者は、キーバインディング[when clause contexts](/docs/getstarted/keybindings.md#when-clause-contexts) を使う `when`節で定義されています。 必須の `command` プロパティに加えて、代替コマンドは `alt` プロパティを使って定義することができます。
メニュー項目の上にあるときに `kbstyle(Alt)` を押すと表示され、呼び出されます。
最後に、 `group` プロパティはメニュー項目のソートとグループ化を定義します。
`navigation` グループは、常にメニューの先頭/先頭にソートされるので特別です。

現在、拡張機能の作家は次のものに貢献できます。

* グローバルコマンドパレット - `commandPalette`
* エクスプローラのコンテキストメニュー - `explorer/context`
* エディタコンテキストメニュー - `エディタ/コンテキスト`
* エディタタイトルメニュー - エディタ/タイトル
* エディタタイトルコンテキストメニュー - `editor/title/context`
* デバッグコールスタックビューコンテキストメニュー - `debug/callstack/context`
* [SCMタイトルメニュー](/docs/extensionAPI/api-scm.md#menus) - `scm/title`
* [SCMリソースグループ](/docs/extensionAPI/api-scm.md#menus) のメニュー - `scm/resourceGroup/context`
* [SCM resources](/docs/extensionAPI/api-scm.md#menus) のメニュー - `scm/resource/context`

> **注:** コマンドが (コンテキスト) メニューから呼び出されると、 VS Code は現在選択されているリソースを推測しようとし、コマンドを呼び出すときにパラメータとして渡します。
たとえば、エクスプローラ内のメニュー項目には選択したリソースの URI が渡され、エディタ内のメニュー項目にはドキュメントの URI が渡されます。

`commandPalette` メニューは、デフォルトですべてのコマンドを含んでいるので特別です。コマンドがそこにのみ表示されるようにするには、 `when` 節を使用します。
タイトルに加えて、コマンドは VS Code がエディタのメニューバーに表示されるアイコンを定義することもできます。

### 例

```json
"contributes": {
    "menus": {
        "editor/title": [{
            "when": "resourceLangId == markdown",
            "command": "markdown.showPreview",
            "alt": "markdown.showPreviewToSide",
            "group": "navigation"
        }]
    }
}
```

![menus extension point example](images/extension-points/menus.png)

### グループのソート

メニュー項目はグループにソートできます。 それらは、次のデフォルト/ルールで辞書順にソートされます。

エディタのコンテキストメニューには、 次のデフォルト値があります。

* `navigation` - すべての場合において、 `navigation` グループが最初に来ます。
* `1_modification` - このグループは次に来て、あなたのコードを変更するコマンドを含んでいます。
* `9_cutcopypaste` - 基本的な編集コマンドを持つ最後のデフォルトグループ。

![Menu Group Sorting](images/extension-points/groupSorting.png)

これらのグループにメニュー項目を追加したり、メニュー項目の新しいグループを間、 下、 または上に追加することができます。
エディタのコンテキストメニューのみがこのグループ化の制御を可能にします。

### グループ内のソート

グループ内の順序は、タイトルまたは順序属性に依存します。
メニュー項目のグループローカル順序は、以下に示すように `@<number>` をグループ識別子に追加することによって指定されます:

```json
"editor/title": [{
    "when": "editorHasSelection",
    "command": "extension.Command",
    "group": "myGroup@1"
}]
```

## contributes.keybindings

ユーザーがキーの組み合わせを押したときに呼び出されるコマンドを定義するキーバインドルールに対応します。
キーバインディングについて詳しく説明している [Key Bindings](/docs/getstarted/keybindings.md) トピックを参照してください。

キーバインディングを提供すると、デフォルトのキーボードショートカットにルールが表示され、コマンドのすべての UI 表現に、追加したキーバインディングが表示されます。
もちろん、ユーザーがキーの組み合わせを押すと、コマンドが呼び出されます。

> **注意:** VS Code は Windows、 Mac、 Linux 上で動作するため、修飾子が異なる場合は "key" を使用してデフォルトのキーの組み合わせを設定し、特定のプラットフォームで上書きすることができます。

> **注:** コマンドが呼び出されると(キーバインディングまたはコマンドパレットから)、 VS Code は activationEvent `onCommand:${command}` を発行します。

### 例

WindowsとLinuxでは `kbstyle(Ctrl+F1)`、 Macでは `kbstyle(Cmd+F1)` を定義すると `"extension.sayHello"` コマンドがトリガされます:

```json
"contributes": {
    "keybindings": [{
        "command": "extension.sayHello",
        "key": "ctrl+f1",
        "mac": "cmd+f1",
        "when": "editorTextFocus"
    }]
}
```

![keybindings extension point example](images/extension-points/keybindings.png)

## contributes.languages

言語の定義に提供します。 これは新しい言語を導入したり、 VS Code が持つ言語に関する知識を充実させます。

この文脈では、言語は基本的にファイルに関連付けられた文字列識別子です (`TextDocument.getLanguageId()` 参照)。

VS Code は、ファイルが関連付けられる言語を決定するために3つのヒントを使用します。 それぞれの「ヒント」を個別に充実させることができます。

1. ファイル名の拡張子 (下記の `extensions`)
2. ファイル名 (下記の `ファイル名`) 
3. ファイル内の最初の行 (下記の `firstLine`)

ユーザーがファイルを開くと、これらの3つのルールが適用され、言語が決定されます。 VS Code は activationEvent `onLanguage:${language}` を出力します (例:下記の例では `onLanguage:python`) 

`aliases`プロパティーには、言語が分かっている人間が読める名前が含まれています。このリストの最初の項目は、言語ラベルとして選択されます(右側のステータスバーに表示されます)。

`configuration` プロパティは、言語設定ファイルへのパスを指定します。 パスは拡張フォルダとの相対パスで、通常は `./language-configuration.json` です。 このファイルは JSON 形式を使用し、次のプロパティを含むことができます。

* `comments` - コメントシンボルを定義します。
  * `blockComment` - ブロックコメントをマークするために使用される begin トークンと end トークン。 'Toggle Block Comment' コマンドで使用されます。
  * `lineComment` - 行コメントをマークするのに使用される begin トークン。 'Add Line Comment' コマンドで使用されます。
* `brackets` - 角括弧の間のコードの字下げに影響する括弧記号を定義します。 改行を入力するときに新しいインデントレベルを決定または修正するためにエディタで使用されます。
* `autoClosingPairs` - 自動クローズ機能のオープンシンボルとクローズシンボルを定義します。 開いているシンボルが入力されると、エディタは自動的に閉じるシンボルを挿入します。 自動的に閉じたペアは、オプションで `notIn` パラメータをとり、文字列やコメント内のペアを非アクティブにします。
* `surroundingPairs` - 選択された文字列を囲むために使用されるオープンペアとクローズペアを定義します。

あなたの言語設定ファイル名が `language-configuration.json` で終わっていれば、 VS Code で検証と編集のサポートを受け取ります。

### 例

```json
...
"contributes": {
    "languages": [{
        "id": "python",
        "extensions": [ ".py" ],
        "aliases": [ "Python", "py" ],
        "filenames": [ ... ],
        "firstLine": "^#!/.*\\bpython[0-9.-]*\\b",
        "configuration": "./language-configuration.json"
    }]
}
```

language-configuration.json

```json
{
    "comments": {
        "lineComment": "//",
        "blockComment": [ "/*", "*/" ]
    },
    "brackets": [
        ["{", "}"],
        ["[", "]"],
        ["(", ")"]
    ],
    "autoClosingPairs": [
        ["{", "}"],
        ["[", "]"],
        ["(", ")"],
        { "open": "'", "close": "'", "notIn": ["string", "comment"] },
        { "open": "/**", "close": " */", "notIn": ["string"] }
    ],
    "surroundingPairs": [
        ["{", "}"],
        ["[", "]"],
        ["(", ")"],
        ["<", ">"],
        ["'", "'"]
    ]
}
```

## contributes.debuggers

デバッガを VS Code に提供します。 デバッガの提供には、以下の特性があります。

* `type` は起動設定でこのデバッガを識別するために使用される一意のIDです。
* `label` はUIのこのデバッガのユーザーが見ることのできる名前です。
* `program` 実際のデバッガまたはランタイムに対して VS Code デバッグプロトコルを実装するデバッグアダプタへのパス。
* `runtime` デバッグアダプタへのパスが実行可能ではないが実行時が必要な場合は、
* `configurationAttributes` は、このデバッガに固有の起動設定引数のスキーマです。
* `initialConfigurations` は、最初の launch.json を生成するために使用される起動設定をリストします。
* `configurationSnippets` は、 launch.json を編集するときに IntelliSense で利用可能な起動設定をリストし、
* `variables` は置換変数を導入し、 デバッガ拡張で実装されたコマンドにバインドします。

### 例

```json
"contributes": {
    "debuggers": [{
        "type": "node",
        "label": "Node Debug",

        "program": "./out/node/nodeDebug.js",
        "runtime": "node",

        "configurationAttributes": {
            "launch": {
                "required": [ "program" ],
                "properties": {
                    "program": {
                        "type": "string",
                        "description": "The program to debug."
                    }
                }
            }
        },

        "initialConfigurations": [{
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "program": "${workspaceRoot}/app.js"
        }],

        "configurationSnippets": [
            {
                "label": "Node.js: Attach Configuration",
                "description": "A new configuration for attaching to a running node program.",
                "body": {
                    "type": "node",
                    "request": "attach",
                    "name": "${2:Attach to Port}",
                    "port": 5858
                }
            }
        ],

        "variables": {
            "PickProcess": "extension.node-debug.pickNodeProcess"
        }
    }]
}
```

`デバッガ` を統合する方法については、 [Debuggers](/docs/extensions/example-debuggers.md) を参照してください。

## contributes.breakpoints

通常、デバッガエクステンションには `contributes.breakpoints` エントリもあります。 このエントリには、設定ブレークポイントを有効にする言語ファイルタイプがリストされています。

```json
"contributes": {
    "breakpoints": [
        {
            "language": "javascript"
        },
        {
            "language": "javascriptreact"
        }
    ]
}
```

## contributes.grammars

TextMate 文法を言語に提供します。 この文法が適用される `language` 文法と、文法とファイルパスのための TextMate `scopeName` を提供しなければなりません。

> **注:** 文法を含むファイルは、 JSON (ファイル名は.jsonで終わる) または XML plist 形式 (他のすべてのファイル) にすることができます。

### 例

```json
"contributes": {
    "grammars": [{
        "language": "shellscript",
        "scopeName": "source.shell",
        "path": "./syntaxes/Shell-Unix-Bash.tmLanguage"
    }]
}
```

TextMate の .tmLanguage ファイルを VS Code 拡張として素早くパッケージ化するための [yo code extension generator](/docs/extensions/yocode.md) の使用方法については、 [言語の色付けの追加](/docs/extensions/themes-snippets-colorizers.md) を参照してください。

![grammars extension point example](images/extension-points/grammars.png)

## contributes.themes

TextMateテーマをVS Code に提供します。 テーマが暗いテーマであるか明るいテーマであるか(テーマに合わせて残りのVS Code が変更されるような) 、ファイルへのパス(XML plist形式) のいずれかを指定する必要があります。

### 例

```json
"contributes": {
    "themes": [{
        "label": "Monokai",
        "uiTheme": "vs-dark",
        "path": "./themes/Monokai.tmTheme"
    }]
}
```

![themes extension point example](images/extension-points/themes.png)

[yoコード拡張ジェネレータ](/docs/extensions/yocode.md) を使用して TextMate .tmTheme ファイルを VS Code 拡張としてすばやくパッケージ化する方法については、[色のテーマの変更](/docs/extensions/themes-snippets-colorizers.md) を参照してください。

## contributes.snippets

```json
"contributes": {
    "snippets": [{
        "language": "go",
        "path": "./snippets/go.json"
    }]
}
```

## contributes.jsonValidation

特定のタイプの `json` ファイルの検証スキーマを提供します。
`url` 値は、拡張に含まれるスキーマファイルへのローカルパスか、 [json schema store](http://schemastore.org/json) のようなリモートサーバの URL です。

```json
"contributes": {
    "jsonValidation": [{
        "fileMatch": ".jshintrc",
        "url": "http://json.schemastore.org/jshintrc"
    }]
}
```

# 次のステップ

VS Code の拡張性モデルの詳細については、次のトピックを参照してください。

* [拡張マニフェストファイル](/docs/extensionAPI/extension-manifest.md) - VS Code package.json 拡張マニフェストファイルリファレンス
* [アクティベーションイベント](/docs/extensionAPI/activation-events.md) - VS Code アクティベーションイベントリファレンス
