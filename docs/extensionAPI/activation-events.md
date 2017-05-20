---
Order: 6
Area: extensionapi
TOCTitle: Activation Events
ContentId: C83BB647-A37E-45CE-BA4C-837B397C2ABE
PageTitle: Visual Studio Code Activation Events - package.json
DateApproved: 5/4/2017
MetaDescription: To support lazy activation of Visual Studio Code extensions (plug-ins), your extension controls when it should be loaded through a set of activation events in the package.json extension manifest file. 
---

# アクティベーションイベント - package.json

拡張機能は、 VS Code で遅延してアクティブ化されます。 その結果、 拡張機能をアクティブにする必要があるときに、 VS Code にコンテキストを提供する必要があります。 私たちは以下のアクティベーションイベントをサポートしています:

* [`onLanguage:${language}`](/docs/extensionAPI/activation-events.md#activationeventsonlanguage)
* [`onCommand:${command}`](/docs/extensionAPI/activation-events.md#activationeventsoncommand)
* [`onDebug:${type}`](/docs/extensionAPI/activation-events.md#activationeventsondebug)
* [`workspaceContains:${toplevelfilename}`](/docs/extensionAPI/activation-events.md#activationeventsworkspacecontains)
* [`*`](/docs/extensionAPI/activation-events.md#activationevents)

また、 [`package.json` 拡張マニフェスト](/docs/extensionAPI/extension-manifest.md) と最小必須フィールドの概要も提供します。

## activationEvents.onLanguage

このアクティベーションイベントが発行され、特定の言語に解決されるファイルが開かれるたびに関心のある拡張機能がアクティブになります。

```json
...
"activationEvents": [
    "onLanguage:python"
]
...
```

## activationEvents.onCommand

この起動イベントが発行され、コマンドが呼び出されるたびに関心のある拡張機能が有効になります:

```json
...
"activationEvents": [
    "onCommand:extension.sayHello"
]
...
```

## activationEvents.onDebug

このアクティベーションイベントが発行され、指定されたタイプのデバッグセッションが開始されるたびに関心のある拡張がアクティブになります:

```json
...
"activationEvents": [
    "onDebug:node"
]
...
```

## activationEvents.workspaceContains

このアクティベーションイベントが発生し、フォルダが開かれ、フォルダにトップレベルのファイルが含まれている場合は、該当する拡張機能が有効になります。

```json
...
"activationEvents": [
    "workspaceContains:.editorconfig"
]
...
```

## activationEvents.*

このアクティベーションイベントが発生し、 VS Code が起動するたびに関心のある内線番号が有効になります。優れたエンドユーザーエクスペリエンスを確保するには、拡張機能でこのアクティベーションイベントを使用してください。

```json
...
"activationEvents": [
    "*"
]
...
```

> **注意:** 拡張機能は、複数の起動イベントを listen することができ、それは `"*"` を listening するよりも好ましい方法です。

> **注意:** 拡張モジュールは主モジュールから `activate()`関数をエクスポート**しなければならず**、
指定された起動イベントのいずれかが発行されると VS Code によって**一度だけ**呼び出されます。
また、拡張モジュールはメインモジュールから  `deactivate()` 関数をエクスポートして、 VS Code のシャットダウン時にクリーンアップタスクを実行する**必要があります**。
クリーンアッププロセスが非同期である場合、 拡張は `deactivate()` から Promise を**返さなければなりません**。
クリーンアップが同期して実行されている場合、拡張機能は `deactivate()` から `undefined` を返します。

## 次のステップ

VS Code の拡張性モデルの詳細については、次のトピックを参照してください:

* [拡張マニフェストファイル](/docs/extensionAPI/extension-manifest.md) - VS Code package.json 拡張マニフェストファイルリファレンス
* [貢献ポイント](/docs/extensionAPI/extension-points.md) - VS Code 投稿ポイントリファレンス