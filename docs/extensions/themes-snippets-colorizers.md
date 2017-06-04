---
Order: 7
Area: extensions
TOCTitle: Themes, Snippets and Colorizers
ContentId: 448E9027-3AD0-420D-9A58-D428D1B1067D
PageTitle: Add Themes, Snippets and Colorizers to Visual Studio Code
DateApproved: 5/4/2017
MetaDescription: How to add themes, snippets and colorization and bracket matching to Visual Studio Code. TextMate .tmLanguage files are supported.
---
# テーマ、スニペット、カラー化ツール

カスタムテーマ、スニペット、および言語構文カラー化ツールは、エディタを人生にもたらすものです。既存のTextMateカスタマイズファイルが多数あり、 VS Code で簡単にパッケージ化して再利用できます。拡張子に `.tmTheme`、` .tmSnippets`、 `.tmLanguage`ファイルを直接使用し、拡張子 [Marketplace](https://marketplace.visualstudio.com/VSCode) で共有することができます。このトピックでは、TextMateファイルを再利用する方法と、独自のテーマ、スニペット、およびカラー化ツールを作成および共有する方法について説明します。

## 新しいテーマを追加する

 VS Code の [Yeoman](http://yeoman.io) 拡張ジェネレータ、 [yo code]((/docs/extensions/yocode.md) を使用して、新しいTextMateテーマファイル.tmTheme)を VS Code のインストールに追加することもできます。拡張ジェネレータは、既存のTextMateテーマファイルを使用し、 VS Code で使用するためにそれをパッケージ化します。

[ColorSublime]((http://colorsublime.com) には、何百もの既存のTextMateテーマがあります。あなたが好きなテーマを選び、ダウンロードリンクをコピーしてYeomanジェネレータで使用します。 「http://colorsublime.com/theme/download/(number)」のような形式になります。 'code'ジェネレータは、.tmThemeファイルのURLまたはファイルの場所、テーマ名、およびテーマに関連するその他の情報を入力するよう求めます。

![yo code theme](images/themes/yocodetheme.png)

生成されたテーマフォルダを [あなたの `.vscode/extensions`フォルダ]((/docs/extensions/yocode.md#your-extensions-folder) の下の新しいフォルダにコピーし、 VS Code を再起動します。

** File **> ** Preferences **> ** Color Theme **でカラーテーマピッカーテーマを開き、ドロップダウンでテーマを確認できます。矢印を上下に移動すると、テーマのライブプレビューが表示されます。

![select my theme](images/themes/mytheme.png)

## エクステンションマーケットプレイスにテーマを公開する

新しいテーマをコミュニティと共有したい場合は、 [Extension Marketplace](/docs/editor/extension-gallery.md) に公開できます。 [vsce公開ツール](/docs/extensions/publish-extension.md) を使用してテーマをパッケージ化し、VS Code Marketplaceに公開します。

> **ヒント:**ユーザがあなたのテーマを見つけやすくするために、拡張の説明に "theme"という単語を入れ、 `package.json`に` Category`を `Theme`に設定します。

また、 [Marketplaceプレゼンテーションのヒント](/docs/extensionAPI/extension-manifest.md#marketplace-presentation-tips) を参照して、 VS Code マーケットプレイスでエクステンションを見栄えよくする方法についての推奨事項もあります。

## カスタムテーマの作成

独自のTextMateテーマを最初から作成することもできます。詳細については、TextMate [theme](https://manual.macromates.com/en/themes) および言語文法 [命名規則](https://manual.macromates.com/en/language_grammars#naming_conventions) を参照してください。

TextMate言語の文法標準スコープに加えて、 VS Code には独自のテーマを調整するために使用できるカスタムテーマ設定があります。

- 'rangeHighlight`:クイックオープンとFind機能のように、ハイライト表示される範囲の背景色です。
- `selectionHighlight`:選択中にハイライト表示される領域の背景色。
- `inactiveSelection`:フォーカスがないときの選択の背景色。
- `wordHighlight`:変数の読み込みのような、読み込みアクセス時のシンボルの背景色です。
- `wordHighlightStrong`:変数への書き込みのような、書き込みアクセス中のシンボルの背景色です。
- findMatchHighlight`:検索に一致する領域の背景色。
- `currentFindMatchHighlight`:検索に一致する現在の領域の背景色です。
- `findRangeHighlight`:検索のために選択された領域の背景色です。
- `linkForeground`:リンクの色です。
- `activeLinkForeground`:アクティブなリンクの色です。
- `hoverHighlight`:ホバリングされたときの背景色。
- `referenceHighlight`:すべての参照を見つけるときのリファレンスの背景色です。
- `guide`:ネストレベルを示すために表示されるガイドの色です。

カスタム設定を含むサンプル VS Code テーマ [here](https://github.com/Microsoft/vscode-extension-samples/tree/master/theme-sample) があります。

文法の作法は少し違うので、テーマの作成はかなり難しいです。文法は拡張機能に置き換えることができるため、TextMateの規則に従い、テーマの言語固有の規則を避けてください。

## TextMate スコープを検査するための新しいツール

テーマオーサリングを支援するために、トークンのスコープと一致するテーマルールを調べるウィジェットがあります。 **Command Palette** `kbworkbench.action.showCommands)`)から **Developer Tools:Inspect TM Scopes** を使ってウィジェットを起動することができます。

![Inspect TM Scopes](images/themes/inspect-tm-scopes.png)

## 新しいアイコンテーマを追加する

あなたはアイコン好ましくはSVG)とアイコンフォントから独自のアイコンテーマを作成できます。例として、 [Minimal](https://github.com/Microsoft/vscode/tree/master/extensions/theme-defaults) と [Seti](https://github.com) の2つのビルトインテーマを確認してください。/Microsoft/vscode/tree/master/extensions/theme-seti)。

まず、 VS Code 拡張を作成し、 `iconTheme` 投稿を追加してください。

```json
"contributes": {
    "iconThemes": [
        {
            "id": "turtles",
            "label": "Turtles",
            "path": "./fileicons/turtles-icon-theme.json"
        }
    ]
}
```

`id` はアイコンテーマの識別子です。現在のところ、内部でのみ使用されています。将来的には、設定で使用される可能性があるため、ユニークで読みやすいものにしてください。アイコンのテーマ選択ツールのドロップダウンに `label`が表示されます。 `path`は、アイコンセットを定義する拡張子内のファイルを指します。あなたのアイコンセット名が `* icon-theme.json`ネームスキームの後にあれば、 VS Code で補完と浮上を得ることができます。

### アイコンセットファイル

アイコンセットファイルは、ファイルアイコンの関連付けとアイコン定義からなるJSONファイルです。

アイコン関連付けは、ファイルタイプ 'file'、 'folder'、 'json-file' ...)をアイコン定義にマップします。アイコンの定義は、アイコンがどこにあるかを定義します。これはイメージファイルでも、フォント内のグリフでもかまいません。

### アイコンの定義

`iconDefinitions`セクションにはすべての定義が含まれています。各定義にはidがあり、定義を参照するために使用されます。定義は、複数のファイル関連によっても参照できます。

```json
    "iconDefinitions": {
        "_folder_dark": {
            "iconPath": "./images/Folder_16x_inverse.svg"
        }
    }
```

上記のアイコンの定義には、識別子が「_folder_dark」の定義が含まれています。

次のプロパティがサポートされています。

`iconPath`:svg/pngを使用する場合:画像へのパス。
- `fontCharacter`:グリフフォントを使用する場合:使用するフォントの文字。
- `fontColor`:グリフフォントを使用する場合:グリフに使用する色です。
- fontSize`:フォントを使用する場合:フォントのサイズ。デフォルトでは、フォント指定で指定されたサイズが使用されます。親フォントサイズの相対サイズたとえば、150％)にする必要があります。
- `fontId`:フォントを使用する場合:フォントのID。指定しない場合、フォント指定セクションで指定された最初のフォントが選択されます。

###ファイルの関連付け

アイコンは、フォルダ、フォルダ名、ファイル、ファイル拡張子、ファイル名、 [言語ID](/docs/extensionAPI /拡張ポイント#_contributeslanguages) に関連付けることができます。

さらに、これらの関連付けのそれぞれは、「明るい」および「高コントラスト」の色テーマについて洗練されることができる。

各ファイル関連付けは、アイコン定義を指し示します。

```json
"file": "_file_dark",
"folder": "_folder_dark",
"folderExpanded": "_folder_open_dark",
"folderNames": {
    ".vscode": "_vscode_folder",
},
"fileExtensions": {
    "ini": "_ini_file",
},
"fileNames": {
    "win.ini": "_win_ini_file",
},
"languageIds": {
    "ini": "_ini_file"
},
"light": {
    "folderExpanded": "_folder_open_light",
    "folder": "_folder_light",
    "file": "_file_light",
    "fileExtensions": {
        "ini": "_ini_file_light",
    }
},
"highContrast": {
}
```

- `file`はデフォルトのファイルアイコンで、拡張子、ファイル名、または言語IDと一致しないすべてのファイルに表示されます。現在、ファイルアイコンの定義で定義されたすべてのプロパティは継承されますフォントグリフにのみ関連し、fontSizeには便利です)。
- `folder`は、折りたたまれたフォルダのためのフォルダアイコンであり、` folderExpanded`が設定されていない場合、展開されたフォルダのアイコンです。特定のフォルダ名のアイコンは、 `folderNames`プロパティを使用して関連付けることができます。
フォルダアイコンはオプションです。設定されていない場合、フォルダのアイコンは表示されません。
- `folderExpanded`は展開されたフォルダのためのフォルダアイコンです。展開されたフォルダアイコンはオプションです。設定されていない場合、 `folder`のために定義されたアイコンが表示されます。
- `folderNames`はフォルダ名をアイコンに関連付けます。セットのキーはフォルダ名であり、パスセグメントは含まれません。パターンやワイルドカードはサポートされていません。フォルダ名の一致は大文字と小文字を区別しません。
- `folderNamesExpanded`は、展開されたフォルダのアイコンにフォルダ名を関連付けます。セットのキーはフォルダ名であり、パスセグメントは含まれません。パターンやワイルドカードはサポートされていません。フォルダ名の一致は大文字と小文字を区別しません。
- `languageIds`は、言語をアイコンに関連付けます。セット内のキーは、 [言語投稿ポイント](/docs/extensionAPI/extension-points#_contributeslanguages) で定義されている言語IDです。ファイルの言語は、言語の貢献度で定義されたファイル拡張子とファイル名に基づいて評価されます。言語提供の "最初の行の一致" は考慮されないことに注意してください。
- `fileExtensions`は、ファイル拡張子をアイコンに関連付けます。セット内のキーは、ファイル拡張子の名前です。拡張名は、ドットの後のファイル名セグメントですドットは含みません)。 `lib.d.ts` のような複数のドットを持つファイル名は、複数の拡張子にマッチすることができます。 "d.ts" と "ts"。 拡張子は大文字小文字を区別して比較されます。
- `fileNames`は、ファイル名をアイコンに関連付けます。セット内のキーは完全なファイル名であり、パスセグメントは含まれません。パターンやワイルドカードはサポートされていません。ファイル名の一致は大文字と小文字を区別しません。 'fileName'の一致が最も強い一致であり、ファイル名に関連付けられたアイコンが、一致するfileExtensionのアイコンおよび一致する言語IDのアイコンより優先されます。

ファイルの拡張子の一致は、言語の一致よりも優先されますが、ファイル名の一致よりも弱いです。

`light`と` highContrast`セクションは、上にリストしたものと同じファイル関連プロパティを持っています。対応するテーマのアイコンを無効にすることができます。

### フォントの定義

'fonts'セクションでは、使用する任意の数のグリフフォントを宣言できます。
後でこれらのフォントをアイコン定義で参照できます。アイコン定義がフォントIDを指定していない場合、最初に宣言されたフォントがデフォルトで使用されます。

拡張子にフォントファイルをコピーし、それに応じてパスを設定します。
[WOFF](https://developer.mozilla.org/en-US/docs/Web/Guide/WOFF) フォントを使用することをお勧めします。

- 'woff'をフォーマットに設定します。
- ウェイトプロパティ値は [ここ](https://developer.mozilla.org/en-US/docs/Web/CSS/font-weight#Values) で定義されています。
- スタイルプロパティの値は [ここ](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/font-style#Values) で定義されています。
- サイズは、アイコンが使用されているフォントサイズに相対的でなければなりません。したがって常にパーセンテージを使用してください。

```json
    "fonts": [
        {
            "id": "turtles-font",
            "src": [
                {
                    "path": "./turtles.woff",
                    "format": "woff"
                }
            ],
            "weight": "normal",
            "style": "normal",
            "size": "150%"
        }
    ],
    "iconDefinitions": {
        "_file": {
            "fontCharacter": "\\E002",
            "fontColor": "#5f8b3b",
            "fontId": "turtles-font"
        }
    }
```

---

## TextMateスニペットの使用

また、 [yo code](/docs/extensions/yocode.md) 拡張ジェネレータを使用して、 VS Code のインストールにTextMateスニペット.tmSnippets)を追加することもできます。ジェネレータには、複数の.tmSnippetsファイルを含むフォルダを指し示すオプション「New Code Snippets」があり、VS Codeスニペット拡張子にパッケージ化されます。ジェネレータは、サブライムスニペット.sublime-snippets)もサポートしています。

最終的なジェネレータ出力には、スニペットを VS Code に統合するためのメタデータを持つ拡張マニフェスト `package.json`と、 VS Code スニペット形式に変換されたスニペットを含む` snippets.json`ファイルという2つのファイルがあります。

```bash
.
├── snippets                    // VS Code integration
│   └── snippets.json           // The JSON file w/ the snippets
└── package.json                // extension's manifest
```

生成されたsnippetsフォルダを [あなたの `.vscode/extensions`フォルダ](/docs/extensions/yocode.md#your-extensions-folder) の下の新しいフォルダにコピーし、 VS Code を再起動します。

## マーケットプレイスでスニペットを共有する

スニペットを作成してテストしたら、コミュニティと共有することができます。

これを行うには、スニペット拡張を作成する必要があります。 `yo code`拡張ジェネレータを使用した場合、スニペット拡張機能は公開準備ができています。

ユーザースニペットを共有する場合は、スニペットを VS Code に統合するのに必要なメタデータを持つ拡張マニフェストとともにスニペットjsonファイルをパッケージ化する必要があります。

プラットフォームに応じて、ユーザースニペットファイルは次の場所にあります。

- ** Windows ** `％APPDATA％\ Code \ User \ snippets \言語).json`
- ** Mac ** `$ HOME /ライブラリ/アプリケーションサポート/コード/ユーザ/スニペット/言語).json`
- ** Linux ** `$ HOME/.config/Code/User/snippets /言語).json`

ここで `language).json`はスニペットのターゲット言語Markdownスニペットの場合は` markdown.json`など)に依存します。あなたのエクステンション用の新しいフォルダを作成し、スニペットファイルを `snippets`サブディレクトリにコピーします。

拡張マニフェストpackage.jsonファイルを拡張フォルダに追加します。スニペット拡張マニフェストは、 [拡張マニフェスト](/docs/extensionAPI/extension-manifest.md) リファレンスで定義された構造に従い、 [`snippets` 提供](/docs/extensionAPI/extension-points.md#contributessnippets) 。

Markdownスニペットのマニフェストの例を以下に示します。

```json
{
    "name": "DM-Markdown",
    "publisher": "mscott",
    "description": "Dunder Mifflin Markdown snippets",
    "version": "0.1.0",
    "engines": { "vscode": "0.10.x" },
    "categories": ["Snippets"](,
    "contributes": {
        "snippets": [
            {
                "language": "markdown",
                "path": "./snippets/markdown.json"
            }
        ]
    }
}
```

スニペットは `language`識別子に関連付ける必要があることに注意してください。これは VS Code または拡張機能によって提供される言語によって直接 [言語サポート](/docs/languages/overview.md) にすることができます。 `language`識別子が正しいことを確認してください。

その後、 [vsce公開ツール](/docs/extensions/publish-extension.md) を使用してスニペット拡張機能を [ VS Code 拡張マーケットプレイス](/docs/editor/extension-gallery.md) に公開します。

> **ヒント:**ユーザがスニペットを簡単に見つけられるようにするには、拡張の説明に「スニペット」を入れ、 `package.json`に` Category`を `Snippets`に設定します。

また、 [Marketplaceプレゼンテーションのヒント](/docs/extensionAPI/extension-manifest.md#marketplace-presentation-tips) を参照して、 VS Code マーケットプレイスでエクステンションを見栄えよくする方法についての推奨事項もあります。

---

##新しい言語を追加するColorizer)

['code' Yeoman generator](/docs/extensions/yocode.md) を使用すると、 VS Code のインストールに言語の構文強調表示とブラケットマッチングを追加する拡張機能を作成できます。

言語サポートの中心は、ColorMakerのルールを記述するTextMate [言語仕様](https://manual.macromates.com/en/language_grammars) ファイル.tmLanguage)です。 Yeomanジェネレータは、既存のTextMate言語仕様ファイルを使用するか、新しいものから開始することができます。

既存のTextMateの.tmLanguageファイルを探す良い場所はGitHubです。興味のある言語のTextMateバンドルを検索し、 `Syntaxes`フォルダに移動します。 'code' Yeomanジェネレータは、.tmLanguageファイルまたは.pListファイルをインポートできます。 URLまたはファイルの場所を入力するように求められたら、生のパスを.tmLanguageファイルに渡します。 https://raw.githubusercontent.com/textmate/ant.tmbundle/master/Syntaxes/Ant.tmLanguage。パスが、コンテンツを示すHTMLファイルではなく、ファイルのコンテンツを指していることを確認してください。

![yo code language support](images/themes-snippets-colorizers/yocodelanguage.png)

ジェネレータは、一意の名前これは他の拡張との衝突を避けるために一意でなければなりません)と言語名、エイリアスおよびファイル拡張子などの他の情報を要求します。また、文法の最上位スコープ名を指定する必要があります。そのスコープ名は、tmLanguageファイル内のスコープ名と一致する必要があります。

ジェネレータが終了したら、Visual Studio Codeで作成したフォルダを開きます。生成された `<languageid> .configuration.json`ファイルを見てください:これは、コメントや括弧に使われるトークンなど、より多くの言語設定を含んでいます。構成が正確であることを確認してください。

以下は、XMLのような角括弧付きの言語の例です。

```json
{
    "comments": {
        "lineComment": "",
        "blockComment": ["<!--", "-->"]
    },
    "brackets": [
        ["<", ">"]
    ],
    "autoClosingPairs": [
        ["<", ">"],
        ["'", "'"],
        ["\"", "\""]
    ],
    "surroundingPairs": [
        ["<", ">"],
        ["'", "'"],
        ["\"", "\""]
    ]
}
```

詳細については、 [言語提供ポイントドキュメント](/docs/extensionAPI/extension-points.md#contributeslanguages) を参照してください。

生成された `vsc-extension-quickstart.md` ファイルには、拡張機能の実行方法とデバッグ方法に関する詳細情報も含まれています。

あなたの安定した VS Code のインストールでエクステンションを使用するには、完全な出力フォルダを [あなたの `.vscode/extensions`フォルダ](/docs/extensions/yocode.md#your-extensions-folder) 下の新しいフォルダにコピーし、 VS Code 。  VS Code を再起動すると、新しい言語が言語指定ドロップダウンに表示され、言語のファイル拡張子に一致するファイルのフルカラー化とブラケット/タグのマッチングが行われます。

![select ant language](images/themes-snippets-colorizers/antlanguage.png)

## エクステンションマーケットプレイスへの言語サポートの公開

新しい言語をコミュニティと共有したい場合は、 [Extension Marketplace](/docs/editor/extension-gallery.md) に公開することができます。 [vsce公開ツール](/docs/extensions/publish-extension.md) を使用して拡張機能をパッケージ化し、 VS Code マーケットプレイスに公開します。

> **ヒント:**あなたの言語サポートを簡単に見つけられるようにするには、拡張機能の説明に言語名と "language"または "language support"を含め、 `category`を` package.json`。

また、 [Marketplaceプレゼンテーションのヒント](/docs/extensionAPI/extension-manifest.md#marketplace-presentation-tips) を参照して、 VS Code マーケットプレイスでエクステンションを見栄えよくする方法についての推奨事項もあります。

## あなたの言語に追加サポート拡張

 VS Code に新しい言語を追加するときに、共通の編集操作をサポートする言語 [スニペット](/docs/editor/userdefinedsnippets.md) を追加することもできます。 スニペットやカラーライザーのような複数の拡張機能/docs/extensionAPI/extension-manifest.md#combined-extension-contribution)を同じ拡張機能に簡単に組み込むことができます。 Colorizer拡張マニフェスト `package.json`を修正して、` snippets`投稿とsnippets.jsonを組み込むことができます。

```json
{
    "name": "language-latex",
    "description": "LaTeX Language Support",
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
        "snippets": [
            {
                "language": "latex",
                "path": "./snippets/snippets.json"
            }
        ]
    }
}
```

## 言語識別子

 VS Code では、各言語モードに固有の固有の言語識別子があります。 その識別子は、設定以外ではユーザにはほとんど見られません。 ファイル拡張子を言語に関連付ける場合:

```json
    "files.associations": {
        "*.myphp": "php"
    }
```

正確な識別子マッチングのためのケーシング事項 'Markdown'！= 'markdown')

言語識別子は、新しい言語機能を追加するときや、言語サポートを置き換えるときに VS Code 拡張開発者にとって不可欠になります。

すべての言語は `languages`設定ポイントを通して* id *を定義します:

```json
    "languages": [{
        "id": "java",
        "extensions": [ ".java", ".jav" ],
        "aliases": [ "Java", "java" ]
    }]
```

言語サポートは、言語識別子を使用して追加されます。

```json
    "grammars": [{
        "language": "groovy",
        "scopeName": "source.groovy",
        "path": "./syntaxes/Groovy.tmLanguage"
    }],
    "snippets": [{
        "language": "groovy",
        "path": "./snippets/groovy.json"
    }]
```

### 新しい識別子のガイドライン

新しい言語識別子を定義するときは、次のガイドラインを使用してください。

- 小文字のプログラミング言語名を使用します。
- Marketplaceで他の拡張機能を検索して、言語識別子がすでに使用されているかどうかを調べます。

既知の言語識別子 [言語識別子の参照](/docs/languages/identifiers.md) のリストがあります。

## 次のステップ

 VS Code の拡張性の詳細については、次のトピックを参照してください。

* [Visual Studioコードを拡張する](/docs/extensions/overview.md) - VS Code を拡張する他の方法について学ぶ
* [その他の拡張の例](/docs/extensions/samples.md) - サンプルの拡張プロジェクトの一覧を見てください。

##よくある質問

**Q:カスタムカラーテーマで VS Code のどの部分をテーマにできますか？**

 VS Code のカラーテーマは、エディタの入力領域テキストの前景、背景、選択、ラインハイライト、キャレット、構文トークン)やカスタムUIの一部に影響します [テーマの作成](/docs/extensions/themes-snippets-colorizers.md#creating-a-custom-theme)) 。テーマを投稿するときは、ライト (`vs`）、ダーク` (vs-dark`）、ハイコントラスト (`hc-black`）という基本テーマも指定します。基本テーマは、ファイルエクスプローラなどのワークベンチ内の他のすべての領域で使用されます。基本テーマは拡張機能によってカスタマイズできないし、貢献できない。

**Q:カスタムカラーテーマで使用できるスコープのリストはありますか？**

 VS Code のテーマは標準のTextMateテーマであり、 VS Code で使用されるトークナイザはよく確立されたTextMateトークナであり、主にコミュニティによって管理され、他の製品で使用されます。

どのスコープがどこで使用されるのかを知るには、[TextMateのドキュメント](https://manual.macromates.com/en/themes）とこの便利な[ブログ投稿]https://www.apeth.com/nonblog）を参照してください。 /stories/textmatebundle.html）。テーマを調べるのに最適な場所は、[ここ]https://tmtheme-editor.herokuapp.com/）です。

** Q:スニペット拡張機能を作成しましたが、 VS Code エディタに表示されませんか？**

** A:**スニペットの `language`識別子を正しく指定してくださいMarkdown .mdファイルの場合は` markdown`、プレーンテキストの.txtファイルの場合は `plaintext '）。また、スニペットjsonファイルへの相対パスが正しいことも確認してください。

** Q:Colorizerにファイル拡張子を追加できますか？**

** A:**はい、 `yo code`ジェネレータは、.tmLanguageファイルからデフォルトのファイル拡張子を提供しますが、` languages` contrib `extensions`配列にファイル拡張子を簡単に追加できます。以下の例では、デフォルトの `.asa`ファイル拡張子に` .asp`ファイル拡張子が追加されています。

```json
{
    "name": "asp",
    "version": "0.0.1",
    "engines": {
        "vscode": "0.10.x"
    },
    "publisher": "none",
    "contributes": {
        "languages": [{
            "id": "asp",
            "aliases": ["ASP", "asp"],
            "extensions": [".asa", ".asp"]
        }],
        "grammars": [{
            "language": "asp",
            "scopeName": "source.asp",
            "path": "./syntaxes/asp.tmLanguage"
        }]
    }
}
```

**Q:既存のカラー化ツールにファイル拡張子を追加できますか？**

**A:** はい。 既存のカラー化ツールを拡張するには、ファイル拡張子を `files.associations` [setting](（/docs/getstarted/settings.md）で既存の言語識別子に関連付けることができます。 IntelliSenseは、現在利用可能な言語IDの一覧を表示します。

例えば、以下の設定では `.mmd`ファイル拡張子を` markdown`カラー化ツールに追加します:

```json
    "files.associations": {
        "*.mmd": "markdown"
    }
```

**Q:既存のカラー化ツールを完全にオーバーライドしたい場合はどうしたらいいですか？**

**A:** はい。 既存の言語IDに対して新しい `grammars`要素を提供することで、色付けをオーバーライドします。 また、置き換える文法を定義する拡張の名前を含む `extensionDependencies`属性を追加します。

```json
{
    "name": "override-xml",
    "version": "0.0.1",
    "engines": {
        "vscode": "0.10.x"
    },
    "publisher": "none",
    "extensionDependencies": [
        "xml"
    ],
    "contributes": {
        "grammars": [{
            "language": "xml",
            "scopeName": "text.xml",
            "path": "./syntaxes/BetterXML.tmLanguage"
        }]
    }
}
```
