---
Order: 2
Area: extensionapi
TOCTitle: Principles and Patterns
ContentId: 36C1E34B-2F41-4AA0-9443-015D92EF85FB
PageTitle: Visual Studio Code Extensibility Patterns and Principles
DateApproved: 5/4/2017
MetaDescription: The Visual Studio Code extensibility (plug-in) API is designed around a set of guiding patterns and principles to promote extension consistency, correctness and ease of development.
---
# 拡張性の原則とパターン

## 拡張性へのアプローチ

Visual Studio Code には非常に豊富な拡張性モデルがあり、ツールを拡張する方法はたくさんあります。ただし、拡張UI作成者に直接アクセスすることはできません。  VS Code では、常時利用可能で、応答性の高いエディタを提供するために、基礎となるWebテクノロジの使用を最適化しようと常に努力しており、これらのテクノロジと製品が進化するにつれて、 DOM の使用を調整し続けます。パフォーマンスと互換性を維持するため、独自のホストプロセスで拡張機能を実行し、 DOM への直接アクセスを防ぎます。  VS Code にはIntelliSense などの一般的なシナリオ用の組み込みUIコンポーネントも含まれているため、これらのエクスペリエンスはプログラミング言語や拡張機能で一貫しており、拡張開発者は独自にビルドする必要はありません。

このアプローチは、当初、拡張開発者に制限されているように感じるかもしれません。私たちは常に、拡張性モデルを改善し、拡張機能が利用できる機能を拡張する方法を模索しています。私たちは皆さんのご意見やご意見をお待ちしております。

## コアの概念

私たちが VS Code に拡張性を加えるために出発したとき、我々はいくつかの考慮事項を念頭に置いていました。以下のセクションでは、いくつかの当社の中核的な決定に関するいくつかの文脈を提供しています。

### 安定性 - 拡張機能分離

拡張機能は素晴らしいですが、拡張機能は起動コードや VS Code 自体の全体的な安定性にも影響を与えます。これらの問題を回避するために、 VS Code は、拡張プロセスを別々のプロセス、つまり拡張ホストプロセスでロードして実行します。誤動作している拡張機能は、 VS Code 、特に起動時間に影響を与えることはできません。

このアーキテクチャにより、エンドユーザが常に VS Code を管理できるようになり、いつでもファイルを開いたりタイプしたり保存したりすることができるため、このアーキテクチャはエンドユーザを念頭に置いて構築されています。拡張機能が何をしているのかにかかわらず、応答性の高いUIです。

`extension host`はNode.jsプロセスであり、 VS Code APIを拡張ライターに公開します。  VS Code は `拡張ホスト`の内部で実行される拡張機能のデバッグをサポートしています。

### パフォーマンス - 拡張機能の有効化

 VS Code はできるだけ遅く拡張をロードし、セッション中に使用されない拡張はロードされず、したがってメモリを消費しません。拡張機能の遅延読み込みをサポートするため、 VS Code はいわゆる「活性化イベント」を定義します。 [起動イベント](/docs/extensionAPI/activation-events.md) は特定のアクティビティに基づいて VS Code によって起動され、拡張機能はどのイベントをアクティブにする必要があるかを定義することができます。たとえば、 Markdown を編集する拡張機能は、ユーザーが Markdown ファイルを開いたときにアクティブにする必要があります。

### 拡張マニフェスト

遅延を有効にするには、 VS Code に拡張の説明が必要です。拡張マニフェストは、いくつかの [VS Code 固有のフィールド](/docs/extensionAPI/extension-manifest.md) で充実した `package.json`ファイルです。 )。これには、拡張のロードをトリガする [activation events](/docs/extensionAPI/activation-events.md) が含まれます。  VS Code は、 [拡張機能が追加できる](/docs/extensionAPI/extension-points.md) のセットを提供します。たとえば、 VS Code にコマンドを追加するときは、 `commands` 寄与ポイントを通じてコマンド定義を提供します。あなたはあなたの拡張の貢献をpackage.jsonに定義します。  VS Code は起動時にマニフェストを読み込んで解釈し、それに従ってUIを準備します。

`extension host` は Node.js プロセスなので、拡張モジュールで Node API を使うことができ、拡張モジュールを実装する際に既存のNode.jsモジュールを再利用することができます。モジュールの依存関係を `package.json` の中で定義し、 npm を使って Node.js モジュールをインストールします。

詳細については、[package.json貢献点のリファレンス](/docs/extensionAPI/extension-points.md) を参照してください。

### 拡張性API

別のプロセスで分離された拡張機能を実行するアプローチにより、 VS Code はエクステンダーに公開されたAPIを厳密に制御することができます。現在のAPIの詳細については、 [拡張APIの概要](/docs/extensionAPI/overview.md) を参照してください。

 VS Code はウェブ技術 (HTML、CSS) を使用して実装されており、ウェブ技術はUIの変更やスタイリングに関して非常に強力です。 DOM にノードを簡単に追加し、 CSS を使用してカスタム外観を実装することができます。しかし、 VS Code のような複雑なアプリケーションを進化させる際には、このような問題はありません。構造が変わることがあり、UIに密接に結合している拡張が壊れてしまいます。この理由から、 VS Code は DOM をエクステンダーに公開しないために防御的なアプローチを採用しました。

### プロトコルベースの拡張

 VS Code の一般的な拡張パターンは、プロトコルを通じて VS Code と通信する別のプロセスで拡張コードを実行することです。この VS Code の例は、言語サーバーとデバッグアダプターです。通常、このプロトコルは stdin/stdout を使用して、 JSON ペイロードを使用するプロセス間で通信します。別々のプロセスを使用すると、分離境界が良好になり、 VS Code がコアエディタの安定性を保持するのに役立ちます。さらに、エクステンダーは、特定の拡張実装に最も適したプログラミング言語を選択することができます。

## 拡張パターン

Visual Studio Code の拡張 API は、API全体に適用されるいくつかのガイダンスパターンに従います。

## Promises 約束

 VS Code API は、 [promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) を使用した非同期操作を表します。拡張機能から、ES6、WinJS、A+ などのような、__any__ タイプの約束を返すことができます。

特定の約束ライブラリとは独立しているため、APIには `Thenable` 型で表現されています。 `thenable` は `then` プロパティである共通の分母を表します。

ほとんどの場合、約束の使用はオプションであり、 VS Code が拡張機能を呼び出すとき、 _result type_ と _result type_ の `Thenable ` を処理できます。約束の使用がオプションの場合、 API は `then` 型を返すことでこれを示します。

```typescript
provideNumber(): number | Thenable<number>
```

## キャンセルトークン

多くの場合、操作は、操作が完了する前に変更される揮発性の状態で開始されます。たとえば、 IntelliSense の計算が開始され、ユーザーは入力を続けてその操作の結果を廃止します。

そのような振る舞いにさらされている API は、 CancellationToken に渡されます。 CancellationToken では、キャンセルをチェックする (`isCancellationRequested`) か、キャンセルが発生したときに通知を受け取ることができます (`onCancellationRequested`)。 取り消しトークンは通常、関数呼び出しの最後のパラメータであり、オプションです。

## Disposables 使い捨て

VS Code API は、 VS Code から取得したリソースに対して[dispose pattern](https://en.wikipedia.org/wiki/Dispose_pattern)を使用します。これは、イベントリスニング、コマンド、UIとのやりとり、およびさまざまな言語の貢献に適用されます。

たとえば、 `setStatusBarMessage(value:string)` 関数は、 `dispose` を呼び出すと再びメッセージを削除する `Disposable` を返します。

## イベント

VS Code API のイベントは、サブスクライブするリスナー関数で呼び出す関数として公開されています。サブスクライブするコールは、ディスポーザブル時にイベントリスナを削除する `Disposable` を返します。

```javascript
var listener = function(event) {
	console.log("It happened", event);
};

// start listening リスニングを開始する
var subscription = fsWatcher.onDidDelete(listener);

// do more stuff もっとやる

subscription.dispose(); // stop listening 聞いていない
```

イベントの名前は、 `` Will [did] VerbNoun？ 'パターンに従います。 *(onWill)*またはすでに発生した*(onDid)*、何が起こったか*(動詞)*、およびコンテキスト*(名詞)*は、文脈から明らかでない限り、

 VS Code API の例は、アクティブテキストエディタ (*onDid*) が変更されたとき (*verb*) に発生したイベントである `window.onDidChangeActiveTextEditor` です。

## 厳密な null

 VS Code API は、 [厳密な null チェック](https://github.com/Microsoft/TypeScript/pull/7140) をサポートするために、適切な場合には　Typescript の `undefined` と `null` 型を使用します。

## Node.js モジュールを使用した拡張機能

あなたの拡張モジュールは実行時に [Node.js](https://nodejs.org) モジュールに依存することができます。 Node モジュール自体と同様に、依存関係を `dependency` フィールドを使って [`package.json`拡張マニフェスト](/docs/extensionAPI/extension-manifest.md) に追加できます。

VS Code 固有の Node.js モジュールでさえ、 [拡張開発で役立つ](/docs/extensionAPI/extension-manifest.md#useful-node-modules) があります。

### インストールとパッケージ化

Visual Studio Code は、ユーザーがインストールしたときに拡張機能の依存関係をインストール**しない**ので、公開前に `npm install` する必要があります。拡張機能の公開パッケージには、すべての依存関係が含まれます。 `vsce ls` を実行すると、`vsce` がパッケージに含めるすべてのファイルをリストすることができます。

`.vscodeignore` ファイルを作成して、拡張パッケージに含まれていないファイルを除外することができます。 `.vscodeignore` ファイルの使用については、 [詳細](https://code.visualstudio.com/docs/extensions/publish-extension.md#vscodeignore) の `vsce` 公開ツールのトピックを参照してください。

## 次のステップ

* [拡張マニフェストファイル](/docs/extensionAPI/extension-manifest.md) - Visual Studio Code package.json 拡張マニフェストファイルリファレンス
* [Contribution Points](/docs/extensionAPI/extension-points.md) - VS Code contribution point リファレンス
* [アクティベーションイベント](/docs/extensionAPI/activation-events.md) - VS Code アクティベーションイベントリファレンス

## よくある質問

**Q: 拡張モジュールでネイティブNode.jsモジュールを使用できますか？**

**A:** Visual Studioのコード拡張パッケージには、すべての依存関係が含まれています。これは、Windowsで拡張機能を開発し、その拡張機能を公開するときにネイティブNode.jsモジュールに依存する場合、Windowsでコンパイルされたネイティブ依存関係が拡張機能に含まれることを意味します。 MacまたはLinuxのユーザーはこの拡張機能を使用できません。

今のところこの作業を行う唯一の方法は、 VS Code の4つのプラットフォーム(Windows x86とx64、Linux、Mac)のすべてのバイナリを拡張機能に組み込み、動的に正しいコードをロードするコードを持つことです。

拡張機能にバンドルされたネイティブモジュールは、 VS Code が同梱されている同じNode.jsバージョンに対して VS Code の新しいバージョンごとに再コンパイルする必要があるため、ネイティブ `npm`モジュールを使用する拡張機能は推奨しません。開発ツールコンソール (**Help** > **Toggle Developer Tools**) から `process.versions` を実行すると、Node.jsとモジュールのバージョンが見つかります。