---
Order: 10
Area: extensions
TOCTitle: Publishing Extensions
ContentId: 7EA90618-43A3-4873-A9B5-61CC131CE4EE
PageTitle: Publishing Visual Studio Code Extensions
DateApproved: 5/4/2017
MetaDescription: Learn how to publish Visual Studio Code extensions to the public Marketplace and share them with other developers.
---
# 公開拡張機能

## vsce  - 公開ツールのリファレンス

[vsce](https://github.com/Microsoft/vsce) は、 [Extension Marketplace](/docs/editor/extension-gallery.md) に拡張機能を公開するために使用するコマンドラインツールです。

## インストール

[Node.js](https://nodejs.org/) がインストールされていることを確認してください。 それから以下を実行します:

```
npm install -g vsce
```

## 使用法

`vsce`　コマンドをコマンドラインから直接使用します。
たとえば、拡張機能をすばやく公開する方法は次のとおりです:

```
$ vsce publish
Publishing uuid@0.0.1...
Successfully published uuid@0.0.1!
```

使用可能なすべてのコマンドのリファレンスを得るには、 `vsce --help`　を実行してください。

## 拡張の公開

Visual Studio Code は、マーケットプレースサービスについて[Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs) を利用しています。 つまり、拡張機能の認証、ホスティング、および管理は、そのサービスを通じて提供されます。

`vsce` は [Personal Access Tokens](https://www.visualstudio.com/en-us/news/2015-jul-7-vso.aspx) を使って拡張機能を公開することしかできません。 拡張機能を公開するには、少なくとも1つ作成する必要があります。

### 個人アクセストークンを取得する

まず、 [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-visual-studio-online) アカウントがあることを確認します。

次の例では、アカウント名は `monacotools` です。 あなたのアカウントのホームページ (例えば、 `https：//monacotools.visualstudio.com`) から、 **セキュリティ** ページに行きます:

![Security page](images/publish-extension/publishers1.png)

新しい個人用アクセストークンを作成するには、 **追加** をクリックします:

![Add personal access token](images/publish-extension/publishers2.png)

パーソナルアクセストークンに素敵な説明を与え、オプションとして有効期限を1年間に延長し、すべてのアカウントにアクセスさせ、 **すべてのスコープ** への権限を設定します:

![Personal access token details](images/publish-extension/publishers3.png)

次の画面には、新しく作成したパーソナルアクセストークンが表示されます。 **コピー** それは公開するために必要です。

### Publisher を作成する

**Publisher** は、 Visual Studio Code マーケットプレイスの拡張機能を公開できるユーザーです。 すべての拡張機能は、[`package.json` ファイル](/docs/extensionAPI/extension-manifest.md) に `publisher` という名前を入れる必要があります。

[Personal Access Token](/docs/extensions/publish-extension.md#get-a-personal-access-token) を取得したら、 `vsce` を使用して新しいパブリッシャを作成することができます：

```bash
vsce create-publisher (publisher name)
```

`vsce` は、この publisher への今後の参照のために提供された Personal Access Token を覚えています。

**注意：** 次のセクションで説明するように、 https://marketplace.visualstudio.com/manage であなたのサイト運営者を作成し、 `vsce` でログインしてください。

### Publisher へのログイン

すでに Publisher を作成していて、 `vsce` でそれを使用したい場合は:

```bash
vsce login (publisher name)
```

`create-publisher` コマンドと同様に、 `vsce` はあなたに Personal Access Token を尋ね、将来のコマンドのためにそれを覚えています。

また、オプションのパラメータ `-p <token>` を発行して Personal Access Token を入力することもできます。

```bash
vsce publish -p <token>
```

##拡張バージョンの自動インクリメント

[SemVer](http://semver.org/) 互換番号を指定することで、拡張時に拡張子のバージョン番号を自動的にインクリメントすることができます： `major`、 `minor`、 `patch`。


たとえば、拡張機能のバージョンを 1.0.0 から 1.1.0 に更新する場合は、 `minor` を指定します。

```bash
vsce publish minor
```

これにより、拡張機能を公開する前に、拡張機能の `package.json` [version](/docs/extension-manifest.md#fields) 属性が変更されます。
また、完全な SemVer 互換バージョンをコマンドラインで指定することもできます:

```bash
vsce publish 2.0.1
```

## パッケージ拡張

拡張機能をストアに公開せずにパッケージ化することができます。 拡張機能は常に `.vsix` ファイルにパッケージ化されます。 次を実行します:

```bash
vsce package
```

拡張モジュールを `.vsix`　ファイルにパッケージ化し、それを現在のディレクトリに置きます。 Visual Studio Code に `.vsix` ファイルをインストールすることは可能です。 詳細は、 [VSIXからのインストール](/docs/editor/extension-gallery.md#install-from-a-vsix) を参照してください。

### 他者と個人情報を共有する

あなたの拡張を個人的に他の人と共有したい場合は、あなたのパッケージ化された拡張子 `.vsix`　ファイルを送ることができます。

## Visual Studio Code の互換性

拡張機能の作成時には、拡張機能が Visual Studio にどのような互換性があるかを記述する必要があります。 これは `package.json` 内の `engine.vscode` フィールドで行うことができます:

```json
{
  "engines": {
    "vscode": "^1.8.0"
  }
}
```

値 `1.8.0` は、あなたの拡張が VS Code `1.8.0` としか互換性がないことを意味します。 `^1.8.0` の値はあなたの拡張が VS Code `1.8.0` 以降と互換性があることを意味し、 `1.8.1`、 `1.9.0` などを含みます。

`engine.vscode` フィールドを使って、あなたが依存している API を含むクライアントのためだけに拡張機能がインストールされるようにすることができます。
このメカニズムは、安定版リリースと Insider リリースでうまくいきます。

たとえば、VSコードの最新の安定版が 1.8.0 で、 `1.9.0` の開発中に新しい API が導入され、 Insider リリースでバージョン 1.9.0-insider で利用可能になったとします。
この API の恩恵を受ける拡張バージョンを公開したい場合は、バージョン依存性を `^1.9.0` で示す必要があります。 あなたの新しい拡張バージョンは、VS Code `>=1.9.0` にのみインストールされます。つまり、現在のすべての Insider のお客様はそれを取得しますが、安定版は Stable が 1.9.0 になったときにのみアップデートを取得します。

## 高度な使用法

### マーケットプレース Integration

Visual Studio マーケットプレース で拡張機能がどのように表示されるかをカスタマイズすることができます。 例については、[Go 拡張](https://marketplace.visualstudio.com/items/lukehoban.Go) を参照してください。

マーケットプレースでエクステンションをすばらしいものにするためのヒントをいくつか紹介します：

 - 拡張機能のルートにある `README.md` ファイルを使用して、拡張機能の マーケットプレースページの内容を入力します。 `vsce`　は2種類の方法で　README　リンクを変更します：
  - `package.json`　に `repository`フィールドを追加し、それが公開 GitHub リポジトリであれば、 `vsce` はそれを自動的に検出し、それに応じてリンクを調整します。
  - `vsce package` を実行するときに `--baseContentUrl` と `--baseImagesUrl` フラグを使って、その動作を無効にしたり、設定したりすることができます。 次に、パッケージ化された `.vsix` ファイルへのパスを `vsce publish` の引数として渡して拡張子を公開します。
- 拡張機能のルートにある `LICENSE` ファイルは、拡張機能のライセンスの内容として使用されます。
- 拡張子のルートにある `CHANGELOG.md` ファイルは、拡張機能の変更履歴の内容として使用されます。
- バナーの背景色は `galleryBanner.color` を `package.json` の目的の16進値に設定することで設定できます。
- 拡張に含まれる `128px` PNG ファイルの相対パスに` icon` を `package.json` で設定して、アイコンを設定することができます。

[マーケットプレースプレゼンテーションのヒント](/docs/extensionAPI/extension-manifest.md＃marketplace-presentation-tips) も参照してください。

### `.vscodeignore`

`.vscodeignore`　ファイルを作成して、拡張機能の　package にいくつかのファイルが含まれないようにすることができます。 このファイルは、1行に1つずつ [glob](https://github.com/isaacs/minimatch) パターンのコレクションです。

例:

```
**/*.ts
**/tsconfig.json
!file.ts
```

実行時に不要なファイルはすべて無視する必要があります。 例えば、 あなたの拡張が TypeScript で書かれている場合は、前の例のように `**/*.ts` ファイルをすべて無視する必要があります。

**注意： `devDependencies` にリストされている開発依存関係は自動的に無視されるので、 `.vscodeignore` ファイルに追加する必要はありません。

### 事前公開ステップ

マニフェストファイルに事前公開ステップを追加することは可能です。 このコマンドは、拡張機能がパッケージ化されるたびに呼び出されます。

```json
{
    "name": "uuid",
    "version": "0.0.1",
    "publisher": "joaomoreno",
    "engines": {
        "vscode": "0.10.x"
    },
    "scripts": {
        "vscode:prepublish": "tsc"
    }
}
```

拡張モジュールがパッケージ化されるときは常に、 [TypeScript](https://www.typescriptlang.org/) コンパイラが呼び出されます。

## 次のステップ

* [Extension Marketplace](/docs/editor/extension-gallery.md) - VS Code の公開拡張マーケットプレイスの詳細をご覧ください。
* [Testing Extensions](/docs/extensions/testing-extensions.md) - 拡張プロジェクトにテストを追加して高品質を確保します。

## よくある質問

**Q: なぜエクステンションを公開しようとすると、403 Forbidden (または 401 Unauthorized) エラーが表示されるのですか？**

**A:** PAT (Personal Access Token) を作成するときに間違いを犯すのは、 Accounts フィールドのプルダウンで `all accessible accounts` を選択しないことです。 また、公開スコープを `All scopes` に設定して、公開が機能するようにする必要があります。

**Q: `vsce` ツールを使って拡張機能を公開解除できますか?**

**A:** publisher name やサイト運営者名を変更した可能性があります。 また、[管理ページ](https://marketplace.visualstudio.com/manage) に移動してマーケットプレースで直接管理することもできます。 サイト運営者の管理ページから拡張機能を更新したり、公開を解除したりすることができます。

**Q: vsce　がファイル属性を保持しないのはなぜですか？**

**A:** Windows　から拡張機能をビルドして公開する場合、拡張パッケージに含まれるすべてのファイルは POSIX ファイル属性、つまり実行可能ビットがありません。 いくつかの `node_modules` 依存関係は、正しく機能するためにそれらの属性に依存しています。 Linux および OS X からの公開は期待通りに機能します。
