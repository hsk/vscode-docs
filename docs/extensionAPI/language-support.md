---
Order: 3
Area: extensionapi
TOCTitle: Language Extension Guidelines
ContentId: A9D40038-7837-4320-8C2D-E0CA5769AA69
PageTitle: Visual Studio Code Language Extension Guidelines
DateApproved: 5/4/2017
MetaDescription: Visual Studio Code language extensions contribute new programming language features to VS Code. These guidelines present the language extensibility points and how to implement them.
---
# 言語拡張ガイドライン

VS Code でサポートされている言語について聞かれれば、通常、構文のハイライト、コード補完や場合によっては、デバッグサポートを思い浮かべるでしょう。 これは始まりとしては良いですが、言語拡張はもっと多くのことを行うことができます。

設定ファイルだけで、拡張機能は構文の強調表示、スニペット、およびスマートブラケットのマッチングをサポートすることができます。高度な言語機能を使用するには、拡張性 [API](/docs/extensionAPI/vscode-api.md) または [言語サーバー](/docs/extensions/example-language-server) を使用して VS Code を拡張する必要があります。

言語サーバーは、 [言語サーバープロトコル](https://github.com/Microsoft/language-server-protocol/blob/master/protocol.md) を使用するスタンドアロンサーバーです。タスクに最も適したプログラミング言語でサーバーを実装できます。たとえば、サポートしたい言語用の Python で書かれた良いライブラリがある場合は、 Python で言語サーバを実装することを検討することをお勧めします。言語サーバーを JavaScript または TypeScript で実装する場合は、 VS Code [npmモジュール](https://github.com/Microsoft/vscode-languageserver-node) の上に構築できます。

実装言語に加えて、言語サーバーが実装する言語サーバープロトコルのどの部分を柔軟に決定することができます。言語サーバーは、プロトコルの `initialize` メソッドに対応して、その機能をアナウンスします。

ただし、言語サーバーアーキテクチャは、拡張機能で言語機能を提供する唯一の方法ではありません。メインの拡張コードに直接フィーチャーを実装することもできます。以下のガイドラインでは、 **Language Server Protocol** のアプローチ(設定と必要なイベント) と、特定の言語機能プロバイダ (例: `registerHoverProvider`) をプログラムで登録する方法を示す **Direct Implementation** セクションを示します。

最初に実装するものと後で改良するものを簡単に決定できるように、 VS Code に表示されている言語機能を表示し、それらにマップされるクラスとメソッド、または言語サーバープロトコルメッセージに従います。また、 **基本的な** サポートの要望、 **高度な** 実装の説明も含まれています。

## 構成ベースの言語サポート

[構文の強調表示](/docs/extensionAPI/language-support.md#syntax-highlighting)、[スニペット](/docs/extensionAPI/language- support.md#source-code-snippets)、[スマートブラケットマッチング](/docs/extensionAPI/language-support.md#smart-bracket-matching) は、設定ファイルで宣言的に実装でき、拡張コードを書く必要はありません。

### 言語識別子

 VS Code は、異なる言語構成とプロバイダを言語識別子によって特定のプログラミング言語にマッピングします。これは、プログラミング言語またはファイルタイプを表す小文字の文字列です。たとえば、 JavaScript の言語IDは `javascript` 、 Markdown ファイルは `markdown` です。

## 構文ハイライト

![syntax highlighting](images/language-support/syntax-highlighting.png)

構文の強調表示をサポートするには、拡張機能で TextMate の文法 `.tmLanguage` を言語の `package.json` ファイルに登録する必要があります。

```json
"contributes": {
    "languages": [
        {
            "id": "markdown",
            ...
        }
    ],
    "grammars": [
        {
            "language": "markdown",
            "scopeName": "text.html.markdown",
            "path": "./syntaxes/markdown.tmLanguage"
        }
    ], ...
}
```

> **基本**
>
>文字列、コメント、キーワードの色付けをサポートする簡単な文法から始めましょう。

> **上級**
>
>用語や表現を理解し、変数や関数の参照などの色付けをサポートする文法を提供する

## ソースコードスニペット

![Snippets at work](images/language-support/snippets.gif)

コードスニペットを使用すると、便利なソースコードテンプレートをプレースホルダで提供できます。拡張機能の `package.json` ファイルに、あなたの言語のスニペットを含むファイルを登録する必要があります。  VS Code のスニペットスキーマについては、[独自スニペットの作成](/docs/editor/userdefinedsnippets.md#creating-your-own-snippets) で学ぶことができます。

```json
"contributes": {
    "snippets": [
        {
            "language": "javascript",
            "path": "./snippets/javascript.json"
        }, ...
    ], ...
}
```

> **基本**
>
>この例のようなプレースホルダをスニペットに `markdown` のために提供してください:
>
>```json
>"Insert ordered list": {
>    "prefix": "ordered list",
>    "body": [
>        "1. ${first}",
>        "2. ${second}",
>        "3. ${third}",
>        "$0"
>    ],
>    "description": "Insert ordered list"
>}
>```

> **上級**
>
>明示的なタブストップを使用してユーザを誘導するスニペットを提供し、この例のようなネストされたプレースホルダを `groovy` のために使用してください:
>
>```json
>"key: \"value\" (Hash Pair)": {
>        "prefix": "key",
>        "body": "${1:key}: ${2:\"${3:value}\"}"
>    }
>```

## スマートブラケットマッチング

![Smart Editing At Work](images/language-support/smart-editing.gif)

拡張機能の `package.json` ファイルに言語設定を提供することができます。

```json
"contributes": {
    "languages": [
        {
            "id": "typescript",
            ...
            "configuration": "./language-configuration.json"
        }, ...
    ]
    ...
}
```

> **基本**
>
>なし

> **上級**
>
>以下は `TypeScript` の例です:
>
>```json
>{
>    "comments": {
>        "lineComment": "//",
>        "blockComment": [ "/*", "*/" ]
>    },
>    "brackets": [
>        ["{", "}"],
>        ["[", "]"],
>        ["(", ")"],
>        ["<", ">"]
>    ],
>    "autoClosingPairs": [
>        { "open": "{", "close": "}" },
>        { "open": "[", "close": "]" },
>        { "open": "(", "close": ")" },
>        { "open": "'", "close": "'", "notIn": ["string", "comment"] },
>        { "open": "\"", "close": "\"", "notIn": ["string"] },
>        { "open": "`", "close": "`", "notIn": ["string", "comment"] },
>        { "open": "/**", "close": " */", "notIn": ["string"] }
>    ],
>    "surroundingPairs": [
>        ["{", "}"],
>        ["[", "]"],
>        ["(", ")"],
>        ["<", ">"],
>        ["'", "'"],
>        ["\"", "\""],
>        ["`", "`"]
>    ]
>}
>```

## プログラム言語サポート

残りの言語機能では、 VS Code からの要求を処理するための拡張コードの作成が必要です。言語拡張は、[言語サーバープロトコル](https://github.com/Microsoft/language-server-protocol/blob/master/protocol.md) を実装するスタンドアロンサーバーとして実装することも、拡張機能の `activate` メソッドを呼び出して実装することもできます。どちらのアプローチも **LANGUAGE SERVER PROTOCOL** と **DIRECT IMPLEMENTATION** の2つのセクションに示されています。

言語サーバープロトコルのアプローチは、 `initialize` リクエストへの応答でサーバーの機能を記述し、ユーザーの動作に基づいて特定の要求を処理するパターンに従います。

直接実装のアプローチでは、拡張機能がアクティブ化されたときにフィーチャープロバイダを登録する必要があり、プロバイダがサポートするプログラミング言語を識別するための `DocumentSelector` を提供することがよくあります。

以下の例では、プロバイダがGo言語ファイルに登録されています。

```typescript
const GO_MODE: vscode.DocumentFilter = { language: 'go', scheme: 'file' };
```

## Show Hovers

ホバーは、マウスカーソルの下にあるシンボル/オブジェクトに関する情報を表示します。これは、通常、シンボルのタイプと説明です。

![Hovers at Work](images/language-support/hovers.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、言語サーバは、それがホバースを提供することをアナウンスする必要があります。

```json
{
    ...
    "capabilities" : {
        "hoverProvider" : "true",
        ...
    }
}
```

さらに、言語サーバーは `textDocument/hover` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoHoverProvider implements HoverProvider {
    public provideHover(
        document: TextDocument, position: Position, token: CancellationToken):
        Thenable<Hover> {
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerHoverProvider(
            GO_MODE, new GoHoverProvider()));
    ...
}
```

> **基本**
>
>型情報を表示し、使用可能な場合はドキュメントを含めます。

> **上級**
>
>コードを色付けするのと同じスタイルでメソッドのシグネチャを色付けします。

## コード補完候補を表示する

コードの補完は、状況に応じた候補をユーザーに提示します。

![Code Completion at Work](images/language-support/code-completion.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、あなたの言語サーバは補完を提供し、 `completionItem\resolve` メソッドをサポートしているかどうかを宣言して、計算された補完アイテムの追加情報を提供する必要があります。

```json
{
    ...
    "capabilities" : {
        "completionProvider" : {
            "resolveProvider": "true",
            "triggerCharacters": [ '.' ]
        }
        ...
    }
}
```

#### 直接実装

```typescript
class GoCompletionItemProvider implements vscode.CompletionItemProvider {
    public provideCompletionItems(
        document: vscode.TextDocument, position: vscode.Position, token: vscode.CancellationToken):
        Thenable<vscode.CompletionItem[]> {
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(getDisposable());
    ctx.subscriptions.push(
        vscode.languages.registerCompletionItemProvider(
            GO_MODE, new GoCompletionItemProvider(), '.', '\"'));
    ...
}
```

> **基本**
>
>解決プロバイダはサポートしません。

> **上級**
>
>ユーザーが選択した補完候補の追加情報を計算する解決プロバイダをサポートします。この情報は、選択したアイテムの横に表示されます。

## 診断を提供する

診断は、コードの問題を示す方法です。

![Diagnostics at Work](images/language-support/diagnostics.gif)

#### 言語サーバープロトコル

言語サーバーは `textDocument/publishDiagnostics` メッセージを言語クライアントに送信します。このメッセージには、リソース URI の診断項目の配列が格納されます。

**注**: クライアントはサーバーに診断を依頼しません。サーバーは診断情報をクライアントにプッシュします。

#### 直接実装

```typescript
let diagnosticCollection: vscode.DiagnosticCollection;

export function activate(ctx: vscode.ExtensionContext): void {
  ...
  ctx.subscriptions.push(getDisposable());
  diagnosticCollection = vscode.languages.createDiagnosticCollection('go');
  ctx.subscriptions.push(diagnosticCollection);
  ...
}

function onChange() {
  let uri = document.uri;
  check(uri.fsPath, goConfig).then(errors => {
    diagnosticCollection.clear();
    let diagnosticMap: Map<string, vscode.Diagnostic[]> = new Map();
    errors.forEach(error => {
      let canonicalFile = vscode.Uri.file(error.file).toString();
      let range = new vscode.Range(error.line-1, error.startColumn, error.line-1, error.endColumn);
      let diagnostics = diagnosticMap.get(canonicalFile);
      if (!diagnostics) { diagnostics = []; }
      diagnostics.push(new vscode.Diagnostic(range, error.msg, error.severity));
      diagnosticMap.set(canonicalFile, diagnostics);
    });
    diagnosticMap.forEach((diags, file) => {
      diagnosticCollection.set(vscode.Uri.parse(file), diags);
    });
  })
}
```

> **基本**
>
>開いているエディタの診断を報告します。最小限には、これはすべての保存時に発生する必要があります。より良い診断は、エディタの保存されていない内容に基づいて計算する必要があります。

> **上級**
>
>開いているエディターだけでなく、開いたフォルダー内のすべてのリソースについて、エディターで開くかどうかにかかわらず、診断レポートを報告します。

## 関数とメソッドシグネチャのヘルプ

ユーザーが関数またはメソッドを入力すると、呼び出されている関数/メソッドに関する情報が表示されます。

![Type Hover](images/language-support/signature-help.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、言語サーバーが署名のヘルプを提供することをアナウンスする必要があります。

```json
{
    ...
    "capabilities" : {
        "signatureHelpProvider" : {
            "triggerCharacters": [ '(' ]
        }
        ...
    }
}
```

また、言語サーバーは `textDocument/signatureHelp` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoSignatureHelpProvider implements SignatureHelpProvider {
    public provideSignatureHelp(
        document: TextDocument, position: Position, token: CancellationToken):
        Promise<SignatureHelp> {
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerSignatureHelpProvider(
            GO_MODE, new GoSignatureHelpProvider(), '(', ','));
    ...
}
```

> **基本**
>
>署名ヘルプに関数またはメソッドのパラメータのドキュメントが含まれていることを確認します。

> **上級**
>
>何も追加しません。

## シンボルの定義を表示する

変数/関数/メソッドが使用されているところで、変数/関数/メソッドの定義をユーザが見られるようにします。

![Type Hover](images/language-support/goto-definition.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、言語サーバは、 goto 定義の場所を提供することをアナウンスする必要があります。

```json
{
    ...
    "capabilities" : {
        "definitionProvider" : "true"
        ...
    }
}
```

さらに、言語サーバは `textDocument/definition` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoDefinitionProvider implements vscode.DefinitionProvider {
    public provideDefinition(
        document: vscode.TextDocument, position: vscode.Position, token: vscode.CancellationToken):
        Thenable<vscode.Location> {
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerDefinitionProvider(
            GO_MODE, new GoDefinitionProvider()));
    ...
}
```

> **基本**
>
>シンボルに矛盾がある場合は、複数の定義を表示できます。

> **上級**
>
>何も追加しません。

## シンボルへのすべての参照を見つける

特定の変数/関数/メソッド/シンボルが使用されているすべてのソースコードの場所をユーザーに表示させます。

![Type Hover](images/language-support/find-references.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、言語サーバーがシンボル参照場所を提供することをアナウンスする必要があります。

```json
{
    ...
    "capabilities" : {
        "referencesProvider" : "true"
        ...
    }
}
```

さらに、言語サーバは `textDocument/references` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoReferenceProvider implements vscode.ReferenceProvider {
    public provideReferences(
        document: vscode.TextDocument, position: vscode.Position,
        options: { includeDeclaration: boolean }, token: vscode.CancellationToken):
        Thenable<vscode.Location[]> {
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerReferenceProvider(
            GO_MODE, new GoReferenceProvider()));
    ...
}
```

> **基本**
>
>すべての参照の場所 (リソース URI と範囲) を返します。

> **上級**
>
>何も追加しません。

## ドキュメント内のシンボルのすべての出現を強調表示する

開いているエディタでシンボルのすべての出現をユーザが見ることを可能にします。

![Type Hover](images/language-support/document-highlights.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、言語サーバはシンボル文書の場所を提供することをアナウンスする必要があります。

```json
{
    ...
    "capabilities" : {
        "documentHighlightProvider" : "true"
        ...
    }
}
```

さらに、言語サーバーは `textDocument/documentHighlight` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoDocumentHighlightProvider implements vscode.DocumentHighlightProvider {
    public provideDocumentHighlights(
        document: vscode.TextDocument, position: vscode.Position, token: vscode.CancellationToken):
        vscode.DocumentHighlight[] | Thenable<vscode.DocumentHighlight[]>;
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerDocumentHighlightProvider(
            GO_MODE, new GoDocumentHighlightProvider()));
    ...
}
```

> **基本**
>
>参照が見つかったエディタのドキュメントの範囲を返します。

> **上級**
>
>何も追加しません。

## ドキュメント内のすべてのシンボル定義を表示する

ユーザが開いているエディタ内の任意のシンボル定義にすばやく移動できるようにします。

![Type Hover](images/language-support/document-symbols.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、言語サーバはシンボル文書の場所を提供することをアナウンスする必要があります。

```json
{
    ...
    "capabilities" : {
        "documentSymbolProvider" : "true"
        ...
    }
}
```

さらに、言語サーバーは `textDocument/documentSymbol` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoDocumentSymbolProvider implements vscode.DocumentSymbolProvider {
    public provideDocumentSymbols(
        document: vscode.TextDocument, token: vscode.CancellationToken):
        Thenable<vscode.SymbolInformation[]> {
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerDocumentSymbolProvider(
            GO_MODE, new GoDocumentSymbolProvider()));
    ...
}
```

> **基本**
>
>ドキュメント内のすべてのシンボルを返します。変数、関数、クラス、メソッドなどのシンボルの種類を定義します

> **上級**
>
>何も追加しません。

## フォルダ内のすべてのシンボル定義を表示する

 VS Code で開いたフォルダ(ワークスペース) 内の任意の場所にあるシンボル定義にすばやく移動できます。

![Type Hover](images/language-support/workspace-symbols.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、あなたの言語サーバがグローバルシンボルの場所を提供することをアナウンスする必要があります。

```json
{
    ...
    "capabilities" : {
        "workspaceSymbolProvider" : "true"
        ...
    }
}
```

さらに、言語サーバは `workspace/symbol` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoWorkspaceSymbolProvider implements vscode.WorkspaceSymbolProvider {
    public provideWorkspaceSymbols(
        query: string, token: vscode.CancellationToken):
        Thenable<vscode.SymbolInformation[]> {
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerWorkspaceSymbolProvider(
            new GoWorkspaceSymbolProvider()));
    ...
}
```

> **基本**
>
>開いているフォルダ内のソースコードで定義されているすべてのシンボルを返します。 変数、関数、クラス、メソッドなどのシンボルの種類を定義します

> **上級**
>
>何も追加しません。

## エラーまたは警告に関する考えられる処置

エラーまたは警告の直後にユーザーに可能な修正措置を提供します。対応可能な場合は、エラーまたは警告の横に電球が表示されます。 ユーザが電球をクリックすると、利用可能なコードアクションのリストが提示されます。

![Type Hover](images/language-support/quick-fixes.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、言語サーバーがコードアクションを提供することをアナウンスする必要があります。

```json
{
    ...
    "capabilities" : {
        "codeActionProvider" : "true"
        ...
    }
}
```

さらに、言語サーバは `textDocument/codeAction` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoCodeActionProvider implements vscode.CodeActionProvider {
    public provideCodeActions(
        document: vscode.TextDocument, range: vscode.Range,
        context: vscode.CodeActionContext, token: vscode.CancellationToken):
        Thenable<vscode.Command[]> {
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerCodeActionsProvider(
            GO_MODE, new GoCodeActionProvider()));
    ...
}
```

> **基本**
>
>エラー/警告修正アクションのコードアクションを提供します。

> **上級**
>
>さらに、リファクタリングなどのソースコード操作アクションを提供します。たとえば、`Extract メソッド` です。

## CodeLens - ソースコード内で実行可能なコンテキスト情報を表示する

ソースコードに散在して表示される実行可能なコンテキスト情報をユーザーに提供します。

![Type Hover](images/language-support/code-lens.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、言語サーバーは CodeLens の結果を提供し、 CodeLens をそのコマンドにバインドする` codeLens\resolve` メソッドをサポートするかどうかをアナウンスする必要があります。

```json
{
    ...
    "capabilities" : {
        "codeLensProvider" : {
            "resolveProvider": "true"
        }
        ...
    }
}
```

さらに、言語サーバーは `textDocument/codeLens` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoRCodeLensProvider implements vscode.CodeLensProvider {
    public provideCodeLenses(document: TextDocument, token: CancellationToken):
        CodeLens[] | Thenable<CodeLens[]> {
    ...
    }

    public resolveCodeLens?(codeLens: CodeLens, token: CancellationToken):
         CodeLens | Thenable<CodeLens> {
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerCodeLensProvider(
            GO_MODE, new GoCodeLensProvider()));
    ...
}
```

> **基本**
>
>ドキュメントで使用できる CodeLens の結果を定義します。

> **上級**
>
> `codeLens/resolve` に応答して、 CodeLens の結果をコマンドにバインドします。

## シンボルの名前を変更する

ユーザーがシンボルの名前を変更し、シンボルへのすべての参照を更新できるようにします。

![Type Hover](images/language-support/rename.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、あなたの言語サーバは名前の変更を提供することを宣言する必要があります。

```json
{
    ...
    "capabilities" : {
        "renameProvider" : "true"
        ...
    }
}
```

さらに、あなたの言語サーバは `textDocument/rename` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoRenameProvider implements vscode.RenameProvider {
    public provideRenameEdits(
        document: vscode.TextDocument, position: vscode.Position,
        newName: string, token: vscode.CancellationToken):
        Thenable<vscode.WorkspaceEdit> {
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerRenameProvider(
            GO_MODE, new GoRenameProvider()));
    ...
}
```

> **基本**
>
>名前の変更をサポートしません。

> **上級**
>
>実行する必要のあるすべてのワークスペース編集のリストを返します。たとえば、シンボルへの参照を含むすべてのファイルのすべての編集を返します。

## エディタでのソースコードの書式設定

ユーザーに文書全体の書式設定のサポートを提供します。

![Document Formatting at Work](images/language-support/format-document.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、あなたの言語サーバは文書フォーマットを提供することをアナウンスする必要があります。

```json
{
    ...
    "capabilities" : {
        "documentFormattingProvider" : "true"
        ...
    }
}
```

さらに、言語サーバーは `textDocument/formatting` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoDocumentFormatter implements vscode.DocumentFormattingEditProvider {
    public formatDocument(document: vscode.TextDocument):
        Thenable<vscode.TextEdit[]> {
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerDocumentFormattingEditProvider(
            GO_MODE, new GoDocumentFormatter()));
    ...
}
```

> **基本**
>
>書式設定をサポートしません。

> **上級**
>
>ソースコードを書式設定するための最小限のテキスト編集を常に返す必要があります。 これは、診断結果などのマーカーが正しく調整され、失われないようにするために重要です。

## エディタで選択した行をフォーマットする

ドキュメント内の選択された範囲の行を書式設定するためのサポートをユーザーに提供します。

![Document Formatting at Work](images/language-support/format-document-range.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、言語サーバーは、行範囲の書式設定をサポートすることをアナウンスする必要があります。

```json
{
    ...
    "capabilities" : {
        "documentRangeFormattingProvider" : "true"
        ...
    }
}
```

さらに、言語サーバは `textDocument/rangeFormatting` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoDocumentRangeFormatter implements vscode.DocumentRangeFormattingEditProvider{
    public provideDocumentRangeFormattingEdits(
        document: vscode.TextDocument, range: vscode.Range,
        options: vscode.FormattingOptions, token: vscode.CancellationToken):
        Thenable<vscode.TextEdit[]>;
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerDocumentRangeFormattingEditProvider(
            GO_MODE, new GoDocumentRangeFormatter()));
    ...
}
```

> **基本**
>
>書式設定をサポートしません。

> **上級**
>
>ソースコードを書式設定するための最小限のテキスト編集を常に返す必要があります。これは、診断結果などのマーカーが補正され、失われないようにするために重要です。

## ユーザタイプとしてコードをインクリメンタルにフォーマットする

入力時にテキストを書式設定するためのサポートをユーザーに提供します。

**注意**: ユーザ [設定](/docs/getstarted/settings.md) `editor.formatOnType` は、ユーザの入力時にソースコードがフォーマットされるかどうかを制御します。

![Document Formatting at Work](images/language-support/format-on-type.gif)

#### 言語サーバープロトコル

`initialize` メソッドへの応答では、言語サーバーは、ユーザーが入力する際に​​フォーマットを提供することをアナウンスする必要があります。また、どの文字の書式設定をトリガーするかをクライアントに伝える必要があります。 `moreTriggerCharacters` はオプションです。

```json
{
    ...
    "capabilities" : {
        "documentOnTypeFormattingProvider" : {
            "firstTriggerCharacter": "}",
            "moreTriggerCharacter": [";", ","]
        }
        ...
    }
}
```

さらに、言語サーバーは `textDocument/onTypeFormatting` リクエストに応答する必要があります。

#### 直接実装

```typescript
class GoOnTypingFormatter implements vscode.OnTypeFormattingEditProvider{
    public provideOnTypeFormattingEdits(
        document: vscode.TextDocument, position: vscode.Position,
        ch: string, options: vscode.FormattingOptions, token: vscode.CancellationToken):
        Thenable<vscode.TextEdit[]>;
    ...
    }
}

export function activate(ctx: vscode.ExtensionContext): void {
    ...
    ctx.subscriptions.push(
        vscode.languages.registerOnTypeFormattingEditProvider(
            GO_MODE, new GoOnTypingFormatter()));
    ...
}
```

> **基本**
>
>書式設定をサポートしません。

> **上級**
>
>ソースコードを書式設定するための最小限のテキスト編集を常に返す必要があります。これは、診断結果などのマーカーが補正され、失われないようにするために重要です。























