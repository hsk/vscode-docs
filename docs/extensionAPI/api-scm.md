---
Order: 9
Area: extensionapi
TOCTitle: Source Control API
ContentId: 79996489-8D16-4C0A-8BE8-FF4B1E9C223A
PageTitle: Visual Studio Code Source Control API
DateApproved: 5/4/2017
MetaDescription: Visual Studio Code extensions (plug-ins) Source Control API.
---
# VS Code のソース管理

Visual Studio Code を使用すると、拡張機能の作成者は拡張機能APIを通じてソース管理 (SCM) 機能を定義できます。 スリムでありながら強力な API サーフェスがあり、さまざまな SCM システムを VS Code に統合できます。同時に、すべての SCM システムと共通のユーザーインターフェイスを備えています。

![VS Code SCM](images/api-scm/main.png)

 VS Code 自体は、1つのソース管理プロバイダ Git と一緒に出荷されます。このドキュメントは、独自の SCM システムを統合するのに役立ちます。

このドキュメントでは、常に[`vscode` 名前空間 API リファレンス](/docs/extensionAPI/vscode-api.md#scm)を参照できることに注意してください。

## ソース管理モデル

`SourceControl` は、ソース管理モデルに **リソース状態**、` SourceControlResourceState` のインスタンスを設定する責任を負うエンティティです。リソース状態は、それ自体、 **グループ**、 `SourceControlResourceGroup` のインスタンスにまとめられています。

`vscode.scm.createSourceControl` で新しい SourceControl を作成することができます。

これらの3つのエンティティがどのように相互に関連しているかをよりよく理解するために、 [Git](https://github.com/Microsoft/vscode/tree/master/extensions/git) を例にしましょう。 `git status` の次の出力を考えてみましょう：

```bash
vsce master* → git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.md
        renamed:    src/api.ts -> src/test/api.ts

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        deleted:    .travis.yml
        modified:   README.md
```

このワークスペースでは多くのことが起こっています。 最初に、 `README.md` ファイルが変更され、ステージングされ、再度修正されました。次に、 `src/api.ts` ファイルが `src/test/api.ts` に移動され、その移動が実行されました。最後に、 `.travis.yml` ファイルが削除されました。

このワークスペースでは、 **作業ツリー** と **インデックス** という2つのリソースグループを定義しています。そのグループ内の各 **ファイル変更** は **リソース状態** です:

- **インデックス** - リソースグループ
   - `README.md`、変更されたリソース状態
   - `src/test/api.ts`、 `src/api.ts` から名前を変更した - リソース状態
- **ワーキングツリー** - リソースグループ
   - `.travis.yml`、 削除 - リソース状態
   - `README.md`、 変更されたリソース状態

同じファイル `README.md` が2つの別個のリソース状態の一部であることに注意してください。

Git がこのモデルを作成する方法は次のとおりです:

```ts
function createResourceUri(relativePath: string): vscode.Uri {
  const absolutePath = path.join(vscode.workspace.rootPath, relativePath);
  return vscode.Uri.file(absolutePath);
}

const gitSCM = vscode.scm.createSourceControl('git', "Git");

const index = gitSCM.createResourceGroup('index', "Index");
index.resourceStates = [
  { resourceUri: createResourceUri('README.md') },
  { resourceUri: createResourceUri('src/test/api.ts') }
];

const workingTree = gitSCM.createResourceGroup('workingTree', "Changes");
workingTree.resourceStates = [
  { resourceUri: createResourceUri('.travis.yml') },
  { resourceUri: createResourceUri('README.md') }
];
```

ソースコントロールとリソースグループに対する変更は、ソースコントロールビューに反映されます。

## ソースコントロールビュー

 VS Code は、ソース管理モデルが変更されると、ソース管理ビューに移入することができます。リソース状態は `SourceControlResourceDecorations` を使ってカスタマイズできます:

```ts
export interface SourceControlResourceState {
  readonly decorations?: SourceControlResourceDecorations;
}
```

前の例では、ソース管理ビューに単純なリストを作成するのには十分ですが、ユーザーが各リソースで実行したいと思う多くのユーザー操作があります。たとえば、ユーザーがリソース状態をクリックするとどうなりますか？リソース状態には、このアクションを処理するコマンドをオプションで指定できます。

```ts
export interface SourceControlResourceState {
  readonly command?: Command;
}
```

### メニュー

ユーザーにもっと豊かなユーザーインターフェイスを提供するために、メニュー項目を配置できる3つのソース管理メニューIDがあります。

`scm/title` メニューは、 SCM ビューのタイトルの右側にあります。 `navigation` グループのメニュー項目はインラインになり、他の項目は `...` ドロップダウン内に表示されます。

`scm/resourceGroup/context` と `scm/resourceState/context` は似ています。前者はリソースグループをカスタマイズできるようにし、後者はリソース状態を参照します。 `inline` グループにメニューアイテムを配置し、インラインにします。他のすべてのメニュー項目グループは、マウスの右クリックで通常アクセスできるコンテキストメニューで表示されます。これらのメニューから呼び出されたコマンドは、それぞれのリソース状態が引数として渡されます。 SCM ビューでは複数選択がサポートされているため、コマンドは一度に複数のリソースを引数で受け取ることがあります。

たとえば、 Git は複数のファイルをステージングするために `git.stage` コマンドを `scm/resourceState/context` メニューに追加し、そのようなメソッド宣言を使用します:

```ts
stage(...resourceStates: SourceControlResourceState[]): Promise<void>;
```

それらを作成するとき、 `SourceControl` と `SourceControlResourceGroup` インスタンスは `id` 文字列を提供する必要があります。これらの値は、 `scmProvider` コンテキストキーと `scmResourceGroup` コンテキストキーにそれぞれ設定されます。これらのコンテキストキーは、メニューアイテムの `when` 節に依存することができます。 Git が `git.stage` コマンドのメニュー項目を表示する方法は次のとおりです:

```json
{
  "command": "git.stage",
  "when": "scmProvider == git && scmResourceGroup == merge",
  "group": "inline"
}
```

### SCM 入力ボックス

Source Control ビューの上部にある Source Control Input Box では、ユーザーがメッセージを入力できます。操作を実行するためにこのメッセージを取得(および設定)することができます。たとえば Git では、これはコミットボックスとして使用され、ユーザがコミットメッセージを入力し、 `git commit` コマンドがそれらをピックアップします。

```ts
export interface SourceControlInputBox {
  value: string;
}

export namespace scm {
  export const inputBox: SourceControlInputBox;
}
```

ユーザは任意のメッセージを受け入れるために、<kbd>Ctrl+Enter</kbd> (または macOS では <kbd>Cmd+Enter</kbd>) と入力することができます。あなたはあなたの `SourceControl` インスタンスに `acceptInputCommand` を提供することでこのイベントを処理できます。

```ts
export interface SourceControl {
  readonly acceptInputCommand?: Command;
}
```

## クイック差分

VS Code は、 **quick diff** エディターガターデコレーションの表示もサポートしています。

![VS Code SCM](images/api-scm/quickdiff.png)

これらのデコレーションは、 VS Code 自体によって計算されます。任意のファイルの元の内容を VS Code で提供するだけです。

```ts
export interface SourceControl {
  quickDiffProvider?: QuickDiffProvider;
}
```

`QuickDiffProvider` を使って、あなたの実装は、 `Uri` が引数として提供されるリソースと一致する元のリソースの `Uri` を VS Code に伝えることができます。

このAPIを [`workspace` 名前空間の`registerTextDocumentContentProvider`メソッド](/docs/extensionAPI/vscode-api.md#workspace) と組み合わせることができます。これは、 `Uri` を使って任意のリソースの内容を提供することができます。

## 次のステップ

 VS Code 拡張モデルの詳細については、次のトピックを参照してください。

* [SCM APIリファレンス](/docs/extensionAPI/vscode-api.md#scm) - 完全な SCM API ドキュメントを読む
* [Git Extension](https://github.com/Microsoft/vscode/tree/master/extensions/git) - Git 拡張の実装を読むことで学びます。
* [Extension API Overview](/docs/extensionAPI/overview.md) - 完全な VS Code 拡張性モデルについて学びます。
* [拡張マニフェストファイル](/docs/extensionAPI/extension-manifest.md) - VS Code package.json 拡張マニフェストファイルリファレンス
* [Contribution Points](/docs/extensionAPI/extension-points.md) - VS Code 投稿ポイントの参照
