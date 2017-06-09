---
Order: 6
Area: extensionapi
TOCTitle: vscode namespace API
ContentId: 8CEBCDF8-4F0A-4C81-A904-3DEA43480EA6
PageTitle: Visual Studio Code API Reference
DateApproved: 5/4/2017
MetaDescription: Visual Studio Code extensions (plug-ins) API Reference.  
---

# vscode namespace API
## commands



<div class="comment"><p>コマンドを扱うための名前空間。
つまり、コマンドは固有の識別子を持つ関数です。
この関数は、 <em>command handler</em> と呼ばれることもあります。</p>
<p>コマンドは<a href="#commands.registerCommand">registerCommand</a>コマンドを使ってエディタに追加することができます。
および<a href="#commands.registerTextEditorCommand">registerTextEditorCommand</a>関数を使用します。
コマンドは<a href="#commands.executeCommand">手動で</a>またはUIジェスチャーから実行できます。
それらは：</p>
<ul>
<li>palette - <code>package.json</code> の <code>commands</code> セクションを使って<a href="https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette">command palette</a>にコマンドを表示させます。</li>
<li>keybinding - <code>package.json</code> の <code>keybindings</code> セクションを有効にするには
<a href="https://code.visualstudio.com/docs/getstarted/keybindings#_customizing-shortcuts">keybindings</a>
あなたの内線番号。</li>
</ul>
<p>他の拡張機能やエディタ自体からのコマンドは、拡張機能からアクセスできます。
ただし、エディタコマンドを呼び出すときは、すべての引数タイプがサポートされているわけではありません。</p>
<p>これは、コマンドハンドラを登録し、そのコマンドのエントリをパレットに追加するサンプルです。
最初に識別子 &#39;extension.sayHello`を持つコマンドハンドラを登録します。</p>

<pre><code class="lang-javascript">commands.registerCommand(<span class="hljs-string">'extension.sayHello'</span>, () =&gt; {
    <span class="hljs-built_in">window</span>.showInformationMessage(<span class="hljs-string">'Hello World!'</span>);
});
</code></pre>
<p>次に、コマンド識別子をパレットに表示するタイトル( <code>package.json</code> )にバインドします。</p>

<pre><code class="lang-json">{
    <span class="hljs-attr">"contributes"</span>: {
        <span class="hljs-attr">"commands"</span>: [{
            <span class="hljs-attr">"command"</span>: <span class="hljs-string">"extension.sayHello"</span>,
            <span class="hljs-attr">"title"</span>: <span class="hljs-string">"Hello World"</span>
        }]
    }
}
</code></pre>
</div>

#### Functions



<a name="commands.executeCommand"></a><span class="ts" id=1192 data-target="#details-1192" data-toggle="collapse"><span class="ident">executeCommand</span><span>&lt;</span>T<span>&gt;</span><span>(</span><span class="ident">command</span><span>: </span><a class="type-instrinct">string</a>, <span>...</span><span class="ident">rest</span><span>: </span><a class="type-instrinct">any</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1192">
<div class="comment"><p>指定されたコマンド識別子で指定されたコマンドを実行します。</p>
<p>エディタコマンドを実行する際、すべての型を引数として渡すことはできません。
使用できるプリミティブ型は <code>string</code> 、 <code>boolean</code> 、
<code>number</code> 、 <code>undefined</code> 、および <code>null</code> 、およびこのAPIで定義されたクラスです。
提供されたコマンドを実行するときに制限はありません
拡張によって*。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="command"></a><span class="ts" id=1194 data-target="#details-1194" data-toggle="collapse"><span class="ident">command</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="rest"></a><span class="ts" id=1195 data-target="#details-1195" data-toggle="collapse"><span>...</span><span class="ident">rest</span><span>: </span><a class="type-instrinct">any</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>指定されたコマンドの戻り値に解決されるthenable。
コマンドハンドラ関数が何も返さないときは <code>undefined</code> を返します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="commands.getCommands"></a><span class="ts" id=1197 data-target="#details-1197" data-toggle="collapse"><span class="ident">getCommands</span><span>(</span><span class="ident">filterInternal</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a>[]&gt;</span>
<div class="details collapse" id="details-1197">
<div class="comment"><p>使用可能なすべてのコマンドのリストを取得します。アンダースコアを開始するコマンドは次のとおりです。
内部コマンドとして扱われます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="filterInternal"></a><span class="ts" id=1198 data-target="#details-1198" data-toggle="collapse"><span class="ident">filterInternal</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a>[]&gt;</span></td><td><div class="comment"><p>コマンドIDのリストに解決されるThenable。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="commands.registerCommand"></a><span class="ts" id=1174 data-target="#details-1174" data-toggle="collapse"><span class="ident">registerCommand</span><span>(</span><span class="ident">command</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">callback</span><span>: </span>(args: <a class="type-instrinct">any</a>[]) =&gt; <a class="type-instrinct">any</a>, <span class="ident">thisArg</span><span>?</span><span>: </span><a class="type-instrinct">any</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1174">
<div class="comment"><p>キーボードショートカット、メニューアイテム、アクション、または直接、呼び出すことができるコマンドを登録します。</p>
<p>既存のコマンド識別子を2回使用してコマンドを登録すると、エラーが発生します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="command"></a><span class="ts" id=1175 data-target="#details-1175" data-toggle="collapse"><span class="ident">command</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="callback"></a><span class="ts" id=1176 data-target="#details-1176" data-toggle="collapse"><span class="ident">callback</span><span>: </span>(args: <a class="type-instrinct">any</a>[]) =&gt; <a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="thisArg"></a><span class="ts" id=1180 data-target="#details-1180" data-toggle="collapse"><span class="ident">thisArg</span><span>?</span><span>: </span><a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのコマンドの登録を解除するDisposable。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="commands.registerTextEditorCommand"></a><span class="ts" id=1182 data-target="#details-1182" data-toggle="collapse"><span class="ident">registerTextEditorCommand</span><span>(</span><span class="ident">command</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">callback</span><span>: </span>(textEditor: <a class="type-ref" href="#TextEditor">TextEditor</a>, edit: <a class="type-ref" href="#TextEditorEdit">TextEditorEdit</a>, args: <a class="type-instrinct">any</a>[]) =&gt; <a class="type-instrinct">void</a>, <span class="ident">thisArg</span><span>?</span><span>: </span><a class="type-instrinct">any</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1182">
<div class="comment"><p>キーボードショートカット、メニュー項目、アクション、または直接呼び出すことができるテキストエディタコマンドを登録します。</p>
<p>テキストエディタコマンドは、コマンドが呼び出されたときにアクティブなエディタがある場合にのみ実行されるため、通常の<a href="#commands.registerCommand">commands</a>とは異なります。
また、エディタコマンドのコマンドハンドラは、アクティブなエディタと
<a href="#TextEditorEdit">編集</a>-builder。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="command"></a><span class="ts" id=1183 data-target="#details-1183" data-toggle="collapse"><span class="ident">command</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="callback"></a><span class="ts" id=1184 data-target="#details-1184" data-toggle="collapse"><span class="ident">callback</span><span>: </span>(textEditor: <a class="type-ref" href="#TextEditor">TextEditor</a>, edit: <a class="type-ref" href="#TextEditorEdit">TextEditorEdit</a>, args: <a class="type-instrinct">any</a>[]) =&gt; <a class="type-instrinct">void</a></span></td><td><div class="comment"><p>(#TextEditor)と<a href="#TextEditorEdit">edit</a>にアクセスできるコマンドハンドラ関数です。</p>
</div></td></tr>
<tr><td><a name="thisArg"></a><span class="ts" id=1190 data-target="#details-1190" data-toggle="collapse"><span class="ident">thisArg</span><span>?</span><span>: </span><a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのコマンドの登録を解除するDisposable。</p>
</div></td></tr>
</table>
</div>
</div>

## env



<div class="comment"><p>エディタが実行される環境を説明する名前空間。</p>
</div>

#### Variables



<a name="env.appName"></a><span class="ts" id=1168 data-target="#details-1168" data-toggle="collapse"><span class="ident">appName</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1168">
<div class="comment"><p>&#39;VSコード&#39;のようなエディタのアプリケーション名。</p>
<ul>
<li><em>readonly</em></li>
</ul>
</div>
</div>



<a name="env.language"></a><span class="ts" id=1169 data-target="#details-1169" data-toggle="collapse"><span class="ident">language</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1169">
<div class="comment"><p><code>de-CH</code> 、 <code>fr</code> 、 <code>en-US</code> のような好みのユーザ言語を表します。</p>
<ul>
<li><em>readonly</em></li>
</ul>
</div>
</div>



<a name="env.machineId"></a><span class="ts" id=1170 data-target="#details-1170" data-toggle="collapse"><span class="ident">machineId</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1170">
<div class="comment"><p>コンピュータの一意の識別子。</p>
<ul>
<li><em>readonly</em></li>
</ul>
</div>
</div>



<a name="env.sessionId"></a><span class="ts" id=1171 data-target="#details-1171" data-toggle="collapse"><span class="ident">sessionId</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1171">
<div class="comment"><p>現在のセッションの一意の識別子。
エディタが起動するたびに変更されます。</p>
<ul>
<li><em>readonly</em></li>
</ul>
</div>
</div>

## extensions



<div class="comment"><p>インストールされた拡張機能を扱うための名前空間。
拡張機能は、拡張機能(#拡張機能) - それらを反映できるインタフェースで表されます。</p>
<p>拡張ライターは、API公開サーフェスを <code>activate</code> -callから返すことによって、他の拡張機能にAPIを提供することができます。</p>
<p>```javascript エクスポート関数activate(context：vscode.ExtensionContext){ let api = { sum(a、b){ a + bを返します。
}、 mul(a、b){ a * bを返します。
}
};</p>
</div>

#### Variables



<a name="extensions.all"></a><span class="ts" id=1474 data-target="#details-1474" data-toggle="collapse"><span class="ident">all</span><span>: </span><a class="type-ref" href="#Extension">Extension</a>&lt;<a class="type-instrinct">any</a>&gt;[]</span>
<div class="details collapse" id="details-1474">
<div class="comment"><p>システムに現在知られているすべての拡張機能。</p>
</div>
</div>

#### Functions



<a name="extensions.getExtension"></a><span class="ts" id=1469 data-target="#details-1469" data-toggle="collapse"><span class="ident">getExtension</span><span>(</span><span class="ident">extensionId</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#Extension">Extension</a>&lt;<a class="type-instrinct">any</a>&gt; &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-1469">
<div class="comment"><p>拡張子を <code>publisher.name</code> の形式で完全な識別子で取得します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="extensionId"></a><span class="ts" id=1470 data-target="#details-1470" data-toggle="collapse"><span class="ident">extensionId</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Extension">Extension</a>&lt;<a class="type-instrinct">any</a>&gt; &#124; <a class="type-instrinct">undefined</a></span></td><td><div class="comment"><p>拡張子または <code>undefined</code> です。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="extensions.getExtension"></a><span class="ts" id=1471 data-target="#details-1471" data-toggle="collapse"><span class="ident">getExtension</span><span>&lt;</span>T<span>&gt;</span><span>(</span><span class="ident">extensionId</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#Extension">Extension</a>&lt;<a class="type-instrinct">T</a>&gt; &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-1471">
<div class="comment"><p>拡張子を <code>publisher.name</code> の形式で取得します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="extensionId"></a><span class="ts" id=1473 data-target="#details-1473" data-toggle="collapse"><span class="ident">extensionId</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Extension">Extension</a>&lt;<a class="type-instrinct">T</a>&gt; &#124; <a class="type-instrinct">undefined</a></span></td><td><div class="comment"><p>拡張子または <code>undefined</code> です。</p>
</div></td></tr>
</table>
</div>
</div>

## languages



<div class="comment"><p>IntelliSense、コードアクション、診断などの言語固有のエディタ<a href="https://code.visualstudio.com/docs/editor/editingevolved">機能</a>に参加するための名前空間</p>
<p>多くのプログラミング言語が存在し、シンタックス、セマンティクス、およびパラダイムには多種多様があります。
それにもかかわらず、自動ワード補完、コードナビゲーション、コードチェックなどの機能は、さまざまなプログラミング言語で異なるツール間で普及しています。</p>
<p>エディタには、すべてのUIとアクションを既に用意し、データのみを提供することで参加できるようにすることで、共通の機能を簡単に提供できるAPIが提供されています。
例えば、ホバーに貢献するには、<a href="#TextDocument">TextDocument</a>とホバー情報を返す<a href="#Position">Position</a>で呼び出せる関数を用意するだけです。残りの部分は、
マウス、ホバーの位置を決める、ホバーを安定に保つなどはエディターが行います。</p>

<pre><code class="lang-javascript">languages.registerHoverProvider( <span class="hljs-string">'javascript'</span>、{
provideHover(ドキュメント、位置、トークン){
新しいホバーを返す(「私はホバーです！」);
}
});
</code></pre>
<p>登録は <code>javascript</code> のような言語IDか <code>{language： &#39;typescript&#39;、scheme： &#39;file&#39;のようなもっと複雑な[filter](#DocumentFilter)のいずれかである[document selector](#DocumentSelector) }</code>。
ドキュメントをそのようなセレクタに照合すると、プロバイダの使用方法と使用方法を決定するために使用される<a href="#languages.match">score</a>が返されます。
スコアが等しい場合は、最後に来たプロバイダが勝ちます。</p>
<ul>
<li><a href="#languages.registerHoverProvider">hover</a>のようなフルアリティを可能にする機能の場合、スコアは<a href="#languages.registerCompletionItemProvider">IntelliSense</a>などの他の機能の場合にのみスコアが使用されますプロバイダが参加するように求められる順序を決定する。</li>
</ul>
</div>

#### Functions



<a name="languages.createDiagnosticCollection"></a><span class="ts" id=1384 data-target="#details-1384" data-toggle="collapse"><span class="ident">createDiagnosticCollection</span><span>(</span><span class="ident">name</span><span>?</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#DiagnosticCollection">DiagnosticCollection</a></span>
<div class="details collapse" id="details-1384">
<div class="comment"><p>診断コレクションを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="name"></a><span class="ts" id=1385 data-target="#details-1385" data-toggle="collapse"><span class="ident">name</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#DiagnosticCollection">DiagnosticCollection</a></span></td><td><div class="comment"><p>新しい診断コレクションです。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.getLanguages"></a><span class="ts" id=1378 data-target="#details-1378" data-toggle="collapse"><span class="ident">getLanguages</span><span>(</span><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a>[]&gt;</span>
<div class="details collapse" id="details-1378">
<div class="comment"><p>既知のすべての言語の識別子を返します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a>[]&gt;</span></td><td><div class="comment"><p>識別子文字列の配列への解決を約束します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.match"></a><span class="ts" id=1380 data-target="#details-1380" data-toggle="collapse"><span class="ident">match</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a><span>)</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-1380">
<div class="comment"><p>ドキュメント<a href="#DocumentSelector">selector</a>とドキュメントの一致を計算します。
0より大きい値は、セレクタがドキュメントと一致することを意味します。</p>
<p>マッチは以下のルールに従って計算されます：1。</p>
<p><a href="#DocumentSelector"><code>DocumentSelector</code></a>が配列の場合、含まれる各DocumentFilterまたは言語識別子の一致を計算し、最大値をとります。
2。
文字列は<a href="#DocumentFilter">DocumentFilter`</a>の <code>language</code> 部分になるようにdesugaredされるので、 <code>` fooLang&quot;</code>は` {language： &quot;fooLang&quot;}と似ています。
3。</p>
<p><a href="#DocumentFilter">DocumentFilter`</a>は、その部分をドキュメントと比較することによってドキュメントと照合されます。
以下の規則が適用されます： 1。</p>
<p><code>DocumentFilter</code> が空の場合( <code>{}</code> )、結果は <code>0</code> です 2。</p>
<p><code>scheme</code> 、 <code>language</code> または <code>pattern</code> が定義されているが、一致しない場合は <code>0</code> です。
3。
`* &#39;とのマッチングはスコア「5」を与え、等価またはグロブパターンを介したマッチングは「10」のスコアを与える
4.結果は各試合の最大値です</p>
<p>サンプル：
```js</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1381 data-target="#details-1381" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="document"></a><span class="ts" id=1382 data-target="#details-1382" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">number</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="languages.registerCodeActionsProvider"></a><span class="ts" id=1392 data-target="#details-1392" data-toggle="collapse"><span class="ident">registerCodeActionsProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#CodeActionProvider">CodeActionProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1392">
<div class="comment"><p>コードアクションプロバイダを登録する。</p>
<p>複数のプロバイダを言語に登録することができます。その場合、プロバイダーは
パラレルに変換し、結果をマージします。失敗したプロバイダ(約束または例外を拒否)は、
操作全体の失敗を引き起こさない。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1393 data-target="#details-1393" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1394 data-target="#details-1394" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#CodeActionProvider">CodeActionProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerCodeLensProvider"></a><span class="ts" id=1396 data-target="#details-1396" data-toggle="collapse"><span class="ident">registerCodeLensProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#CodeLensProvider">CodeLensProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1396">
<div class="comment"><p>コードレンズ提供者を登録する。</p>
<p>複数のプロバイダを言語に登録することができます。その場合、プロバイダーは
パラレルに変換し、結果をマージします。失敗したプロバイダ(約束または例外を拒否)は、
操作全体の失敗を引き起こさない。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1397 data-target="#details-1397" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1398 data-target="#details-1398" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#CodeLensProvider">CodeLensProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerCompletionItemProvider"></a><span class="ts" id=1387 data-target="#details-1387" data-toggle="collapse"><span class="ident">registerCompletionItemProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#CompletionItemProvider">CompletionItemProvider</a>, <span>...</span><span class="ident">triggerCharacters</span><span>: </span><a class="type-instrinct">string</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1387">
<div class="comment"><p>補完提供者を登録する。</p>
<p>複数のプロバイダを言語に登録することができます。
その場合、プロバイダは<a href="#languages.match">score</a>でソートされ、等しいスコアのグループには
完成品。このプロセスは、グループの1人または複数のプロバイダが
結果。失敗したプロバイダ(約束または例外が拒否された場合)
動作。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1388 data-target="#details-1388" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1389 data-target="#details-1389" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#CompletionItemProvider">CompletionItemProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="triggerCharacters"></a><span class="ts" id=1390 data-target="#details-1390" data-toggle="collapse"><span>...</span><span class="ident">triggerCharacters</span><span>: </span><a class="type-instrinct">string</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerDefinitionProvider"></a><span class="ts" id=1400 data-target="#details-1400" data-toggle="collapse"><span class="ident">registerDefinitionProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#DefinitionProvider">DefinitionProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1400">
<div class="comment"><p>定義プロバイダを登録します。</p>
<p>複数のプロバイダを言語に登録することができます。その場合、プロバイダーは
パラレルに変換し、結果をマージします。失敗したプロバイダ(約束または例外を拒否)は、
操作全体の失敗を引き起こさない。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1401 data-target="#details-1401" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1402 data-target="#details-1402" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#DefinitionProvider">DefinitionProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerDocumentFormattingEditProvider"></a><span class="ts" id=1435 data-target="#details-1435" data-toggle="collapse"><span class="ident">registerDocumentFormattingEditProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#DocumentFormattingEditProvider">DocumentFormattingEditProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1435">
<div class="comment"><p>ドキュメントの書式設定プロバイダを登録します。</p>
<p>複数のプロバイダを言語に登録することができます。
その場合、プロバイダーは<a href="#languages.match">score</a>でソートされ、最も一致するプロバイダーが使用されます。失敗
が選択されたプロバイダーの場合、全体の操作が失敗することになります。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1436 data-target="#details-1436" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1437 data-target="#details-1437" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#DocumentFormattingEditProvider">DocumentFormattingEditProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerDocumentHighlightProvider"></a><span class="ts" id=1416 data-target="#details-1416" data-toggle="collapse"><span class="ident">registerDocumentHighlightProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#DocumentHighlightProvider">DocumentHighlightProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1416">
<div class="comment"><p>文書ハイライト提供者を登録する。</p>
<p>複数のプロバイダを言語に登録することができます。
その場合、プロバイダーは<a href="#languages.match">スコア</a>でソートされ、グループではドキュメントのハイライトが順番に求められます。
プロバイダが「偽でない」または「失敗していない」結果を返すと、プロセスは停止します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1417 data-target="#details-1417" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1418 data-target="#details-1418" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#DocumentHighlightProvider">DocumentHighlightProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerDocumentLinkProvider"></a><span class="ts" id=1454 data-target="#details-1454" data-toggle="collapse"><span class="ident">registerDocumentLinkProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#DocumentLinkProvider">DocumentLinkProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1454">
<div class="comment"><p>ドキュメントリンクプロバイダを登録します。</p>
<p>複数のプロバイダを言語に登録することができます。その場合、プロバイダーは
パラレルに変換し、結果をマージします。失敗したプロバイダ(約束または例外を拒否)は、
操作全体の失敗を引き起こさない。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1455 data-target="#details-1455" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1456 data-target="#details-1456" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#DocumentLinkProvider">DocumentLinkProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerDocumentRangeFormattingEditProvider"></a><span class="ts" id=1439 data-target="#details-1439" data-toggle="collapse"><span class="ident">registerDocumentRangeFormattingEditProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#DocumentRangeFormattingEditProvider">DocumentRangeFormattingEditProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1439">
<div class="comment"><p>ドキュメント範囲の書式設定プロバイダを登録します。</p>
<p><em>注：</em>ドキュメント範囲プロバイダも<a href="#DocumentFormattingEditProvider">ドキュメントフォーマッタ</a>です。
これは、範囲プロバイダを登録するときに、ドキュメントフォーマッタを<a href="registerDocumentFormattingEditProvider">register</a>する必要がないことを意味します。</p>
<p>複数のプロバイダを言語に登録することができます。
その場合、プロバイダーは<a href="#languages.match">score</a>でソートされ、最も一致するプロバイダーが使用されます。失敗
が選択されたプロバイダーの場合、全体の操作が失敗することになります。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1440 data-target="#details-1440" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1441 data-target="#details-1441" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#DocumentRangeFormattingEditProvider">DocumentRangeFormattingEditProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="languages.registerDocumentSymbolProvider"></a><span class="ts" id=1420 data-target="#details-1420" data-toggle="collapse"><span class="ident">registerDocumentSymbolProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#DocumentSymbolProvider">DocumentSymbolProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1420">
<div class="comment"><p>ドキュメントシンボルプロバイダを登録します。</p>
<p>複数のプロバイダを言語に登録することができます。その場合、プロバイダーは
パラレルに変換し、結果をマージします。失敗したプロバイダ(約束または例外を拒否)は、
操作全体の失敗を引き起こさない。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1421 data-target="#details-1421" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1422 data-target="#details-1422" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#DocumentSymbolProvider">DocumentSymbolProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerHoverProvider"></a><span class="ts" id=1412 data-target="#details-1412" data-toggle="collapse"><span class="ident">registerHoverProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#HoverProvider">HoverProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1412">
<div class="comment"><p>ホバー提供者を登録する。</p>
<p>複数のプロバイダを言語に登録することができます。その場合、プロバイダーは
パラレルに変換し、結果をマージします。失敗したプロバイダ(約束または例外を拒否)は、
操作全体の失敗を引き起こさない。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1413 data-target="#details-1413" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1414 data-target="#details-1414" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#HoverProvider">HoverProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerImplementationProvider"></a><span class="ts" id=1404 data-target="#details-1404" data-toggle="collapse"><span class="ident">registerImplementationProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#ImplementationProvider">ImplementationProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1404">
<div class="comment"><p>実装プロバイダを登録する。</p>
<p>複数のプロバイダを言語に登録することができます。その場合、プロバイダーは
パラレルに変換し、結果をマージします。失敗したプロバイダ(約束または例外を拒否)は、
操作全体の失敗を引き起こさない。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1405 data-target="#details-1405" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1406 data-target="#details-1406" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#ImplementationProvider">ImplementationProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerOnTypeFormattingEditProvider"></a><span class="ts" id=1443 data-target="#details-1443" data-toggle="collapse"><span class="ident">registerOnTypeFormattingEditProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#OnTypeFormattingEditProvider">OnTypeFormattingEditProvider</a>, <span class="ident">firstTriggerCharacter</span><span>: </span><a class="type-instrinct">string</a>, <span>...</span><span class="ident">moreTriggerCharacter</span><span>: </span><a class="type-instrinct">string</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1443">
<div class="comment"><p>型で動作する書式設定プロバイダを登録します。
プロバイダは、ユーザが <code>editor.formatOnType</code> の設定を有効にするとアクティブになります。</p>
<p>複数のプロバイダを言語に登録することができます。
その場合、プロバイダーは<a href="#languages.match">score</a>でソートされ、最も一致するプロバイダーが使用されます。失敗
が選択されたプロバイダーの場合、全体の操作が失敗することになります。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1444 data-target="#details-1444" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1445 data-target="#details-1445" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#OnTypeFormattingEditProvider">OnTypeFormattingEditProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="firstTriggerCharacter"></a><span class="ts" id=1446 data-target="#details-1446" data-toggle="collapse"><span class="ident">firstTriggerCharacter</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"><p><code>}</code> のように、書式設定を開始する文字。</p>
</div></td></tr>
<tr><td><a name="moreTriggerCharacter"></a><span class="ts" id=1447 data-target="#details-1447" data-toggle="collapse"><span>...</span><span class="ident">moreTriggerCharacter</span><span>: </span><a class="type-instrinct">string</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerReferenceProvider"></a><span class="ts" id=1427 data-target="#details-1427" data-toggle="collapse"><span class="ident">registerReferenceProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#ReferenceProvider">ReferenceProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1427">
<div class="comment"><p>参照プロバイダーを登録する。</p>
<p>複数のプロバイダを言語に登録することができます。その場合、プロバイダーは
パラレルに変換し、結果をマージします。失敗したプロバイダ(約束または例外を拒否)は、
操作全体の失敗を引き起こさない。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1428 data-target="#details-1428" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1429 data-target="#details-1429" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#ReferenceProvider">ReferenceProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerRenameProvider"></a><span class="ts" id=1431 data-target="#details-1431" data-toggle="collapse"><span class="ident">registerRenameProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#RenameProvider">RenameProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1431">
<div class="comment"><p>参照プロバイダーを登録する。</p>
<p>複数のプロバイダを言語に登録することができます。
その場合、プロバイダーは<a href="#languages.match">score</a>でソートされ、最も一致するプロバイダーが使用されます。失敗
が選択されたプロバイダーの場合、全体の操作が失敗することになります。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1432 data-target="#details-1432" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1433 data-target="#details-1433" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#RenameProvider">RenameProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerSignatureHelpProvider"></a><span class="ts" id=1449 data-target="#details-1449" data-toggle="collapse"><span class="ident">registerSignatureHelpProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#SignatureHelpProvider">SignatureHelpProvider</a>, <span>...</span><span class="ident">triggerCharacters</span><span>: </span><a class="type-instrinct">string</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1449">
<div class="comment"><p>署名のヘルププロバイダを登録してください。</p>
<p>複数のプロバイダを言語に登録することができます。
この場合、プロバイダは<a href="#languages.match">スコア</a>でソートされ、プロバイダが返すまで順番に呼び出されます
有効な結果。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1450 data-target="#details-1450" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1451 data-target="#details-1451" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#SignatureHelpProvider">SignatureHelpProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="triggerCharacters"></a><span class="ts" id=1452 data-target="#details-1452" data-toggle="collapse"><span>...</span><span class="ident">triggerCharacters</span><span>: </span><a class="type-instrinct">string</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerTypeDefinitionProvider"></a><span class="ts" id=1408 data-target="#details-1408" data-toggle="collapse"><span class="ident">registerTypeDefinitionProvider</span><span>(</span><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#TypeDefinitionProvider">TypeDefinitionProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1408">
<div class="comment"><p>型定義プロバイダを登録する。</p>
<p>複数のプロバイダを言語に登録することができます。その場合、プロバイダーは
パラレルに変換し、結果をマージします。失敗したプロバイダ(約束または例外を拒否)は、
操作全体の失敗を引き起こさない。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="selector"></a><span class="ts" id=1409 data-target="#details-1409" data-toggle="collapse"><span class="ident">selector</span><span>: </span><a class="type-ref" href="#DocumentSelector">DocumentSelector</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1410 data-target="#details-1410" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#TypeDefinitionProvider">TypeDefinitionProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.registerWorkspaceSymbolProvider"></a><span class="ts" id=1424 data-target="#details-1424" data-toggle="collapse"><span class="ident">registerWorkspaceSymbolProvider</span><span>(</span><span class="ident">provider</span><span>: </span><a class="type-ref" href="#WorkspaceSymbolProvider">WorkspaceSymbolProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1424">
<div class="comment"><p>ワークスペースシンボルプロバイダを登録します。</p>
<p>複数のプロバイダを登録することができます。その場合、プロバイダは並行して質問され、
結果がマージされます。失敗したプロバイダ(約束または例外を拒否)は、
全体の操作の失敗。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="provider"></a><span class="ts" id=1425 data-target="#details-1425" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#WorkspaceSymbolProvider">WorkspaceSymbolProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="languages.setLanguageConfiguration"></a><span class="ts" id=1458 data-target="#details-1458" data-toggle="collapse"><span class="ident">setLanguageConfiguration</span><span>(</span><span class="ident">language</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">configuration</span><span>: </span><a class="type-ref" href="#LanguageConfiguration">LanguageConfiguration</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1458">
<div class="comment"><p>言語の<a href="#LanguageConfiguration">言語設定</a>を設定します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="language"></a><span class="ts" id=1459 data-target="#details-1459" data-toggle="collapse"><span class="ident">language</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"><p><code>typescript</code> のような言語識別子。</p>
</div></td></tr>
<tr><td><a name="configuration"></a><span class="ts" id=1460 data-target="#details-1460" data-toggle="collapse"><span class="ident">configuration</span><span>: </span><a class="type-ref" href="#LanguageConfiguration">LanguageConfiguration</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>この設定を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>

## scm



<div class="comment"></div>

#### Variables



<a name="scm.inputBox"></a><span class="ts" id=1462 data-target="#details-1462" data-toggle="collapse"><span class="ident">inputBox</span><span>: </span><a class="type-ref" href="#SourceControlInputBox">SourceControlInputBox</a></span>
<div class="details collapse" id="details-1462">
<div class="comment"><p>ソースコントロールビューレットの<a href="#SourceControlInputBox">入力ボックス</a>。</p>
</div>
</div>

#### Functions



<a name="scm.createSourceControl"></a><span class="ts" id=1464 data-target="#details-1464" data-toggle="collapse"><span class="ident">createSourceControl</span><span>(</span><span class="ident">id</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">label</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#SourceControl">SourceControl</a></span>
<div class="details collapse" id="details-1464">
<div class="comment"><p>新しい<a href="#SourceControl">ソースコントロール</a>インスタンスを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="id"></a><span class="ts" id=1465 data-target="#details-1465" data-toggle="collapse"><span class="ident">id</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="label"></a><span class="ts" id=1466 data-target="#details-1466" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#SourceControl">SourceControl</a></span></td><td><div class="comment"><p>のインスタンス(#SourceControl)。</p>
</div></td></tr>
</table>
</div>
</div>

## window



<div class="comment"><p>エディタの現在のウィンドウを扱うための名前空間。
これは、目に見えてアクティブなエディタだけでなく、メッセージ、選択、およびユーザー入力を表示するUI要素です。</p>
</div>

#### Variables



<a name="window.activeTextEditor"></a><span class="ts" id=1200 data-target="#details-1200" data-toggle="collapse"><span class="ident">activeTextEditor</span><span>: </span><a class="type-ref" href="#TextEditor">TextEditor</a> &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-1200">
<div class="comment"><p>現在アクティブなエディタまたは <code>undefined</code>。
現在アクティブなエディタは、現在フォーカスを持っているエディタです。
フォーカスがない場合は、直前に入力を変更したエディタです。</p>
</div>
</div>



<a name="window.visibleTextEditors"></a><span class="ts" id=1201 data-target="#details-1201" data-toggle="collapse"><span class="ident">visibleTextEditors</span><span>: </span><a class="type-ref" href="#TextEditor">TextEditor</a>[]</span>
<div class="details collapse" id="details-1201">
<div class="comment"><p>現在表示されているエディタまたは空の配列。</p>
</div>
</div>

#### Events



<a name="window.onDidChangeActiveTextEditor"></a><span class="ts" id=1202 data-target="#details-1202" data-toggle="collapse"><span class="ident">onDidChangeActiveTextEditor</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#TextEditor">TextEditor</a>&gt;</span>
<div class="details collapse" id="details-1202">
<div class="comment"><p><a href="#window.activeTextEditor">アクティブなエディタ</a>が起動したときに起動する<a href="#イベント">イベント</a>
変更されました。</p>
<ul>
<li>*アクティブなエディタが <code>undefined</code> に変わったときにイベントが発生することもあります。</li>
</ul>
</div>
</div>



<a name="window.onDidChangeTextEditorOptions"></a><span class="ts" id=1205 data-target="#details-1205" data-toggle="collapse"><span class="ident">onDidChangeTextEditorOptions</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#TextEditorOptionsChangeEvent">TextEditorOptionsChangeEvent</a>&gt;</span>
<div class="details collapse" id="details-1205">
<div class="comment"><p><a href="#イベント">イベント</a>エディタのオプションが変更されたときに起動します。</p>
</div>
</div>



<a name="window.onDidChangeTextEditorSelection"></a><span class="ts" id=1204 data-target="#details-1204" data-toggle="collapse"><span class="ident">onDidChangeTextEditorSelection</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#TextEditorSelectionChangeEvent">TextEditorSelectionChangeEvent</a>&gt;</span>
<div class="details collapse" id="details-1204">
<div class="comment"><p>エディタでの選択が変更されたときに発生する<a href="#イベント">イベント</a>。</p>
</div>
</div>



<a name="window.onDidChangeTextEditorViewColumn"></a><span class="ts" id=1206 data-target="#details-1206" data-toggle="collapse"><span class="ident">onDidChangeTextEditorViewColumn</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#TextEditorViewColumnChangeEvent">TextEditorViewColumnChangeEvent</a>&gt;</span>
<div class="details collapse" id="details-1206">
<div class="comment"><p>エディタのビュー列が変更されたときに発生する<a href="#イベント">イベント</a>。</p>
</div>
</div>



<a name="window.onDidChangeVisibleTextEditors"></a><span class="ts" id=1203 data-target="#details-1203" data-toggle="collapse"><span class="ident">onDidChangeVisibleTextEditors</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#TextEditor">TextEditor</a>[]&gt;</span>
<div class="details collapse" id="details-1203">
<div class="comment"><p>[visible editor]の配列(#window.visibleTextEditors)が呼び出されたときに発生する<a href="#Event">event</a>
変更されました。</p>
</div>
</div>



<a name="window.onDidCloseTerminal"></a><span class="ts" id=1207 data-target="#details-1207" data-toggle="collapse"><span class="ident">onDidCloseTerminal</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#Terminal">Terminal</a>&gt;</span>
<div class="details collapse" id="details-1207">
<div class="comment"><p>端末が破棄されたときに起動する<a href="#イベント">イベント</a>。</p>
</div>
</div>

#### Functions



<a name="window.createOutputChannel"></a><span class="ts" id=1285 data-target="#details-1285" data-toggle="collapse"><span class="ident">createOutputChannel</span><span>(</span><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#OutputChannel">OutputChannel</a></span>
<div class="details collapse" id="details-1285">
<div class="comment"><p>指定した名前で新しい<a href="#OutputChannel">出力チャネル</a>を作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="name"></a><span class="ts" id=1286 data-target="#details-1286" data-toggle="collapse"><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"><p>UIでチャンネルを表すために使用される人間が読める文字列です。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#OutputChannel">OutputChannel</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="window.createStatusBarItem"></a><span class="ts" id=1314 data-target="#details-1314" data-toggle="collapse"><span class="ident">createStatusBarItem</span><span>(</span><span class="ident">alignment</span><span>?</span><span>: </span><a class="type-ref" href="#StatusBarAlignment">StatusBarAlignment</a>, <span class="ident">priority</span><span>?</span><span>: </span><a class="type-instrinct">number</a><span>)</span><span>: </span><a class="type-ref" href="#StatusBarItem">StatusBarItem</a></span>
<div class="details collapse" id="details-1314">
<div class="comment"><p>ステータスバー<a href="#StatusBarItem">item</a>を作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="alignment"></a><span class="ts" id=1315 data-target="#details-1315" data-toggle="collapse"><span class="ident">alignment</span><span>?</span><span>: </span><a class="type-ref" href="#StatusBarAlignment">StatusBarAlignment</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="priority"></a><span class="ts" id=1316 data-target="#details-1316" data-toggle="collapse"><span class="ident">priority</span><span>?</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#StatusBarItem">StatusBarItem</a></span></td><td><div class="comment"><p>新しいステータスバー項目。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.createTerminal"></a><span class="ts" id=1318 data-target="#details-1318" data-toggle="collapse"><span class="ident">createTerminal</span><span>(</span><span class="ident">name</span><span>?</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">shellPath</span><span>?</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">shellArgs</span><span>?</span><span>: </span><a class="type-instrinct">string</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Terminal">Terminal</a></span>
<div class="details collapse" id="details-1318">
<div class="comment"><p><a href="#端末">端末</a>を作成します。ターミナルのcwdはワークスペースディレクトリになります
明示的なcustomStartPath設定が存在するかどうかに関係なく、存在する場合は*。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="name"></a><span class="ts" id=1319 data-target="#details-1319" data-toggle="collapse"><span class="ident">name</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"><p>UIで端末を表すために人間が読める文字列(オプション)。</p>
</div></td></tr>
<tr><td><a name="shellPath"></a><span class="ts" id=1320 data-target="#details-1320" data-toggle="collapse"><span class="ident">shellPath</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="shellArgs"></a><span class="ts" id=1321 data-target="#details-1321" data-toggle="collapse"><span class="ident">shellArgs</span><span>?</span><span>: </span><a class="type-instrinct">string</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Terminal">Terminal</a></span></td><td><div class="comment"><p>新しい端末。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.createTerminal"></a><span class="ts" id=1322 data-target="#details-1322" data-toggle="collapse"><span class="ident">createTerminal</span><span>(</span><span class="ident">options</span><span>: </span><a class="type-ref" href="#TerminalOptions">TerminalOptions</a><span>)</span><span>: </span><a class="type-ref" href="#Terminal">Terminal</a></span>
<div class="details collapse" id="details-1322">
<div class="comment"><p><a href="#端末">端末</a>を作成します。ターミナルのcwdはワークスペースディレクトリになります
明示的なcustomStartPath設定が存在するかどうかに関係なく、存在する場合は*。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="options"></a><span class="ts" id=1323 data-target="#details-1323" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#TerminalOptions">TerminalOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Terminal">Terminal</a></span></td><td><div class="comment"><p>新しい端末。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.createTextEditorDecorationType"></a><span class="ts" id=1217 data-target="#details-1217" data-toggle="collapse"><span class="ident">createTextEditorDecorationType</span><span>(</span><span class="ident">options</span><span>: </span><a class="type-ref" href="#DecorationRenderOptions">DecorationRenderOptions</a><span>)</span><span>: </span><a class="type-ref" href="#TextEditorDecorationType">TextEditorDecorationType</a></span>
<div class="details collapse" id="details-1217">
<div class="comment"><p>テキストエディタに装飾を追加するために使用できるTextEditorDecorationTypeを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="options"></a><span class="ts" id=1218 data-target="#details-1218" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#DecorationRenderOptions">DecorationRenderOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#TextEditorDecorationType">TextEditorDecorationType</a></span></td><td><div class="comment"><p>新しいデコレーションタイプのインスタンス。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.registerTreeDataProvider"></a><span class="ts" id=1325 data-target="#details-1325" data-toggle="collapse"><span class="ident">registerTreeDataProvider</span><span>&lt;</span>T<span>&gt;</span><span>(</span><span class="ident">viewId</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">treeDataProvider</span><span>: </span><a class="type-ref" href="#TreeDataProvider">TreeDataProvider</a>&lt;<a class="type-instrinct">T</a>&gt;<span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1325">
<div class="comment"><p>拡張ポイント <code>views</code> を使って提供されたビューの<a href="#TreeDataProvider">TreeDataProvider</a>を登録します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="viewId"></a><span class="ts" id=1327 data-target="#details-1327" data-toggle="collapse"><span class="ident">viewId</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="treeDataProvider"></a><span class="ts" id=1328 data-target="#details-1328" data-toggle="collapse"><span class="ident">treeDataProvider</span><span>: </span><a class="type-ref" href="#TreeDataProvider">TreeDataProvider</a>&lt;<a class="type-instrinct">T</a>&gt;</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="window.setStatusBarMessage"></a><span class="ts" id=1288 data-target="#details-1288" data-toggle="collapse"><span class="ident">setStatusBarMessage</span><span>(</span><span class="ident">text</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">hideAfterTimeout</span><span>: </span><a class="type-instrinct">number</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1288">
<div class="comment"><p>ステータスバーにメッセージを設定します。
これは、より強力なステータスバー<a href="#window.createStatusBarItem">items</a>の短い手です。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="text"></a><span class="ts" id=1289 data-target="#details-1289" data-toggle="collapse"><span class="ident">text</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="hideAfterTimeout"></a><span class="ts" id=1290 data-target="#details-1290" data-toggle="collapse"><span class="ident">hideAfterTimeout</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>ステータスバーメッセージを隠す使い捨て。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.setStatusBarMessage"></a><span class="ts" id=1291 data-target="#details-1291" data-toggle="collapse"><span class="ident">setStatusBarMessage</span><span>(</span><span class="ident">text</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">hideWhenDone</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">any</a>&gt;<span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1291">
<div class="comment"><p>ステータスバーにメッセージを設定します。
*これは、より強力なステータスバー<a href="#window.createStatusBarItem">items</a>の短い手です。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="text"></a><span class="ts" id=1292 data-target="#details-1292" data-toggle="collapse"><span class="ident">text</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="hideWhenDone"></a><span class="ts" id=1293 data-target="#details-1293" data-toggle="collapse"><span class="ident">hideWhenDone</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">any</a>&gt;</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>ステータスバーメッセージを隠す使い捨て。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.setStatusBarMessage"></a><span class="ts" id=1294 data-target="#details-1294" data-toggle="collapse"><span class="ident">setStatusBarMessage</span><span>(</span><span class="ident">text</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1294">
<div class="comment"><p>ステータスバーにメッセージを設定します。
これは、より強力なステータスバー<a href="#window.createStatusBarItem">items</a>の短い手です。</p>
<p><em>注</em>ステータスバーメッセージはスタックしています。
より長い使用。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="text"></a><span class="ts" id=1295 data-target="#details-1295" data-toggle="collapse"><span class="ident">text</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>ステータスバーメッセージを隠す使い捨て。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showErrorMessage"></a><span class="ts" id=1254 data-target="#details-1254" data-toggle="collapse"><span class="ident">showErrorMessage</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1254">
<div class="comment"><p>エラーメッセージを表示します。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1255 data-target="#details-1255" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1256 data-target="#details-1256" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目に解決されるthenable、または却下されるときに <code>undefined</code> が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showErrorMessage"></a><span class="ts" id=1257 data-target="#details-1257" data-toggle="collapse"><span class="ident">showErrorMessage</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1257">
<div class="comment"><p>エラーメッセージを表示します。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1258 data-target="#details-1258" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=1259 data-target="#details-1259" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1260 data-target="#details-1260" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目に解決されるthenable、または却下されるときに <code>undefined</code> が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showErrorMessage"></a><span class="ts" id=1261 data-target="#details-1261" data-toggle="collapse"><span class="ident">showErrorMessage</span><span>&lt;</span>T extends <a class="type-ref" href="#MessageItem">MessageItem</a><span>&gt;</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1261">
<div class="comment"><p>エラーメッセージを表示します。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1263 data-target="#details-1263" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1264 data-target="#details-1264" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目に解決されるthenable、または却下されるときに <code>undefined</code> が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showErrorMessage"></a><span class="ts" id=1265 data-target="#details-1265" data-toggle="collapse"><span class="ident">showErrorMessage</span><span>&lt;</span>T extends <a class="type-ref" href="#MessageItem">MessageItem</a><span>&gt;</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1265">
<div class="comment"><p>エラーメッセージを表示します。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1267 data-target="#details-1267" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=1268 data-target="#details-1268" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1269 data-target="#details-1269" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目に解決されるthenable、または却下されるときに <code>undefined</code> が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showInformationMessage"></a><span class="ts" id=1220 data-target="#details-1220" data-toggle="collapse"><span class="ident">showInformationMessage</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1220">
<div class="comment"><p>ユーザーに情報メッセージを表示する。必要に応じて提示されるアイテムの配列を提供する
クリック可能なボタン。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1221 data-target="#details-1221" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1222 data-target="#details-1222" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="window.showInformationMessage"></a><span class="ts" id=1223 data-target="#details-1223" data-toggle="collapse"><span class="ident">showInformationMessage</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1223">
<div class="comment"><p>ユーザーに情報メッセージを表示する。必要に応じて提示されるアイテムの配列を提供する
クリック可能なボタン。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1224 data-target="#details-1224" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=1225 data-target="#details-1225" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1226 data-target="#details-1226" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目に解決されるthenable、または却下されるときに <code>undefined</code> が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showInformationMessage"></a><span class="ts" id=1227 data-target="#details-1227" data-toggle="collapse"><span class="ident">showInformationMessage</span><span>&lt;</span>T extends <a class="type-ref" href="#MessageItem">MessageItem</a><span>&gt;</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1227">
<div class="comment"><p>情報メッセージを表示する。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1229 data-target="#details-1229" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1230 data-target="#details-1230" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目に解決されるthenable、または却下されるときに <code>undefined</code> が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showInformationMessage"></a><span class="ts" id=1231 data-target="#details-1231" data-toggle="collapse"><span class="ident">showInformationMessage</span><span>&lt;</span>T extends <a class="type-ref" href="#MessageItem">MessageItem</a><span>&gt;</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1231">
<div class="comment"><p>情報メッセージを表示する。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1233 data-target="#details-1233" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=1234 data-target="#details-1234" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1235 data-target="#details-1235" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目に解決されるthenable、または却下されるときに <code>undefined</code> が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showInputBox"></a><span class="ts" id=1281 data-target="#details-1281" data-toggle="collapse"><span class="ident">showInputBox</span><span>(</span><span class="ident">options</span><span>?</span><span>: </span><a class="type-ref" href="#InputBoxOptions">InputBoxOptions</a>, <span class="ident">token</span><span>?</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1281">
<div class="comment"><p>ユーザーに入力を求める入力ボックスを開きます。</p>
<p>入力ボックスがキャンセルされた場合(ESCを押すなど)、戻り値は <code>undefined</code> になります。それ以外の場合
戻り値はユーザーが入力した文字列、またはユーザーが入力しなかった場合は空の文字列です
何でもOKで入力ボックスを却下しました。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="options"></a><span class="ts" id=1282 data-target="#details-1282" data-toggle="collapse"><span class="ident">options</span><span>?</span><span>: </span><a class="type-ref" href="#InputBoxOptions">InputBoxOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=1283 data-target="#details-1283" data-toggle="collapse"><span class="ident">token</span><span>?</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>ユーザーが提供した文字列に解決する約束。
解雇の場合は `未定義 &#39;にする。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showQuickPick"></a><span class="ts" id=1271 data-target="#details-1271" data-toggle="collapse"><span class="ident">showQuickPick</span><span>(</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[] &#124; <a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a>[]&gt;, <span class="ident">options</span><span>?</span><span>: </span><a class="type-ref" href="#QuickPickOptions">QuickPickOptions</a>, <span class="ident">token</span><span>?</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1271">
<div class="comment"><p>選択リストを表示します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="items"></a><span class="ts" id=1272 data-target="#details-1272" data-toggle="collapse"><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[] &#124; <a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a>[]&gt;</span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=1273 data-target="#details-1273" data-toggle="collapse"><span class="ident">options</span><span>?</span><span>: </span><a class="type-ref" href="#QuickPickOptions">QuickPickOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=1274 data-target="#details-1274" data-toggle="collapse"><span class="ident">token</span><span>?</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択または「未定義」に解決する約束。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showQuickPick"></a><span class="ts" id=1275 data-target="#details-1275" data-toggle="collapse"><span class="ident">showQuickPick</span><span>&lt;</span>T extends <a class="type-ref" href="#QuickPickItem">QuickPickItem</a><span>&gt;</span><span>(</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[] &#124; <a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a>[]&gt;, <span class="ident">options</span><span>?</span><span>: </span><a class="type-ref" href="#QuickPickOptions">QuickPickOptions</a>, <span class="ident">token</span><span>?</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1275">
<div class="comment"><p>選択リストを表示します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="items"></a><span class="ts" id=1277 data-target="#details-1277" data-toggle="collapse"><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[] &#124; <a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a>[]&gt;</span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=1278 data-target="#details-1278" data-toggle="collapse"><span class="ident">options</span><span>?</span><span>: </span><a class="type-ref" href="#QuickPickOptions">QuickPickOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=1279 data-target="#details-1279" data-toggle="collapse"><span class="ident">token</span><span>?</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目または <code>undefined</code> を解決する約束です。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showTextDocument"></a><span class="ts" id=1209 data-target="#details-1209" data-toggle="collapse"><span class="ident">showTextDocument</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">column</span><span>?</span><span>: </span><a class="type-ref" href="#ViewColumn">ViewColumn</a>, <span class="ident">preserveFocus</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextEditor">TextEditor</a>&gt;</span>
<div class="details collapse" id="details-1209">
<div class="comment"><p>テキストエディタで指定のドキュメントを表示します。</p>
<p><a href="#ViewColumn">column</a>は、エディタが表示されている場所を制御するために提供されます。</p>
<p><a href="#window.activeTextEditor">アクティブエディタ</a>を変更することがあります。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=1210 data-target="#details-1210" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="column"></a><span class="ts" id=1211 data-target="#details-1211" data-toggle="collapse"><span class="ident">column</span><span>?</span><span>: </span><a class="type-ref" href="#ViewColumn">ViewColumn</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="preserveFocus"></a><span class="ts" id=1212 data-target="#details-1212" data-toggle="collapse"><span class="ident">preserveFocus</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p><code>true</code> の場合、エディタはフォーカスを取得しません。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextEditor">TextEditor</a>&gt;</span></td><td><div class="comment"><p>(#TextEditor)に解決する約束です。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showTextDocument"></a><span class="ts" id=1213 data-target="#details-1213" data-toggle="collapse"><span class="ident">showTextDocument</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">options</span><span>?</span><span>: </span><a class="type-ref" href="#TextDocumentShowOptions">TextDocumentShowOptions</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextEditor">TextEditor</a>&gt;</span>
<div class="details collapse" id="details-1213">
<div class="comment"><p>テキストエディタで指定のドキュメントを表示します。</p>
<p><a href="#ViewColumn">column</a>は、エディタが表示されている場所を制御するために提供されます。</p>
<p><a href="#window.activeTextEditor">アクティブエディタ</a>を変更することがあります。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=1214 data-target="#details-1214" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=1215 data-target="#details-1215" data-toggle="collapse"><span class="ident">options</span><span>?</span><span>: </span><a class="type-ref" href="#TextDocumentShowOptions">TextDocumentShowOptions</a></span></td><td><div class="comment"><p>(#ShowTextDocumentOptions)は、<a href="#TextEditor">editor</a>を表示する動作を設定します。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextEditor">TextEditor</a>&gt;</span></td><td><div class="comment"><p>(#TextEditor)に解決する約束です。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showWarningMessage"></a><span class="ts" id=1237 data-target="#details-1237" data-toggle="collapse"><span class="ident">showWarningMessage</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1237">
<div class="comment"><p>警告メッセージを表示します。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1238 data-target="#details-1238" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1239 data-target="#details-1239" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目に解決されるthenable、または却下されるときに <code>undefined</code> が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showWarningMessage"></a><span class="ts" id=1240 data-target="#details-1240" data-toggle="collapse"><span class="ident">showWarningMessage</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1240">
<div class="comment"><p>警告メッセージを表示します。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1241 data-target="#details-1241" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=1242 data-target="#details-1242" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1243 data-target="#details-1243" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">string</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目に解決されるthenable、または却下されるときに <code>undefined</code> が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showWarningMessage"></a><span class="ts" id=1244 data-target="#details-1244" data-toggle="collapse"><span class="ident">showWarningMessage</span><span>&lt;</span>T extends <a class="type-ref" href="#MessageItem">MessageItem</a><span>&gt;</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1244">
<div class="comment"><p>警告メッセージを表示します。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1246 data-target="#details-1246" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1247 data-target="#details-1247" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目に解決されるthenable、または却下されるときに <code>undefined</code> が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.showWarningMessage"></a><span class="ts" id=1248 data-target="#details-1248" data-toggle="collapse"><span class="ident">showWarningMessage</span><span>&lt;</span>T extends <a class="type-ref" href="#MessageItem">MessageItem</a><span>&gt;</span><span>(</span><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a>, <span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span>
<div class="details collapse" id="details-1248">
<div class="comment"><p>警告メッセージを表示します。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="message"></a><span class="ts" id=1250 data-target="#details-1250" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=1251 data-target="#details-1251" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#MessageOptions">MessageOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="items"></a><span class="ts" id=1252 data-target="#details-1252" data-toggle="collapse"><span>...</span><span class="ident">items</span><span>: </span><a class="type-instrinct">T</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a>&gt;</span></td><td><div class="comment"><p>選択された項目に解決されるthenable、または却下されるときに <code>undefined</code> が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.withProgress"></a><span class="ts" id=1304 data-target="#details-1304" data-toggle="collapse"><span class="ident">withProgress</span><span>&lt;</span>R<span>&gt;</span><span>(</span><span class="ident">options</span><span>: </span><a class="type-ref" href="#ProgressOptions">ProgressOptions</a>, <span class="ident">task</span><span>: </span>(progress: <a class="type-ref" href="#Progress">Progress</a>&lt;{message: <a class="type-instrinct">string</a>}&gt;) =&gt; <a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">R</a>&gt;<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">R</a>&gt;</span>
<div class="details collapse" id="details-1304">
<div class="comment"><p>エディタで進行状況を表示します。
指定されたコールバックを実行している間にプログレスが表示され、返された約束は解決されず、拒否されません。
進捗状況(およびその他の詳細)は、渡された<a href="#ProgressOptions"><code>ProgressOptions</code></a>で定義されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="options"></a><span class="ts" id=1306 data-target="#details-1306" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#ProgressOptions">ProgressOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="task"></a><span class="ts" id=1307 data-target="#details-1307" data-toggle="collapse"><span class="ident">task</span><span>: </span>(progress: <a class="type-ref" href="#Progress">Progress</a>&lt;{message: <a class="type-instrinct">string</a>}&gt;) =&gt; <a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">R</a>&gt;</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">R</a>&gt;</span></td><td><div class="comment"><p>thenableタスクコールバックが返されました。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="window.withScmProgress"></a><span class="ts" id=1297 data-target="#details-1297" data-toggle="collapse"><span class="ident">withScmProgress</span><span>&lt;</span>R<span>&gt;</span><span>(</span><span class="ident">task</span><span>: </span>(progress: <a class="type-ref" href="#Progress">Progress</a>&lt;<a class="type-instrinct">number</a>&gt;) =&gt; <a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">R</a>&gt;<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">R</a>&gt;</span>
<div class="details collapse" id="details-1297">
<div class="comment"><ul>
<li><em>deprecated</em> - この関数は<strong>非推奨</strong>です。
代わりに <code>withProgress</code> を使用してください。</li>
</ul>
<p>~~指定されたコールバックを実行している間、ソースコントロールビューレットの進行状況を表示します。
返された約束は解決されず、却下されません。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="task"></a><span class="ts" id=1299 data-target="#details-1299" data-toggle="collapse"><span class="ident">task</span><span>: </span>(progress: <a class="type-ref" href="#Progress">Progress</a>&lt;<a class="type-instrinct">number</a>&gt;) =&gt; <a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">R</a>&gt;</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">R</a>&gt;</span></td><td><div class="comment"><p>その次のタスクはrseturnでした。</p>
</div></td></tr>
</table>
</div>
</div>

## workspace



<div class="comment"><p>現在のワークスペースを扱うための名前空間。
ワークスペースとは、開かれているフォルダを表します。
ファイルだけでフォルダは開かれていないときは、ワークスペースはありません。</p>
<p>ワークスペースは、<a href="#workspace.createFileSystemWatcher">listening</a>をfsイベントに、<a href="#workspace.findFiles">finding</a>ファイルに対応しています。
どちらもうまく動作し、エディタプロセスをoutside_実行するので、nodejsに相当するものの代わりに常に使用する必要があります。</p>
</div>

#### Variables



<a name="workspace.rootPath"></a><span class="ts" id=1336 data-target="#details-1336" data-toggle="collapse"><span class="ident">rootPath</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-1336">
<div class="comment"><p>エディタで開いているフォルダ。
フォルダがないときは <code>undefined</code>
が開かれました。</p>
<ul>
<li><em>readonly</em></li>
</ul>
</div>
</div>



<a name="workspace.textDocuments"></a><span class="ts" id=1352 data-target="#details-1352" data-toggle="collapse"><span class="ident">textDocuments</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>[]</span>
<div class="details collapse" id="details-1352">
<div class="comment"><p>現在システムに知られているすべてのテキスト文書。</p>
<ul>
<li><em>readonly</em></li>
</ul>
</div>
</div>

#### Events



<a name="workspace.onDidChangeConfiguration"></a><span class="ts" id=1375 data-target="#details-1375" data-toggle="collapse"><span class="ident">onDidChangeConfiguration</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-instrinct">void</a>&gt;</span>
<div class="details collapse" id="details-1375">
<div class="comment"><p><a href="#WorkspaceConfiguration">構成</a>が変更されたときに放出されるイベント。</p>
</div>
</div>



<a name="workspace.onDidChangeTextDocument"></a><span class="ts" id=1369 data-target="#details-1369" data-toggle="collapse"><span class="ident">onDidChangeTextDocument</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#TextDocumentChangeEvent">TextDocumentChangeEvent</a>&gt;</span>
<div class="details collapse" id="details-1369">
<div class="comment"><p><a href="#TextDocument">テキスト文書</a>が変更されたときに発生するイベント。</p>
</div>
</div>



<a name="workspace.onDidCloseTextDocument"></a><span class="ts" id=1368 data-target="#details-1368" data-toggle="collapse"><span class="ident">onDidCloseTextDocument</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#TextDocument">TextDocument</a>&gt;</span>
<div class="details collapse" id="details-1368">
<div class="comment"><p><a href="#TextDocument">テキストドキュメント</a>が配置されたときに放出されるイベント。</p>
</div>
</div>



<a name="workspace.onDidOpenTextDocument"></a><span class="ts" id=1367 data-target="#details-1367" data-toggle="collapse"><span class="ident">onDidOpenTextDocument</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#TextDocument">TextDocument</a>&gt;</span>
<div class="details collapse" id="details-1367">
<div class="comment"><p><a href="#TextDocument">テキストドキュメント</a>が開かれたときに放出されるイベント。</p>
</div>
</div>



<a name="workspace.onDidSaveTextDocument"></a><span class="ts" id=1371 data-target="#details-1371" data-toggle="collapse"><span class="ident">onDidSaveTextDocument</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#TextDocument">TextDocument</a>&gt;</span>
<div class="details collapse" id="details-1371">
<div class="comment"><p><a href="#TextDocument">テキストドキュメント</a>がディスクに保存されたときに放出されるイベント。</p>
</div>
</div>



<a name="workspace.onWillSaveTextDocument"></a><span class="ts" id=1370 data-target="#details-1370" data-toggle="collapse"><span class="ident">onWillSaveTextDocument</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#TextDocumentWillSaveEvent">TextDocumentWillSaveEvent</a>&gt;</span>
<div class="details collapse" id="details-1370">
<div class="comment"><p><a href="#TextDocument">テキスト文書</a>がディスクに保存されるときに放出されるイベント。</p>
<p><em>注1：</em>非同期作業を登録することで、契約者は保存を遅らせることができます。
データの整合性のため、エディタはこのイベントを発生させずに保存できます。
例えば汚れたファイルでシャットダウンする場合など。</p>
<p><em>注2：</em>サブスクライバはシーケンシャルに呼び出され、非同期作業を登録することで<a href="#TextDocumentWillSaveEvent.waitUntil">遅延</a>保存できます。
不正なリスナーに対する保護は、そのように実装されています： *すべてのリスナーが共有する全体的な時間予算があり、それが使い果たされた場合、それ以上のリスナーは呼び出されません 長い時間がかかる、または頻繁にエラーを生成するリスナーは、もはや呼び出されません</p>
<p>現在のしきい値は全体の時間予算として1.5秒であり、リスナーは無視される前に3回不正行為をする可能性があります。</p>
</div>
</div>

#### Functions



<a name="workspace.applyEdit"></a><span class="ts" id=1350 data-target="#details-1350" data-toggle="collapse"><span class="ident">applyEdit</span><span>(</span><span class="ident">edit</span><span>: </span><a class="type-ref" href="#WorkspaceEdit">WorkspaceEdit</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">boolean</a>&gt;</span>
<div class="details collapse" id="details-1350">
<div class="comment"><p>指定された1つまたは複数のリソースに変更を加える
<a href="#WorkspaceEdit">ワークスペース編集</a>。</p>
<p>ワークスペースの編集を適用するとき、エディタは「すべてかどうか」の戦略を実装しますが、
は、1つのドキュメントを読み込んだり、1つのドキュメントを変更したりすると失敗することを意味します
拒否する編集。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="edit"></a><span class="ts" id=1351 data-target="#details-1351" data-toggle="collapse"><span class="ident">edit</span><span>: </span><a class="type-ref" href="#WorkspaceEdit">WorkspaceEdit</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">boolean</a>&gt;</span></td><td><div class="comment"><p>編集可能なときに解決されるthenable。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="workspace.asRelativePath"></a><span class="ts" id=1338 data-target="#details-1338" data-toggle="collapse"><span class="ident">asRelativePath</span><span>(</span><span class="ident">pathOrUri</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#Uri">Uri</a><span>)</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1338">
<div class="comment"><p>ワークスペースのルートに相対的なパスを返します。</p>
<p><a href="#workspace.rootPath">ワークスペースルート</a>がない場合、またはパス
はそのフォルダの子ではないため、入力が返されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="pathOrUri"></a><span class="ts" id=1339 data-target="#details-1339" data-toggle="collapse"><span class="ident">pathOrUri</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">string</a></span></td><td><div class="comment"><p>ルートまたは入力からの相対パス。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="workspace.createFileSystemWatcher"></a><span class="ts" id=1331 data-target="#details-1331" data-toggle="collapse"><span class="ident">createFileSystemWatcher</span><span>(</span><span class="ident">globPattern</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">ignoreCreateEvents</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a>, <span class="ident">ignoreChangeEvents</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a>, <span class="ident">ignoreDeleteEvents</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a><span>)</span><span>: </span><a class="type-ref" href="#FileSystemWatcher">FileSystemWatcher</a></span>
<div class="details collapse" id="details-1331">
<div class="comment"><p>ファイルシステムウォッチャーを作成します。</p>
<p>ファイルイベントをフィルタリングするグロブパターンを提供する必要があります。
オプションで、特定の種類のイベントを無視するフラグを提供することができます。
イベントの受信を停止するには、ウォッチャーを処分する必要があります。</p>
<p> 現在の<a href="#workspace.rootPath">workspace</a>内のファイルのみが監視されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="globPattern"></a><span class="ts" id=1332 data-target="#details-1332" data-toggle="collapse"><span class="ident">globPattern</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="ignoreCreateEvents"></a><span class="ts" id=1333 data-target="#details-1333" data-toggle="collapse"><span class="ident">ignoreCreateEvents</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="ignoreChangeEvents"></a><span class="ts" id=1334 data-target="#details-1334" data-toggle="collapse"><span class="ident">ignoreChangeEvents</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="ignoreDeleteEvents"></a><span class="ts" id=1335 data-target="#details-1335" data-toggle="collapse"><span class="ident">ignoreDeleteEvents</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#FileSystemWatcher">FileSystemWatcher</a></span></td><td><div class="comment"><p>新しいファイルシステムウォッチャーインスタンス。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="workspace.findFiles"></a><span class="ts" id=1341 data-target="#details-1341" data-toggle="collapse"><span class="ident">findFiles</span><span>(</span><span class="ident">include</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">exclude</span><span>?</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">maxResults</span><span>?</span><span>: </span><a class="type-instrinct">number</a>, <span class="ident">token</span><span>?</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#Uri">Uri</a>[]&gt;</span>
<div class="details collapse" id="details-1341">
<div class="comment"><p>ワークスペース内のファイルを検索します。</p>
<p>@@ sample &#39;findFiles(&#39; <strong> &#39;+&#39; / *。js &#39;、&#39; </strong> &#39;&#39; / node_modules / ** &#39;、10) `</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="include"></a><span class="ts" id=1342 data-target="#details-1342" data-toggle="collapse"><span class="ident">include</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="exclude"></a><span class="ts" id=1343 data-target="#details-1343" data-toggle="collapse"><span class="ident">exclude</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="maxResults"></a><span class="ts" id=1344 data-target="#details-1344" data-toggle="collapse"><span class="ident">maxResults</span><span>?</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=1345 data-target="#details-1345" data-toggle="collapse"><span class="ident">token</span><span>?</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#Uri">Uri</a>[]&gt;</span></td><td><div class="comment"><p>リソース識別子の配列に解決されるthenable。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="workspace.getConfiguration"></a><span class="ts" id=1373 data-target="#details-1373" data-toggle="collapse"><span class="ident">getConfiguration</span><span>(</span><span class="ident">section</span><span>?</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#WorkspaceConfiguration">WorkspaceConfiguration</a></span>
<div class="details collapse" id="details-1373">
<div class="comment"><p>設定オブジェクトを取得します。</p>
<p>section-identifierが与えられている場合は、その部分だけが返されます。
セクション識別子のドットは <code>{myExt：{setting：{doIt：true}}</code> や `getConfiguration( &#39;myExt.setting&#39;)などの子アクセスと解釈されます。get( &#39;doIt&#39;)===本当です。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="section"></a><span class="ts" id=1374 data-target="#details-1374" data-toggle="collapse"><span class="ident">section</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#WorkspaceConfiguration">WorkspaceConfiguration</a></span></td><td><div class="comment"><p>完全なワークスペース構成またはサブセット。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="workspace.openTextDocument"></a><span class="ts" id=1354 data-target="#details-1354" data-toggle="collapse"><span class="ident">openTextDocument</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextDocument">TextDocument</a>&gt;</span>
<div class="details collapse" id="details-1354">
<div class="comment"><p>ドキュメントを開きます。
この文書が既に開いている場合は、早期に返却されます。
それ以外の場合は、ドキュメントがロードされ、<a href="#workspace.onDidOpenTextDocument">didOpen</a>-eventが発生します。</p>
<p>この文書は<a href="#Uri">uri</a>で示されています。</p>
<p><a href="#Uri.scheme">scheme</a>に応じて以下の規則が適用されます：* <code>file</code> -scheme：ディスク上のファイルを開きます。
ファイルが存在しないか、読み込めない場合は拒否されます。</p>
<ul>
<li><p><code>untitled</code> -scheme：ディスクに保存すべき新しいファイル。
<code>タイトルなし：c：\ frodo \ new.js</code>。
言語はファイル名から導出されます。
*他のすべてのスキームでは、登録されたテキストドキュメントコンテンツ<a href="#TextDocumentContentProvider">providers</a>が参照されます。</p>
</li>
<li><p>*返されたドキュメントのライフサイクルはエディタが所有し、拡張子は所有していないことに注意してください。
つまり、
<a href="#workspace.onDidCloseTextDocument"><code>onDidClose</code></a>-eventは、それを開いた後いつでも発生する可能性があります。</p>
</li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=1355 data-target="#details-1355" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextDocument">TextDocument</a>&gt;</span></td><td><div class="comment"><p>(#TextDocument)に解決する約束です。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="workspace.openTextDocument"></a><span class="ts" id=1356 data-target="#details-1356" data-toggle="collapse"><span class="ident">openTextDocument</span><span>(</span><span class="ident">fileName</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextDocument">TextDocument</a>&gt;</span>
<div class="details collapse" id="details-1356">
<div class="comment"><p><code>openTextDocument(Uri.file(fileName))</code> の略語。</p>
<ul>
<li><em>see</em> - <a href="#openTextDocument">openTextDocument</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="fileName"></a><span class="ts" id=1357 data-target="#details-1357" data-toggle="collapse"><span class="ident">fileName</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextDocument">TextDocument</a>&gt;</span></td><td><div class="comment"><p>(#TextDocument)に解決する約束です。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="workspace.openTextDocument"></a><span class="ts" id=1358 data-target="#details-1358" data-toggle="collapse"><span class="ident">openTextDocument</span><span>(</span><span class="ident">options</span><span>?</span><span>: </span>{content: <a class="type-instrinct">string</a>, language: <a class="type-instrinct">string</a>}<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextDocument">TextDocument</a>&gt;</span>
<div class="details collapse" id="details-1358">
<div class="comment"><p>タイトルのないテキスト文書を開きます。
エディタは、ドキュメントを保存するときにファイルパスを入力するように求めます。</p>
<p><code>options</code> パラメータは
ドキュメントの<em>言語</em>および/または<em>コンテンツ</em>を指定します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="options"></a><span class="ts" id=1359 data-target="#details-1359" data-toggle="collapse"><span class="ident">options</span><span>?</span><span>: </span>{content: <a class="type-instrinct">string</a>, language: <a class="type-instrinct">string</a>}</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextDocument">TextDocument</a>&gt;</span></td><td><div class="comment"><p>(#TextDocument)に解決する約束です。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="workspace.registerTextDocumentContentProvider"></a><span class="ts" id=1364 data-target="#details-1364" data-toggle="collapse"><span class="ident">registerTextDocumentContentProvider</span><span>(</span><span class="ident">scheme</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">provider</span><span>: </span><a class="type-ref" href="#TextDocumentContentProvider">TextDocumentContentProvider</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-1364">
<div class="comment"><p>テキストドキュメントコンテンツプロバイダを登録します。</p>
<p>スキームごとに登録できるプロバイダは1つだけです。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="scheme"></a><span class="ts" id=1365 data-target="#details-1365" data-toggle="collapse"><span class="ident">scheme</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="provider"></a><span class="ts" id=1366 data-target="#details-1366" data-toggle="collapse"><span class="ident">provider</span><span>: </span><a class="type-ref" href="#TextDocumentContentProvider">TextDocumentContentProvider</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>廃棄時にこのプロバイダの登録を解除する<a href="#Disposable">disposable</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="workspace.saveAll"></a><span class="ts" id=1347 data-target="#details-1347" data-toggle="collapse"><span class="ident">saveAll</span><span>(</span><span class="ident">includeUntitled</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">boolean</a>&gt;</span>
<div class="details collapse" id="details-1347">
<div class="comment"><p>すべてのダーティファイルを保存します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="includeUntitled"></a><span class="ts" id=1348 data-target="#details-1348" data-toggle="collapse"><span class="ident">includeUntitled</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">boolean</a>&gt;</span></td><td><div class="comment"><p>ファイルが保存されたときに解決されるthenable。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="CancellationToken"></a><span class="code-item" id=399>CancellationToken</span>



<div class="comment"><p>キャンセルトークンは、非同期または長時間実行される操作に渡され、ユーザーが入力を続行したために完了アイテムの要求を取り消すなど、取り消しを要求します。</p>
<p>CancellationTokenのインスタンスを取得するには、
<a href="#CancellationTokenSource">CancellationTokenSource</a>。</p>
</div>

#### Properties



<a name="CancellationToken.isCancellationRequested"></a><span class="ts" id=400 data-target="#details-400" data-toggle="collapse"><span class="ident">isCancellationRequested</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-400">
<div class="comment"><p>トークンが取り消されたときは <code>true &#39;、それ以外のときは</code> false`です。</p>
</div>
</div>



<a name="CancellationToken.onCancellationRequested"></a><span class="ts" id=401 data-target="#details-401" data-toggle="collapse"><span class="ident">onCancellationRequested</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-instrinct">any</a>&gt;</span>
<div class="details collapse" id="details-401">
<div class="comment"><p>キャンセル時に発生する<a href="#イベント">イベント</a>。</p>
</div>
</div>

### <a name="CancellationTokenSource"></a><span class="code-item" id=402>CancellationTokenSource</span>



<div class="comment"><p>キャンセルソースは、<a href="#CancellationToken">キャンセルトークン</a>を作成して制御します。</p>
</div>

#### Properties



<a name="CancellationTokenSource.token"></a><span class="ts" id=403 data-target="#details-403" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span>
<div class="details collapse" id="details-403">
<div class="comment"><p>このソースのキャンセルトークン。</p>
</div>
</div>

#### Methods



<a name="CancellationTokenSource.cancel"></a><span class="ts" id=405 data-target="#details-405" data-toggle="collapse"><span class="ident">cancel</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-405">
<div class="comment"><p>トークンのシグナルキャンセル。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="CancellationTokenSource.dispose"></a><span class="ts" id=407 data-target="#details-407" data-toggle="collapse"><span class="ident">dispose</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-407">
<div class="comment"><p>オブジェクトを廃棄し、リソースを解放します。
<a href="#CancellationTokenSource.cancel">キャンセル</a>が呼び出されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="CharacterPair"></a><span class="code-item" id=1166>CharacterPair</span>



<div class="comment"><p>2つの文字のタプル。
一対の開閉括弧のようです。</p>
</div>



<a name="CharacterPair"></a><span class="ts" id=1166 data-target="#details-1166" data-toggle="collapse"><span class="ident">CharacterPair</span><span>: </span>[<a class="type-instrinct">string</a>, <a class="type-instrinct">string</a>]</span>

### <a name="CodeActionContext"></a><span class="code-item" id=495>CodeActionContext</span>



<div class="comment"><p><a href="#CodeActionProvider.provideCodeActions">コードアクション</a>が実行されるコンテキストに関する追加の診断情報を含みます。</p>
</div>

#### Properties



<a name="CodeActionContext.diagnostics"></a><span class="ts" id=496 data-target="#details-496" data-toggle="collapse"><span class="ident">diagnostics</span><span>: </span><a class="type-ref" href="#Diagnostic">Diagnostic</a>[]</span>
<div class="details collapse" id="details-496">
<div class="comment"><p>診断の配列。</p>
</div>
</div>

### <a name="CodeActionProvider"></a><span class="code-item" id=497>CodeActionProvider</span>



<div class="comment"><p>コードアクションインタフェースは、拡張機能と<a href="https://code.visualstudio.com/docs/editor/editingevolved#_code-action">電球</a>機能の間の契約を定義します。</p>
<p>コードアクションは、システムに <a href="#commands.getCommands">登録されている</a> 任意のコマンドにすることができます。</p>
</div>

#### Methods



<a name="CodeActionProvider.provideCodeActions"></a><span class="ts" id=499 data-target="#details-499" data-toggle="collapse"><span class="ident">provideCodeActions</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a>, <span class="ident">context</span><span>: </span><a class="type-ref" href="#CodeActionContext">CodeActionContext</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-499">
<div class="comment"><p>指定されたドキュメントと範囲のコマンドを提供します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=500 data-target="#details-500" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"><p>コマンドが呼び出されたドキュメント。</p>
</div></td></tr>
<tr><td><a name="range"></a><span class="ts" id=501 data-target="#details-501" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>コマンドが呼び出された範囲。</p>
</div></td></tr>
<tr><td><a name="context"></a><span class="ts" id=502 data-target="#details-502" data-toggle="collapse"><span class="ident">context</span><span>: </span><a class="type-ref" href="#CodeActionContext">CodeActionContext</a></span></td><td><div class="comment"><p>追加情報を保持するコンテキスト。</p>
</div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=503 data-target="#details-503" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"><p>キャンセルトークン。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>コマンドの配列またはそのようなものからなる文字列。
結果の不足は、 <code>undefined</code> 、 <code>null</code> 、または空の配列を返すことによって通知することができます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="CodeLens"></a><span class="code-item" id=504>CodeLens</span>



<div class="comment"><p>コードレンズは、参照の数、テストを実行する方法など、ソーステキストとともに表示される<a href="#Command">コマンド</a>を表します</p>
<p>コードレンズは、コマンドが関連付けられていないときは <em>unresolved</em> (未解決) です。
パフォーマンス上の理由から、コードレンズの作成と分解は2つの段階に分かれていなければなりません。</p>
<ul>
<li><em>see</em> - <a href="#CodeLensProvider.provideCodeLenses">CodeLensProvider.provideCodeLenses</a></li>
</ul>
<ul>
<li><em>see</em> - <a href="#CodeLensProvider.resolveCodeLens">CodeLensProvider.resolveCodeLens</a></li>
</ul>
</div>

#### Constructors



<a name="CodeLens.new CodeLens"></a><span class="ts" id=509 data-target="#details-509" data-toggle="collapse"><span class="ident">new CodeLens</span><span>(</span><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a>, <span class="ident">command</span><span>?</span><span>: </span><a class="type-ref" href="#Command">Command</a><span>)</span><span>: </span><a class="type-ref" href="#CodeLens">CodeLens</a></span>
<div class="details collapse" id="details-509">
<div class="comment"><p>新しいコードレンズオブジェクトを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=510 data-target="#details-510" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>このコードレンズが適用される範囲。</p>
</div></td></tr>
<tr><td><a name="command"></a><span class="ts" id=511 data-target="#details-511" data-toggle="collapse"><span class="ident">command</span><span>?</span><span>: </span><a class="type-ref" href="#Command">Command</a></span></td><td><div class="comment"><p>このコードレンズに関連付けられたコマンド。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#CodeLens">CodeLens</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="CodeLens.command"></a><span class="ts" id=506 data-target="#details-506" data-toggle="collapse"><span class="ident">command</span><span>?</span><span>: </span><a class="type-ref" href="#Command">Command</a></span>
<div class="details collapse" id="details-506">
<div class="comment"><p>このコードレンズが表すコマンド。</p>
</div>
</div>



<a name="CodeLens.isResolved"></a><span class="ts" id=507 data-target="#details-507" data-toggle="collapse"><span class="ident">isResolved</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-507">
<div class="comment"><p>関連するコマンドがあるときは <code>true</code>。</p>
</div>
</div>



<a name="CodeLens.range"></a><span class="ts" id=505 data-target="#details-505" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-505">
<div class="comment"><p>このコードレンズが有効な範囲。
1行にまたがるだけです。</p>
</div>
</div>

### <a name="CodeLensProvider"></a><span class="code-item" id=512>CodeLensProvider</span>



<div class="comment"><p>コードレンズプロバイダは、<a href="#コマンド">コマンド</a>をソーステキストに追加します。
コマンドはソーステキストの間に専用水平線として表示されます。</p>
</div>

#### Events



<a name="CodeLensProvider.onDidChangeCodeLenses"></a><span class="ts" id=513 data-target="#details-513" data-toggle="collapse"><span class="ident">onDidChangeCodeLenses</span><span>?</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-instrinct">void</a>&gt;</span>
<div class="details collapse" id="details-513">
<div class="comment"><p>このプロバイダのコードレンズが変更されたことを通知するオプションのイベント。</p>
</div>
</div>

#### Methods



<a name="CodeLensProvider.provideCodeLenses"></a><span class="ts" id=515 data-target="#details-515" data-toggle="collapse"><span class="ident">provideCodeLenses</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-515">
<div class="comment"><p><a href="#CodeLens">レンズ</a>のリストを計算します。
この呼び出しはできるだけ速く返さなければならず、コマンドを計算するのが高価な実装者の場合は、rangeコードセットを返すだけで、<a href="#CodeLensProvider.resolveCodeLens">resolve</a>を実装する必要があります。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=516 data-target="#details-516" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=517 data-target="#details-517" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>コード・レンズの配列またはそれに対応するネクサブル。
結果の欠如は、 <code>undefined</code> 、 <code>null</code> 、または空の配列を返すことによって通知できます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="CodeLensProvider.resolveCodeLens"></a><span class="ts" id=519 data-target="#details-519" data-toggle="collapse"><span class="ident">resolveCodeLens</span><span>(</span><span class="ident">codeLens</span><span>: </span><a class="type-ref" href="#CodeLens">CodeLens</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-519">
<div class="comment"><p>この関数は、通常はスクロールして<a href="#CodeLensProvider.provideCodeLenses">計算</a> - 呼び出しを呼び出したときに、可視コードレンズごとに呼び出されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="codeLens"></a><span class="ts" id=520 data-target="#details-520" data-toggle="collapse"><span class="ident">codeLens</span><span>: </span><a class="type-ref" href="#CodeLens">CodeLens</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=521 data-target="#details-521" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>与えられた、解決されたコードのレンズまたはそれに解決されるネーブル。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="Command"></a><span class="code-item" id=26>Command</span>



<div class="comment"><p>コマンドへの参照を表します。
UIでコマンドを表すのに使用されるタイトルを提供し、オプションで、呼び出されたときにコマンドハンドラー関数に渡される引数の配列も提供します。</p>
</div>

#### Properties



<a name="Command.arguments"></a><span class="ts" id=30 data-target="#details-30" data-toggle="collapse"><span class="ident">arguments</span><span>?</span><span>: </span><a class="type-instrinct">any</a>[]</span>
<div class="details collapse" id="details-30">
<div class="comment"><p>コマンドハンドラが呼び出されるべき引数。</p>
</div>
</div>



<a name="Command.command"></a><span class="ts" id=28 data-target="#details-28" data-toggle="collapse"><span class="ident">command</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-28">
<div class="comment"><p>実際のコマンドハンドラの識別子。</p>
<ul>
<li><em>see</em> - <a href="#commands.registerCommand">commands.registerCommand</a>。</li>
</ul>
</div>
</div>



<a name="Command.title"></a><span class="ts" id=27 data-target="#details-27" data-toggle="collapse"><span class="ident">title</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-27">
<div class="comment"><p><code>save</code> のようなコマンドのタイトル。</p>
</div>
</div>



<a name="Command.tooltip"></a><span class="ts" id=29 data-target="#details-29" data-toggle="collapse"><span class="ident">tooltip</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-29">
<div class="comment"><p>UIで表現されたときのコマンドのツールチップ。</p>
</div>
</div>

### <a name="CommentRule"></a><span class="code-item" id=846>CommentRule</span>



<div class="comment"><p>言語のためのコメントの仕組みを説明します。</p>
</div>

#### Properties



<a name="CommentRule.blockComment"></a><span class="ts" id=848 data-target="#details-848" data-toggle="collapse"><span class="ident">blockComment</span><span>?</span><span>: </span><a class="type-ref" href="#CharacterPair">CharacterPair</a></span>
<div class="details collapse" id="details-848">
<div class="comment"><p>ブロックコメント文字の組は、 `/ * block comment</p>
</div>
</div>



<a name="CommentRule.lineComment"></a><span class="ts" id=847 data-target="#details-847" data-toggle="collapse"><span class="ident">lineComment</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-847">
<div class="comment"><p>``これはコメントです &#39;のような行コメントトークン</p>
</div>
</div>

### <a name="CompletionItem"></a><span class="code-item" id=796>CompletionItem</span>



<div class="comment"><p>完成品目は、入力中のテキストを完成させるために提案されたテキストスニペットを表します。</p>
<p><a href="#CompletionItem.label">ラベル</a>から完成品を作成するだけで十分です。
その場合、補完項目は<a href="#TextDocument.getWordRangeAtPosition">単語</a>を置き換えます。
指定されたラベルまたは<a href="#CompletionItem.insertText">insertText</a>でカーソルを移動します。
それ以外の場合、指定された<a href="#CompletionItem.textEdit">編集</a>が使用されます。</p>
<p>エディタで補完項目を選択すると、その定義または合成されたテキスト編集が*すべてのカーソル/選択項目に適用されますが、<a href="CompletionItem.additionalTextEdits">additionalTextEdits</a>は
提供されたとおりに適用されます。</p>
<ul>
<li><em>see</em> - <a href="#CompletionItemProvider.provideCompletionItems">CompletionItemProvider.provideCompletionItems</a></li>
</ul>
<ul>
<li><em>see</em> - <a href="#CompletionItemProvider.resolveCompletionItem">CompletionItemProvider.resolveCompletionItem</a></li>
</ul>
</div>

#### Constructors



<a name="CompletionItem.new CompletionItem"></a><span class="ts" id=810 data-target="#details-810" data-toggle="collapse"><span class="ident">new CompletionItem</span><span>(</span><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">kind</span><span>?</span><span>: </span><a class="type-ref" href="#CompletionItemKind">CompletionItemKind</a><span>)</span><span>: </span><a class="type-ref" href="#CompletionItem">CompletionItem</a></span>
<div class="details collapse" id="details-810">
<div class="comment"><p>新しい補完項目を作成します。</p>
<p>完成品には少なくとも<a href="#CompletionItem.label">ラベル</a>が必要です。
は、並べ替えやフィルタリングのためだけでなく、挿入テキストとしても使用されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="label"></a><span class="ts" id=811 data-target="#details-811" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="kind"></a><span class="ts" id=812 data-target="#details-812" data-toggle="collapse"><span class="ident">kind</span><span>?</span><span>: </span><a class="type-ref" href="#CompletionItemKind">CompletionItemKind</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#CompletionItem">CompletionItem</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="CompletionItem.additionalTextEdits"></a><span class="ts" id=807 data-target="#details-807" data-toggle="collapse"><span class="ident">additionalTextEdits</span><span>?</span><span>: </span><a class="type-ref" href="#TextEdit">TextEdit</a>[]</span>
<div class="details collapse" id="details-807">
<div class="comment"><p>この補完を選択するときに適用される追加の<a href="#TextEdit">テキスト編集</a>のオプションの配列。
編集はメインの[edit]と重複してはいけません(#CompletionItem.textEdit) それ自体ではありません。</p>
</div>
</div>



<a name="CompletionItem.command"></a><span class="ts" id=808 data-target="#details-808" data-toggle="collapse"><span class="ident">command</span><span>?</span><span>: </span><a class="type-ref" href="#Command">Command</a></span>
<div class="details collapse" id="details-808">
<div class="comment"><p>この補完を挿入した後に<em>実行されるオプションの<a href="#コマンド">command</a>。
</em>注*現在の文書に対する追加の修正は、
<a href="#CompletionItem.additionalTextEdits">additionalTextEdits</a> - プロパティ。</p>
</div>
</div>



<a name="CompletionItem.commitCharacters"></a><span class="ts" id=805 data-target="#details-805" data-toggle="collapse"><span class="ident">commitCharacters</span><span>?</span><span>: </span><a class="type-instrinct">string</a>[]</span>
<div class="details collapse" id="details-805">
<div class="comment"><p>この補完がアクティブである間に押されると、最初にそれを受け入れ、その文字を入力するオプションの文字セットです。
注*すべてのコミット文字は <code>length = 1</code> でなければならず、余計な文字は無視されます。</p>
</div>
</div>



<a name="CompletionItem.detail"></a><span class="ts" id=799 data-target="#details-799" data-toggle="collapse"><span class="ident">detail</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-799">
<div class="comment"><p>人間が読むことができる文字列。
タイプやシンボル情報など、このアイテムに関する追加情報があります。</p>
</div>
</div>



<a name="CompletionItem.documentation"></a><span class="ts" id=800 data-target="#details-800" data-toggle="collapse"><span class="ident">documentation</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-800">
<div class="comment"><p>doc-commentを表す人間が読める文字列。</p>
</div>
</div>



<a name="CompletionItem.filterText"></a><span class="ts" id=802 data-target="#details-802" data-toggle="collapse"><span class="ident">filterText</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-802">
<div class="comment"><p>完了項目のセットをフィルタリングするときに使用する文字列。</p>
<p><a href="#CompletionItem.label">ラベル</a>を <code>偽装する</code>
使用されている。</p>
</div>
</div>



<a name="CompletionItem.insertText"></a><span class="ts" id=803 data-target="#details-803" data-toggle="collapse"><span class="ident">insertText</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#SnippetString">SnippetString</a></span>
<div class="details collapse" id="details-803">
<div class="comment"><p>この完了を選択するときにドキュメントに挿入する文字列またはスニペット。</p>
<p><a href="#CompletionItem.label">ラベル</a>を <code>偽装する</code>
使用されている。</p>
</div>
</div>



<a name="CompletionItem.kind"></a><span class="ts" id=798 data-target="#details-798" data-toggle="collapse"><span class="ident">kind</span><span>?</span><span>: </span><a class="type-ref" href="#CompletionItemKind">CompletionItemKind</a></span>
<div class="details collapse" id="details-798">
<div class="comment"><p>この完成品の種類。
*種類に基づいて、アイコンがエディタによって選択されます。</p>
</div>
</div>



<a name="CompletionItem.label"></a><span class="ts" id=797 data-target="#details-797" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-797">
<div class="comment"><p>この完成品のラベル。
デフォルトでは、これはこの補完を選択するときに挿入されるテキストです。</p>
</div>
</div>



<a name="CompletionItem.range"></a><span class="ts" id=804 data-target="#details-804" data-toggle="collapse"><span class="ident">range</span><span>?</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-804">
<div class="comment"><p>この完成品で置き換えられるテキストの範囲。</p>
<p><a href="#TextDocument.getWordRangeAtPosition">現在の単語</a>の先頭から現在位置までのデフォルト値です。</p>
<p><em>注：</em>範囲は<a href="#Range.isSingleLine">単一行</a>でなければなりません。
完了が[要求された]位置(#CompletionItemProvider.provideCompletionItems)を<a href="#Range.contains">contains</a>します。</p>
</div>
</div>



<a name="CompletionItem.sortText"></a><span class="ts" id=801 data-target="#details-801" data-toggle="collapse"><span class="ident">sortText</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-801">
<div class="comment"><p>この項目を他の項目と比較するときに使用する文字列。</p>
<p><a href="#CompletionItem.label">ラベル</a>を <code>偽装する</code>
使用されている。</p>
</div>
</div>



<a name="CompletionItem.textEdit"></a><span class="ts" id=806 data-target="#details-806" data-toggle="collapse"><span class="ident">textEdit</span><span>?</span><span>: </span><a class="type-ref" href="#TextEdit">TextEdit</a></span>
<div class="details collapse" id="details-806">
<div class="comment"><ul>
<li><em>deprecated</em> - <strong> <code>CompletionItem.insertText</code> と <code>CompletionItem.range</code> のために</strong>非推奨です。</li>
</ul>
<p>~~この補完を選択するときに文書に適用される<a href="#TextEdit">edit</a>。
編集が提供されると、
<a href="#CompletionItem.insertText">insertText</a>は無視されます。
~~</p>
<p>~~編集の<a href="#Range">range</a>はシングルラインでなければならず、同じ行でCompletionItemProvider.provideCompletionItems)が〜要求されました。
~~</p>
</div>
</div>

### <a name="CompletionItemKind"></a><span class="code-item" id=770>CompletionItemKind</span>



<div class="comment"><p>完成品の種類。</p>
</div>

#### Enumeration members



<a name="CompletionItemKind.Class"></a><span class="ts" id=777 data-target="#details-777" data-toggle="collapse"><span class="ident">Class</span></span>
<div class="details collapse" id="details-777">
<em>6</em>
</div>



<a name="CompletionItemKind.Color"></a><span class="ts" id=786 data-target="#details-786" data-toggle="collapse"><span class="ident">Color</span></span>
<div class="details collapse" id="details-786">
<em>15</em>
</div>



<a name="CompletionItemKind.Constant"></a><span class="ts" id=791 data-target="#details-791" data-toggle="collapse"><span class="ident">Constant</span></span>
<div class="details collapse" id="details-791">
<em>20</em>
</div>



<a name="CompletionItemKind.Constructor"></a><span class="ts" id=774 data-target="#details-774" data-toggle="collapse"><span class="ident">Constructor</span></span>
<div class="details collapse" id="details-774">
<em>3</em>
</div>



<a name="CompletionItemKind.Enum"></a><span class="ts" id=783 data-target="#details-783" data-toggle="collapse"><span class="ident">Enum</span></span>
<div class="details collapse" id="details-783">
<em>12</em>
</div>



<a name="CompletionItemKind.EnumMember"></a><span class="ts" id=790 data-target="#details-790" data-toggle="collapse"><span class="ident">EnumMember</span></span>
<div class="details collapse" id="details-790">
<em>19</em>
</div>



<a name="CompletionItemKind.Event"></a><span class="ts" id=793 data-target="#details-793" data-toggle="collapse"><span class="ident">Event</span></span>
<div class="details collapse" id="details-793">
<em>22</em>
</div>



<a name="CompletionItemKind.Field"></a><span class="ts" id=775 data-target="#details-775" data-toggle="collapse"><span class="ident">Field</span></span>
<div class="details collapse" id="details-775">
<em>4</em>
</div>



<a name="CompletionItemKind.File"></a><span class="ts" id=788 data-target="#details-788" data-toggle="collapse"><span class="ident">File</span></span>
<div class="details collapse" id="details-788">
<em>16</em>
</div>



<a name="CompletionItemKind.Folder"></a><span class="ts" id=789 data-target="#details-789" data-toggle="collapse"><span class="ident">Folder</span></span>
<div class="details collapse" id="details-789">
<em>18</em>
</div>



<a name="CompletionItemKind.Function"></a><span class="ts" id=773 data-target="#details-773" data-toggle="collapse"><span class="ident">Function</span></span>
<div class="details collapse" id="details-773">
<em>2</em>
</div>



<a name="CompletionItemKind.Interface"></a><span class="ts" id=778 data-target="#details-778" data-toggle="collapse"><span class="ident">Interface</span></span>
<div class="details collapse" id="details-778">
<em>7</em>
</div>



<a name="CompletionItemKind.Keyword"></a><span class="ts" id=784 data-target="#details-784" data-toggle="collapse"><span class="ident">Keyword</span></span>
<div class="details collapse" id="details-784">
<em>13</em>
</div>



<a name="CompletionItemKind.Method"></a><span class="ts" id=772 data-target="#details-772" data-toggle="collapse"><span class="ident">Method</span></span>
<div class="details collapse" id="details-772">
<em>1</em>
</div>



<a name="CompletionItemKind.Module"></a><span class="ts" id=779 data-target="#details-779" data-toggle="collapse"><span class="ident">Module</span></span>
<div class="details collapse" id="details-779">
<em>8</em>
</div>



<a name="CompletionItemKind.Operator"></a><span class="ts" id=794 data-target="#details-794" data-toggle="collapse"><span class="ident">Operator</span></span>
<div class="details collapse" id="details-794">
<em>23</em>
</div>



<a name="CompletionItemKind.Property"></a><span class="ts" id=780 data-target="#details-780" data-toggle="collapse"><span class="ident">Property</span></span>
<div class="details collapse" id="details-780">
<em>9</em>
</div>



<a name="CompletionItemKind.Reference"></a><span class="ts" id=787 data-target="#details-787" data-toggle="collapse"><span class="ident">Reference</span></span>
<div class="details collapse" id="details-787">
<em>17</em>
</div>



<a name="CompletionItemKind.Snippet"></a><span class="ts" id=785 data-target="#details-785" data-toggle="collapse"><span class="ident">Snippet</span></span>
<div class="details collapse" id="details-785">
<em>14</em>
</div>



<a name="CompletionItemKind.Struct"></a><span class="ts" id=792 data-target="#details-792" data-toggle="collapse"><span class="ident">Struct</span></span>
<div class="details collapse" id="details-792">
<em>21</em>
</div>



<a name="CompletionItemKind.Text"></a><span class="ts" id=771 data-target="#details-771" data-toggle="collapse"><span class="ident">Text</span></span>
<div class="details collapse" id="details-771">
<em>0</em>
</div>



<a name="CompletionItemKind.TypeParameter"></a><span class="ts" id=795 data-target="#details-795" data-toggle="collapse"><span class="ident">TypeParameter</span></span>
<div class="details collapse" id="details-795">
<em>24</em>
</div>



<a name="CompletionItemKind.Unit"></a><span class="ts" id=781 data-target="#details-781" data-toggle="collapse"><span class="ident">Unit</span></span>
<div class="details collapse" id="details-781">
<em>10</em>
</div>



<a name="CompletionItemKind.Value"></a><span class="ts" id=782 data-target="#details-782" data-toggle="collapse"><span class="ident">Value</span></span>
<div class="details collapse" id="details-782">
<em>11</em>
</div>



<a name="CompletionItemKind.Variable"></a><span class="ts" id=776 data-target="#details-776" data-toggle="collapse"><span class="ident">Variable</span></span>
<div class="details collapse" id="details-776">
<em>5</em>
</div>

### <a name="CompletionItemProvider"></a><span class="code-item" id=820>CompletionItemProvider</span>



<div class="comment"><p>補完項目プロバイダインタフェースは、拡張機能と拡張機能の間の契約を定義します。</p>
<p><a href="https://code.visualstudio.com/docs/editor/intellisense">IntelliSense</a>。</p>
<p>完了<em>完了アイテムを計算するのが高価な場合、プロバイダはオプションでresolveCompletionItem関数を実装することができます。
その場合、<a href="#CompletionItem.label">ラベル</a>を持つ補完アイテムを</em> <a href="#CompletionItemProvider.provideCompletionItems">provideCompletionItems</a> - 関数。
その後、完成品がUIに表示され、フォーカスが得られたら、このプロバイダは<a href="#CompletionItem.documentation">doc-comment</a>または<a href="#CompletionItem.detail">details</a>の追加など、項目の解決を求められます。</p>
<p>プロバイダーは、ユーザージェスチャーによって明示的に、または単語またはトリガー文字を入力するときに暗黙的に構成に基づいて補完を求められます。</p>
</div>

#### Methods



<a name="CompletionItemProvider.provideCompletionItems"></a><span class="ts" id=822 data-target="#details-822" data-toggle="collapse"><span class="ident">provideCompletionItems</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-822">
<div class="comment"><p>与えられた位置と文書の完成品を提供する。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=823 data-target="#details-823" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="position"></a><span class="ts" id=824 data-target="#details-824" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=825 data-target="#details-825" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>補完の配列、<a href="#CompletionList">補完リスト</a>、またはどちらかに解決されるthenable。
結果の欠如は、 <code>undefined</code> 、 <code>null</code> 、または空の配列を返すことによって通知できます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="CompletionItemProvider.resolveCompletionItem"></a><span class="ts" id=827 data-target="#details-827" data-toggle="collapse"><span class="ident">resolveCompletionItem</span><span>(</span><span class="ident">item</span><span>: </span><a class="type-ref" href="#CompletionItem">CompletionItem</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-827">
<div class="comment"><p>補完アイテムがあれば、<a href="#CompletionItem.documentation">doc-comment</a>
または<a href="#CompletionItem.detail">詳細</a>。</p>
<p>エディタは完了アイテムを1回だけ解決します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="item"></a><span class="ts" id=828 data-target="#details-828" data-toggle="collapse"><span class="ident">item</span><span>: </span><a class="type-ref" href="#CompletionItem">CompletionItem</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=829 data-target="#details-829" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>解決された完了項目またはそのように解決されるthenable。
返品はOKです。</p>
<p><code>item</code>。
結果が返されない場合、指定された <code>item</code> が使用されます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="CompletionList"></a><span class="code-item" id=813>CompletionList</span>



<div class="comment"><p>エディタに表示される<a href="#CompletionItem">完了項目</a>のコレクションを表します。</p>
</div>

#### Constructors



<a name="CompletionList.new CompletionList"></a><span class="ts" id=817 data-target="#details-817" data-toggle="collapse"><span class="ident">new CompletionList</span><span>(</span><span class="ident">items</span><span>?</span><span>: </span><a class="type-ref" href="#CompletionItem">CompletionItem</a>[], <span class="ident">isIncomplete</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a><span>)</span><span>: </span><a class="type-ref" href="#CompletionList">CompletionList</a></span>
<div class="details collapse" id="details-817">
<div class="comment"><p>新しい完了リストを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="items"></a><span class="ts" id=818 data-target="#details-818" data-toggle="collapse"><span class="ident">items</span><span>?</span><span>: </span><a class="type-ref" href="#CompletionItem">CompletionItem</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="isIncomplete"></a><span class="ts" id=819 data-target="#details-819" data-toggle="collapse"><span class="ident">isIncomplete</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#CompletionList">CompletionList</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="CompletionList.isIncomplete"></a><span class="ts" id=814 data-target="#details-814" data-toggle="collapse"><span class="ident">isIncomplete</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-814">
<div class="comment"><p>このリストは完全ではありません。
さらに入力すると、このリストが再計算されます。</p>
</div>
</div>



<a name="CompletionList.items"></a><span class="ts" id=815 data-target="#details-815" data-toggle="collapse"><span class="ident">items</span><span>: </span><a class="type-ref" href="#CompletionItem">CompletionItem</a>[]</span>
<div class="details collapse" id="details-815">
<div class="comment"><p>完成品。</p>
</div>
</div>

### <a name="DecorationInstanceRenderOptions"></a><span class="code-item" id=312>DecorationInstanceRenderOptions</span>



<div class="comment"></div>

#### Properties



<a name="DecorationInstanceRenderOptions.after"></a><span class="ts" id=316 data-target="#details-316" data-toggle="collapse"><span class="ident">after</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationAttachmentRenderOptions">ThemableDecorationAttachmentRenderOptions</a></span>
<div class="details collapse" id="details-316">
<div class="comment"><p>装飾されたテキストの後に挿入される添付ファイルのレンダリングオプションを定義します</p>
</div>
</div>



<a name="DecorationInstanceRenderOptions.before"></a><span class="ts" id=315 data-target="#details-315" data-toggle="collapse"><span class="ident">before</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationAttachmentRenderOptions">ThemableDecorationAttachmentRenderOptions</a></span>
<div class="details collapse" id="details-315">
<div class="comment"><p>装飾されたテキストの前に挿入される添付ファイルのレンダリングオプションを定義します</p>
</div>
</div>



<a name="DecorationInstanceRenderOptions.dark"></a><span class="ts" id=314 data-target="#details-314" data-toggle="collapse"><span class="ident">dark</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationInstanceRenderOptions">ThemableDecorationInstanceRenderOptions</a></span>
<div class="details collapse" id="details-314">
<div class="comment"><p>暗いテーマの上書きオプション。</p>
</div>
</div>



<a name="DecorationInstanceRenderOptions.light"></a><span class="ts" id=313 data-target="#details-313" data-toggle="collapse"><span class="ident">light</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationInstanceRenderOptions">ThemableDecorationInstanceRenderOptions</a></span>
<div class="details collapse" id="details-313">
<div class="comment"><p>ライトテーマの上書きオプション。</p>
</div>
</div>

### <a name="DecorationOptions"></a><span class="code-item" id=305>DecorationOptions</span>



<div class="comment"><p><a href="#TextEditorDecorationType">デコレーションセット</a>内の特定のデコレーションのオプションを表します。</p>
</div>

#### Properties



<a name="DecorationOptions.hoverMessage"></a><span class="ts" id=307 data-target="#details-307" data-toggle="collapse"><span class="ident">hoverMessage</span><span>?</span><span>: </span><a class="type-ref" href="#MarkedString">MarkedString</a> &#124; <a class="type-ref" href="#MarkedString">MarkedString</a>[]</span>
<div class="details collapse" id="details-307">
<div class="comment"><p>装飾の上を浮遊するときにレンダリングされるべきメッセージ。</p>
</div>
</div>



<a name="DecorationOptions.range"></a><span class="ts" id=306 data-target="#details-306" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-306">
<div class="comment"><p>この装飾が適用される範囲。
範囲は空であってはなりません。</p>
</div>
</div>



<a name="DecorationOptions.renderOptions"></a><span class="ts" id=308 data-target="#details-308" data-toggle="collapse"><span class="ident">renderOptions</span><span>?</span><span>: </span><a class="type-ref" href="#DecorationInstanceRenderOptions">DecorationInstanceRenderOptions</a></span>
<div class="details collapse" id="details-308">
<div class="comment"><p>レンダリングオプションは、現在の装飾に適用されます。
パフォーマンス上の理由から、デコレーション固有のオプションの数を少なくし、可能な限り装飾タイプを使用してください。</p>
</div>
</div>

### <a name="DecorationRangeBehavior"></a><span class="code-item" id=234>DecorationRangeBehavior</span>



<div class="comment"><p>入力/編集時のデコレーションの動作を説明します。</p>
</div>

#### Enumeration members



<a name="DecorationRangeBehavior.ClosedClosed"></a><span class="ts" id=236 data-target="#details-236" data-toggle="collapse"><span class="ident">ClosedClosed</span></span>
<div class="details collapse" id="details-236">
<em>1</em>
</div>



<a name="DecorationRangeBehavior.ClosedOpen"></a><span class="ts" id=238 data-target="#details-238" data-toggle="collapse"><span class="ident">ClosedOpen</span></span>
<div class="details collapse" id="details-238">
<em>3</em>
</div>



<a name="DecorationRangeBehavior.OpenClosed"></a><span class="ts" id=237 data-target="#details-237" data-toggle="collapse"><span class="ident">OpenClosed</span></span>
<div class="details collapse" id="details-237">
<em>2</em>
</div>



<a name="DecorationRangeBehavior.OpenOpen"></a><span class="ts" id=235 data-target="#details-235" data-toggle="collapse"><span class="ident">OpenOpen</span></span>
<div class="details collapse" id="details-235">
<em>0</em>
</div>

### <a name="DecorationRenderOptions"></a><span class="code-item" id=279>DecorationRenderOptions</span>



<div class="comment"><p><a href="#TextEditorDecorationType">テキストエディタの装飾</a>のレンダリングスタイルを表します。</p>
</div>

#### Properties



<a name="DecorationRenderOptions.after"></a><span class="ts" id=304 data-target="#details-304" data-toggle="collapse"><span class="ident">after</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationAttachmentRenderOptions">ThemableDecorationAttachmentRenderOptions</a></span>
<div class="details collapse" id="details-304">
<div class="comment"><p>装飾されたテキストの後に挿入される添付ファイルのレンダリングオプションを定義します</p>
</div>
</div>



<a name="DecorationRenderOptions.backgroundColor"></a><span class="ts" id=285 data-target="#details-285" data-toggle="collapse"><span class="ident">backgroundColor</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-285">
<div class="comment"><p>装飾の背景色。
rgba()を使用し、透明な背景色を定義して他の装飾とうまくやります。
代替的に、カラーレジストリの色が参照されます(#ColorIdentifier)。</p>
</div>
</div>



<a name="DecorationRenderOptions.before"></a><span class="ts" id=303 data-target="#details-303" data-toggle="collapse"><span class="ident">before</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationAttachmentRenderOptions">ThemableDecorationAttachmentRenderOptions</a></span>
<div class="details collapse" id="details-303">
<div class="comment"><p>装飾されたテキストの前に挿入される添付ファイルのレンダリングオプションを定義します</p>
</div>
</div>



<a name="DecorationRenderOptions.border"></a><span class="ts" id=290 data-target="#details-290" data-toggle="collapse"><span class="ident">border</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-290">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="DecorationRenderOptions.borderColor"></a><span class="ts" id=291 data-target="#details-291" data-toggle="collapse"><span class="ident">borderColor</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-291">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々の境界線のプロパティを設定するために、「境界線」を使用する方が効果的です。</p>
</div>
</div>



<a name="DecorationRenderOptions.borderRadius"></a><span class="ts" id=292 data-target="#details-292" data-toggle="collapse"><span class="ident">borderRadius</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-292">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々の境界線のプロパティを設定するために、「境界線」を使用する方が効果的です。</p>
</div>
</div>



<a name="DecorationRenderOptions.borderSpacing"></a><span class="ts" id=293 data-target="#details-293" data-toggle="collapse"><span class="ident">borderSpacing</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-293">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々の境界線のプロパティを設定するために、「境界線」を使用する方が効果的です。</p>
</div>
</div>



<a name="DecorationRenderOptions.borderStyle"></a><span class="ts" id=294 data-target="#details-294" data-toggle="collapse"><span class="ident">borderStyle</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-294">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々の境界線のプロパティを設定するために、「境界線」を使用する方が効果的です。</p>
</div>
</div>



<a name="DecorationRenderOptions.borderWidth"></a><span class="ts" id=295 data-target="#details-295" data-toggle="collapse"><span class="ident">borderWidth</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-295">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々の境界線のプロパティを設定するために、「境界線」を使用する方が効果的です。</p>
</div>
</div>



<a name="DecorationRenderOptions.color"></a><span class="ts" id=298 data-target="#details-298" data-toggle="collapse"><span class="ident">color</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-298">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="DecorationRenderOptions.cursor"></a><span class="ts" id=297 data-target="#details-297" data-toggle="collapse"><span class="ident">cursor</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-297">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="DecorationRenderOptions.dark"></a><span class="ts" id=284 data-target="#details-284" data-toggle="collapse"><span class="ident">dark</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationRenderOptions">ThemableDecorationRenderOptions</a></span>
<div class="details collapse" id="details-284">
<div class="comment"><p>暗いテーマの上書きオプション。</p>
</div>
</div>



<a name="DecorationRenderOptions.gutterIconPath"></a><span class="ts" id=300 data-target="#details-300" data-toggle="collapse"><span class="ident">gutterIconPath</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-300">
<div class="comment"><p><strong>絶対パス</strong>またはガターにレンダリングされる画像へのURI。</p>
</div>
</div>



<a name="DecorationRenderOptions.gutterIconSize"></a><span class="ts" id=301 data-target="#details-301" data-toggle="collapse"><span class="ident">gutterIconSize</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-301">
<div class="comment"><p>ガターアイコンのサイズを指定します。
使用可能な値は &#39;auto&#39;、 &#39;contains&#39;、 &#39;cover&#39;および任意のパーセント値です。
詳細は<a href="https://msdn.microsoft.com/en-us/library/jj127316(v=vs.85).aspxを参照してください。">https://msdn.microsoft.com/en-us/library/jj127316(v=vs.85).aspxを参照してください。</a></p>
</div>
</div>



<a name="DecorationRenderOptions.isWholeLine"></a><span class="ts" id=280 data-target="#details-280" data-toggle="collapse"><span class="ident">isWholeLine</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-280">
<div class="comment"><p>装飾は行テキストの後の空白にも表示されるべきですか？ デフォルトは <code>false</code> です。</p>
</div>
</div>



<a name="DecorationRenderOptions.letterSpacing"></a><span class="ts" id=299 data-target="#details-299" data-toggle="collapse"><span class="ident">letterSpacing</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-299">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="DecorationRenderOptions.light"></a><span class="ts" id=283 data-target="#details-283" data-toggle="collapse"><span class="ident">light</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationRenderOptions">ThemableDecorationRenderOptions</a></span>
<div class="details collapse" id="details-283">
<div class="comment"><p>ライトテーマの*上書きオプション。</p>
</div>
</div>



<a name="DecorationRenderOptions.outline"></a><span class="ts" id=286 data-target="#details-286" data-toggle="collapse"><span class="ident">outline</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-286">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="DecorationRenderOptions.outlineColor"></a><span class="ts" id=287 data-target="#details-287" data-toggle="collapse"><span class="ident">outlineColor</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-287">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々のアウトラインプロパティを設定する場合は、「アウトライン」を使用する方が効果的です。</p>
</div>
</div>



<a name="DecorationRenderOptions.outlineStyle"></a><span class="ts" id=288 data-target="#details-288" data-toggle="collapse"><span class="ident">outlineStyle</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-288">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々のアウトラインプロパティを設定する場合は、「アウトライン」を使用する方が効果的です。</p>
</div>
</div>



<a name="DecorationRenderOptions.outlineWidth"></a><span class="ts" id=289 data-target="#details-289" data-toggle="collapse"><span class="ident">outlineWidth</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-289">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々のアウトラインプロパティを設定する場合は、「アウトライン」を使用する方が効果的です。</p>
</div>
</div>



<a name="DecorationRenderOptions.overviewRulerColor"></a><span class="ts" id=302 data-target="#details-302" data-toggle="collapse"><span class="ident">overviewRulerColor</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-302">
<div class="comment"><p>概観ルーラーの装飾の色。
rgba()を使用し、透明な色を定義して他の装飾とうまく合わせます。</p>
</div>
</div>



<a name="DecorationRenderOptions.overviewRulerLane"></a><span class="ts" id=282 data-target="#details-282" data-toggle="collapse"><span class="ident">overviewRulerLane</span><span>?</span><span>: </span><a class="type-ref" href="#OverviewRulerLane">OverviewRulerLane</a></span>
<div class="details collapse" id="details-282">
<div class="comment"><p>デコレーションをレンダリングすべき概要ルーラの位置。</p>
</div>
</div>



<a name="DecorationRenderOptions.rangeBehavior"></a><span class="ts" id=281 data-target="#details-281" data-toggle="collapse"><span class="ident">rangeBehavior</span><span>?</span><span>: </span><a class="type-ref" href="#DecorationRangeBehavior">DecorationRangeBehavior</a></span>
<div class="details collapse" id="details-281">
<div class="comment"><p>デコレーションの範囲の端で編集が行われたときに、装飾の動作が変化するようにカスタマイズします。
デフォルトは <code>DecorationRangeBehavior.OpenOpen</code> です。</p>
</div>
</div>



<a name="DecorationRenderOptions.textDecoration"></a><span class="ts" id=296 data-target="#details-296" data-toggle="collapse"><span class="ident">textDecoration</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-296">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>

### <a name="Definition"></a><span class="code-item" id=1161>Definition</span>



<div class="comment"><p>1つまたは複数の<a href="#Location">locations</a>として表されるシンボルの定義。
ほとんどのプログラミング言語では、シンボルが定義されている場所は1つだけです。</p>
</div>



<a name="Definition"></a><span class="ts" id=1161 data-target="#details-1161" data-toggle="collapse"><span class="ident">Definition</span><span>: </span><a class="type-ref" href="#Location">Location</a> &#124; <a class="type-ref" href="#Location">Location</a>[]</span>

### <a name="DefinitionProvider"></a><span class="code-item" id=522>DefinitionProvider</span>



<div class="comment"><p>定義プロバイダインタフェースは、拡張と[定義に移動]の間の契約を定義します(<a href="https://code.visualstudio.com/docs/editor/editingevolved#_go-to-definition">https://code.visualstudio.com/docs/editor/editingevolved#_go-to-definition</a>)
とはっきりとした定義機能。</p>
</div>

#### Methods



<a name="DefinitionProvider.provideDefinition"></a><span class="ts" id=524 data-target="#details-524" data-toggle="collapse"><span class="ident">provideDefinition</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-524">
<div class="comment"><p>指定された位置と文書のシンボルの定義を提供する。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=525 data-target="#details-525" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="position"></a><span class="ts" id=526 data-target="#details-526" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=527 data-target="#details-527" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>このように解決される定義または変換可能なテーブル。
結果の不足は、 <code>undefined</code> または <code>null</code> を返すことで通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="Diagnostic"></a><span class="code-item" id=929>Diagnostic</span>



<div class="comment"><p>コンパイラのエラーや警告などの診断を表します。
診断オブジェクトは、ファイルの有効範囲内でのみ有効です。</p>
</div>

#### Constructors



<a name="Diagnostic.new Diagnostic"></a><span class="ts" id=936 data-target="#details-936" data-toggle="collapse"><span class="ident">new Diagnostic</span><span>(</span><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a>, <span class="ident">message</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">severity</span><span>?</span><span>: </span><a class="type-ref" href="#DiagnosticSeverity">DiagnosticSeverity</a><span>)</span><span>: </span><a class="type-ref" href="#Diagnostic">Diagnostic</a></span>
<div class="details collapse" id="details-936">
<div class="comment"><p>新しい診断オブジェクトを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=937 data-target="#details-937" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="message"></a><span class="ts" id=938 data-target="#details-938" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="severity"></a><span class="ts" id=939 data-target="#details-939" data-toggle="collapse"><span class="ident">severity</span><span>?</span><span>: </span><a class="type-ref" href="#DiagnosticSeverity">DiagnosticSeverity</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Diagnostic">Diagnostic</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="Diagnostic.code"></a><span class="ts" id=934 data-target="#details-934" data-toggle="collapse"><span class="ident">code</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-934">
<div class="comment"><p>この診断のコードまたは識別子。
ユーザーには表示されませんが、後で処理するために使用する必要があります。
<a href="#CodeActionContext">コードアクション</a>を提供するとき。</p>
</div>
</div>



<a name="Diagnostic.message"></a><span class="ts" id=931 data-target="#details-931" data-toggle="collapse"><span class="ident">message</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-931">
<div class="comment"><p>人間が読めるメッセージ</p>
</div>
</div>



<a name="Diagnostic.range"></a><span class="ts" id=930 data-target="#details-930" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-930">
<div class="comment"><p>この診断が適用される範囲。</p>
</div>
</div>



<a name="Diagnostic.severity"></a><span class="ts" id=933 data-target="#details-933" data-toggle="collapse"><span class="ident">severity</span><span>: </span><a class="type-ref" href="#DiagnosticSeverity">DiagnosticSeverity</a></span>
<div class="details collapse" id="details-933">
<div class="comment"><p>重大度は、デフォルトは<a href="#DiagnosticSeverity.Error">error</a>です。</p>
</div>
</div>



<a name="Diagnostic.source"></a><span class="ts" id=932 data-target="#details-932" data-toggle="collapse"><span class="ident">source</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-932">
<div class="comment"><p>この診断のソースを説明する人間が判読可能な文字列。
&#39;typescript&#39;または &#39;super lint&#39;。</p>
</div>
</div>

### <a name="DiagnosticCollection"></a><span class="code-item" id=940>DiagnosticCollection</span>



<div class="comment"><p>診断コレクションは、一連の
<a href="#診断">診断</a>。
診断は、常に診断コレクションとリソースのスコープです。</p>
<p><code>DiagnosticCollection</code> のインスタンスを取得するには
<a href="#languages.createDiagnosticCollection">createDiagnosticCollection</a>。</p>
</div>

#### Properties



<a name="DiagnosticCollection.name"></a><span class="ts" id=941 data-target="#details-941" data-toggle="collapse"><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-941">
<div class="comment"><p>この診断コレクションの名前です(例：typescript)。
このコレクションのすべての診断は、この名前に関連付けられます。
また、タスクフレームワークは、<a href="https://code.visualstudio.com/docs/editor/tasks#_defining-a-problem-matcher">problem matchers</a>を定義するときにこの名前を使用します。</p>
</div>
</div>

#### Methods



<a name="DiagnosticCollection.clear"></a><span class="ts" id=952 data-target="#details-952" data-toggle="collapse"><span class="ident">clear</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-952">
<div class="comment"><p>このコレクションからすべての診断を削除します。</p>
<p><code>#set(undefined)</code> を呼び出すのと同じです。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="DiagnosticCollection.delete"></a><span class="ts" id=949 data-target="#details-949" data-toggle="collapse"><span class="ident">delete</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-949">
<div class="comment"><p>提供された <code>uri</code> に属するすべての診断をこのコレクションから削除します。</p>
<p><code>#set(uri、undefined)</code> と同じです。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=950 data-target="#details-950" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="DiagnosticCollection.dispose"></a><span class="ts" id=969 data-target="#details-969" data-toggle="collapse"><span class="ident">dispose</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-969">
<div class="comment"><p>廃棄し、関連するリソースを解放します。
通話
<a href="#DiagnosticCollection.clear">クリア</a>。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="DiagnosticCollection.forEach"></a><span class="ts" id=954 data-target="#details-954" data-toggle="collapse"><span class="ident">forEach</span><span>(</span><span class="ident">callback</span><span>: </span>(uri: <a class="type-ref" href="#Uri">Uri</a>, diagnostics: <a class="type-ref" href="#Diagnostic">Diagnostic</a>[], collection: <a class="type-ref" href="#DiagnosticCollection">DiagnosticCollection</a>) =&gt; <a class="type-instrinct">any</a>, <span class="ident">thisArg</span><span>?</span><span>: </span><a class="type-instrinct">any</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-954">
<div class="comment"><p>このコレクションの各エントリを繰り返し処理します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="callback"></a><span class="ts" id=955 data-target="#details-955" data-toggle="collapse"><span class="ident">callback</span><span>: </span>(uri: <a class="type-ref" href="#Uri">Uri</a>, diagnostics: <a class="type-ref" href="#Diagnostic">Diagnostic</a>[], collection: <a class="type-ref" href="#DiagnosticCollection">DiagnosticCollection</a>) =&gt; <a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="thisArg"></a><span class="ts" id=961 data-target="#details-961" data-toggle="collapse"><span class="ident">thisArg</span><span>?</span><span>: </span><a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="DiagnosticCollection.get"></a><span class="ts" id=963 data-target="#details-963" data-toggle="collapse"><span class="ident">get</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a><span>)</span><span>: </span><a class="type-ref" href="#Diagnostic">Diagnostic</a>[] &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-963">
<div class="comment"><p>特定のリソースの診断を取得します。 <em>注意</em>あなたはできません
この呼び出しから返された診断配列を変更する。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=964 data-target="#details-964" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Diagnostic">Diagnostic</a>[] &#124; <a class="type-instrinct">undefined</a></span></td><td><div class="comment"><p>(#Diagnostic)または <code>undefined</code> の不変な配列です。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="DiagnosticCollection.has"></a><span class="ts" id=966 data-target="#details-966" data-toggle="collapse"><span class="ident">has</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-966">
<div class="comment"><p>このコレクションに
与えられたリソース。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=967 data-target="#details-967" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>このコレクションが指定されたリソースの診断を持っている場合はtrueを返します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="DiagnosticCollection.set"></a><span class="ts" id=943 data-target="#details-943" data-toggle="collapse"><span class="ident">set</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a>, <span class="ident">diagnostics</span><span>: </span><a class="type-ref" href="#Diagnostic">Diagnostic</a>[] &#124; <a class="type-instrinct">undefined</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-943">
<div class="comment"><p>与えられたリソースに対して診断を割り当てます。置き換える
そのリソースの既存の診断。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=944 data-target="#details-944" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="diagnostics"></a><span class="ts" id=945 data-target="#details-945" data-toggle="collapse"><span class="ident">diagnostics</span><span>: </span><a class="type-ref" href="#Diagnostic">Diagnostic</a>[] &#124; <a class="type-instrinct">undefined</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="DiagnosticCollection.set"></a><span class="ts" id=946 data-target="#details-946" data-toggle="collapse"><span class="ident">set</span><span>(</span><span class="ident">entries</span><span>: </span>[<a class="type-ref" href="#Uri">Uri</a>, <a class="type-ref" href="#Diagnostic">Diagnostic</a>[] &#124; <a class="type-instrinct">undefined</a>][]<span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-946">
<div class="comment"><p>このコレクション内のすべてのエントリを置き換えます。</p>
<p>同じURIの複数のタプルの診断がマージされます。
[[file1、[d1]]、[file1、[d2]]] <code>は[[file1、[d1、d2]]]と同等です。
診断項目が</code>[file1、undefined]<code>のように</code>undefined` である場合
前の診断診断はすべて削除されますが、その後の診断は削除されません。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="entries"></a><span class="ts" id=947 data-target="#details-947" data-toggle="collapse"><span class="ident">entries</span><span>: </span>[<a class="type-ref" href="#Uri">Uri</a>, <a class="type-ref" href="#Diagnostic">Diagnostic</a>[] &#124; <a class="type-instrinct">undefined</a>][]</span></td><td><div class="comment"><p><code>[[file1、[d1、d2]]、[file2、[d3、d4、d5]]]、または</code> undefined`のようなタプルの配列。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="DiagnosticSeverity"></a><span class="code-item" id=924>DiagnosticSeverity</span>



<div class="comment"><p>診断の重大度を表します。</p>
</div>

#### Enumeration members



<a name="DiagnosticSeverity.Error"></a><span class="ts" id=925 data-target="#details-925" data-toggle="collapse"><span class="ident">Error</span></span>
<div class="details collapse" id="details-925">
<em>0</em>
</div>



<a name="DiagnosticSeverity.Hint"></a><span class="ts" id=928 data-target="#details-928" data-toggle="collapse"><span class="ident">Hint</span></span>
<div class="details collapse" id="details-928">
<em>3</em>
</div>



<a name="DiagnosticSeverity.Information"></a><span class="ts" id=927 data-target="#details-927" data-toggle="collapse"><span class="ident">Information</span></span>
<div class="details collapse" id="details-927">
<em>2</em>
</div>



<a name="DiagnosticSeverity.Warning"></a><span class="ts" id=926 data-target="#details-926" data-toggle="collapse"><span class="ident">Warning</span></span>
<div class="details collapse" id="details-926">
<em>1</em>
</div>

### <a name="Disposable"></a><span class="code-item" id=408>Disposable</span>



<div class="comment"><p>イベントリスニングやタイマーなど、リソースを解放できるタイプを表します。</p>
</div>

#### Static



<a name="Disposable.from"></a><span class="ts" id=410 data-target="#details-410" data-toggle="collapse"><span class="ident">from</span><span>(</span><span>...</span><span class="ident">disposableLikes</span><span>: </span>{dispose: () =&gt; <a class="type-instrinct">any</a>}[]<span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-410">
<div class="comment"><p>1つに多くの使い捨ての好きなものを組み合わせる。このメソッドを使用する
dispose関数を持つオブジェクトがない場合
Disposableのインスタンス。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="disposableLikes"></a><span class="ts" id=411 data-target="#details-411" data-toggle="collapse"><span>...</span><span class="ident">disposableLikes</span><span>: </span>{dispose: () =&gt; <a class="type-instrinct">any</a>}[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>新しいディスポーザブルを返します。
このディスポーザブルは、処分すると、すべてのディスポーザブルを処分します。</p>
</div></td></tr>
</table>
</div>
</div>

#### Constructors



<a name="Disposable.new Disposable"></a><span class="ts" id=417 data-target="#details-417" data-toggle="collapse"><span class="ident">new Disposable</span><span>(</span><span class="ident">callOnDispose</span><span>: </span><a class="type-ref" href="#Function">Function</a><span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-417">
<div class="comment"><p>提供された処分する関数を呼び出す新しいDisposableを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="callOnDispose"></a><span class="ts" id=418 data-target="#details-418" data-toggle="collapse"><span class="ident">callOnDispose</span><span>: </span><a class="type-ref" href="#Function">Function</a></span></td><td><div class="comment"><p>何かを処理する関数。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Methods



<a name="Disposable.dispose"></a><span class="ts" id=420 data-target="#details-420" data-toggle="collapse"><span class="ident">dispose</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">any</a></span>
<div class="details collapse" id="details-420">
<div class="comment"><p>このオブジェクトを廃棄します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="DocumentFilter"></a><span class="code-item" id=491>DocumentFilter</span>



<div class="comment"><p>ドキュメントフィルタは、ドキュメントの<a href="#TextDocument.languageId">言語</a>、リソースの<a href="#Uri.scheme">スキーム</a>、または[パス]に適用されるグロブパターン( #TextDocument.fileName)。</p>
<ul>
<li><em>sample</em> - ディスク上のtypescriptファイルに適用される言語フィルタ： <code>{language： &#39;typescript&#39;、scheme： &#39;file&#39;}</code></li>
</ul>
<ul>
<li><em>sample</em> - すべてのpackage.jsonパスに適用される言語フィルタ： `{language： &#39;json&#39;、pattern： &#39;*</li>
</ul>
</div>

#### Properties



<a name="DocumentFilter.language"></a><span class="ts" id=492 data-target="#details-492" data-toggle="collapse"><span class="ident">language</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-492">
<div class="comment"><p><code>typescript</code> のような言語IDです。</p>
</div>
</div>



<a name="DocumentFilter.pattern"></a><span class="ts" id=494 data-target="#details-494" data-toggle="collapse"><span class="ident">pattern</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-494">
<div class="comment"><p>グロブパターン。
<code>*。{ts、js}</code> のようです。</p>
</div>
</div>



<a name="DocumentFilter.scheme"></a><span class="ts" id=493 data-target="#details-493" data-toggle="collapse"><span class="ident">scheme</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-493">
<div class="comment"><p>Uri <a href="#Uri.scheme">scheme</a>、 <code>file</code> や <code>untitled</code> のように。</p>
</div>
</div>

### <a name="DocumentFormattingEditProvider"></a><span class="code-item" id=724>DocumentFormattingEditProvider</span>



<div class="comment"><p>文書フォーマットプロバイダインタフェースは、拡張機能と書式設定機能の間の契約を定義します。</p>
</div>

#### Methods



<a name="DocumentFormattingEditProvider.provideDocumentFormattingEdits"></a><span class="ts" id=726 data-target="#details-726" data-toggle="collapse"><span class="ident">provideDocumentFormattingEdits</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">options</span><span>: </span><a class="type-ref" href="#FormattingOptions">FormattingOptions</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-726">
<div class="comment"><p>ドキュメント全体の書式設定の編集を提供します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=727 data-target="#details-727" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=728 data-target="#details-728" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#FormattingOptions">FormattingOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=729 data-target="#details-729" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>テキストの編集のセットまたはそのように解決されるthenable。
結果の欠如は、 <code>undefined</code> 、 <code>null</code> 、または空の配列を返すことによって通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="DocumentHighlight"></a><span class="code-item" id=557>DocumentHighlight</span>



<div class="comment"><p>ドキュメントハイライトは、特に注意を要するテキストドキュメント内の範囲です。
通常、ドキュメントのハイライトは、その範囲の背景色を変更することによって視覚化されます。</p>
</div>

#### Constructors



<a name="DocumentHighlight.new DocumentHighlight"></a><span class="ts" id=561 data-target="#details-561" data-toggle="collapse"><span class="ident">new DocumentHighlight</span><span>(</span><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a>, <span class="ident">kind</span><span>?</span><span>: </span><a class="type-ref" href="#DocumentHighlightKind">DocumentHighlightKind</a><span>)</span><span>: </span><a class="type-ref" href="#DocumentHighlight">DocumentHighlight</a></span>
<div class="details collapse" id="details-561">
<div class="comment"><p>新しいドキュメントハイライトオブジェクトを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=562 data-target="#details-562" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="kind"></a><span class="ts" id=563 data-target="#details-563" data-toggle="collapse"><span class="ident">kind</span><span>?</span><span>: </span><a class="type-ref" href="#DocumentHighlightKind">DocumentHighlightKind</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#DocumentHighlight">DocumentHighlight</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="DocumentHighlight.kind"></a><span class="ts" id=559 data-target="#details-559" data-toggle="collapse"><span class="ident">kind</span><span>?</span><span>: </span><a class="type-ref" href="#DocumentHighlightKind">DocumentHighlightKind</a></span>
<div class="details collapse" id="details-559">
<div class="comment"><p>ハイライトの種類は、デフォルトで<a href="#DocumentHighlightKind.Text">text</a>です。</p>
</div>
</div>



<a name="DocumentHighlight.range"></a><span class="ts" id=558 data-target="#details-558" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-558">
<div class="comment"><p>このハイライトに適用される範囲。</p>
</div>
</div>

### <a name="DocumentHighlightKind"></a><span class="code-item" id=553>DocumentHighlightKind</span>



<div class="comment"><p>文書ハイライトの種類。</p>
</div>

#### Enumeration members



<a name="DocumentHighlightKind.Read"></a><span class="ts" id=555 data-target="#details-555" data-toggle="collapse"><span class="ident">Read</span></span>
<div class="details collapse" id="details-555">
<em>1</em>
</div>



<a name="DocumentHighlightKind.Text"></a><span class="ts" id=554 data-target="#details-554" data-toggle="collapse"><span class="ident">Text</span></span>
<div class="details collapse" id="details-554">
<em>0</em>
</div>



<a name="DocumentHighlightKind.Write"></a><span class="ts" id=556 data-target="#details-556" data-toggle="collapse"><span class="ident">Write</span></span>
<div class="details collapse" id="details-556">
<em>2</em>
</div>

### <a name="DocumentHighlightProvider"></a><span class="code-item" id=564>DocumentHighlightProvider</span>



<div class="comment"><p>ドキュメントハイライトプロバイダーインターフェイスは、エクステンションと単語ハイライト機能の間の契約を定義します。</p>
</div>

#### Methods



<a name="DocumentHighlightProvider.provideDocumentHighlights"></a><span class="ts" id=566 data-target="#details-566" data-toggle="collapse"><span class="ident">provideDocumentHighlights</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-566">
<div class="comment"><p>すべての変数のように、ドキュメントハイライトのセットを提供する
関数のすべての出口点。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=567 data-target="#details-567" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="position"></a><span class="ts" id=568 data-target="#details-568" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=569 data-target="#details-569" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>ドキュメントハイライトの配列またはそのように解釈されるネーブル。
結果の欠如は、 <code>undefined</code> 、 <code>null</code> 、または空の配列を返すことによって通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="DocumentLink"></a><span class="code-item" id=830>DocumentLink</span>



<div class="comment"><p>ドキュメントリンクは、テキストドキュメント内の範囲で、別のテキストドキュメントやWebサイトなどの内部リソースまたは外部リソースにリンクします。</p>
</div>

#### Constructors



<a name="DocumentLink.new DocumentLink"></a><span class="ts" id=834 data-target="#details-834" data-toggle="collapse"><span class="ident">new DocumentLink</span><span>(</span><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a>, <span class="ident">target</span><span>?</span><span>: </span><a class="type-ref" href="#Uri">Uri</a><span>)</span><span>: </span><a class="type-ref" href="#DocumentLink">DocumentLink</a></span>
<div class="details collapse" id="details-834">
<div class="comment"><p>新しい文書リンクを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=835 data-target="#details-835" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="target"></a><span class="ts" id=836 data-target="#details-836" data-toggle="collapse"><span class="ident">target</span><span>?</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#DocumentLink">DocumentLink</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="DocumentLink.range"></a><span class="ts" id=831 data-target="#details-831" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-831">
<div class="comment"><p>このリンクが適用される範囲。</p>
</div>
</div>



<a name="DocumentLink.target"></a><span class="ts" id=832 data-target="#details-832" data-toggle="collapse"><span class="ident">target</span><span>?</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-832">
<div class="comment"><p>このリンク先のuri。</p>
</div>
</div>

### <a name="DocumentLinkProvider"></a><span class="code-item" id=837>DocumentLinkProvider</span>



<div class="comment"><p>ドキュメントリンクプロバイダは、エクステンションとエディタでリンクを表示する機能との間のコントラクトを定義します。</p>
</div>

#### Methods



<a name="DocumentLinkProvider.provideDocumentLinks"></a><span class="ts" id=839 data-target="#details-839" data-toggle="collapse"><span class="ident">provideDocumentLinks</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-839">
<div class="comment"><p>与えられた文書へのリンクを提供する。
エディタにはデフォルトのプロバイダが付属していることに注意してください
<code>http(s)</code> と <code>file</code> リンク。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=840 data-target="#details-840" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=841 data-target="#details-841" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>(#DocumentLink)の配列またはそのように解決されるthenable。
結果の欠如は、 <code>undefined</code> 、 <code>null</code> 、または空の配列を返すことによって通知できます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="DocumentLinkProvider.resolveDocumentLink"></a><span class="ts" id=843 data-target="#details-843" data-toggle="collapse"><span class="ident">resolveDocumentLink</span><span>(</span><span class="ident">link</span><span>: </span><a class="type-ref" href="#DocumentLink">DocumentLink</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-843">
<div class="comment"><p><a href="#DocumentLink.target">target</a>にリンクを入力します。
このメソッドは、UIで不完全なリンクが選択されたときに呼び出されます。
プロバイダはこのメソッドを実装し、<a href="#DocumentLinkProvider.provideDocumentLinks"><code>provideDocumentLinks</code></a>メソッドから不完全なリンク(ターゲットなし)を返すことができます。
パフォーマンス向上に役立ちます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="link"></a><span class="ts" id=844 data-target="#details-844" data-toggle="collapse"><span class="ident">link</span><span>: </span><a class="type-ref" href="#DocumentLink">DocumentLink</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=845 data-target="#details-845" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="DocumentRangeFormattingEditProvider"></a><span class="code-item" id=730>DocumentRangeFormattingEditProvider</span>



<div class="comment"><p>文書フォーマットプロバイダインタフェースは、拡張機能と書式設定機能の間の契約を定義します。</p>
</div>

#### Methods



<a name="DocumentRangeFormattingEditProvider.provideDocumentRangeFormattingEdits"></a><span class="ts" id=732 data-target="#details-732" data-toggle="collapse"><span class="ident">provideDocumentRangeFormattingEdits</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a>, <span class="ident">options</span><span>: </span><a class="type-ref" href="#FormattingOptions">FormattingOptions</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-732">
<div class="comment"><p>ドキュメントの範囲の書式設定を編集します。</p>
<p>指定された範囲はヒントであり、プロバイダはより小さな
以上の範囲。多くの場合、これは開始点と終了点を調整することによって行われます
の完全な構文ノードの範囲。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=733 data-target="#details-733" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="range"></a><span class="ts" id=734 data-target="#details-734" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=735 data-target="#details-735" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#FormattingOptions">FormattingOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=736 data-target="#details-736" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>テキストの編集のセットまたはそのように解決されるthenable。
結果の欠如は、 <code>undefined</code> 、 <code>null</code> 、または空の配列を返すことによって通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="DocumentSelector"></a><span class="code-item" id=1159>DocumentSelector</span>



<div class="comment"><p>言語セレクタは、1つまたは複数の言語識別子と<a href="#DocumentFilter">言語フィルタ</a>の組み合わせです。</p>
<ul>
<li><em>sample</em> - <code>let sel：DocumentSelector = &#39;typescript&#39;</code>;</li>
</ul>
<ul>
<li><em>sample</em> - `let sel：DocumentSelector = [&#39;typescript&#39;、{言語： &#39;json&#39;、パターン： &#39;*</li>
</ul>
</div>



<a name="DocumentSelector"></a><span class="ts" id=1159 data-target="#details-1159" data-toggle="collapse"><span class="ident">DocumentSelector</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#DocumentFilter">DocumentFilter</a> &#124; <a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#DocumentFilter">DocumentFilter</a>[]</span>

### <a name="DocumentSymbolProvider"></a><span class="code-item" id=614>DocumentSymbolProvider</span>



<div class="comment"><p>ドキュメントシンボルプロバイダインタフェースは、エクステンションと<a href="https://code.visualstudio.com/docs/editor/editingevolved#_go-to-symbol">go to symbol</a>の間のコントラクトを定義します。</p>
</div>

#### Methods



<a name="DocumentSymbolProvider.provideDocumentSymbols"></a><span class="ts" id=616 data-target="#details-616" data-toggle="collapse"><span class="ident">provideDocumentSymbols</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-616">
<div class="comment"><p>与えられた文書のシンボル情報を提供する。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=617 data-target="#details-617" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=618 data-target="#details-618" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>ドキュメントハイライトの配列またはそのように解釈されるネーブル。
*結果の欠如は、 <code>undefined</code> 、 <code>null</code> 、または空の配列を返すことによって通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="EndOfLine"></a><span class="code-item" id=354>EndOfLine</span>



<div class="comment"><p><a href="#TextDocument">document</a>内の行末の文字列を表します。</p>
</div>

#### Enumeration members



<a name="EndOfLine.CRLF"></a><span class="ts" id=356 data-target="#details-356" data-toggle="collapse"><span class="ident">CRLF</span></span>
<div class="details collapse" id="details-356">
<em>2</em>
</div>



<a name="EndOfLine.LF"></a><span class="ts" id=355 data-target="#details-355" data-toggle="collapse"><span class="ident">LF</span></span>
<div class="details collapse" id="details-355">
<em>1</em>
</div>

### <a name="EnterAction"></a><span class="code-item" id=859>EnterAction</span>



<div class="comment"><p>Enterキーを押したときの処理について説明します。</p>
</div>

#### Properties



<a name="EnterAction.appendText"></a><span class="ts" id=861 data-target="#details-861" data-toggle="collapse"><span class="ident">appendText</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-861">
<div class="comment"><p>改行の後と字下げの後に追加するテキストを記述します。</p>
</div>
</div>



<a name="EnterAction.indentAction"></a><span class="ts" id=860 data-target="#details-860" data-toggle="collapse"><span class="ident">indentAction</span><span>: </span><a class="type-ref" href="#IndentAction">IndentAction</a></span>
<div class="details collapse" id="details-860">
<div class="comment"><p>インデントで何をするか説明してください。</p>
</div>
</div>



<a name="EnterAction.removeText"></a><span class="ts" id=862 data-target="#details-862" data-toggle="collapse"><span class="ident">removeText</span><span>?</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-862">
<div class="comment"><p>新しい行のインデントから削除する文字数を記述します。</p>
</div>
</div>

### <a name="Event"></a><span class="code-item" id=421>Event&lt;T&gt;</span>



<div class="comment"><p>型付きイベントを表します。</p>
<p>あなたがそれを呼び出すことによって購読するイベントを表す関数。
引数としてのリスナー関数。</p>
<ul>
<li><em>sample</em> - <code>item.onDidChange(function(event) { console.log(&quot;Event happened: &quot; + event); });</code></li>
</ul>
</div>



<a name="__call"></a><span class="ts" id=423 data-target="#details-423" data-toggle="collapse"><span>(</span><span class="ident">listener</span><span>: </span>(e: <a class="type-instrinct">T</a>) =&gt; <a class="type-instrinct">any</a>, <span class="ident">thisArgs</span><span>?</span><span>: </span><a class="type-instrinct">any</a>, <span class="ident">disposables</span><span>?</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a>[]<span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-423">
<div class="comment"><p>あなたがそれを呼び出すことによって購読するイベントを表す関数。
引数としてのリスナー関数。</p>
<p>あなたがそれを呼び出すことによって購読するイベントを表す関数。
引数としてのリスナー関数。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="listener"></a><span class="ts" id=424 data-target="#details-424" data-toggle="collapse"><span class="ident">listener</span><span>: </span>(e: <a class="type-instrinct">T</a>) =&gt; <a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="thisArgs"></a><span class="ts" id=428 data-target="#details-428" data-toggle="collapse"><span class="ident">thisArgs</span><span>?</span><span>: </span><a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="disposables"></a><span class="ts" id=429 data-target="#details-429" data-toggle="collapse"><span class="ident">disposables</span><span>?</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a>[]</span></td><td><div class="comment"><p>(#Disposable) が追加される配列。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>イベントリスナーの登録を解除する使い捨て</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="EventEmitter"></a><span class="code-item" id=430>EventEmitter&lt;T&gt;</span>



<div class="comment"><p>イベントエミッターを使用すると、他の人が購読する<a href="#イベント">イベント</a>を作成および管理できます。
1つのエミッタは常に1つのイベントを所有します。</p>
<p><a href="#TextDocumentContentProvider">TextDocumentContentProvider</a>内などの拡張機能内からイベントを提供する場合や、他の拡張機能にAPIを提供する場合は、このクラスを使用します。</p>
</div>

#### Properties



<a name="EventEmitter.event"></a><span class="ts" id=432 data-target="#details-432" data-toggle="collapse"><span class="ident">event</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-instrinct">T</a>&gt;</span>
<div class="details collapse" id="details-432">
<div class="comment"><p>イベントリスナーは購読できます。</p>
</div>
</div>

#### Methods



<a name="EventEmitter.dispose"></a><span class="ts" id=437 data-target="#details-437" data-toggle="collapse"><span class="ident">dispose</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-437">
<div class="comment"><p>このオブジェクトを廃棄し、リソースを解放します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="EventEmitter.fire"></a><span class="ts" id=434 data-target="#details-434" data-toggle="collapse"><span class="ident">fire</span><span>(</span><span class="ident">data</span><span>?</span><span>: </span><a class="type-instrinct">T</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-434">
<div class="comment"><p><a href="EventEmitter#イベント">イベント</a>のすべての加入者に通知します。失敗
 1つ以上のリスナーの*はこの関数呼び出しを失敗しません。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="data"></a><span class="ts" id=435 data-target="#details-435" data-toggle="collapse"><span class="ident">data</span><span>?</span><span>: </span><a class="type-instrinct">T</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="Extension"></a><span class="code-item" id=1029>Extension&lt;T&gt;</span>



<div class="comment"><p>拡張子を表します。</p>
<p>Extensionのインスタンスを取得するには、<a href="#extensions.getExtension">getExtension</a>を使用します。</p>
</div>

#### Properties



<a name="Extension.exports"></a><span class="ts" id=1035 data-target="#details-1035" data-toggle="collapse"><span class="ident">exports</span><span>: </span><a class="type-instrinct">T</a></span>
<div class="details collapse" id="details-1035">
<div class="comment"><p>この拡張機能によってエクスポートされたパブリックAPI。
この拡張機能が有効になる前に、このフィールドにアクセスするのは無効な操作です。</p>
</div>
</div>



<a name="Extension.extensionPath"></a><span class="ts" id=1032 data-target="#details-1032" data-toggle="collapse"><span class="ident">extensionPath</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1032">
<div class="comment"><p>この拡張子を含むディレクトリの絶対パス。</p>
</div>
</div>



<a name="Extension.id"></a><span class="ts" id=1031 data-target="#details-1031" data-toggle="collapse"><span class="ident">id</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1031">
<div class="comment"><p>正式な拡張識別子は <code>publisher.name</code> の形式です。</p>
</div>
</div>



<a name="Extension.isActive"></a><span class="ts" id=1033 data-target="#details-1033" data-toggle="collapse"><span class="ident">isActive</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-1033">
<div class="comment"><p>拡張機能が有効になっている場合は `true &#39;。</p>
</div>
</div>



<a name="Extension.packageJSON"></a><span class="ts" id=1034 data-target="#details-1034" data-toggle="collapse"><span class="ident">packageJSON</span><span>: </span><a class="type-instrinct">any</a></span>
<div class="details collapse" id="details-1034">
<div class="comment"><p>拡張機能のpackage.jsonの解析された内容。</p>
</div>
</div>

#### Methods



<a name="Extension.activate"></a><span class="ts" id=1037 data-target="#details-1037" data-toggle="collapse"><span class="ident">activate</span><span>(</span><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a>&gt;</span>
<div class="details collapse" id="details-1037">
<div class="comment"><p>この拡張機能を有効にして、公開APIを返します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a>&gt;</span></td><td><div class="comment"><p>この拡張機能がアクティブになったときに解決される約束です。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="ExtensionContext"></a><span class="code-item" id=1038>ExtensionContext</span>



<div class="comment"><p>拡張コンテキストは、拡張機能専用のユーティリティの集合です。</p>
<p><code>ExtensionContext</code> のインスタンスは、拡張機能の <code>activate</code> -callに対する最初のパラメータとして提供されます。</p>
</div>

#### Properties



<a name="ExtensionContext.extensionPath"></a><span class="ts" id=1045 data-target="#details-1045" data-toggle="collapse"><span class="ident">extensionPath</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1045">
<div class="comment"><p>拡張子を含むディレクトリの絶対パス。</p>
</div>
</div>



<a name="ExtensionContext.globalState"></a><span class="ts" id=1044 data-target="#details-1044" data-toggle="collapse"><span class="ident">globalState</span><span>: </span><a class="type-ref" href="#Memento">Memento</a></span>
<div class="details collapse" id="details-1044">
<div class="comment"><p>現在開いている<a href="#workspace.rootPath">workspace</a>に依存しない状態を保存するメモオブジェクト。</p>
</div>
</div>



<a name="ExtensionContext.storagePath"></a><span class="ts" id=1049 data-target="#details-1049" data-toggle="collapse"><span class="ident">storagePath</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-1049">
<div class="comment"><p>エクステンションがプライベート状態を格納できるワークスペース固有のディレクトリの絶対ファイルパス。
ディレクトリがディスク上に存在せず、作成が拡張子までです。
ただし、親ディレクトリは存在することが保証されています。</p>
<p><a href="#ExtensionContext.workspaceState"><code>workspaceState</code></a>を使用するか、
<a href="#ExtensionContext.globalState"><code>globalState</code></a>キー値のデータを格納します。</p>
</div>
</div>



<a name="ExtensionContext.subscriptions"></a><span class="ts" id=1039 data-target="#details-1039" data-toggle="collapse"><span class="ident">subscriptions</span><span>: </span>{dispose}[]</span>
<div class="details collapse" id="details-1039">
<div class="comment"><p>ディスポーザブルを追加できる配列。
この拡張機能を無効にすると、ディスポーザブルが破棄されます。</p>
</div>
</div>



<a name="ExtensionContext.workspaceState"></a><span class="ts" id=1043 data-target="#details-1043" data-toggle="collapse"><span class="ident">workspaceState</span><span>: </span><a class="type-ref" href="#Memento">Memento</a></span>
<div class="details collapse" id="details-1043">
<div class="comment"><p>現在開いている<a href="#workspace.rootPath">workspace</a>のコンテキストに状態を保存するメモオブジェクト。</p>
</div>
</div>

#### Methods



<a name="ExtensionContext.asAbsolutePath"></a><span class="ts" id=1047 data-target="#details-1047" data-toggle="collapse"><span class="ident">asAbsolutePath</span><span>(</span><span class="ident">relativePath</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1047">
<div class="comment"><p>エクステンションに含まれるリソースの絶対パスを取得します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="relativePath"></a><span class="ts" id=1048 data-target="#details-1048" data-toggle="collapse"><span class="ident">relativePath</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">string</a></span></td><td><div class="comment"><p>リソースの絶対パス。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="FileSystemWatcher"></a><span class="code-item" id=438>FileSystemWatcher</span>



<div class="comment"><p>ファイルシステムウォッチャーは、ディスク上のファイルやフォルダの変更を通知します。</p>
<p><code>FileSystemWatcher</code> のインスタンスを取得するには
<a href="#workspace.createFileSystemWatcher">createFileSystemWatcher</a>。</p>
</div>

#### Events



<a name="FileSystemWatcher.onDidChange"></a><span class="ts" id=443 data-target="#details-443" data-toggle="collapse"><span class="ident">onDidChange</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#Uri">Uri</a>&gt;</span>
<div class="details collapse" id="details-443">
<div class="comment"><p>ファイル/フォルダの変更で発生するイベント。</p>
</div>
</div>



<a name="FileSystemWatcher.onDidCreate"></a><span class="ts" id=442 data-target="#details-442" data-toggle="collapse"><span class="ident">onDidCreate</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#Uri">Uri</a>&gt;</span>
<div class="details collapse" id="details-442">
<div class="comment"><p>ファイル/フォルダ作成時に発生するイベント。</p>
</div>
</div>



<a name="FileSystemWatcher.onDidDelete"></a><span class="ts" id=444 data-target="#details-444" data-toggle="collapse"><span class="ident">onDidDelete</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#Uri">Uri</a>&gt;</span>
<div class="details collapse" id="details-444">
<div class="comment"><p>ファイル/フォルダの削除で発生するイベント。</p>
</div>
</div>

#### Static



<a name="FileSystemWatcher.from"></a><span class="ts" id=446 data-target="#details-446" data-toggle="collapse"><span class="ident">from</span><span>(</span><span>...</span><span class="ident">disposableLikes</span><span>: </span>{dispose: () =&gt; <a class="type-instrinct">any</a>}[]<span>)</span><span>: </span><a class="type-ref" href="#Disposable">Disposable</a></span>
<div class="details collapse" id="details-446">
<div class="comment"><p>1つに多くの使い捨ての好きなものを組み合わせる。このメソッドを使用する
dispose関数を持つオブジェクトがない場合
Disposableのインスタンス。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="disposableLikes"></a><span class="ts" id=447 data-target="#details-447" data-toggle="collapse"><span>...</span><span class="ident">disposableLikes</span><span>: </span>{dispose: () =&gt; <a class="type-instrinct">any</a>}[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Disposable">Disposable</a></span></td><td><div class="comment"><p>新しいディスポーザブルを返します。
このディスポーザブルは、処分すると、すべてのディスポーザブルを処分します。</p>
</div></td></tr>
</table>
</div>
</div>

#### Constructors



<a name="FileSystemWatcher.new FileSystemWatcher"></a><span class="ts" id=453 data-target="#details-453" data-toggle="collapse"><span class="ident">new FileSystemWatcher</span><span>(</span><span class="ident">callOnDispose</span><span>: </span><a class="type-ref" href="#Function">Function</a><span>)</span><span>: </span><a class="type-ref" href="#FileSystemWatcher">FileSystemWatcher</a></span>
<div class="details collapse" id="details-453">
<div class="comment"><p>提供された処分する関数を呼び出す新しいDisposableを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="callOnDispose"></a><span class="ts" id=454 data-target="#details-454" data-toggle="collapse"><span class="ident">callOnDispose</span><span>: </span><a class="type-ref" href="#Function">Function</a></span></td><td><div class="comment"><p>何かを処理する関数。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#FileSystemWatcher">FileSystemWatcher</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="FileSystemWatcher.ignoreChangeEvents"></a><span class="ts" id=440 data-target="#details-440" data-toggle="collapse"><span class="ident">ignoreChangeEvents</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-440">
<div class="comment"><p>このファイルシステムウォッチャーが変更されたファイルシステムイベントを無視するように作成されている場合はtrue。</p>
</div>
</div>



<a name="FileSystemWatcher.ignoreCreateEvents"></a><span class="ts" id=439 data-target="#details-439" data-toggle="collapse"><span class="ident">ignoreCreateEvents</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-439">
<div class="comment"><p>このファイルシステムウォッチャーが作成ファイルシステムイベントを無視するように作成されている場合はtrue。</p>
</div>
</div>



<a name="FileSystemWatcher.ignoreDeleteEvents"></a><span class="ts" id=441 data-target="#details-441" data-toggle="collapse"><span class="ident">ignoreDeleteEvents</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-441">
<div class="comment"><p>このファイルシステムウォッチャーがファイルシステムイベントの削除を無視するように作成されている場合はtrue。</p>
</div>
</div>

#### Methods



<a name="FileSystemWatcher.dispose"></a><span class="ts" id=456 data-target="#details-456" data-toggle="collapse"><span class="ident">dispose</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">any</a></span>
<div class="details collapse" id="details-456">
<div class="comment"><p>このオブジェクトを廃棄します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="FormattingOptions"></a><span class="code-item" id=719>FormattingOptions</span>



<div class="comment"><p>オプション - どのオプションの書式設定を使用するかを記述するValueオブジェクト。</p>
</div>

#### Properties



<a name="FormattingOptions.insertSpaces"></a><span class="ts" id=721 data-target="#details-721" data-toggle="collapse"><span class="ident">insertSpaces</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-721">
<div class="comment"><p>タブ上のスペースを優先する。</p>
</div>
</div>



<a name="FormattingOptions.tabSize"></a><span class="ts" id=720 data-target="#details-720" data-toggle="collapse"><span class="ident">tabSize</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-720">
<div class="comment"><p>スペース内のタブのサイズ。</p>
</div>
</div>

### <a name="Hover"></a><span class="code-item" id=540>Hover</span>



<div class="comment"><p>ホバーは記号や単語の追加情報を表します。
ホバーは、ツールチップのようなウィジェットでレンダリングされます。</p>
</div>

#### Constructors



<a name="Hover.new Hover"></a><span class="ts" id=544 data-target="#details-544" data-toggle="collapse"><span class="ident">new Hover</span><span>(</span><span class="ident">contents</span><span>: </span><a class="type-ref" href="#MarkedString">MarkedString</a> &#124; <a class="type-ref" href="#MarkedString">MarkedString</a>[], <span class="ident">range</span><span>?</span><span>: </span><a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-ref" href="#Hover">Hover</a></span>
<div class="details collapse" id="details-544">
<div class="comment"><p>新しいホバーオブジェクトを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="contents"></a><span class="ts" id=545 data-target="#details-545" data-toggle="collapse"><span class="ident">contents</span><span>: </span><a class="type-ref" href="#MarkedString">MarkedString</a> &#124; <a class="type-ref" href="#MarkedString">MarkedString</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="range"></a><span class="ts" id=546 data-target="#details-546" data-toggle="collapse"><span class="ident">range</span><span>?</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Hover">Hover</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="Hover.contents"></a><span class="ts" id=541 data-target="#details-541" data-toggle="collapse"><span class="ident">contents</span><span>: </span><a class="type-ref" href="#MarkedString">MarkedString</a>[]</span>
<div class="details collapse" id="details-541">
<div class="comment"><p>このホバーの内容。</p>
</div>
</div>



<a name="Hover.range"></a><span class="ts" id=542 data-target="#details-542" data-toggle="collapse"><span class="ident">range</span><span>?</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-542">
<div class="comment"><p>このホバーが適用される範囲。
行方不明の場合、エディタは現在の位置の範囲または現在の位置自体を使用します。</p>
</div>
</div>

### <a name="HoverProvider"></a><span class="code-item" id=547>HoverProvider</span>



<div class="comment"><p>ホバープロバイダインタフェースは、拡張機能と<a href="https://code.visualstudio.com/docs/editor/intellisense">ホバー</a>機能の間の契約を定義します。</p>
</div>

#### Methods



<a name="HoverProvider.provideHover"></a><span class="ts" id=549 data-target="#details-549" data-toggle="collapse"><span class="ident">provideHover</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-549">
<div class="comment"><p>与えられた位置とドキュメントのホバーを提供する。同じ複数のホバー
位置はエディタによってマージされます。ホバーにはデフォルトの範囲があります
省略された位置の単語範囲に*。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=550 data-target="#details-550" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="position"></a><span class="ts" id=551 data-target="#details-551" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=552 data-target="#details-552" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>そのように解決するホバーまたはネクサブルです。
結果の不足は、 <code>undefined</code> または <code>null</code> を返すことで通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="ImplementationProvider"></a><span class="code-item" id=528>ImplementationProvider</span>



<div class="comment"><p>実装プロバイダインタフェースは、拡張機能と実装機能の間の契約を定義します。</p>
</div>

#### Methods



<a name="ImplementationProvider.provideImplementation"></a><span class="ts" id=530 data-target="#details-530" data-toggle="collapse"><span class="ident">provideImplementation</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-530">
<div class="comment"><p>与えられた位置と文書でシンボルの実装を提供する。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=531 data-target="#details-531" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="position"></a><span class="ts" id=532 data-target="#details-532" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=533 data-target="#details-533" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>このように解決される定義または変換可能なテーブル。
結果の不足は、 <code>undefined</code> または <code>null</code> を返すことで通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="IndentAction"></a><span class="code-item" id=854>IndentAction</span>



<div class="comment"><p>Enterキーを押したときのインデントの処理方法を説明します。</p>
</div>

#### Enumeration members



<a name="IndentAction.Indent"></a><span class="ts" id=856 data-target="#details-856" data-toggle="collapse"><span class="ident">Indent</span></span>
<div class="details collapse" id="details-856">
<em>1</em>
</div>



<a name="IndentAction.IndentOutdent"></a><span class="ts" id=857 data-target="#details-857" data-toggle="collapse"><span class="ident">IndentOutdent</span></span>
<div class="details collapse" id="details-857">
<em>2</em>
</div>



<a name="IndentAction.None"></a><span class="ts" id=855 data-target="#details-855" data-toggle="collapse"><span class="ident">None</span></span>
<div class="details collapse" id="details-855">
<em>0</em>
</div>



<a name="IndentAction.Outdent"></a><span class="ts" id=858 data-target="#details-858" data-toggle="collapse"><span class="ident">Outdent</span></span>
<div class="details collapse" id="details-858">
<em>3</em>
</div>

### <a name="IndentationRule"></a><span class="code-item" id=849>IndentationRule</span>



<div class="comment"><p>言語の字下げ規則について説明します。</p>
</div>

#### Properties



<a name="IndentationRule.decreaseIndentPattern"></a><span class="ts" id=850 data-target="#details-850" data-toggle="collapse"><span class="ident">decreaseIndentPattern</span><span>: </span><a class="type-ref" href="#RegExp">RegExp</a></span>
<div class="details collapse" id="details-850">
<div class="comment"><p>行がこのパターンと一致する場合、その行の後ろにあるすべての行は、(他の規則が一致するまで)一度インデントされていないはずです。</p>
</div>
</div>



<a name="IndentationRule.increaseIndentPattern"></a><span class="ts" id=851 data-target="#details-851" data-toggle="collapse"><span class="ident">increaseIndentPattern</span><span>: </span><a class="type-ref" href="#RegExp">RegExp</a></span>
<div class="details collapse" id="details-851">
<div class="comment"><p>行がこのパターンと一致する場合、その行の後ろにあるすべての行は(別の規則が一致するまで)一度インデントされる必要があります。</p>
</div>
</div>



<a name="IndentationRule.indentNextLinePattern"></a><span class="ts" id=852 data-target="#details-852" data-toggle="collapse"><span class="ident">indentNextLinePattern</span><span>?</span><span>: </span><a class="type-ref" href="#RegExp">RegExp</a></span>
<div class="details collapse" id="details-852">
<div class="comment"><p>行がこのパターンと一致する場合は、<strong>一度インデントされた後に</strong>次の行**のみが表示されます。</p>
</div>
</div>



<a name="IndentationRule.unIndentedLinePattern"></a><span class="ts" id=853 data-target="#details-853" data-toggle="collapse"><span class="ident">unIndentedLinePattern</span><span>?</span><span>: </span><a class="type-ref" href="#RegExp">RegExp</a></span>
<div class="details collapse" id="details-853">
<div class="comment"><p>行がこのパターンと一致する場合、インデントを変更してはならず、他のルールに対して評価するべきではありません。</p>
</div>
</div>

### <a name="InputBoxOptions"></a><span class="code-item" id=481>InputBoxOptions</span>



<div class="comment"><p>入力ボックスのUIの動作を設定するオプション。</p>
</div>

#### Properties



<a name="InputBoxOptions.ignoreFocusOut"></a><span class="ts" id=487 data-target="#details-487" data-toggle="collapse"><span class="ident">ignoreFocusOut</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-487">
<div class="comment"><p>フォーカスがエディタの別の部分または別のウィンドウに移動したときに入力ボックスを開いたままにするには、「true」に設定します。</p>
</div>
</div>



<a name="InputBoxOptions.password"></a><span class="ts" id=486 data-target="#details-486" data-toggle="collapse"><span class="ident">password</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-486">
<div class="comment"><p>入力された値を表示しないパスワードプロンプトを表示するには、 <code>true</code> に設定します。</p>
</div>
</div>



<a name="InputBoxOptions.placeHolder"></a><span class="ts" id=485 data-target="#details-485" data-toggle="collapse"><span class="ident">placeHolder</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-485">
<div class="comment"><p>入力ボックスにプレースホルダとして表示して、ユーザーに何を入力するかを案内するオプションの文字列。</p>
</div>
</div>



<a name="InputBoxOptions.prompt"></a><span class="ts" id=484 data-target="#details-484" data-toggle="collapse"><span class="ident">prompt</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-484">
<div class="comment"><p>入力ボックスの下に表示するテキスト。</p>
</div>
</div>



<a name="InputBoxOptions.value"></a><span class="ts" id=482 data-target="#details-482" data-toggle="collapse"><span class="ident">value</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-482">
<div class="comment"><p>入力ボックスにプレフィルする値。</p>
</div>
</div>



<a name="InputBoxOptions.valueSelection"></a><span class="ts" id=483 data-target="#details-483" data-toggle="collapse"><span class="ident">valueSelection</span><span>?</span><span>: </span>[<a class="type-instrinct">number</a>, <a class="type-instrinct">number</a>]</span>
<div class="details collapse" id="details-483">
<div class="comment"><p>プレフィルド[ <code>value</code> ]の選択(#InputBoxOptions.value)。
2つの数値のタプルとして定義され、最初はインクルーシブ開始インデックス、2番目は排他終了インデックスです。
`undefined &#39;のときは単語全体が選択され、空の場合(start equals end)はカーソルのみが設定され、そうでなければ定義された範囲が選択されます。</p>
</div>
</div>

#### Methods



<a name="InputBoxOptions.validateInput"></a><span class="ts" id=489 data-target="#details-489" data-toggle="collapse"><span class="ident">validateInput</span><span>(</span><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a> &#124; <a class="type-instrinct">null</a></span>
<div class="details collapse" id="details-489">
<div class="comment"><p>入力を検証してヒントを与えるために呼び出されるオプションの関数
をユーザーに送信します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="value"></a><span class="ts" id=490 data-target="#details-490" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a> &#124; <a class="type-instrinct">null</a></span></td><td><div class="comment"><p>診断メッセージとして表示される人間が読める文字列。
&#39;value&#39;が有効な場合は <code>undefined</code> 、 <code>null</code> 、または空文字列を返します。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="LanguageConfiguration"></a><span class="code-item" id=867>LanguageConfiguration</span>



<div class="comment"><p>言語設定インターフェースは、自動ブラケット挿入、自動インデントなどの拡張機能とさまざまなエディタ機能の間の契約を定義します。</p>
</div>

#### Properties



<a name="LanguageConfiguration.___characterPairSupport"></a><span class="ts" id=882 data-target="#details-882" data-toggle="collapse"><span class="ident">___characterPairSupport</span><span>?</span><span>: </span>{autoClosingPairs: {close: <a class="type-instrinct">string</a>, notIn: <a class="type-instrinct">string</a>[], open: <a class="type-instrinct">string</a>}[]}</span>
<div class="details collapse" id="details-882">
<div class="comment"><p><strong>非推奨* </strong>使用しないでください。</p>
<ul>
<li><em>deprecated</em> - *代わりに言語設定ファイルのautoClosingPairsプロパティを使用します。</li>
</ul>
</div>
</div>



<a name="LanguageConfiguration.___electricCharacterSupport"></a><span class="ts" id=873 data-target="#details-873" data-toggle="collapse"><span class="ident">___electricCharacterSupport</span><span>?</span><span>: </span>{brackets: <a class="type-instrinct">any</a>, docComment: {close: <a class="type-instrinct">string</a>, lineStart: <a class="type-instrinct">string</a>, open: <a class="type-instrinct">string</a>, scope: <a class="type-instrinct">string</a>}}</span>
<div class="details collapse" id="details-873">
<div class="comment"><p><strong>非推奨* </strong>使用しないでください。</p>
<ul>
<li><em>deprecated</em> - すぐにより良いAPIに置き換えられます。</li>
</ul>
</div>
</div>



<a name="LanguageConfiguration.brackets"></a><span class="ts" id=869 data-target="#details-869" data-toggle="collapse"><span class="ident">brackets</span><span>?</span><span>: </span><a class="type-ref" href="#CharacterPair">CharacterPair</a>[]</span>
<div class="details collapse" id="details-869">
<div class="comment"><p>言語の括弧。
この設定は、これらの括弧のまわりでEnterキーを押すことに暗黙のうちに影響します。</p>
</div>
</div>



<a name="LanguageConfiguration.comments"></a><span class="ts" id=868 data-target="#details-868" data-toggle="collapse"><span class="ident">comments</span><span>?</span><span>: </span><a class="type-ref" href="#CommentRule">CommentRule</a></span>
<div class="details collapse" id="details-868">
<div class="comment"><p>言語のコメント設定。</p>
</div>
</div>



<a name="LanguageConfiguration.indentationRules"></a><span class="ts" id=871 data-target="#details-871" data-toggle="collapse"><span class="ident">indentationRules</span><span>?</span><span>: </span><a class="type-ref" href="#IndentationRule">IndentationRule</a></span>
<div class="details collapse" id="details-871">
<div class="comment"><p>言語のインデント設定。</p>
</div>
</div>



<a name="LanguageConfiguration.onEnterRules"></a><span class="ts" id=872 data-target="#details-872" data-toggle="collapse"><span class="ident">onEnterRules</span><span>?</span><span>: </span><a class="type-ref" href="#OnEnterRule">OnEnterRule</a>[]</span>
<div class="details collapse" id="details-872">
<div class="comment"><p>Enterキーを押したときに評価される言語のルール。</p>
</div>
</div>



<a name="LanguageConfiguration.wordPattern"></a><span class="ts" id=870 data-target="#details-870" data-toggle="collapse"><span class="ident">wordPattern</span><span>?</span><span>: </span><a class="type-ref" href="#RegExp">RegExp</a></span>
<div class="details collapse" id="details-870">
<div class="comment"><p>言語の単語定義。
言語がUnicode識別子(JavaScriptなど)をサポートしている場合は、既知の区切り文字の除外を使用する単語定義を提供することが望ましいです。
例：既知の区切り文字以外のものにマッチする正規表現です(ドットは浮動小数点数で使用できます)。</p>
</div>
</div>

### <a name="Location"></a><span class="code-item" id=917>Location</span>



<div class="comment"><p>リソース内の場所(テキストファイル内の行など)を表します。</p>
</div>

#### Constructors



<a name="Location.new Location"></a><span class="ts" id=921 data-target="#details-921" data-toggle="collapse"><span class="ident">new Location</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a>, <span class="ident">rangeOrPosition</span><span>: </span><a class="type-ref" href="#Range">Range</a> &#124; <a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-ref" href="#Location">Location</a></span>
<div class="details collapse" id="details-921">
<div class="comment"><p>新しいロケーションオブジェクトを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=922 data-target="#details-922" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="rangeOrPosition"></a><span class="ts" id=923 data-target="#details-923" data-toggle="collapse"><span class="ident">rangeOrPosition</span><span>: </span><a class="type-ref" href="#Range">Range</a> &#124; <a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Location">Location</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="Location.range"></a><span class="ts" id=919 data-target="#details-919" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-919">
<div class="comment"><p>この場所の文書の範囲。</p>
</div>
</div>



<a name="Location.uri"></a><span class="ts" id=918 data-target="#details-918" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-918">
<div class="comment"><p>このロケーションのリソース識別子。</p>
</div>
</div>

### <a name="MarkedString"></a><span class="code-item" id=1162>MarkedString</span>



<div class="comment"><p>MarkedStringは、人間が読めるテキストを表示するために使用できます。
マークダウン文字列か、言語とコードスニペットを提供するコードブロックのいずれかです。
マークダウン文字列はサニタイズされます。
つまり、HTMLはエスケープされます。</p>
</div>



<a name="MarkedString"></a><span class="ts" id=1162 data-target="#details-1162" data-toggle="collapse"><span class="ident">MarkedString</span><span>: </span><a class="type-instrinct">string</a> &#124; {language: <a class="type-instrinct">string</a>, value: <a class="type-instrinct">string</a>}</span>

### <a name="Memento"></a><span class="code-item" id=1050>Memento</span>



<div class="comment"><p>記念品は、ストレージユーティリティを表します。
値を格納して取り出すことができます。</p>
</div>

#### Methods



<a name="Memento.get"></a><span class="ts" id=1052 data-target="#details-1052" data-toggle="collapse"><span class="ident">get</span><span>&lt;</span>T<span>&gt;</span><span>(</span><span class="ident">key</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-1052">
<div class="comment"><p>値を返します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="key"></a><span class="ts" id=1054 data-target="#details-1054" data-toggle="collapse"><span class="ident">key</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a></span></td><td><div class="comment"><p>格納された値または <code>undefined</code>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Memento.get"></a><span class="ts" id=1055 data-target="#details-1055" data-toggle="collapse"><span class="ident">get</span><span>&lt;</span>T<span>&gt;</span><span>(</span><span class="ident">key</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">defaultValue</span><span>: </span><a class="type-instrinct">T</a><span>)</span><span>: </span><a class="type-instrinct">T</a></span>
<div class="details collapse" id="details-1055">
<div class="comment"><p>値を返します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="key"></a><span class="ts" id=1057 data-target="#details-1057" data-toggle="collapse"><span class="ident">key</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="defaultValue"></a><span class="ts" id=1058 data-target="#details-1058" data-toggle="collapse"><span class="ident">defaultValue</span><span>: </span><a class="type-instrinct">T</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">T</a></span></td><td><div class="comment"><p>格納された値またはdefaultValue</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Memento.update"></a><span class="ts" id=1060 data-target="#details-1060" data-toggle="collapse"><span class="ident">update</span><span>(</span><span class="ident">key</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">value</span><span>: </span><a class="type-instrinct">any</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">void</a>&gt;</span>
<div class="details collapse" id="details-1060">
<div class="comment"><p>値を保存します。値はJSON文字列でなければなりません。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="key"></a><span class="ts" id=1061 data-target="#details-1061" data-toggle="collapse"><span class="ident">key</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="value"></a><span class="ts" id=1062 data-target="#details-1062" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">void</a>&gt;</span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="MessageItem"></a><span class="code-item" id=476>MessageItem</span>



<div class="comment"><p>情報、警告、または情報とともに表示されるアクションを表します。
エラーメッセージ。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a>* @@see <a href="#window.showWarningMessage">showWarningMessage</a></li>
</ul>
<ul>
<li><em>see</em> - <a href="#window.showErrorMessage">showErrorMessage</a></li>
</ul>
</div>

#### Properties



<a name="MessageItem.isCloseAffordance"></a><span class="ts" id=478 data-target="#details-478" data-toggle="collapse"><span class="ident">isCloseAffordance</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-478">
<div class="comment"><p>この項目がデフォルトの「閉じる」アクションを置き換えることを示します。</p>
</div>
</div>



<a name="MessageItem.title"></a><span class="ts" id=477 data-target="#details-477" data-toggle="collapse"><span class="ident">title</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-477">
<div class="comment"><p>&#39;Retry&#39;、 &#39;Open Log&#39;などの短いタイトル</p>
</div>
</div>

### <a name="MessageOptions"></a><span class="code-item" id=479>MessageOptions</span>



<div class="comment"><p>メッセージの動作を設定するオプション。</p>
<ul>
<li><em>see</em> - <a href="#window.showInformationMessage">showInformationMessage</a></li>
</ul>
<ul>
<li><em>see</em> - <a href="#window.showWarningMessage">showWarningMessage</a></li>
</ul>
<ul>
<li><em>see</em> - <a href="#window.showErrorMessage">showErrorMessage</a></li>
</ul>
</div>

#### Properties



<a name="MessageOptions.modal"></a><span class="ts" id=480 data-target="#details-480" data-toggle="collapse"><span class="ident">modal</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-480">
<div class="comment"><p>このメッセージはモーダルであることを示します。</p>
</div>
</div>

### <a name="OnEnterRule"></a><span class="code-item" id=863>OnEnterRule</span>



<div class="comment"><p>Enterキーを押したときに評価されるルールを説明します。</p>
</div>

#### Properties



<a name="OnEnterRule.action"></a><span class="ts" id=866 data-target="#details-866" data-toggle="collapse"><span class="ident">action</span><span>: </span><a class="type-ref" href="#EnterAction">EnterAction</a></span>
<div class="details collapse" id="details-866">
<div class="comment"><p>実行するアクション。</p>
</div>
</div>



<a name="OnEnterRule.afterText"></a><span class="ts" id=865 data-target="#details-865" data-toggle="collapse"><span class="ident">afterText</span><span>?</span><span>: </span><a class="type-ref" href="#RegExp">RegExp</a></span>
<div class="details collapse" id="details-865">
<div class="comment"><p>このルールは、カーソルの後のテキストがこの正規表現に一致する場合にのみ実行されます。</p>
</div>
</div>



<a name="OnEnterRule.beforeText"></a><span class="ts" id=864 data-target="#details-864" data-toggle="collapse"><span class="ident">beforeText</span><span>: </span><a class="type-ref" href="#RegExp">RegExp</a></span>
<div class="details collapse" id="details-864">
<div class="comment"><p>このルールは、カーソルの前のテキストがこの正規表現と一致する場合にのみ実行されます。</p>
</div>
</div>

### <a name="OnTypeFormattingEditProvider"></a><span class="code-item" id=737>OnTypeFormattingEditProvider</span>



<div class="comment"><p>文書フォーマットプロバイダインタフェースは、拡張機能と書式設定機能の間の契約を定義します。</p>
</div>

#### Methods



<a name="OnTypeFormattingEditProvider.provideOnTypeFormattingEdits"></a><span class="ts" id=739 data-target="#details-739" data-toggle="collapse"><span class="ident">provideOnTypeFormattingEdits</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">ch</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">options</span><span>: </span><a class="type-ref" href="#FormattingOptions">FormattingOptions</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-739">
<div class="comment"><p>文字の入力後に書式の編集を行います。</p>
<p>与えられた位置と文字は、展開する位置の範囲をプロバイダに示唆する必要があります。
一致する <code>{</code>
<code>}</code> が入力されたとき*。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=740 data-target="#details-740" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="position"></a><span class="ts" id=741 data-target="#details-741" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="ch"></a><span class="ts" id=742 data-target="#details-742" data-toggle="collapse"><span class="ident">ch</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=743 data-target="#details-743" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#FormattingOptions">FormattingOptions</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=744 data-target="#details-744" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>テキストの編集のセットまたはそのように解決されるthenable。
結果の欠如は、 <code>undefined</code> 、 <code>null</code> 、または空の配列を返すことによって通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="OutputChannel"></a><span class="code-item" id=974>OutputChannel</span>



<div class="comment"><p>出力チャネルは、読み込み専用のテキスト情報のコンテナです。</p>
<p><code>OutputChannel</code> のインスタンスを取得するには
<a href="#window.createOutputChannel">createOutputChannel</a>。</p>
</div>

#### Properties



<a name="OutputChannel.name"></a><span class="ts" id=975 data-target="#details-975" data-toggle="collapse"><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-975">
<div class="comment"><p>この出力チャネルの人間が読める名前。</p>
</div>
</div>

#### Methods



<a name="OutputChannel.append"></a><span class="ts" id=977 data-target="#details-977" data-toggle="collapse"><span class="ident">append</span><span>(</span><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-977">
<div class="comment"><p>与えられた値をチャンネルに追加します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="value"></a><span class="ts" id=978 data-target="#details-978" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="OutputChannel.appendLine"></a><span class="ts" id=980 data-target="#details-980" data-toggle="collapse"><span class="ident">appendLine</span><span>(</span><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-980">
<div class="comment"><p>与えられた値と改行文字を追加する
をチャンネルに追加します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="value"></a><span class="ts" id=981 data-target="#details-981" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="OutputChannel.clear"></a><span class="ts" id=983 data-target="#details-983" data-toggle="collapse"><span class="ident">clear</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-983">
<div class="comment"><p>チャンネルからすべての出力を削除します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="OutputChannel.dispose"></a><span class="ts" id=993 data-target="#details-993" data-toggle="collapse"><span class="ident">dispose</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-993">
<div class="comment"><p>廃棄し、関連するリソースを解放します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="OutputChannel.hide"></a><span class="ts" id=991 data-target="#details-991" data-toggle="collapse"><span class="ident">hide</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-991">
<div class="comment"><p>UIからこのチャンネルを非表示にします。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="OutputChannel.show"></a><span class="ts" id=985 data-target="#details-985" data-toggle="collapse"><span class="ident">show</span><span>(</span><span class="ident">preserveFocus</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-985">
<div class="comment"><p>UIでこのチャンネルを明らかにする。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="preserveFocus"></a><span class="ts" id=986 data-target="#details-986" data-toggle="collapse"><span class="ident">preserveFocus</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p><code>true</code> の場合、チャンネルはフォーカスを取得しません。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="OutputChannel.show"></a><span class="ts" id=987 data-target="#details-987" data-toggle="collapse"><span class="ident">show</span><span>(</span><span class="ident">column</span><span>?</span><span>: </span><a class="type-ref" href="#ViewColumn">ViewColumn</a>, <span class="ident">preserveFocus</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-987">
<div class="comment"><p>UIでこのチャンネルを明らかにする。</p>
<ul>
<li><em>deprecated</em> - このメソッドは<strong>推奨されていません</strong>、1つのパラメータでオーバーロードを使用する必要があります( <code>show(preserveFocus ?: boolean)：void</code> )。</li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="column"></a><span class="ts" id=988 data-target="#details-988" data-toggle="collapse"><span class="ident">column</span><span>?</span><span>: </span><a class="type-ref" href="#ViewColumn">ViewColumn</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="preserveFocus"></a><span class="ts" id=989 data-target="#details-989" data-toggle="collapse"><span class="ident">preserveFocus</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p><code>true</code> の場合、チャンネルはフォーカスを取得しません。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="OverviewRulerLane"></a><span class="code-item" id=229>OverviewRulerLane</span>



<div class="comment"><p><a href="#DecorationRenderOptions.overviewRulerLane">概要ルーラー</a>で装飾をレンダリングするための異なる位置を表します。
概観ルーラーは3つのレーンをサポートしています。</p>
</div>

#### Enumeration members



<a name="OverviewRulerLane.Center"></a><span class="ts" id=231 data-target="#details-231" data-toggle="collapse"><span class="ident">Center</span></span>
<div class="details collapse" id="details-231">
<em>2</em>
</div>



<a name="OverviewRulerLane.Full"></a><span class="ts" id=233 data-target="#details-233" data-toggle="collapse"><span class="ident">Full</span></span>
<div class="details collapse" id="details-233">
<em>7</em>
</div>



<a name="OverviewRulerLane.Left"></a><span class="ts" id=230 data-target="#details-230" data-toggle="collapse"><span class="ident">Left</span></span>
<div class="details collapse" id="details-230">
<em>1</em>
</div>



<a name="OverviewRulerLane.Right"></a><span class="ts" id=232 data-target="#details-232" data-toggle="collapse"><span class="ident">Right</span></span>
<div class="details collapse" id="details-232">
<em>4</em>
</div>

### <a name="ParameterInformation"></a><span class="code-item" id=745>ParameterInformation</span>



<div class="comment"><p>呼び出し可能な署名のパラメータを表します。
*パラメータには、ラベルとドキュメントコメントを付けることができます。</p>
</div>

#### Constructors



<a name="ParameterInformation.new ParameterInformation"></a><span class="ts" id=749 data-target="#details-749" data-toggle="collapse"><span class="ident">new ParameterInformation</span><span>(</span><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">documentation</span><span>?</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#ParameterInformation">ParameterInformation</a></span>
<div class="details collapse" id="details-749">
<div class="comment"><p>新しいパラメータ情報オブジェクトを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="label"></a><span class="ts" id=750 data-target="#details-750" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="documentation"></a><span class="ts" id=751 data-target="#details-751" data-toggle="collapse"><span class="ident">documentation</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ParameterInformation">ParameterInformation</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="ParameterInformation.documentation"></a><span class="ts" id=747 data-target="#details-747" data-toggle="collapse"><span class="ident">documentation</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-747">
<div class="comment"><p>この署名の人間が読めるdocコメント。
UIに表示されますが、省略することができます。</p>
</div>
</div>



<a name="ParameterInformation.label"></a><span class="ts" id=746 data-target="#details-746" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-746">
<div class="comment"><p>この署名のラベル。
UIに表示されます。</p>
</div>
</div>

### <a name="Position"></a><span class="code-item" id=74>Position</span>



<div class="comment"><p>カーソルの位置などの行と文字の位置を表します。</p>
<p>位置オブジェクトは<strong>immutable</strong>です。
<a href="#Position.with">with</a>または <a href="#Position.translate">translate</a>メソッドを使用して、既存の位置から新しい position を派生させます。</p>
</div>

#### Constructors



<a name="Position.new Position"></a><span class="ts" id=78 data-target="#details-78" data-toggle="collapse"><span class="ident">new Position</span><span>(</span><span class="ident">line</span><span>: </span><a class="type-instrinct">number</a>, <span class="ident">character</span><span>: </span><a class="type-instrinct">number</a><span>)</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-78">
<div class="comment"></div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="line"></a><span class="ts" id=79 data-target="#details-79" data-toggle="collapse"><span class="ident">line</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>0から始まる行の値。</p>
</div></td></tr>
<tr><td><a name="character"></a><span class="ts" id=80 data-target="#details-80" data-toggle="collapse"><span class="ident">character</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>0から始まる文字値。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="Position.character"></a><span class="ts" id=76 data-target="#details-76" data-toggle="collapse"><span class="ident">character</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-76">
<div class="comment"><p>ゼロベースの文字値。</p>
</div>
</div>



<a name="Position.line"></a><span class="ts" id=75 data-target="#details-75" data-toggle="collapse"><span class="ident">line</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-75">
<div class="comment"><p>0から始まる行の値。</p>
</div>
</div>

#### Methods



<a name="Position.compareTo"></a><span class="ts" id=97 data-target="#details-97" data-toggle="collapse"><span class="ident">compareTo</span><span>(</span><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-97">
<div class="comment"><p>これを <code>other</code> と比較します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="other"></a><span class="ts" id=98 data-target="#details-98" data-toggle="collapse"><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>その他の位置。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>この位置が指定された位置の前にある場合は0より小さい数値、この位置が指定された位置の後にある場合は0より大きい数値、これと指定された位置が等しい場合はゼロです。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Position.isAfter"></a><span class="ts" id=88 data-target="#details-88" data-toggle="collapse"><span class="ident">isAfter</span><span>(</span><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-88">
<div class="comment"><p>この位置の後ろに <code>other</code> があるか確認します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="other"></a><span class="ts" id=89 data-target="#details-89" data-toggle="collapse"><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>positionが大きい行にある場合、または大きい文字の同じ行にある場合は `true &#39;</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Position.isAfterOrEqual"></a><span class="ts" id=91 data-target="#details-91" data-toggle="collapse"><span class="ident">isAfterOrEqual</span><span>(</span><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-91">
<div class="comment"><p><code>other</code> がこの位置に等しいかそれ以下であることを確認します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="other"></a><span class="ts" id=92 data-target="#details-92" data-toggle="collapse"><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>その他の位置。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>positionがより大きい行にあるか、より大きいか等しい文字の同じ行にある場合はtrueを返します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Position.isBefore"></a><span class="ts" id=82 data-target="#details-82" data-toggle="collapse"><span class="ident">isBefore</span><span>(</span><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-82">
<div class="comment"><p>この位置の前に <code>other</code> があるか確認してください。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="other"></a><span class="ts" id=83 data-target="#details-83" data-toggle="collapse"><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>positionが小さい行にある場合、または小さい文字の同じ行にある場合は <code>true</code></p>
</div></td></tr>
</table>
</div>
</div>



<a name="Position.isBeforeOrEqual"></a><span class="ts" id=85 data-target="#details-85" data-toggle="collapse"><span class="ident">isBeforeOrEqual</span><span>(</span><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-85">
<div class="comment"><p><code>other</code> がこの position の前かどうかを確認します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="other"></a><span class="ts" id=86 data-target="#details-86" data-toggle="collapse"><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>その他の位置。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>position が小さい行にある場合、または小さい文字または同じ文字の同じ行にある場合はtrueを返します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Position.isEqual"></a><span class="ts" id=94 data-target="#details-94" data-toggle="collapse"><span class="ident">isEqual</span><span>(</span><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-94">
<div class="comment"><p><code>other</code> がこの位置に等しいかどうか確認します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="other"></a><span class="ts" id=95 data-target="#details-95" data-toggle="collapse"><span class="ident">other</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>その他の位置。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>指定された位置の行と文字がこの位置の行と文字と等しい場合は <code>true</code></p>
</div></td></tr>
</table>
</div>
</div>



<a name="Position.translate"></a><span class="ts" id=100 data-target="#details-100" data-toggle="collapse"><span class="ident">translate</span><span>(</span><span class="ident">lineDelta</span><span>?</span><span>: </span><a class="type-instrinct">number</a>, <span class="ident">characterDelta</span><span>?</span><span>: </span><a class="type-instrinct">number</a><span>)</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-100">
<div class="comment"><p>この位置に関連して新しい位置を作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="lineDelta"></a><span class="ts" id=101 data-target="#details-101" data-toggle="collapse"><span class="ident">lineDelta</span><span>?</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>ライン値のデルタ値。
デフォルトは <code>0</code> です。</p>
</div></td></tr>
<tr><td><a name="characterDelta"></a><span class="ts" id=102 data-target="#details-102" data-toggle="collapse"><span class="ident">characterDelta</span><span>?</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>文字値のデルタ値。
デフォルトは <code>0</code> です。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>現在の行と文字、および対応するデルタの合計である行と文字の位置。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Position.translate"></a><span class="ts" id=103 data-target="#details-103" data-toggle="collapse"><span class="ident">translate</span><span>(</span><span class="ident">change</span><span>: </span>{characterDelta: <a class="type-instrinct">number</a>, lineDelta: <a class="type-instrinct">number</a>}<span>)</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-103">
<div class="comment"><p>このポジションに関連して新しいポジションを導出します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="change"></a><span class="ts" id=104 data-target="#details-104" data-toggle="collapse"><span class="ident">change</span><span>: </span>{characterDelta: <a class="type-instrinct">number</a>, lineDelta: <a class="type-instrinct">number</a>}</span></td><td><div class="comment"><p>この位置へのデルタを記述するオブジェクト。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>指定されたデルタを反映する位置。
変更が何も変更していない場合、 <code>this</code> の位置が返ります。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Position.with"></a><span class="ts" id=109 data-target="#details-109" data-toggle="collapse"><span class="ident">with</span><span>(</span><span class="ident">line</span><span>?</span><span>: </span><a class="type-instrinct">number</a>, <span class="ident">character</span><span>?</span><span>: </span><a class="type-instrinct">number</a><span>)</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-109">
<div class="comment"><p>このポジションから派生した新しいポジションを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="line"></a><span class="ts" id=110 data-target="#details-110" data-toggle="collapse"><span class="ident">line</span><span>?</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="character"></a><span class="ts" id=111 data-target="#details-111" data-toggle="collapse"><span class="ident">character</span><span>?</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>行と文字が指定された値で置き換えられた位置。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Position.with"></a><span class="ts" id=112 data-target="#details-112" data-toggle="collapse"><span class="ident">with</span><span>(</span><span class="ident">change</span><span>: </span>{character: <a class="type-instrinct">number</a>, line: <a class="type-instrinct">number</a>}<span>)</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-112">
<div class="comment"><p>このポジションから新しいポジションを導き出します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="change"></a><span class="ts" id=113 data-target="#details-113" data-toggle="collapse"><span class="ident">change</span><span>: </span>{character: <a class="type-instrinct">number</a>, line: <a class="type-instrinct">number</a>}</span></td><td><div class="comment"><p>この位置への変更を記述するオブジェクトです。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>指定された変更を反映する位置。
変更が何も変更していない場合、 <code>this</code> の位置が返ります。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="Progress"></a><span class="code-item" id=1010>Progress&lt;T&gt;</span>



<div class="comment"><p>進行状況の更新を報告する一般的な方法を定義します。</p>
</div>

#### Methods



<a name="Progress.report"></a><span class="ts" id=1013 data-target="#details-1013" data-toggle="collapse"><span class="ident">report</span><span>(</span><span class="ident">value</span><span>: </span><a class="type-instrinct">T</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1013">
<div class="comment"><p>進行状況の更新を報告します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="value"></a><span class="ts" id=1014 data-target="#details-1014" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">T</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="ProgressLocation"></a><span class="code-item" id=1093>ProgressLocation</span>



<div class="comment"><p>進捗情報を表示できるエディタ内の場所。
進行状況を視覚的にどのように表現するかは、場所によって異なります。</p>
</div>

#### Enumeration members



<a name="ProgressLocation.SourceControl"></a><span class="ts" id=1094 data-target="#details-1094" data-toggle="collapse"><span class="ident">SourceControl</span></span>
<div class="details collapse" id="details-1094">
<em>1</em>
</div>



<a name="ProgressLocation.Window"></a><span class="ts" id=1095 data-target="#details-1095" data-toggle="collapse"><span class="ident">Window</span></span>
<div class="details collapse" id="details-1095">
<em>10</em>
</div>

### <a name="ProgressOptions"></a><span class="code-item" id=1096>ProgressOptions</span>



<div class="comment"><p>値のオブジェクトは、進捗状況とその進捗状況を記述する。</p>
</div>

#### Properties



<a name="ProgressOptions.location"></a><span class="ts" id=1097 data-target="#details-1097" data-toggle="collapse"><span class="ident">location</span><span>: </span><a class="type-ref" href="#ProgressLocation">ProgressLocation</a></span>
<div class="details collapse" id="details-1097">
<div class="comment"><p>進捗状況が表示される場所。</p>
</div>
</div>



<a name="ProgressOptions.title"></a><span class="ts" id=1098 data-target="#details-1098" data-toggle="collapse"><span class="ident">title</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1098">
<div class="comment"><p>操作を説明するために人間が読める文字列。</p>
</div>
</div>

### <a name="ProviderResult"></a><span class="code-item" id=1160>ProviderResult</span>



<div class="comment"><p>プロバイダ結果は、<a href="#HoverProvider">HoverProvider</a>のようなプロバイダが返す値を表します。
一度これは <code>Hover</code> のような実際の結果の型 <code>T</code> 、または <code>T</code> 型に解決されるthenableです。
さらに、 <code>null</code> と <code>undefined</code> を返すことができます - 直接またはthenableから返すことができます。</p>
<p>以下のスニペットはすべて<a href="#HoverProvider">HoverProvider</a>の有効な実装です：</p>

<pre><code class="lang-ts"><span class="hljs-keyword">let</span> a：HoverProvider = {
provideHover(doc、pos、token)：ProviderResult &lt;Hover&gt; {
新しいホバー( <span class="hljs-string">'Hello World'</span>)を返します。
}
}

<span class="hljs-keyword">let</span> b：HoverProvider = {
provideHover(doc、pos、token)：ProviderResult &lt;Hover&gt; {
新しい約束を返す(解決=&gt; {
resolve(新しいホバー( <span class="hljs-string">'Hello World'</span>));
});
}
}
* <span class="hljs-keyword">let</span> c：HoverProvider = {
provideHover(doc、pos、token)：ProviderResult &lt;Hover&gt; {
リターン; <span class="hljs-comment">//未定義</span>
}
}
</code></pre>
</div>



<a name="ProviderResult"></a><span class="ts" id=1160 data-target="#details-1160" data-toggle="collapse"><span class="ident">ProviderResult</span><span>: </span><a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a> &#124; <a class="type-instrinct">null</a> &#124; <a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a> &#124; <a class="type-instrinct">null</a>&gt;</span>

### <a name="QuickDiffProvider"></a><span class="code-item" id=1120>QuickDiffProvider</span>



<div class="comment"></div>

#### Methods



<a name="QuickDiffProvider.provideOriginalResource"></a><span class="ts" id=1122 data-target="#details-1122" data-toggle="collapse"><span class="ident">provideOriginalResource</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-1122">
<div class="comment"><p>任意のリソースURIの元のリソースに<a href="#Uri">uri</a>を提供します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=1123 data-target="#details-1123" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=1124 data-target="#details-1124" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>一致する元のリソースのuriに解決されるthenable。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="QuickPickItem"></a><span class="code-item" id=463>QuickPickItem</span>



<div class="comment"><p>項目のリストから選択できる項目を表します。</p>
</div>

#### Properties



<a name="QuickPickItem.description"></a><span class="ts" id=465 data-target="#details-465" data-toggle="collapse"><span class="ident">description</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-465">
<div class="comment"><p>あまり目立たない人間が読める文字列。</p>
</div>
</div>



<a name="QuickPickItem.detail"></a><span class="ts" id=466 data-target="#details-466" data-toggle="collapse"><span class="ident">detail</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-466">
<div class="comment"><p>あまり目立たない人間が読める文字列。</p>
</div>
</div>



<a name="QuickPickItem.label"></a><span class="ts" id=464 data-target="#details-464" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-464">
<div class="comment"><p>人間が読める文字列で、目立つように表示されます。</p>
</div>
</div>

### <a name="QuickPickOptions"></a><span class="code-item" id=467>QuickPickOptions</span>



<div class="comment"><p>クイックピックUIの動作を設定するオプション。</p>
</div>

#### Events



<a name="QuickPickOptions.onDidSelectItem"></a><span class="ts" id=473 data-target="#details-473" data-toggle="collapse"><span class="ident">onDidSelectItem</span><span>&lt;</span>T extends <a class="type-ref" href="#QuickPickItem">QuickPickItem</a><span>&gt;</span><span>(</span><span class="ident">item</span><span>: </span><a class="type-instrinct">T</a> &#124; <a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">any</a></span>
<div class="details collapse" id="details-473">
<div class="comment"><p>アイテムが選択されたときに呼び出されるオプションの関数。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="item"></a><span class="ts" id=475 data-target="#details-475" data-toggle="collapse"><span class="ident">item</span><span>: </span><a class="type-instrinct">T</a> &#124; <a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="QuickPickOptions.ignoreFocusOut"></a><span class="ts" id=471 data-target="#details-471" data-toggle="collapse"><span class="ident">ignoreFocusOut</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-471">
<div class="comment"><p>フォーカスがエディタの別の部分または別のウィンドウに移動したときにピッカーを開いたままにするには、「true」に設定します。</p>
</div>
</div>



<a name="QuickPickOptions.matchOnDescription"></a><span class="ts" id=468 data-target="#details-468" data-toggle="collapse"><span class="ident">matchOnDescription</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-468">
<div class="comment"><p>ピックをフィルタリングするときに説明を含めるオプションのフラグ。</p>
</div>
</div>



<a name="QuickPickOptions.matchOnDetail"></a><span class="ts" id=469 data-target="#details-469" data-toggle="collapse"><span class="ident">matchOnDetail</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-469">
<div class="comment"><p>ピックをフィルタリングするときに詳細を含めるオプションのフラグ。</p>
</div>
</div>



<a name="QuickPickOptions.placeHolder"></a><span class="ts" id=470 data-target="#details-470" data-toggle="collapse"><span class="ident">placeHolder</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-470">
<div class="comment"><p>入力ボックスにプレースホルダーとして表示してユーザーに何を選択させるかを案内するオプションのストリング。</p>
</div>
</div>

### <a name="Range"></a><span class="code-item" id=117>Range</span>



<div class="comment"><p>範囲は、2つの位置の順序付けられたペアを表します。
<a href="#Range.start">開始</a>.isBeforeOrEqual(<a href="#Range.end">終了</a>)が保証されます。</p>
<p>Rangeオブジェクトは<strong>immutable</strong>です。</p>
<p><a href="#Range.with">with</a>、
<a href="#Range.intersection">intersection</a>、または<a href="#Range.union">union</a>メソッドを使用して、既存の範囲から新しい範囲を派生させます。</p>
</div>

#### Constructors



<a name="Range.new Range"></a><span class="ts" id=121 data-target="#details-121" data-toggle="collapse"><span class="ident">new Range</span><span>(</span><span class="ident">start</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">end</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-121">
<div class="comment"><p>2つの位置から新しい範囲を作成します。</p>
<p><code>start</code> が <code>end</code> の前にないか等しい場合、値は入れ替えられます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="start"></a><span class="ts" id=122 data-target="#details-122" data-toggle="collapse"><span class="ident">start</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>位置。</p>
</div></td></tr>
<tr><td><a name="end"></a><span class="ts" id=123 data-target="#details-123" data-toggle="collapse"><span class="ident">end</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>位置。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="Range.new Range"></a><span class="ts" id=124 data-target="#details-124" data-toggle="collapse"><span class="ident">new Range</span><span>(</span><span class="ident">startLine</span><span>: </span><a class="type-instrinct">number</a>, <span class="ident">startCharacter</span><span>: </span><a class="type-instrinct">number</a>, <span class="ident">endLine</span><span>: </span><a class="type-instrinct">number</a>, <span class="ident">endCharacter</span><span>: </span><a class="type-instrinct">number</a><span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-124">
<div class="comment"><p>数値座標から新しい範囲を作成します。
新しい範囲 <code>new Range(new Position(startLine, startCharacter), new Position(endLine, endCharacter))</code> を使用することと同等です。</p>
<p><code>start</code> が <code>end</code> の前にないか等しい場合、値は入れ替えられます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="startLine"></a><span class="ts" id=125 data-target="#details-125" data-toggle="collapse"><span class="ident">startLine</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>0から始まる行の値。</p>
</div></td></tr>
<tr><td><a name="startCharacter"></a><span class="ts" id=126 data-target="#details-126" data-toggle="collapse"><span class="ident">startCharacter</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>ゼロから始まる文字値。</p>
</div></td></tr>
<tr><td><a name="endLine"></a><span class="ts" id=127 data-target="#details-127" data-toggle="collapse"><span class="ident">endLine</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>0から始まる行の値。</p>
</div></td></tr>
<tr><td><a name="endCharacter"></a><span class="ts" id=128 data-target="#details-128" data-toggle="collapse"><span class="ident">endCharacter</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>0から始まる文字値。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="Range.end"></a><span class="ts" id=119 data-target="#details-119" data-toggle="collapse"><span class="ident">end</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-119">
<div class="comment"><p>終了位置。</p>
<p><a href="#Range.start">start</a> と同じか後ろです。</p>
</div>
</div>



<a name="Range.isEmpty"></a><span class="ts" id=129 data-target="#details-129" data-toggle="collapse"><span class="ident">isEmpty</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-129">
<div class="comment"><p><code>start</code> と <code>end</code> が等しい場合は <code>true</code> を返します。</p>
</div>
</div>



<a name="Range.isSingleLine"></a><span class="ts" id=130 data-target="#details-130" data-toggle="collapse"><span class="ident">isSingleLine</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-130">
<div class="comment"><p><code>start.line</code> と <code>end.line</code> が等しい場合は <code>true</code> を返します。</p>
</div>
</div>



<a name="Range.start"></a><span class="ts" id=118 data-target="#details-118" data-toggle="collapse"><span class="ident">start</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-118">
<div class="comment"><p>開始位置。
これは <a href="#Range.end">end</a> と同じか手前です。</p>
</div>
</div>

#### Methods



<a name="Range.contains"></a><span class="ts" id=132 data-target="#details-132" data-toggle="collapse"><span class="ident">contains</span><span>(</span><span class="ident">positionOrRange</span><span>: </span><a class="type-ref" href="#Position">Position</a> &#124; <a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-132">
<div class="comment"><p>この範囲に位置または範囲が含まれているかどうかを確認します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="positionOrRange"></a><span class="ts" id=133 data-target="#details-133" data-toggle="collapse"><span class="ident">positionOrRange</span><span>: </span><a class="type-ref" href="#Position">Position</a> &#124; <a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>位置または範囲です。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>位置または範囲がこの範囲の中またはそれに等しい場合は <code>true</code></p>
</div></td></tr>
</table>
</div>
</div>



<a name="Range.intersection"></a><span class="ts" id=138 data-target="#details-138" data-toggle="collapse"><span class="ident">intersection</span><span>(</span><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a> &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-138">
<div class="comment"><p>この範囲で <code>range</code> を交差させ、新しい範囲または 範囲に重複がない場合 <code>undefined</code> を返します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=139 data-target="#details-139" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>範囲です。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a> &#124; <a class="type-instrinct">undefined</a></span></td><td><div class="comment"><p>より大きい開始位置と終了位置の範囲。
オーバーラップがない場合は未定義に戻ります。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Range.isEqual"></a><span class="ts" id=135 data-target="#details-135" data-toggle="collapse"><span class="ident">isEqual</span><span>(</span><span class="ident">other</span><span>: </span><a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-135">
<div class="comment"><p><code>other</code> がこの範囲に等しいかどうか確認します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="other"></a><span class="ts" id=136 data-target="#details-136" data-toggle="collapse"><span class="ident">other</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>その他の範囲。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>この範囲の開始と終了を開始と終了が <a href="#Position.isEqual">等しい</a> 場合は <code>true</code> を返します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Range.union"></a><span class="ts" id=141 data-target="#details-141" data-toggle="collapse"><span class="ident">union</span><span>(</span><span class="ident">other</span><span>: </span><a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-141">
<div class="comment"><p>この範囲で <code>other</code> の和集合を計算します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="other"></a><span class="ts" id=142 data-target="#details-142" data-toggle="collapse"><span class="ident">other</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>その他の範囲。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>小さい開始位置と大きい終了位置の範囲。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Range.with"></a><span class="ts" id=144 data-target="#details-144" data-toggle="collapse"><span class="ident">with</span><span>(</span><span class="ident">start</span><span>?</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">end</span><span>?</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-144">
<div class="comment"><p>この範囲から新しい範囲を導き出します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="start"></a><span class="ts" id=145 data-target="#details-145" data-toggle="collapse"><span class="ident">start</span><span>?</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>startとして使用する位置。
デフォルト値は<a href="#Range.start">現在の開始位置</a>です。</p>
</div></td></tr>
<tr><td><a name="end"></a><span class="ts" id=146 data-target="#details-146" data-toggle="collapse"><span class="ident">end</span><span>?</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>指定された開始位置と終了位置でこの範囲から派生した範囲。
開始と終了が異なる場合、この範囲が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Range.with"></a><span class="ts" id=147 data-target="#details-147" data-toggle="collapse"><span class="ident">with</span><span>(</span><span class="ident">change</span><span>: </span>{end: <a class="type-ref" href="#Position">Position</a>, start: <a class="type-ref" href="#Position">Position</a>}<span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-147">
<div class="comment"><p>この範囲から新しい範囲を導き出します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="change"></a><span class="ts" id=148 data-target="#details-148" data-toggle="collapse"><span class="ident">change</span><span>: </span>{end: <a class="type-ref" href="#Position">Position</a>, start: <a class="type-ref" href="#Position">Position</a>}</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>指定された変更を反映する範囲。
変更が何も変更していない場合、 <code>this</code> の範囲を返します。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="ReferenceContext"></a><span class="code-item" id=628>ReferenceContext</span>



<div class="comment"><p>Valueオブジェクト。
参照を要求するときに追加情報が含まれます。</p>
</div>

#### Properties



<a name="ReferenceContext.includeDeclaration"></a><span class="ts" id=629 data-target="#details-629" data-toggle="collapse"><span class="ident">includeDeclaration</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-629">
<div class="comment"><p>現在のシンボルの宣言を含めます。</p>
</div>
</div>

### <a name="ReferenceProvider"></a><span class="code-item" id=630>ReferenceProvider</span>



<div class="comment"><p>参照プロバイダーインターフェイスは、拡張機能と<a href="https://code.visualstudio.com/docs/editor/editingevolved#_peek">参照の参照</a> - 機能の間の契約を定義します。</p>
</div>

#### Methods



<a name="ReferenceProvider.provideReferences"></a><span class="ts" id=632 data-target="#details-632" data-toggle="collapse"><span class="ident">provideReferences</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">context</span><span>: </span><a class="type-ref" href="#ReferenceContext">ReferenceContext</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-632">
<div class="comment"><p>与えられた位置と文書のプロジェクト全体の参照のセットを提供する。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=633 data-target="#details-633" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="position"></a><span class="ts" id=634 data-target="#details-634" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="context"></a><span class="ts" id=635 data-target="#details-635" data-toggle="collapse"><span class="ident">context</span><span>: </span><a class="type-ref" href="#ReferenceContext">ReferenceContext</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=636 data-target="#details-636" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>そのように解決される場所またはthenableの配列。
結果の欠如は、 <code>undefined</code> 、 <code>null</code> 、または空の配列を返すことによって通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="RenameProvider"></a><span class="code-item" id=712>RenameProvider</span>



<div class="comment"><p>リネームプロバイダインタフェースは、拡張機能と<a href="https://code.visualstudio.com/docs/editor/editingevolved#_rename-symbol">名前変更</a>機能の間の契約を定義します。</p>
</div>

#### Methods



<a name="RenameProvider.provideRenameEdits"></a><span class="ts" id=714 data-target="#details-714" data-toggle="collapse"><span class="ident">provideRenameEdits</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">newName</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-714">
<div class="comment"><p>1つに加えなければならない変更を記述する編集を提供する
シンボルの名前を別の名前に変更するためのリソース</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=715 data-target="#details-715" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="position"></a><span class="ts" id=716 data-target="#details-716" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="newName"></a><span class="ts" id=717 data-target="#details-717" data-toggle="collapse"><span class="ident">newName</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=718 data-target="#details-718" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>ワークスペースの編集またはそのように解決されるthenable。
結果の不足は、 <code>undefined</code> または <code>null</code> を返すことで通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="Selection"></a><span class="code-item" id=152>Selection</span>



<div class="comment"><p>エディター内のテキスト選択を表します。</p>
</div>

#### Constructors



<a name="Selection.new Selection"></a><span class="ts" id=156 data-target="#details-156" data-toggle="collapse"><span class="ident">new Selection</span><span>(</span><span class="ident">anchor</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">active</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-ref" href="#Selection">Selection</a></span>
<div class="details collapse" id="details-156">
<div class="comment"><p>2つのポーションから選択を作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="anchor"></a><span class="ts" id=157 data-target="#details-157" data-toggle="collapse"><span class="ident">anchor</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="active"></a><span class="ts" id=158 data-target="#details-158" data-toggle="collapse"><span class="ident">active</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Selection">Selection</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="Selection.new Selection"></a><span class="ts" id=159 data-target="#details-159" data-toggle="collapse"><span class="ident">new Selection</span><span>(</span><span class="ident">anchorLine</span><span>: </span><a class="type-instrinct">number</a>, <span class="ident">anchorCharacter</span><span>: </span><a class="type-instrinct">number</a>, <span class="ident">activeLine</span><span>: </span><a class="type-instrinct">number</a>, <span class="ident">activeCharacter</span><span>: </span><a class="type-instrinct">number</a><span>)</span><span>: </span><a class="type-ref" href="#Selection">Selection</a></span>
<div class="details collapse" id="details-159">
<div class="comment"><p>4つの座標から選択を作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="anchorLine"></a><span class="ts" id=160 data-target="#details-160" data-toggle="collapse"><span class="ident">anchorLine</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>0から始まる行の値。</p>
</div></td></tr>
<tr><td><a name="anchorCharacter"></a><span class="ts" id=161 data-target="#details-161" data-toggle="collapse"><span class="ident">anchorCharacter</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>0から始まる文字値。</p>
</div></td></tr>
<tr><td><a name="activeLine"></a><span class="ts" id=162 data-target="#details-162" data-toggle="collapse"><span class="ident">activeLine</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>0から始まる行の値。</p>
</div></td></tr>
<tr><td><a name="activeCharacter"></a><span class="ts" id=163 data-target="#details-163" data-toggle="collapse"><span class="ident">activeCharacter</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>0から始まる文字値。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Selection">Selection</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="Selection.active"></a><span class="ts" id=154 data-target="#details-154" data-toggle="collapse"><span class="ident">active</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-154">
<div class="comment"><p>カーソルの位置。
この位置は <a href="#Selection.anchor">anchor</a> の前後にある可能性があります。</p>
</div>
</div>



<a name="Selection.anchor"></a><span class="ts" id=153 data-target="#details-153" data-toggle="collapse"><span class="ident">anchor</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-153">
<div class="comment"><p>選択が始まる位置。
この位置は、 <a href="#Selection.active">アクティブ</a> の前後にある可能性があります。</p>
</div>
</div>



<a name="Selection.end"></a><span class="ts" id=166 data-target="#details-166" data-toggle="collapse"><span class="ident">end</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-166">
<div class="comment"><p>終了位置。</p>
<p><a href="#Range.start">start</a> と同じか後ろです。</p>
</div>
</div>



<a name="Selection.isEmpty"></a><span class="ts" id=167 data-target="#details-167" data-toggle="collapse"><span class="ident">isEmpty</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-167">
<div class="comment"><p><code>start</code> と <code>end</code> が等しい場合は <code>true</code> を返します。</p>
</div>
</div>



<a name="Selection.isReversed"></a><span class="ts" id=164 data-target="#details-164" data-toggle="collapse"><span class="ident">isReversed</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-164">
<div class="comment"><p><a href="#Selection.active">アクティブ</a>.isBefore(<a href="#Selection.anchor">anchor</a>)を選択すると、選択範囲が逆になります。</p>
</div>
</div>



<a name="Selection.isSingleLine"></a><span class="ts" id=168 data-target="#details-168" data-toggle="collapse"><span class="ident">isSingleLine</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-168">
<div class="comment"><p><code>start.line</code> と <code>end.line</code> が等しい場合は <code>true</code> を返します。</p>
</div>
</div>



<a name="Selection.start"></a><span class="ts" id=165 data-target="#details-165" data-toggle="collapse"><span class="ident">start</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-165">
<div class="comment"><p>開始位置。
これは <a href="#Range.end">end</a> と同じか手前です。</p>
</div>
</div>

#### Methods



<a name="Selection.contains"></a><span class="ts" id=170 data-target="#details-170" data-toggle="collapse"><span class="ident">contains</span><span>(</span><span class="ident">positionOrRange</span><span>: </span><a class="type-ref" href="#Position">Position</a> &#124; <a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-170">
<div class="comment"><p>この範囲に位置または範囲が含まれているかどうかを確認します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="positionOrRange"></a><span class="ts" id=171 data-target="#details-171" data-toggle="collapse"><span class="ident">positionOrRange</span><span>: </span><a class="type-ref" href="#Position">Position</a> &#124; <a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>位置または範囲です。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>位置または範囲がこの範囲の中またはそれに等しい場合は <code>true</code></p>
</div></td></tr>
</table>
</div>
</div>



<a name="Selection.intersection"></a><span class="ts" id=176 data-target="#details-176" data-toggle="collapse"><span class="ident">intersection</span><span>(</span><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a> &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-176">
<div class="comment"><p>この範囲で <code>range</code> を交差させ、新しい範囲または 範囲に重複がない場合 <code>undefined</code> を返します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=177 data-target="#details-177" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>範囲です。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a> &#124; <a class="type-instrinct">undefined</a></span></td><td><div class="comment"><p>より大きい開始位置と終了位置の範囲。
オーバーラップがない場合は未定義に戻ります。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Selection.isEqual"></a><span class="ts" id=173 data-target="#details-173" data-toggle="collapse"><span class="ident">isEqual</span><span>(</span><span class="ident">other</span><span>: </span><a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-173">
<div class="comment"><p><code>other</code> がこの範囲に等しいかどうか確認します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="other"></a><span class="ts" id=174 data-target="#details-174" data-toggle="collapse"><span class="ident">other</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>その他の範囲。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>この範囲の開始と終了を開始と終了が <a href="#Position.isEqual">等しい</a> 場合は <code>true</code> を返します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Selection.union"></a><span class="ts" id=179 data-target="#details-179" data-toggle="collapse"><span class="ident">union</span><span>(</span><span class="ident">other</span><span>: </span><a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-179">
<div class="comment"><p>この範囲で <code>other</code> の和集合を計算します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="other"></a><span class="ts" id=180 data-target="#details-180" data-toggle="collapse"><span class="ident">other</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>その他の範囲。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>小さい開始位置と大きい終了位置の範囲。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Selection.with"></a><span class="ts" id=182 data-target="#details-182" data-toggle="collapse"><span class="ident">with</span><span>(</span><span class="ident">start</span><span>?</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">end</span><span>?</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-182">
<div class="comment"><p>この範囲から新しい範囲を導き出します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="start"></a><span class="ts" id=183 data-target="#details-183" data-toggle="collapse"><span class="ident">start</span><span>?</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>startとして使用する位置。
デフォルト値は<a href="#Range.start">現在の開始位置</a>です。</p>
</div></td></tr>
<tr><td><a name="end"></a><span class="ts" id=184 data-target="#details-184" data-toggle="collapse"><span class="ident">end</span><span>?</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>指定された開始位置と終了位置でこの範囲から派生した範囲。
開始と終了が異なる場合、この範囲が返されます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Selection.with"></a><span class="ts" id=185 data-target="#details-185" data-toggle="collapse"><span class="ident">with</span><span>(</span><span class="ident">change</span><span>: </span>{end: <a class="type-ref" href="#Position">Position</a>, start: <a class="type-ref" href="#Position">Position</a>}<span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-185">
<div class="comment"><p>この範囲から新しい範囲を導き出します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="change"></a><span class="ts" id=186 data-target="#details-186" data-toggle="collapse"><span class="ident">change</span><span>: </span>{end: <a class="type-ref" href="#Position">Position</a>, start: <a class="type-ref" href="#Position">Position</a>}</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>指定された変更を反映する範囲。
変更が何も変更していない場合、 <code>this</code> の範囲を返します。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="SignatureHelp"></a><span class="code-item" id=760>SignatureHelp</span>



<div class="comment"><p>署名ヘルプは、呼び出し可能なものの署名を表します。
複数の署名がありますが、有効なパラメータは1つだけです。
アクティブなパラメータは1つのみです。</p>
</div>

#### Properties



<a name="SignatureHelp.activeParameter"></a><span class="ts" id=763 data-target="#details-763" data-toggle="collapse"><span class="ident">activeParameter</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-763">
<div class="comment"><p>アクティブな署名のアクティブなパラメータ。</p>
</div>
</div>



<a name="SignatureHelp.activeSignature"></a><span class="ts" id=762 data-target="#details-762" data-toggle="collapse"><span class="ident">activeSignature</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-762">
<div class="comment"><p>アクティブな署名。</p>
</div>
</div>



<a name="SignatureHelp.signatures"></a><span class="ts" id=761 data-target="#details-761" data-toggle="collapse"><span class="ident">signatures</span><span>: </span><a class="type-ref" href="#SignatureInformation">SignatureInformation</a>[]</span>
<div class="details collapse" id="details-761">
<div class="comment"><p>1つ以上の署名。</p>
</div>
</div>

### <a name="SignatureHelpProvider"></a><span class="code-item" id=764>SignatureHelpProvider</span>



<div class="comment"><p>シグネチャヘルププロバイダインターフェイスは、拡張機能と<a href="https://code.visualstudio.com/docs/editor/intellisense">パラメータヒント</a>の間のコントラクトを定義します。</p>
</div>

#### Methods



<a name="SignatureHelpProvider.provideSignatureHelp"></a><span class="ts" id=766 data-target="#details-766" data-toggle="collapse"><span class="ident">provideSignatureHelp</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-766">
<div class="comment"><p>指定された位置と文書で署名の助けを提供する。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=767 data-target="#details-767" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="position"></a><span class="ts" id=768 data-target="#details-768" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=769 data-target="#details-769" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>署名のヘルプまたはそれに解決されるネーブル。
結果の不足は、 <code>undefined</code> または <code>null</code> を返すことで通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="SignatureInformation"></a><span class="code-item" id=752>SignatureInformation</span>



<div class="comment"><p>呼び出し可能なものの署名を表します。
署名には、関数名、doc-comment、および一連のパラメータのようなラベルを付けることができます。</p>
</div>

#### Constructors



<a name="SignatureInformation.new SignatureInformation"></a><span class="ts" id=757 data-target="#details-757" data-toggle="collapse"><span class="ident">new SignatureInformation</span><span>(</span><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">documentation</span><span>?</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#SignatureInformation">SignatureInformation</a></span>
<div class="details collapse" id="details-757">
<div class="comment"><p>新しい署名情報オブジェクトを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="label"></a><span class="ts" id=758 data-target="#details-758" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="documentation"></a><span class="ts" id=759 data-target="#details-759" data-toggle="collapse"><span class="ident">documentation</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#SignatureInformation">SignatureInformation</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="SignatureInformation.documentation"></a><span class="ts" id=754 data-target="#details-754" data-toggle="collapse"><span class="ident">documentation</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-754">
<div class="comment"><p>この署名の人間が読めるdocコメント。
UIに表示されますが、省略することができます。</p>
</div>
</div>



<a name="SignatureInformation.label"></a><span class="ts" id=753 data-target="#details-753" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-753">
<div class="comment"><p>この署名のラベル。
UIに表示されます。</p>
</div>
</div>



<a name="SignatureInformation.parameters"></a><span class="ts" id=755 data-target="#details-755" data-toggle="collapse"><span class="ident">parameters</span><span>: </span><a class="type-ref" href="#ParameterInformation">ParameterInformation</a>[]</span>
<div class="details collapse" id="details-755">
<div class="comment"><p>この署名のパラメータ。</p>
</div>
</div>

### <a name="SnippetString"></a><span class="code-item" id=687>SnippetString</span>



<div class="comment"><p>スニペット文字列は、挿入時にテキストを挿入し、エディタカーソルを制御するためのテンプレートです。</p>
<p>スニペットは <code>$ 1</code> 、 <code>$ 2</code> でタブストップとプレースホルダを定義できます と <code>$ {3：foo}</code> になります。
<code>$ 0</code> は最後のタブストップを定義します。
デフォルトはスニペットの終わりです。
変数は <code>$ name</code> で定義されています。</p>
<p><code>$ {名前：デフォルト値}</code>。
スニペットの完全な構文が文書化されています
<a href="http://code.visualstudio.com/docs/editor/userdefinedsnippets#_creating-your-own-snippets">ここ</a></p>
</div>

#### Constructors



<a name="SnippetString.new SnippetString"></a><span class="ts" id=690 data-target="#details-690" data-toggle="collapse"><span class="ident">new SnippetString</span><span>(</span><span class="ident">value</span><span>?</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#SnippetString">SnippetString</a></span>
<div class="details collapse" id="details-690">
<div class="comment"></div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="value"></a><span class="ts" id=691 data-target="#details-691" data-toggle="collapse"><span class="ident">value</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#SnippetString">SnippetString</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="SnippetString.value"></a><span class="ts" id=688 data-target="#details-688" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-688">
<div class="comment"><p>スニペット文字列。</p>
</div>
</div>

#### Methods



<a name="SnippetString.appendPlaceholder"></a><span class="ts" id=699 data-target="#details-699" data-toggle="collapse"><span class="ident">appendPlaceholder</span><span>(</span><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a> &#124; (snippet: <a class="type-ref" href="#SnippetString">SnippetString</a>) =&gt; <a class="type-instrinct">any</a>, <span class="ident">number</span><span>?</span><span>: </span><a class="type-instrinct">number</a><span>)</span><span>: </span><a class="type-ref" href="#SnippetString">SnippetString</a></span>
<div class="details collapse" id="details-699">
<div class="comment"><p>このスニペット文字列の<a href="#SnippetString.value"><code>value</code></a>にプレースホルダ( <code>$ {1：value}</code> )を追加するBuilder関数。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="value"></a><span class="ts" id=700 data-target="#details-700" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a> &#124; (snippet: <a class="type-ref" href="#SnippetString">SnippetString</a>) =&gt; <a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="number"></a><span class="ts" id=704 data-target="#details-704" data-toggle="collapse"><span class="ident">number</span><span>?</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#SnippetString">SnippetString</a></span></td><td><div class="comment"><p>このスニペット文字列。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="SnippetString.appendTabstop"></a><span class="ts" id=696 data-target="#details-696" data-toggle="collapse"><span class="ident">appendTabstop</span><span>(</span><span class="ident">number</span><span>?</span><span>: </span><a class="type-instrinct">number</a><span>)</span><span>: </span><a class="type-ref" href="#SnippetString">SnippetString</a></span>
<div class="details collapse" id="details-696">
<div class="comment"><p>ビルダー - このスニペット文字列の<a href="#SnippetString.value"><code>value</code></a>にタブストップ( <code>$ 1</code> 、 <code>$ 2</code> など)を追加する関数。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="number"></a><span class="ts" id=697 data-target="#details-697" data-toggle="collapse"><span class="ident">number</span><span>?</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#SnippetString">SnippetString</a></span></td><td><div class="comment"><p>このスニペット文字列。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="SnippetString.appendText"></a><span class="ts" id=693 data-target="#details-693" data-toggle="collapse"><span class="ident">appendText</span><span>(</span><span class="ident">string</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#SnippetString">SnippetString</a></span>
<div class="details collapse" id="details-693">
<div class="comment"><p>ビルダ - このスニペット文字列の<a href="#SnippetString.value"><code>value</code></a>に指定された文字列を追加します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="string"></a><span class="ts" id=694 data-target="#details-694" data-toggle="collapse"><span class="ident">string</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"><p>&#39;given as&#39;を追加する値。文字列はエスケープされます。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#SnippetString">SnippetString</a></span></td><td><div class="comment"><p>このスニペット文字列。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="SnippetString.appendVariable"></a><span class="ts" id=706 data-target="#details-706" data-toggle="collapse"><span class="ident">appendVariable</span><span>(</span><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">defaultValue</span><span>: </span><a class="type-instrinct">string</a> &#124; (snippet: <a class="type-ref" href="#SnippetString">SnippetString</a>) =&gt; <a class="type-instrinct">any</a><span>)</span><span>: </span><a class="type-ref" href="#SnippetString">SnippetString</a></span>
<div class="details collapse" id="details-706">
<div class="comment"><p>ビルダ - このスニペット文字列の<a href="#SnippetString.value"><code>value</code></a>に変数( <code>$ {VAR}</code> )を追加する関数。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="name"></a><span class="ts" id=707 data-target="#details-707" data-toggle="collapse"><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="defaultValue"></a><span class="ts" id=708 data-target="#details-708" data-toggle="collapse"><span class="ident">defaultValue</span><span>: </span><a class="type-instrinct">string</a> &#124; (snippet: <a class="type-ref" href="#SnippetString">SnippetString</a>) =&gt; <a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#SnippetString">SnippetString</a></span></td><td><div class="comment"><p>このスニペット文字列。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="SourceControl"></a><span class="code-item" id=1144>SourceControl</span>



<div class="comment"><p>ソースコントロールは<a href="#SourceControlResourceState">リソース状態</a>を提供することができます。
をエディタに追加し、いくつかのソース管理関連の方法でエディタとやり取りします。</p>
</div>

#### Properties



<a name="SourceControl.acceptInputCommand"></a><span class="ts" id=1150 data-target="#details-1150" data-toggle="collapse"><span class="ident">acceptInputCommand</span><span>?</span><span>: </span><a class="type-ref" href="#Command">Command</a></span>
<div class="details collapse" id="details-1150">
<div class="comment"><p>オプションの入力コマンドを受け入れます。</p>
<p>このコマンドは、ユーザーがソースコントロール入力の値を受け入れると呼び出されます。</p>
</div>
</div>



<a name="SourceControl.commitTemplate"></a><span class="ts" id=1149 data-target="#details-1149" data-toggle="collapse"><span class="ident">commitTemplate</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1149">
<div class="comment"><p>オプションのコミットテンプレート文字列。</p>
<p>ソースコントロールのビューレットは、必要に応じてソースコントロール入力にこの値を入力します。</p>
</div>
</div>



<a name="SourceControl.count"></a><span class="ts" id=1147 data-target="#details-1147" data-toggle="collapse"><span class="ident">count</span><span>?</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-1147">
<div class="comment"><p>このソースコントロールのUI表示可能な<a href="#SourceControlResourceState">リソース状態</a>の数。</p>
<p><a href="#SourceControlResourceState">リソース状態</a>の合計数に等しい が定義されていない場合、このソースコントロールの*。</p>
</div>
</div>



<a name="SourceControl.id"></a><span class="ts" id=1145 data-target="#details-1145" data-toggle="collapse"><span class="ident">id</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1145">
<div class="comment"><p>このソースコントロールのID。</p>
</div>
</div>



<a name="SourceControl.label"></a><span class="ts" id=1146 data-target="#details-1146" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1146">
<div class="comment"><p>このソースコントロールの人間が読めるラベル。</p>
</div>
</div>



<a name="SourceControl.quickDiffProvider"></a><span class="ts" id=1148 data-target="#details-1148" data-toggle="collapse"><span class="ident">quickDiffProvider</span><span>?</span><span>: </span><a class="type-ref" href="#QuickDiffProvider">QuickDiffProvider</a></span>
<div class="details collapse" id="details-1148">
<div class="comment"><p>オプションの<a href="#QuickDiffProvider">Quick Diff Provider</a>。</p>
</div>
</div>



<a name="SourceControl.statusBarCommands"></a><span class="ts" id=1151 data-target="#details-1151" data-toggle="collapse"><span class="ident">statusBarCommands</span><span>?</span><span>: </span><a class="type-ref" href="#Command">Command</a>[]</span>
<div class="details collapse" id="details-1151">
<div class="comment"><p>オプションのステータスバーコマンド。</p>
<p>これらのコマンドはエディタのステータスバーに表示されます。</p>
</div>
</div>

#### Methods



<a name="SourceControl.createResourceGroup"></a><span class="ts" id=1153 data-target="#details-1153" data-toggle="collapse"><span class="ident">createResourceGroup</span><span>(</span><span class="ident">id</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">label</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#SourceControlResourceGroup">SourceControlResourceGroup</a></span>
<div class="details collapse" id="details-1153">
<div class="comment"><p>新しい<a href="#SourceControlResourceGroup">リソースグループ</a>を作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="id"></a><span class="ts" id=1154 data-target="#details-1154" data-toggle="collapse"><span class="ident">id</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="label"></a><span class="ts" id=1155 data-target="#details-1155" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#SourceControlResourceGroup">SourceControlResourceGroup</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="SourceControl.dispose"></a><span class="ts" id=1157 data-target="#details-1157" data-toggle="collapse"><span class="ident">dispose</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1157">
<div class="comment"><p>このソースコントロールを破棄します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="SourceControlInputBox"></a><span class="code-item" id=1118>SourceControlInputBox</span>



<div class="comment"><p>ソースコントロールビューレットの入力ボックスを表します。</p>
</div>

#### Properties



<a name="SourceControlInputBox.value"></a><span class="ts" id=1119 data-target="#details-1119" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1119">
<div class="comment"><p>入力ボックスの内容のセッターとゲッター。</p>
</div>
</div>

### <a name="SourceControlResourceDecorations"></a><span class="code-item" id=1127>SourceControlResourceDecorations</span>



<div class="comment"><p><a href="#SourceControlResourceState">ソースコントロールリソース状態</a>の装飾。
*明るいテーマと暗いテーマを個別に指定できます。</p>
</div>

#### Properties



<a name="SourceControlResourceDecorations.dark"></a><span class="ts" id=1131 data-target="#details-1131" data-toggle="collapse"><span class="ident">dark</span><span>?</span><span>: </span><a class="type-ref" href="#SourceControlResourceThemableDecorations">SourceControlResourceThemableDecorations</a></span>
<div class="details collapse" id="details-1131">
<div class="comment"><p>暗いテーマの装飾。</p>
</div>
</div>



<a name="SourceControlResourceDecorations.faded"></a><span class="ts" id=1129 data-target="#details-1129" data-toggle="collapse"><span class="ident">faded</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-1129">
<div class="comment"><p><a href="#SourceControlResourceState">Source control resource state</a>をUIでフェードするかどうか。</p>
</div>
</div>



<a name="SourceControlResourceDecorations.iconPath"></a><span class="ts" id=1132 data-target="#details-1132" data-toggle="collapse"><span class="ident">iconPath</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-1132">
<div class="comment"><p>特定のアイコンのパス
<a href="#SourceControlResourceState">ソース制御リソースの状態</a>。</p>
</div>
</div>



<a name="SourceControlResourceDecorations.light"></a><span class="ts" id=1130 data-target="#details-1130" data-toggle="collapse"><span class="ident">light</span><span>?</span><span>: </span><a class="type-ref" href="#SourceControlResourceThemableDecorations">SourceControlResourceThemableDecorations</a></span>
<div class="details collapse" id="details-1130">
<div class="comment"><p>明るいテーマの装飾。</p>
</div>
</div>



<a name="SourceControlResourceDecorations.strikeThrough"></a><span class="ts" id=1128 data-target="#details-1128" data-toggle="collapse"><span class="ident">strikeThrough</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-1128">
<div class="comment"><p><a href="#SourceControlResourceState">Source control resource state</a>をUIでストライクするかどうか。</p>
</div>
</div>

### <a name="SourceControlResourceGroup"></a><span class="code-item" id=1137>SourceControlResourceGroup</span>



<div class="comment"><p>ソース管理リソースグループは、
<a href="#SourceControlResourceState">ソース制御リソースの状態</a>。</p>
</div>

#### Properties



<a name="SourceControlResourceGroup.hideWhenEmpty"></a><span class="ts" id=1140 data-target="#details-1140" data-toggle="collapse"><span class="ident">hideWhenEmpty</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-1140">
<div class="comment"><p><a href="#SourceControlResourceState">ソース制御リソースの状態</a>が含まれていない場合、このソース管理リソースグループが非表示になっているかどうか。</p>
</div>
</div>



<a name="SourceControlResourceGroup.id"></a><span class="ts" id=1138 data-target="#details-1138" data-toggle="collapse"><span class="ident">id</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1138">
<div class="comment"><p>このソース管理リソースグループのID。</p>
</div>
</div>



<a name="SourceControlResourceGroup.label"></a><span class="ts" id=1139 data-target="#details-1139" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1139">
<div class="comment"><p>このソース管理リソースグループのラベル。</p>
</div>
</div>



<a name="SourceControlResourceGroup.resourceStates"></a><span class="ts" id=1141 data-target="#details-1141" data-toggle="collapse"><span class="ident">resourceStates</span><span>: </span><a class="type-ref" href="#SourceControlResourceState">SourceControlResourceState</a>[]</span>
<div class="details collapse" id="details-1141">
<div class="comment"><p>このグループのコレクション
<a href="#SourceControlResourceState">ソース制御リソースの状態</a>。</p>
</div>
</div>

#### Methods



<a name="SourceControlResourceGroup.dispose"></a><span class="ts" id=1143 data-target="#details-1143" data-toggle="collapse"><span class="ident">dispose</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1143">
<div class="comment"><p>このソース管理リソースグループを廃棄します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="SourceControlResourceState"></a><span class="code-item" id=1133>SourceControlResourceState</span>



<div class="comment"><p>ソース管理リソース状態は、特定の<a href="#SourceControlResourceGroup">ソース管理グループ</a>内の基礎となるワークスペースリソースの状態を表します。</p>
</div>

#### Properties



<a name="SourceControlResourceState.command"></a><span class="ts" id=1135 data-target="#details-1135" data-toggle="collapse"><span class="ident">command</span><span>?</span><span>: </span><a class="type-ref" href="#Command">Command</a></span>
<div class="details collapse" id="details-1135">
<div class="comment"><p>[ソース制御]ビューレットでリソース状態が開いているときに実行する<a href="#コマンド">コマンド</a>。</p>
</div>
</div>



<a name="SourceControlResourceState.decorations"></a><span class="ts" id=1136 data-target="#details-1136" data-toggle="collapse"><span class="ident">decorations</span><span>?</span><span>: </span><a class="type-ref" href="#SourceControlResourceDecorations">SourceControlResourceDecorations</a></span>
<div class="details collapse" id="details-1136">
<div class="comment"><p>このソース制御リソース状態の<a href="#SourceControlResourceDecorations">装飾</a>。</p>
</div>
</div>



<a name="SourceControlResourceState.resourceUri"></a><span class="ts" id=1134 data-target="#details-1134" data-toggle="collapse"><span class="ident">resourceUri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-1134">
<div class="comment"><p>ワークスペース内の基礎となるリソースの<a href="#Uri">uri</a>。</p>
</div>
</div>

### <a name="SourceControlResourceThemableDecorations"></a><span class="code-item" id=1125>SourceControlResourceThemableDecorations</span>



<div class="comment"><p>aのためのテーマを意識した装飾
<a href="#SourceControlResourceState">ソース制御リソースの状態</a>。</p>
</div>

#### Properties



<a name="SourceControlResourceThemableDecorations.iconPath"></a><span class="ts" id=1126 data-target="#details-1126" data-toggle="collapse"><span class="ident">iconPath</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-1126">
<div class="comment"><p>特定のアイコンのパス
<a href="#SourceControlResourceState">ソース制御リソースの状態</a>。</p>
</div>
</div>

### <a name="StatusBarAlignment"></a><span class="code-item" id=994>StatusBarAlignment</span>



<div class="comment"><p>ステータスバー項目の配置を表します。</p>
</div>

#### Enumeration members



<a name="StatusBarAlignment.Left"></a><span class="ts" id=995 data-target="#details-995" data-toggle="collapse"><span class="ident">Left</span></span>
<div class="details collapse" id="details-995">
<em>1</em>
</div>



<a name="StatusBarAlignment.Right"></a><span class="ts" id=996 data-target="#details-996" data-toggle="collapse"><span class="ident">Right</span></span>
<div class="details collapse" id="details-996">
<em>2</em>
</div>

### <a name="StatusBarItem"></a><span class="code-item" id=997>StatusBarItem</span>



<div class="comment"><p>ステータスバー項目はステータスバーの投稿で、テキストとアイコンを表示し、クリック時にコマンドを実行できます。</p>
</div>

#### Properties



<a name="StatusBarItem.alignment"></a><span class="ts" id=998 data-target="#details-998" data-toggle="collapse"><span class="ident">alignment</span><span>: </span><a class="type-ref" href="#StatusBarAlignment">StatusBarAlignment</a></span>
<div class="details collapse" id="details-998">
<div class="comment"><p>このアイテムのアラインメント。</p>
</div>
</div>



<a name="StatusBarItem.color"></a><span class="ts" id=1002 data-target="#details-1002" data-toggle="collapse"><span class="ident">color</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a> &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-1002">
<div class="comment"><p>このエントリの前景色。</p>
</div>
</div>



<a name="StatusBarItem.command"></a><span class="ts" id=1003 data-target="#details-1003" data-toggle="collapse"><span class="ident">command</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-1003">
<div class="comment"><p>クリック時に実行するコマンドの識別子。
コマンドは
<a href="#commands.getCommands">known</a>。</p>
</div>
</div>



<a name="StatusBarItem.priority"></a><span class="ts" id=999 data-target="#details-999" data-toggle="collapse"><span class="ident">priority</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-999">
<div class="comment"><p>このアイテムの優先順位。
値が高いほど、アイテムが左に表示されることを意味します。</p>
</div>
</div>



<a name="StatusBarItem.text"></a><span class="ts" id=1000 data-target="#details-1000" data-toggle="collapse"><span class="ident">text</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1000">
<div class="comment"><p>エントリに表示するテキスト。
以下の構文を利用して、テキストにアイコンを埋め込むことができます：</p>
<p>`My text $(アイコン名)には$(アイコン名)のようなアイコンが含まれています。
&#39;</p>
<p>アイコン名が<a href="https://octicons.github.com">octicon</a>アイコンセットから取得された場合、 ライトバルブ、サムズアップ、ザップなど</p>
</div>
</div>



<a name="StatusBarItem.tooltip"></a><span class="ts" id=1001 data-target="#details-1001" data-toggle="collapse"><span class="ident">tooltip</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-1001">
<div class="comment"><p>このエントリの上にカーソルを置くと、ツールヒントのテキストが表示されます。</p>
</div>
</div>

#### Methods



<a name="StatusBarItem.dispose"></a><span class="ts" id=1009 data-target="#details-1009" data-toggle="collapse"><span class="ident">dispose</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1009">
<div class="comment"><p>廃棄し、関連するリソースを解放します。
お電話
<a href="#StatusBarItem.hide">非表示</a>。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="StatusBarItem.hide"></a><span class="ts" id=1007 data-target="#details-1007" data-toggle="collapse"><span class="ident">hide</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1007">
<div class="comment"><p>ステータスバーのエントリを非表示にします。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="StatusBarItem.show"></a><span class="ts" id=1005 data-target="#details-1005" data-toggle="collapse"><span class="ident">show</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1005">
<div class="comment"><p>ステータスバーにエントリが表示されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="SymbolInformation"></a><span class="code-item" id=597>SymbolInformation</span>



<div class="comment"><p>変数、クラス、インターフェースなどのプログラミング構造に関する情報を表します。</p>
</div>

#### Constructors



<a name="SymbolInformation.new SymbolInformation"></a><span class="ts" id=603 data-target="#details-603" data-toggle="collapse"><span class="ident">new SymbolInformation</span><span>(</span><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">kind</span><span>: </span><a class="type-ref" href="#SymbolKind">SymbolKind</a>, <span class="ident">containerName</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">location</span><span>: </span><a class="type-ref" href="#Location">Location</a><span>)</span><span>: </span><a class="type-ref" href="#SymbolInformation">SymbolInformation</a></span>
<div class="details collapse" id="details-603">
<div class="comment"><p>新しいシンボル情報オブジェクトを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="name"></a><span class="ts" id=604 data-target="#details-604" data-toggle="collapse"><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="kind"></a><span class="ts" id=605 data-target="#details-605" data-toggle="collapse"><span class="ident">kind</span><span>: </span><a class="type-ref" href="#SymbolKind">SymbolKind</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="containerName"></a><span class="ts" id=606 data-target="#details-606" data-toggle="collapse"><span class="ident">containerName</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="location"></a><span class="ts" id=607 data-target="#details-607" data-toggle="collapse"><span class="ident">location</span><span>: </span><a class="type-ref" href="#Location">Location</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#SymbolInformation">SymbolInformation</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="SymbolInformation.new SymbolInformation"></a><span class="ts" id=608 data-target="#details-608" data-toggle="collapse"><span class="ident">new SymbolInformation</span><span>(</span><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">kind</span><span>: </span><a class="type-ref" href="#SymbolKind">SymbolKind</a>, <span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a>, <span class="ident">uri</span><span>?</span><span>: </span><a class="type-ref" href="#Uri">Uri</a>, <span class="ident">containerName</span><span>?</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#SymbolInformation">SymbolInformation</a></span>
<div class="details collapse" id="details-608">
<div class="comment"><p>新しいシンボル情報オブジェクトを作成します。</p>
<ul>
<li><em>deprecated</em> - <a href="#Location">location</a>オブジェクトを使用してコンストラクタを使用してください。</li>
</ul>
<p>新しいシンボル情報オブジェクトを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="name"></a><span class="ts" id=609 data-target="#details-609" data-toggle="collapse"><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="kind"></a><span class="ts" id=610 data-target="#details-610" data-toggle="collapse"><span class="ident">kind</span><span>: </span><a class="type-ref" href="#SymbolKind">SymbolKind</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="range"></a><span class="ts" id=611 data-target="#details-611" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="uri"></a><span class="ts" id=612 data-target="#details-612" data-toggle="collapse"><span class="ident">uri</span><span>?</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="containerName"></a><span class="ts" id=613 data-target="#details-613" data-toggle="collapse"><span class="ident">containerName</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#SymbolInformation">SymbolInformation</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="SymbolInformation.containerName"></a><span class="ts" id=599 data-target="#details-599" data-toggle="collapse"><span class="ident">containerName</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-599">
<div class="comment"><p>このシンボルを含むシンボルの名前。</p>
</div>
</div>



<a name="SymbolInformation.kind"></a><span class="ts" id=600 data-target="#details-600" data-toggle="collapse"><span class="ident">kind</span><span>: </span><a class="type-ref" href="#SymbolKind">SymbolKind</a></span>
<div class="details collapse" id="details-600">
<div class="comment"><p>このシンボルの種類。</p>
</div>
</div>



<a name="SymbolInformation.location"></a><span class="ts" id=601 data-target="#details-601" data-toggle="collapse"><span class="ident">location</span><span>: </span><a class="type-ref" href="#Location">Location</a></span>
<div class="details collapse" id="details-601">
<div class="comment"><p>このシンボルの位置。</p>
</div>
</div>



<a name="SymbolInformation.name"></a><span class="ts" id=598 data-target="#details-598" data-toggle="collapse"><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-598">
<div class="comment"><p>このシンボルの名前。</p>
</div>
</div>

### <a name="SymbolKind"></a><span class="code-item" id=570>SymbolKind</span>



<div class="comment"><p>記号の種類。</p>
</div>

#### Enumeration members



<a name="SymbolKind.Array"></a><span class="ts" id=588 data-target="#details-588" data-toggle="collapse"><span class="ident">Array</span></span>
<div class="details collapse" id="details-588">
<em>17</em>
</div>



<a name="SymbolKind.Boolean"></a><span class="ts" id=587 data-target="#details-587" data-toggle="collapse"><span class="ident">Boolean</span></span>
<div class="details collapse" id="details-587">
<em>16</em>
</div>



<a name="SymbolKind.Class"></a><span class="ts" id=575 data-target="#details-575" data-toggle="collapse"><span class="ident">Class</span></span>
<div class="details collapse" id="details-575">
<em>4</em>
</div>



<a name="SymbolKind.Constant"></a><span class="ts" id=584 data-target="#details-584" data-toggle="collapse"><span class="ident">Constant</span></span>
<div class="details collapse" id="details-584">
<em>13</em>
</div>



<a name="SymbolKind.Constructor"></a><span class="ts" id=579 data-target="#details-579" data-toggle="collapse"><span class="ident">Constructor</span></span>
<div class="details collapse" id="details-579">
<em>8</em>
</div>



<a name="SymbolKind.Enum"></a><span class="ts" id=580 data-target="#details-580" data-toggle="collapse"><span class="ident">Enum</span></span>
<div class="details collapse" id="details-580">
<em>9</em>
</div>



<a name="SymbolKind.EnumMember"></a><span class="ts" id=592 data-target="#details-592" data-toggle="collapse"><span class="ident">EnumMember</span></span>
<div class="details collapse" id="details-592">
<em>21</em>
</div>



<a name="SymbolKind.Event"></a><span class="ts" id=594 data-target="#details-594" data-toggle="collapse"><span class="ident">Event</span></span>
<div class="details collapse" id="details-594">
<em>23</em>
</div>



<a name="SymbolKind.Field"></a><span class="ts" id=578 data-target="#details-578" data-toggle="collapse"><span class="ident">Field</span></span>
<div class="details collapse" id="details-578">
<em>7</em>
</div>



<a name="SymbolKind.File"></a><span class="ts" id=571 data-target="#details-571" data-toggle="collapse"><span class="ident">File</span></span>
<div class="details collapse" id="details-571">
<em>0</em>
</div>



<a name="SymbolKind.Function"></a><span class="ts" id=582 data-target="#details-582" data-toggle="collapse"><span class="ident">Function</span></span>
<div class="details collapse" id="details-582">
<em>11</em>
</div>



<a name="SymbolKind.Interface"></a><span class="ts" id=581 data-target="#details-581" data-toggle="collapse"><span class="ident">Interface</span></span>
<div class="details collapse" id="details-581">
<em>10</em>
</div>



<a name="SymbolKind.Key"></a><span class="ts" id=590 data-target="#details-590" data-toggle="collapse"><span class="ident">Key</span></span>
<div class="details collapse" id="details-590">
<em>19</em>
</div>



<a name="SymbolKind.Method"></a><span class="ts" id=576 data-target="#details-576" data-toggle="collapse"><span class="ident">Method</span></span>
<div class="details collapse" id="details-576">
<em>5</em>
</div>



<a name="SymbolKind.Module"></a><span class="ts" id=572 data-target="#details-572" data-toggle="collapse"><span class="ident">Module</span></span>
<div class="details collapse" id="details-572">
<em>1</em>
</div>



<a name="SymbolKind.Namespace"></a><span class="ts" id=573 data-target="#details-573" data-toggle="collapse"><span class="ident">Namespace</span></span>
<div class="details collapse" id="details-573">
<em>2</em>
</div>



<a name="SymbolKind.Null"></a><span class="ts" id=591 data-target="#details-591" data-toggle="collapse"><span class="ident">Null</span></span>
<div class="details collapse" id="details-591">
<em>20</em>
</div>



<a name="SymbolKind.Number"></a><span class="ts" id=586 data-target="#details-586" data-toggle="collapse"><span class="ident">Number</span></span>
<div class="details collapse" id="details-586">
<em>15</em>
</div>



<a name="SymbolKind.Object"></a><span class="ts" id=589 data-target="#details-589" data-toggle="collapse"><span class="ident">Object</span></span>
<div class="details collapse" id="details-589">
<em>18</em>
</div>



<a name="SymbolKind.Operator"></a><span class="ts" id=595 data-target="#details-595" data-toggle="collapse"><span class="ident">Operator</span></span>
<div class="details collapse" id="details-595">
<em>24</em>
</div>



<a name="SymbolKind.Package"></a><span class="ts" id=574 data-target="#details-574" data-toggle="collapse"><span class="ident">Package</span></span>
<div class="details collapse" id="details-574">
<em>3</em>
</div>



<a name="SymbolKind.Property"></a><span class="ts" id=577 data-target="#details-577" data-toggle="collapse"><span class="ident">Property</span></span>
<div class="details collapse" id="details-577">
<em>6</em>
</div>



<a name="SymbolKind.String"></a><span class="ts" id=585 data-target="#details-585" data-toggle="collapse"><span class="ident">String</span></span>
<div class="details collapse" id="details-585">
<em>14</em>
</div>



<a name="SymbolKind.Struct"></a><span class="ts" id=593 data-target="#details-593" data-toggle="collapse"><span class="ident">Struct</span></span>
<div class="details collapse" id="details-593">
<em>22</em>
</div>



<a name="SymbolKind.TypeParameter"></a><span class="ts" id=596 data-target="#details-596" data-toggle="collapse"><span class="ident">TypeParameter</span></span>
<div class="details collapse" id="details-596">
<em>25</em>
</div>



<a name="SymbolKind.Variable"></a><span class="ts" id=583 data-target="#details-583" data-toggle="collapse"><span class="ident">Variable</span></span>
<div class="details collapse" id="details-583">
<em>12</em>
</div>

### <a name="Terminal"></a><span class="code-item" id=1015>Terminal</span>



<div class="comment"><p>統合端末内の個々の端末インスタンス。</p>
</div>

#### Properties



<a name="Terminal.name"></a><span class="ts" id=1016 data-target="#details-1016" data-toggle="collapse"><span class="ident">name</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1016">
<div class="comment"><p>端末の名前。</p>
</div>
</div>



<a name="Terminal.processId"></a><span class="ts" id=1017 data-target="#details-1017" data-toggle="collapse"><span class="ident">processId</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">number</a>&gt;</span>
<div class="details collapse" id="details-1017">
<div class="comment"><p>シェルプロセスのプロセスID。</p>
</div>
</div>

#### Methods



<a name="Terminal.dispose"></a><span class="ts" id=1028 data-target="#details-1028" data-toggle="collapse"><span class="ident">dispose</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1028">
<div class="comment"><p>廃棄し、関連するリソースを解放します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="Terminal.hide"></a><span class="ts" id=1026 data-target="#details-1026" data-toggle="collapse"><span class="ident">hide</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1026">
<div class="comment"><p>この端末が現在表示されている場合、端末パネルを非表示にします。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="Terminal.sendText"></a><span class="ts" id=1019 data-target="#details-1019" data-toggle="collapse"><span class="ident">sendText</span><span>(</span><span class="ident">text</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">addNewLine</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1019">
<div class="comment"><p>端末にテキストを送信します。テキストは、基本となるptyプロセスのstdinに書き込まれます。
(シェル)。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="text"></a><span class="ts" id=1020 data-target="#details-1020" data-toggle="collapse"><span class="ident">text</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="addNewLine"></a><span class="ts" id=1021 data-target="#details-1021" data-toggle="collapse"><span class="ident">addNewLine</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="Terminal.show"></a><span class="ts" id=1023 data-target="#details-1023" data-toggle="collapse"><span class="ident">show</span><span>(</span><span class="ident">preserveFocus</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1023">
<div class="comment"><p>ターミナルパネルを表示し、このターミナルをUIに表示します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="preserveFocus"></a><span class="ts" id=1024 data-target="#details-1024" data-toggle="collapse"><span class="ident">preserveFocus</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p><code>true</code> の場合、端末はフォーカスを取得しません。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="TerminalOptions"></a><span class="code-item" id=1089>TerminalOptions</span>



<div class="comment"><p>端末が使用すべきオプションを記述するValueオブジェクト。</p>
</div>

#### Properties



<a name="TerminalOptions.name"></a><span class="ts" id=1090 data-target="#details-1090" data-toggle="collapse"><span class="ident">name</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1090">
<div class="comment"><p>UIで端末を表すために人間が読める文字列。</p>
</div>
</div>



<a name="TerminalOptions.shellArgs"></a><span class="ts" id=1092 data-target="#details-1092" data-toggle="collapse"><span class="ident">shellArgs</span><span>?</span><span>: </span><a class="type-instrinct">string</a>[]</span>
<div class="details collapse" id="details-1092">
<div class="comment"><p>カスタムシェル実行ファイルのためのArgs、これはWindowsでは動作しません(#8429を参照)</p>
</div>
</div>



<a name="TerminalOptions.shellPath"></a><span class="ts" id=1091 data-target="#details-1091" data-toggle="collapse"><span class="ident">shellPath</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1091">
<div class="comment"><p>ターミナルで使用するカスタムシェル実行可能ファイルへのパス。</p>
</div>
</div>

### <a name="TextDocument"></a><span class="code-item" id=38>TextDocument</span>



<div class="comment"><p>ソースファイルなどのテキストドキュメントを表します。
テキストドキュメントには <a href="#TextLine">lines</a> とファイルのような基礎となるリソースに関する情報があります。</p>
</div>

#### Properties



<a name="TextDocument.eol"></a><span class="ts" id=48 data-target="#details-48" data-toggle="collapse"><span class="ident">eol</span><span>: </span><a class="type-ref" href="#EndOfLine">EndOfLine</a></span>
<div class="details collapse" id="details-48">
<div class="comment"><p>この文書で主に使用されている<a href="#EndOfLine">end of line</a>シーケンス。</p>
</div>
</div>



<a name="TextDocument.fileName"></a><span class="ts" id=40 data-target="#details-40" data-toggle="collapse"><span class="ident">fileName</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-40">
<div class="comment"><p>関連リソースのファイルシステムパス。
<a href="#TextDocument.uri">TextDocument.uri.fsPath</a> の省略記​​法。
uri スキームとは独立しています。</p>
</div>
</div>



<a name="TextDocument.isClosed"></a><span class="ts" id=45 data-target="#details-45" data-toggle="collapse"><span class="ident">isClosed</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-45">
<div class="comment"><p>ドキュメントが閉じられている場合は `true &#39;。
閉じたドキュメントはもう同期されず、同じリソースが再度開かれたときに再利用されません。</p>
</div>
</div>



<a name="TextDocument.isDirty"></a><span class="ts" id=44 data-target="#details-44" data-toggle="collapse"><span class="ident">isDirty</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-44">
<div class="comment"><p>無修正の変更がある場合は <code>true</code>。</p>
</div>
</div>



<a name="TextDocument.isUntitled"></a><span class="ts" id=41 data-target="#details-41" data-toggle="collapse"><span class="ident">isUntitled</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-41">
<div class="comment"><p>この文書が無題のファイルを表しているか？</p>
</div>
</div>



<a name="TextDocument.languageId"></a><span class="ts" id=42 data-target="#details-42" data-toggle="collapse"><span class="ident">languageId</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-42">
<div class="comment"><p>この文書に関連する言語の識別子。</p>
</div>
</div>



<a name="TextDocument.lineCount"></a><span class="ts" id=49 data-target="#details-49" data-toggle="collapse"><span class="ident">lineCount</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-49">
<div class="comment"><p>この文書の行数。</p>
</div>
</div>



<a name="TextDocument.uri"></a><span class="ts" id=39 data-target="#details-39" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-39">
<div class="comment"><p>このドキュメントの関連する URI。
ほとんどのドキュメントには <strong>file</strong>-スキームがあり、ディスク上のファイルを表すことを示しています。
ただし、ディスクによっては利用できないことを示す別のスキームがあるドキュメントもあります。</p>
</div>
</div>



<a name="TextDocument.version"></a><span class="ts" id=43 data-target="#details-43" data-toggle="collapse"><span class="ident">version</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-43">
<div class="comment"><p>このドキュメントのバージョン番号(各変更後、元に戻す/やり直しを含めて厳密に増加します)。</p>
</div>
</div>

#### Methods



<a name="TextDocument.getText"></a><span class="ts" id=62 data-target="#details-62" data-toggle="collapse"><span class="ident">getText</span><span>(</span><span class="ident">range</span><span>?</span><span>: </span><a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-62">
<div class="comment"><p>この文書のテキストを取得します。
範囲を指定すると、部分文字列を取得できます。
範囲は <a href="#TextDocument.validateRange">調整</a> されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=63 data-target="#details-63" data-toggle="collapse"><span class="ident">range</span><span>?</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>範囲に含まれるテキストのみを含めます。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">string</a></span></td><td><div class="comment"><p>指定された範囲内のテキストまたはテキスト全体。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextDocument.getWordRangeAtPosition"></a><span class="ts" id=65 data-target="#details-65" data-toggle="collapse"><span class="ident">getWordRangeAtPosition</span><span>(</span><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">regex</span><span>?</span><span>: </span><a class="type-ref" href="#RegExp">RegExp</a><span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a> &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-65">
<div class="comment"><p>与えられた位置で単語の範囲を取得します。
デフォルトでは、単語はスペース、 - 、_などの共通の区切り文字で定義されます。
また、langugeカスタムごとに
<a href="#LanguageConfiguration.wordPattern">単語の定義</a>を定義することができます。
カスタム正規表現を提供することも可能です。
<em>注</em> カスタム正規表現は空の文字列と一致してはならず、そうであれば無視されます。</p>
<p>位置は <a href="#TextDocument.validatePosition">調整</a> されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="position"></a><span class="ts" id=66 data-target="#details-66" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>位置です。</p>
</div></td></tr>
<tr><td><a name="regex"></a><span class="ts" id=67 data-target="#details-67" data-toggle="collapse"><span class="ident">regex</span><span>?</span><span>: </span><a class="type-ref" href="#RegExp">RegExp</a></span></td><td><div class="comment"><p>単語が何であるかを記述するオプションの正規表現。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a> &#124; <a class="type-instrinct">undefined</a></span></td><td><div class="comment"><p>単語にまたがる範囲、または <code>undefined</code> です。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextDocument.lineAt"></a><span class="ts" id=51 data-target="#details-51" data-toggle="collapse"><span class="ident">lineAt</span><span>(</span><span class="ident">line</span><span>: </span><a class="type-instrinct">number</a><span>)</span><span>: </span><a class="type-ref" href="#TextLine">TextLine</a></span>
<div class="details collapse" id="details-51">
<div class="comment"><p>行番号で示されるテキスト行を返します。注意 返されたオブジェクトは live では <em>なく</em>、
文書は反映されません。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="line"></a><span class="ts" id=52 data-target="#details-52" data-toggle="collapse"><span class="ident">line</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>[0、lineCount) の行番号です。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#TextLine">TextLine</a></span></td><td><div class="comment"><p>A <a href="#TextLine">行</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextDocument.lineAt"></a><span class="ts" id=53 data-target="#details-53" data-toggle="collapse"><span class="ident">lineAt</span><span>(</span><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-ref" href="#TextLine">TextLine</a></span>
<div class="details collapse" id="details-53">
<div class="comment"><p>位置によって示されるテキスト行を返します。
返されたオブジェクトは生きて<em>いない</em>ことに注意してください。文書への変更は反映されません。</p>
<p>位置は調整されます(#TextDocument.validatePosition)。</p>
<ul>
<li><em>see</em> - <a href="#TextDocument.lineAt">TextDocument.lineAt</a></li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="position"></a><span class="ts" id=54 data-target="#details-54" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#TextLine">TextLine</a></span></td><td><div class="comment"><p>A <a href="#TextLine">行</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextDocument.offsetAt"></a><span class="ts" id=56 data-target="#details-56" data-toggle="collapse"><span class="ident">offsetAt</span><span>(</span><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-56">
<div class="comment"><p>位置をゼロベースのオフセットに変換します。</p>
<p>位置は <a href="#TextDocument.validatePosition">調整</a> されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="position"></a><span class="ts" id=57 data-target="#details-57" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>位置です。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>有効なゼロベースのオフセットです。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextDocument.positionAt"></a><span class="ts" id=59 data-target="#details-59" data-toggle="collapse"><span class="ident">positionAt</span><span>(</span><span class="ident">offset</span><span>: </span><a class="type-instrinct">number</a><span>)</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-59">
<div class="comment"><p>ゼロベースのオフセットを Position に変換します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="offset"></a><span class="ts" id=60 data-target="#details-60" data-toggle="collapse"><span class="ident">offset</span><span>: </span><a class="type-instrinct">number</a></span></td><td><div class="comment"><p>ゼロベースのオフセット。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>有効な <a href="#Position">Position</a>。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextDocument.save"></a><span class="ts" id=47 data-target="#details-47" data-toggle="collapse"><span class="ident">save</span><span>(</span><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">boolean</a>&gt;</span>
<div class="details collapse" id="details-47">
<div class="comment"><p>基礎となるファイルを保存します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">boolean</a>&gt;</span></td><td><div class="comment"><p>ファイルが保存されたときにtrueに解決される約束。
ファイルがダーティでないか、保存に失敗した場合はfalseを返します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextDocument.validatePosition"></a><span class="ts" id=72 data-target="#details-72" data-toggle="collapse"><span class="ident">validatePosition</span><span>(</span><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a><span>)</span><span>: </span><a class="type-ref" href="#Position">Position</a></span>
<div class="details collapse" id="details-72">
<div class="comment"><p>この文書の範囲に position が含まれていることを確認します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="position"></a><span class="ts" id=73 data-target="#details-73" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>位置です。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"><p>指定された位置または新しい、調整された位置。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextDocument.validateRange"></a><span class="ts" id=69 data-target="#details-69" data-toggle="collapse"><span class="ident">validateRange</span><span>(</span><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-69">
<div class="comment"><p>この文書に範囲が完全に含まれていることを確認します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=70 data-target="#details-70" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>範囲です。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"><p>指定された範囲または新しい調整済み範囲。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="TextDocumentChangeEvent"></a><span class="code-item" id=1103>TextDocumentChangeEvent</span>



<div class="comment"><p>トランザクション<a href="#TextDocument">ドキュメント</a>の変更を表すイベント。</p>
</div>

#### Properties



<a name="TextDocumentChangeEvent.contentChanges"></a><span class="ts" id=1105 data-target="#details-1105" data-toggle="collapse"><span class="ident">contentChanges</span><span>: </span><a class="type-ref" href="#TextDocumentContentChangeEvent">TextDocumentContentChangeEvent</a>[]</span>
<div class="details collapse" id="details-1105">
<div class="comment"><p>コンテンツの変更の配列。</p>
</div>
</div>



<a name="TextDocumentChangeEvent.document"></a><span class="ts" id=1104 data-target="#details-1104" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span>
<div class="details collapse" id="details-1104">
<div class="comment"><p>影響を受ける文書。</p>
</div>
</div>

### <a name="TextDocumentContentChangeEvent"></a><span class="code-item" id=1099>TextDocumentContentChangeEvent</span>



<div class="comment"><p><a href="#TextDocument">document</a>のテキストにおける個々の変更を記述するイベント。</p>
</div>

#### Properties



<a name="TextDocumentContentChangeEvent.range"></a><span class="ts" id=1100 data-target="#details-1100" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-1100">
<div class="comment"><p>置き換えられた範囲。</p>
</div>
</div>



<a name="TextDocumentContentChangeEvent.rangeLength"></a><span class="ts" id=1101 data-target="#details-1101" data-toggle="collapse"><span class="ident">rangeLength</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-1101">
<div class="comment"><p>置き換えられた範囲の長さ。</p>
</div>
</div>



<a name="TextDocumentContentChangeEvent.text"></a><span class="ts" id=1102 data-target="#details-1102" data-toggle="collapse"><span class="ident">text</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1102">
<div class="comment"><p>範囲の新しいテキスト。</p>
</div>
</div>

### <a name="TextDocumentContentProvider"></a><span class="code-item" id=457>TextDocumentContentProvider</span>



<div class="comment"><p>テキストドキュメントコンテンツプロバイダは、dllからのソースやmdから生成されたhtmlなど、読取り専用のドキュメントをエディタに追加することができます。</p>
<p>コンテンツプロバイダは<a href="#workspace.registerTextDocumentContentProvider">登録済み</a>
<a href="#Uri.scheme">uri-scheme</a>の場合。
そのスキームを持つURIが読み込まれると(#workspace.openTextDocument)、コンテンツプロバイダーに尋ねられます。</p>
</div>

#### Events



<a name="TextDocumentContentProvider.onDidChange"></a><span class="ts" id=458 data-target="#details-458" data-toggle="collapse"><span class="ident">onDidChange</span><span>?</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-ref" href="#Uri">Uri</a>&gt;</span>
<div class="details collapse" id="details-458">
<div class="comment"><p>リソースへの通知イベントが変更されました。</p>
</div>
</div>

#### Methods



<a name="TextDocumentContentProvider.provideTextDocumentContent"></a><span class="ts" id=460 data-target="#details-460" data-toggle="collapse"><span class="ident">provideTextDocumentContent</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-460">
<div class="comment"><p>与えられたURIのテキストコンテンツを提供する。</p>
<p>エディタは返された文字列コンテンツを使用して読み取り専用を作成します
<a href="#TextDocument">document</a>。
割り当てられたリソースは、対応するドキュメントが<a href="#workspace.onDidCloseTextDocument">閉じる</a>されたときに解放される必要があります。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=461 data-target="#details-461" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=462 data-target="#details-462" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>このように解決される文字列または文字列。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="TextDocumentSaveReason"></a><span class="code-item" id=1106>TextDocumentSaveReason</span>



<div class="comment"><p>テキスト文書が保存される理由を表します。</p>
</div>

#### Enumeration members



<a name="TextDocumentSaveReason.AfterDelay"></a><span class="ts" id=1108 data-target="#details-1108" data-toggle="collapse"><span class="ident">AfterDelay</span></span>
<div class="details collapse" id="details-1108">
<em>2</em>
</div>



<a name="TextDocumentSaveReason.FocusOut"></a><span class="ts" id=1109 data-target="#details-1109" data-toggle="collapse"><span class="ident">FocusOut</span></span>
<div class="details collapse" id="details-1109">
<em>3</em>
</div>



<a name="TextDocumentSaveReason.Manual"></a><span class="ts" id=1107 data-target="#details-1107" data-toggle="collapse"><span class="ident">Manual</span></span>
<div class="details collapse" id="details-1107">
<em>1</em>
</div>

### <a name="TextDocumentShowOptions"></a><span class="code-item" id=239>TextDocumentShowOptions</span>



<div class="comment"><p><a href="#TextDocument">document</a>を<a href="#TextEditor">editor</a>に表示する動作を設定するオプションを表します。</p>
</div>

#### Properties



<a name="TextDocumentShowOptions.preserveFocus"></a><span class="ts" id=241 data-target="#details-241" data-toggle="collapse"><span class="ident">preserveFocus</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-241">
<div class="comment"><p>`true &#39;のときに<a href="#TextEditor">エディタ</a>がフォーカスを止めるオプションのフラグ。</p>
</div>
</div>



<a name="TextDocumentShowOptions.preview"></a><span class="ts" id=242 data-target="#details-242" data-toggle="collapse"><span class="ident">preview</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-242">
<div class="comment"><p><a href="#TextEditor">エディタ</a>タブが次のエディタに置き換えられるかどうか、またはそれが保持されるかどうかを制御するオプションのフラグ。</p>
</div>
</div>



<a name="TextDocumentShowOptions.viewColumn"></a><span class="ts" id=240 data-target="#details-240" data-toggle="collapse"><span class="ident">viewColumn</span><span>?</span><span>: </span><a class="type-ref" href="#ViewColumn">ViewColumn</a></span>
<div class="details collapse" id="details-240">
<div class="comment"><p><a href="#TextEditor">editor</a>が表示されるオプションのビュー列。
デフォルトは<a href="#ViewColumn.One">1</a>です。
他の値は<strong>Min(column、columnCount + 1)</strong>に調整されます。</p>
</div>
</div>

### <a name="TextDocumentWillSaveEvent"></a><span class="code-item" id=1110>TextDocumentWillSaveEvent</span>



<div class="comment"><p><a href="#TextDocument">document</a>が保存されたときに発生するイベント。</p>
<p>文書を保存する前に変更を加えるには、
<a href="#TextDocumentWillSaveEvent.waitUntil"><code>waitUntil</code></a> - [text edits]の配列(#TextEdit)に解決されるthenableで機能します。</p>
</div>

#### Properties



<a name="TextDocumentWillSaveEvent.document"></a><span class="ts" id=1111 data-target="#details-1111" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span>
<div class="details collapse" id="details-1111">
<div class="comment"><p>保存される文書。</p>
</div>
</div>



<a name="TextDocumentWillSaveEvent.reason"></a><span class="ts" id=1112 data-target="#details-1112" data-toggle="collapse"><span class="ident">reason</span><span>: </span><a class="type-ref" href="#TextDocumentSaveReason">TextDocumentSaveReason</a></span>
<div class="details collapse" id="details-1112">
<div class="comment"><p>セーブがトリガーされた理由。</p>
</div>
</div>

#### Methods



<a name="TextDocumentWillSaveEvent.waitUntil"></a><span class="ts" id=1114 data-target="#details-1114" data-toggle="collapse"><span class="ident">waitUntil</span><span>(</span><span class="ident">thenable</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextEdit">TextEdit</a>[]&gt;<span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1114">
<div class="comment"><p>イベントループを一時停止し、<a href="#TextEdit">保存前編集</a>を適用することができます。
この関数の後続の呼び出しの編集は、順番に適用されます。ザ
ドキュメントの同時修正が行われた場合、編集内容は無視されます。</p>
<p><em>注：</em>この関数は、イベントのディスパッチ中にのみ呼び出すことができます。
非同期で：</p>
<p>```ts workspace.onWillSaveTextDocument(イベント=&gt; {</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="thenable"></a><span class="ts" id=1115 data-target="#details-1115" data-toggle="collapse"><span class="ident">thenable</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TextEdit">TextEdit</a>[]&gt;</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="TextDocumentWillSaveEvent.waitUntil"></a><span class="ts" id=1116 data-target="#details-1116" data-toggle="collapse"><span class="ident">waitUntil</span><span>(</span><span class="ident">thenable</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">any</a>&gt;<span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-1116">
<div class="comment"><p>提供されたthenableが解決されるまで、イベントループを一時停止することができます。</p>
<p><em>注：</em>この関数は、イベントのディスパッチ中にのみ呼び出すことができます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="thenable"></a><span class="ts" id=1117 data-target="#details-1117" data-toggle="collapse"><span class="ident">thenable</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">any</a>&gt;</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="TextEdit"></a><span class="code-item" id=637>TextEdit</span>



<div class="comment"><p>テキスト編集は、文書に適用する編集を表します。</p>
</div>

#### Static



<a name="TextEdit.delete"></a><span class="ts" id=647 data-target="#details-647" data-toggle="collapse"><span class="ident">delete</span><span>(</span><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-ref" href="#TextEdit">TextEdit</a></span>
<div class="details collapse" id="details-647">
<div class="comment"><p>削除編集を作成するユーティリティ。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=648 data-target="#details-648" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#TextEdit">TextEdit</a></span></td><td><div class="comment"><p>新しいテキスト編集オブジェクト。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextEdit.insert"></a><span class="ts" id=643 data-target="#details-643" data-toggle="collapse"><span class="ident">insert</span><span>(</span><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">newText</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#TextEdit">TextEdit</a></span>
<div class="details collapse" id="details-643">
<div class="comment"><p>挿入編集を作成するユーティリティ。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="position"></a><span class="ts" id=644 data-target="#details-644" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="newText"></a><span class="ts" id=645 data-target="#details-645" data-toggle="collapse"><span class="ident">newText</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#TextEdit">TextEdit</a></span></td><td><div class="comment"><p>新しいテキスト編集オブジェクト。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextEdit.replace"></a><span class="ts" id=639 data-target="#details-639" data-toggle="collapse"><span class="ident">replace</span><span>(</span><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a>, <span class="ident">newText</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#TextEdit">TextEdit</a></span>
<div class="details collapse" id="details-639">
<div class="comment"><p>置換編集を作成するユーティリティ。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=640 data-target="#details-640" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="newText"></a><span class="ts" id=641 data-target="#details-641" data-toggle="collapse"><span class="ident">newText</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#TextEdit">TextEdit</a></span></td><td><div class="comment"><p>新しいテキスト編集オブジェクト。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextEdit.setEndOfLine"></a><span class="ts" id=650 data-target="#details-650" data-toggle="collapse"><span class="ident">setEndOfLine</span><span>(</span><span class="ident">eol</span><span>: </span><a class="type-ref" href="#EndOfLine">EndOfLine</a><span>)</span><span>: </span><a class="type-ref" href="#TextEdit">TextEdit</a></span>
<div class="details collapse" id="details-650">
<div class="comment"><p>eol-editを作成するユーティリティ。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="eol"></a><span class="ts" id=651 data-target="#details-651" data-toggle="collapse"><span class="ident">eol</span><span>: </span><a class="type-ref" href="#EndOfLine">EndOfLine</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#TextEdit">TextEdit</a></span></td><td><div class="comment"><p>新しいテキスト編集オブジェクト。</p>
</div></td></tr>
</table>
</div>
</div>

#### Constructors



<a name="TextEdit.new TextEdit"></a><span class="ts" id=656 data-target="#details-656" data-toggle="collapse"><span class="ident">new TextEdit</span><span>(</span><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a>, <span class="ident">newText</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#TextEdit">TextEdit</a></span>
<div class="details collapse" id="details-656">
<div class="comment"><p>新しいTextEditを作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=657 data-target="#details-657" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="newText"></a><span class="ts" id=658 data-target="#details-658" data-toggle="collapse"><span class="ident">newText</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#TextEdit">TextEdit</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="TextEdit.newEol"></a><span class="ts" id=654 data-target="#details-654" data-toggle="collapse"><span class="ident">newEol</span><span>: </span><a class="type-ref" href="#EndOfLine">EndOfLine</a></span>
<div class="details collapse" id="details-654">
<div class="comment"><p>この文書で使用されているeol-sequence。</p>
<p>注* eol-sequenceは文書全体に適用されます。</p>
</div>
</div>



<a name="TextEdit.newText"></a><span class="ts" id=653 data-target="#details-653" data-toggle="collapse"><span class="ident">newText</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-653">
<div class="comment"><p>この編集が挿入する文字列。</p>
</div>
</div>



<a name="TextEdit.range"></a><span class="ts" id=652 data-target="#details-652" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-652">
<div class="comment"><p>この編集が適用される範囲。</p>
</div>
</div>

### <a name="TextEditor"></a><span class="code-item" id=317>TextEditor</span>



<div class="comment"><p><a href="#TextDocument">document</a>に添付されたエディタを表します。</p>
</div>

#### Properties



<a name="TextEditor.document"></a><span class="ts" id=318 data-target="#details-318" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span>
<div class="details collapse" id="details-318">
<div class="comment"><p>このテキストエディタに関連付けられたドキュメント。
このテキストエディタの生涯にわたってドキュメントは同じになります。</p>
</div>
</div>



<a name="TextEditor.options"></a><span class="ts" id=321 data-target="#details-321" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#TextEditorOptions">TextEditorOptions</a></span>
<div class="details collapse" id="details-321">
<div class="comment"><p>テキストエディタのオプション。</p>
</div>
</div>



<a name="TextEditor.selection"></a><span class="ts" id=319 data-target="#details-319" data-toggle="collapse"><span class="ident">selection</span><span>: </span><a class="type-ref" href="#Selection">Selection</a></span>
<div class="details collapse" id="details-319">
<div class="comment"><p>このテキストエディタの主な選択肢。</p>
<p><code>TextEditor.selections [0]</code> の短縮形です。</p>
</div>
</div>



<a name="TextEditor.selections"></a><span class="ts" id=320 data-target="#details-320" data-toggle="collapse"><span class="ident">selections</span><span>: </span><a class="type-ref" href="#Selection">Selection</a>[]</span>
<div class="details collapse" id="details-320">
<div class="comment"><p>このテキストエディタの選択肢。
主な選択は常にインデックス0になります。</p>
</div>
</div>



<a name="TextEditor.viewColumn"></a><span class="ts" id=322 data-target="#details-322" data-toggle="collapse"><span class="ident">viewColumn</span><span>?</span><span>: </span><a class="type-ref" href="#ViewColumn">ViewColumn</a></span>
<div class="details collapse" id="details-322">
<div class="comment"><p>このエディターが表示する列。
これが3つのメインエディタの1つではない場合、例えば埋め込みエディタの場合は「未定義」になります。</p>
</div>
</div>

#### Methods



<a name="TextEditor.edit"></a><span class="ts" id=324 data-target="#details-324" data-toggle="collapse"><span class="ident">edit</span><span>(</span><span class="ident">callback</span><span>: </span>(editBuilder: <a class="type-ref" href="#TextEditorEdit">TextEditorEdit</a>) =&gt; <a class="type-instrinct">void</a>, <span class="ident">options</span><span>?</span><span>: </span>{undoStopAfter: <a class="type-instrinct">boolean</a>, undoStopBefore: <a class="type-instrinct">boolean</a>}<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">boolean</a>&gt;</span>
<div class="details collapse" id="details-324">
<div class="comment"><p>このテキストエディタに関連付けられたドキュメントの編集を実行します。</p>
<p>与えられたコールバック関数は<a href="#TextEditorEdit">edit-builder</a>で呼び出されます。
編集に使用すること。編集ビルダーは有効ですが、
コールバックが実行されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="callback"></a><span class="ts" id=325 data-target="#details-325" data-toggle="collapse"><span class="ident">callback</span><span>: </span>(editBuilder: <a class="type-ref" href="#TextEditorEdit">TextEditorEdit</a>) =&gt; <a class="type-instrinct">void</a></span></td><td><div class="comment"><p>(#TextEditorEdit)を使用して編集を作成できる関数です。</p>
</div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=329 data-target="#details-329" data-toggle="collapse"><span class="ident">options</span><span>?</span><span>: </span>{undoStopAfter: <a class="type-instrinct">boolean</a>, undoStopBefore: <a class="type-instrinct">boolean</a>}</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">boolean</a>&gt;</span></td><td><div class="comment"><p>編集が適用可能かどうかを示す値で解決される約束。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextEditor.hide"></a><span class="ts" id=353 data-target="#details-353" data-toggle="collapse"><span class="ident">hide</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-353">
<div class="comment"><p>テキストエディタを非表示にします。</p>
<ul>
<li><em>deprecated</em> - <strong>このメソッドは非推奨です</strong> コマンド &#39;workbench.action.closeActiveEditor&#39;を代わりに使用してください。
このメソッドは予期しない動作を示し、次のメジャーアップデートで削除されます。</li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="TextEditor.insertSnippet"></a><span class="ts" id=334 data-target="#details-334" data-toggle="collapse"><span class="ident">insertSnippet</span><span>(</span><span class="ident">snippet</span><span>: </span><a class="type-ref" href="#SnippetString">SnippetString</a>, <span class="ident">location</span><span>?</span><span>: </span><a class="type-ref" href="#Position">Position</a> &#124; <a class="type-ref" href="#Range">Range</a> &#124; <a class="type-ref" href="#Position">Position</a>[] &#124; <a class="type-ref" href="#Range">Range</a>[], <span class="ident">options</span><span>?</span><span>: </span>{undoStopAfter: <a class="type-instrinct">boolean</a>, undoStopBefore: <a class="type-instrinct">boolean</a>}<span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">boolean</a>&gt;</span>
<div class="details collapse" id="details-334">
<div class="comment"><p><a href="#SnippetString">Snippet</a>を挿入し、エディタをスニペットモードにします。 「スニペットモード」
は、エディターがプレースホルダーと追加カーソルを追加してユーザーが完了できることを意味します
スニペットを受け入れる。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="snippet"></a><span class="ts" id=335 data-target="#details-335" data-toggle="collapse"><span class="ident">snippet</span><span>: </span><a class="type-ref" href="#SnippetString">SnippetString</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="location"></a><span class="ts" id=336 data-target="#details-336" data-toggle="collapse"><span class="ident">location</span><span>?</span><span>: </span><a class="type-ref" href="#Position">Position</a> &#124; <a class="type-ref" href="#Range">Range</a> &#124; <a class="type-ref" href="#Position">Position</a>[] &#124; <a class="type-ref" href="#Range">Range</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="options"></a><span class="ts" id=337 data-target="#details-337" data-toggle="collapse"><span class="ident">options</span><span>?</span><span>: </span>{undoStopAfter: <a class="type-instrinct">boolean</a>, undoStopBefore: <a class="type-instrinct">boolean</a>}</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">boolean</a>&gt;</span></td><td><div class="comment"><p>スニペットを挿入できるかどうかを示す値で解決する約束。
約束は、スニペットが完全に埋め込まれているか、受け入れられていることを示すものではありません。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TextEditor.revealRange"></a><span class="ts" id=346 data-target="#details-346" data-toggle="collapse"><span class="ident">revealRange</span><span>(</span><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a>, <span class="ident">revealType</span><span>?</span><span>: </span><a class="type-ref" href="#TextEditorRevealType">TextEditorRevealType</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-346">
<div class="comment"><p>与えられた範囲を明らかにするために <code>revealType</code> で示されるようにスクロールします。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="range"></a><span class="ts" id=347 data-target="#details-347" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="revealType"></a><span class="ts" id=348 data-target="#details-348" data-toggle="collapse"><span class="ident">revealType</span><span>?</span><span>: </span><a class="type-ref" href="#TextEditorRevealType">TextEditorRevealType</a></span></td><td><div class="comment"><p><code>range</code> を明らかにするためのスクロール戦略。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="TextEditor.setDecorations"></a><span class="ts" id=342 data-target="#details-342" data-toggle="collapse"><span class="ident">setDecorations</span><span>(</span><span class="ident">decorationType</span><span>: </span><a class="type-ref" href="#TextEditorDecorationType">TextEditorDecorationType</a>, <span class="ident">rangesOrOptions</span><span>: </span><a class="type-ref" href="#Range">Range</a>[] &#124; <a class="type-ref" href="#DecorationOptions">DecorationOptions</a>[]<span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-342">
<div class="comment"><p>装飾セットをテキストエディタに追加します。
指定された<a href="#TextEditorDecorationType">デコレーションタイプ</a>でデコレーションのセットがすでに存在する場合、それらは置き換えられます。</p>
<ul>
<li><em>see</em> - <a href="#window.createTextEditorDecorationType">createTextEditorDecorationType</a>を参照してください。</li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="decorationType"></a><span class="ts" id=343 data-target="#details-343" data-toggle="collapse"><span class="ident">decorationType</span><span>: </span><a class="type-ref" href="#TextEditorDecorationType">TextEditorDecorationType</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="rangesOrOptions"></a><span class="ts" id=344 data-target="#details-344" data-toggle="collapse"><span class="ident">rangesOrOptions</span><span>: </span><a class="type-ref" href="#Range">Range</a>[] &#124; <a class="type-ref" href="#DecorationOptions">DecorationOptions</a>[]</span></td><td><div class="comment"><p>(#Range)またはより詳細な<a href="#DecorationOptions">options</a>のいずれかです。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="TextEditor.show"></a><span class="ts" id=350 data-target="#details-350" data-toggle="collapse"><span class="ident">show</span><span>(</span><span class="ident">column</span><span>?</span><span>: </span><a class="type-ref" href="#ViewColumn">ViewColumn</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-350">
<div class="comment"><p>テキストエディタを表示します。</p>
<ul>
<li><em>deprecated</em> - <strong>このメソッドは非推奨です</strong>
[window.showTextDocument]を使用する(#window.showTextDocument)*代わりに。このメソッドは予期しない動作を示し、次のメジャーアップデートで削除されます。</li>
</ul>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="column"></a><span class="ts" id=351 data-target="#details-351" data-toggle="collapse"><span class="ident">column</span><span>?</span><span>: </span><a class="type-ref" href="#ViewColumn">ViewColumn</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="TextEditorCursorStyle"></a><span class="code-item" id=204>TextEditorCursorStyle</span>



<div class="comment"><p>カーソルの描画スタイル。</p>
</div>

#### Enumeration members



<a name="TextEditorCursorStyle.Block"></a><span class="ts" id=206 data-target="#details-206" data-toggle="collapse"><span class="ident">Block</span></span>
<div class="details collapse" id="details-206">
<em>2</em>
</div>



<a name="TextEditorCursorStyle.BlockOutline"></a><span class="ts" id=209 data-target="#details-209" data-toggle="collapse"><span class="ident">BlockOutline</span></span>
<div class="details collapse" id="details-209">
<em>5</em>
</div>



<a name="TextEditorCursorStyle.Line"></a><span class="ts" id=205 data-target="#details-205" data-toggle="collapse"><span class="ident">Line</span></span>
<div class="details collapse" id="details-205">
<em>1</em>
</div>



<a name="TextEditorCursorStyle.LineThin"></a><span class="ts" id=208 data-target="#details-208" data-toggle="collapse"><span class="ident">LineThin</span></span>
<div class="details collapse" id="details-208">
<em>4</em>
</div>



<a name="TextEditorCursorStyle.Underline"></a><span class="ts" id=207 data-target="#details-207" data-toggle="collapse"><span class="ident">Underline</span></span>
<div class="details collapse" id="details-207">
<em>3</em>
</div>



<a name="TextEditorCursorStyle.UnderlineThin"></a><span class="ts" id=210 data-target="#details-210" data-toggle="collapse"><span class="ident">UnderlineThin</span></span>
<div class="details collapse" id="details-210">
<em>6</em>
</div>

### <a name="TextEditorDecorationType"></a><span class="code-item" id=220>TextEditorDecorationType</span>



<div class="comment"><p><a href="#TextEditor">テキストエディタ</a>で同じ<a href="#DecorationRenderOptions">スタイルオプション</a>を共有する一連の装飾のハンドルを表します。</p>
<p><code>TextEditorDecorationType</code> のインスタンスを取得するには
<a href="#window.createTextEditorDecorationType">createTextEditorDecorationType</a>。</p>
</div>

#### Properties



<a name="TextEditorDecorationType.key"></a><span class="ts" id=221 data-target="#details-221" data-toggle="collapse"><span class="ident">key</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-221">
<div class="comment"><p>ハンドルの内部表現。</p>
</div>
</div>

#### Methods



<a name="TextEditorDecorationType.dispose"></a><span class="ts" id=223 data-target="#details-223" data-toggle="collapse"><span class="ident">dispose</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-223">
<div class="comment"><p>この装飾タイプとそれを使用するすべてのテキストエディタのすべての装飾を削除します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="TextEditorEdit"></a><span class="code-item" id=357>TextEditorEdit</span>



<div class="comment"><p>TextEditorの1つのトランザクションに適用される複雑な編集。
これは編集の説明を保持し、編集が有効な場合(つまり、重複していない領域、文書が変更されなかった場合など)、<a href="[テキストエディタ] ](#テキストエディタ">テキストエディタ</a>。</p>
</div>

#### Methods



<a name="TextEditorEdit.delete"></a><span class="ts" id=367 data-target="#details-367" data-toggle="collapse"><span class="ident">delete</span><span>(</span><span class="ident">location</span><span>: </span><a class="type-ref" href="#Range">Range</a> &#124; <a class="type-ref" href="#Selection">Selection</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-367">
<div class="comment"><p>特定のテキスト領域を削除する。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="location"></a><span class="ts" id=368 data-target="#details-368" data-toggle="collapse"><span class="ident">location</span><span>: </span><a class="type-ref" href="#Range">Range</a> &#124; <a class="type-ref" href="#Selection">Selection</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="TextEditorEdit.insert"></a><span class="ts" id=363 data-target="#details-363" data-toggle="collapse"><span class="ident">insert</span><span>(</span><span class="ident">location</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">value</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-363">
<div class="comment"><p>場所にテキストを挿入します。</p>
<p><code>value</code> で\ r \ nまたは\ nを使うことができ、現在の<a href="#TextDocument">document</a>に正規化されます。
同等のテキスト編集は<a href="#TextEditorEdit.replace">replace</a>で行うことができますが、 <code>insert</code> は別の結果の選択を生成します(移動します)。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="location"></a><span class="ts" id=364 data-target="#details-364" data-toggle="collapse"><span class="ident">location</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="value"></a><span class="ts" id=365 data-target="#details-365" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="TextEditorEdit.replace"></a><span class="ts" id=359 data-target="#details-359" data-toggle="collapse"><span class="ident">replace</span><span>(</span><span class="ident">location</span><span>: </span><a class="type-ref" href="#Position">Position</a> &#124; <a class="type-ref" href="#Range">Range</a> &#124; <a class="type-ref" href="#Selection">Selection</a>, <span class="ident">value</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-359">
<div class="comment"><p>特定のテキスト領域を新しい値に置き換えます。</p>
<p><code>value</code> で\ r \ nまたは\ nを使うことができ、現在の<a href="#TextDocument">document</a>に正規化されます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="location"></a><span class="ts" id=360 data-target="#details-360" data-toggle="collapse"><span class="ident">location</span><span>: </span><a class="type-ref" href="#Position">Position</a> &#124; <a class="type-ref" href="#Range">Range</a> &#124; <a class="type-ref" href="#Selection">Selection</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="value"></a><span class="ts" id=361 data-target="#details-361" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="TextEditorEdit.setEndOfLine"></a><span class="ts" id=370 data-target="#details-370" data-toggle="collapse"><span class="ident">setEndOfLine</span><span>(</span><span class="ident">endOfLine</span><span>: </span><a class="type-ref" href="#EndOfLine">EndOfLine</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-370">
<div class="comment"><p>行末のシーケンスを設定します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="endOfLine"></a><span class="ts" id=371 data-target="#details-371" data-toggle="collapse"><span class="ident">endOfLine</span><span>: </span><a class="type-ref" href="#EndOfLine">EndOfLine</a></span></td><td><div class="comment"><p>(#TextDocument)の新しい行の終わりです。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="TextEditorLineNumbersStyle"></a><span class="code-item" id=211>TextEditorLineNumbersStyle</span>



<div class="comment"><p>行番号のレンダリングスタイル。</p>
</div>

#### Enumeration members



<a name="TextEditorLineNumbersStyle.Off"></a><span class="ts" id=212 data-target="#details-212" data-toggle="collapse"><span class="ident">Off</span></span>
<div class="details collapse" id="details-212">
<em>0</em>
</div>



<a name="TextEditorLineNumbersStyle.On"></a><span class="ts" id=213 data-target="#details-213" data-toggle="collapse"><span class="ident">On</span></span>
<div class="details collapse" id="details-213">
<em>1</em>
</div>



<a name="TextEditorLineNumbersStyle.Relative"></a><span class="ts" id=214 data-target="#details-214" data-toggle="collapse"><span class="ident">Relative</span></span>
<div class="details collapse" id="details-214">
<em>2</em>
</div>

### <a name="TextEditorOptions"></a><span class="code-item" id=215>TextEditorOptions</span>



<div class="comment"><p><a href="#TextEditor">テキストエディタ</a>の<a href="#TextEditor.options">options</a>を表します。</p>
</div>

#### Properties



<a name="TextEditorOptions.cursorStyle"></a><span class="ts" id=218 data-target="#details-218" data-toggle="collapse"><span class="ident">cursorStyle</span><span>?</span><span>: </span><a class="type-ref" href="#TextEditorCursorStyle">TextEditorCursorStyle</a></span>
<div class="details collapse" id="details-218">
<div class="comment"><p>このエディターでのカーソルのレンダリングスタイル。
テキストエディタのオプションを取得するとき、このプロパティは常に存在します。
テキストエディタのオプションを設定する場合、このプロパティはオプションです。</p>
</div>
</div>



<a name="TextEditorOptions.insertSpaces"></a><span class="ts" id=217 data-target="#details-217" data-toggle="collapse"><span class="ident">insertSpaces</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a> &#124; <a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-217">
<div class="comment"><p>Tabを押すと<a href="#TextEditorOptions.tabSize">n</a>個のスペースが挿入されます。
テキストエディタのオプションを取得すると、このプロパティは常にブール値(解決済み)になります。
テキストエディタのオプションを設定する場合、このプロパティはオプションでブール値または <code>` auto &#39;</code>にすることができます。</p>
</div>
</div>



<a name="TextEditorOptions.lineNumbers"></a><span class="ts" id=219 data-target="#details-219" data-toggle="collapse"><span class="ident">lineNumbers</span><span>?</span><span>: </span><a class="type-ref" href="#TextEditorLineNumbersStyle">TextEditorLineNumbersStyle</a></span>
<div class="details collapse" id="details-219">
<div class="comment"><p>相対線番号w.r.tをレンダリングします。
現在の行番号 テキストエディタのオプションを取得するとき、このプロパティは常に存在します。
テキストエディタのオプションを設定する場合、このプロパティはオプションです。</p>
</div>
</div>



<a name="TextEditorOptions.tabSize"></a><span class="ts" id=216 data-target="#details-216" data-toggle="collapse"><span class="ident">tabSize</span><span>?</span><span>: </span><a class="type-instrinct">number</a> &#124; <a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-216">
<div class="comment"><p>タブにかかるスペースのサイズ。
これは2つの目的のために使用されます： - タブ文字の描画幅。</p>
<ul>
<li><a href="#TextEditorOptions.insertSpaces">insertSpaces</a>がtrueのときに挿入するスペースの数。</li>
</ul>
<p>テキストエディタのオプションを取得すると、このプロパティは常に数値(解決済み)になります。
テキストエディタのオプションを設定する場合、このプロパティはオプションであり、数値または <code>` auto &#39;</code>にすることができます。</p>
</div>
</div>

### <a name="TextEditorOptionsChangeEvent"></a><span class="code-item" id=198>TextEditorOptionsChangeEvent</span>



<div class="comment"><p><a href="#TextEditor.options">テキストエディタのオプション</a>の変更を説明するイベントを表します。</p>
</div>

#### Properties



<a name="TextEditorOptionsChangeEvent.options"></a><span class="ts" id=200 data-target="#details-200" data-toggle="collapse"><span class="ident">options</span><span>: </span><a class="type-ref" href="#TextEditorOptions">TextEditorOptions</a></span>
<div class="details collapse" id="details-200">
<div class="comment"><p><a href="#TextEditor.options">テキストエディタのオプション</a>の新しい値。</p>
</div>
</div>



<a name="TextEditorOptionsChangeEvent.textEditor"></a><span class="ts" id=199 data-target="#details-199" data-toggle="collapse"><span class="ident">textEditor</span><span>: </span><a class="type-ref" href="#TextEditor">TextEditor</a></span>
<div class="details collapse" id="details-199">
<div class="comment"><p>オプションが変更された<a href="#TextEditor">テキストエディタ</a>。</p>
</div>
</div>

### <a name="TextEditorRevealType"></a><span class="code-item" id=224>TextEditorRevealType</span>



<div class="comment"><p>異なる<a href="#TextEditor.revealRange">reveal</a>戦略をテキストエディタで表します。</p>
</div>

#### Enumeration members



<a name="TextEditorRevealType.AtTop"></a><span class="ts" id=228 data-target="#details-228" data-toggle="collapse"><span class="ident">AtTop</span></span>
<div class="details collapse" id="details-228">
<em>3</em>
</div>



<a name="TextEditorRevealType.Default"></a><span class="ts" id=225 data-target="#details-225" data-toggle="collapse"><span class="ident">Default</span></span>
<div class="details collapse" id="details-225">
<em>0</em>
</div>



<a name="TextEditorRevealType.InCenter"></a><span class="ts" id=226 data-target="#details-226" data-toggle="collapse"><span class="ident">InCenter</span></span>
<div class="details collapse" id="details-226">
<em>1</em>
</div>



<a name="TextEditorRevealType.InCenterIfOutsideViewport"></a><span class="ts" id=227 data-target="#details-227" data-toggle="collapse"><span class="ident">InCenterIfOutsideViewport</span></span>
<div class="details collapse" id="details-227">
<em>2</em>
</div>

### <a name="TextEditorSelectionChangeEvent"></a><span class="code-item" id=194>TextEditorSelectionChangeEvent</span>



<div class="comment"><p><a href="#TextEditor.selections">テキストエディタの選択</a>の変更を説明するイベントを表します。</p>
</div>

#### Properties



<a name="TextEditorSelectionChangeEvent.kind"></a><span class="ts" id=197 data-target="#details-197" data-toggle="collapse"><span class="ident">kind</span><span>?</span><span>: </span><a class="type-ref" href="#TextEditorSelectionChangeKind">TextEditorSelectionChangeKind</a></span>
<div class="details collapse" id="details-197">
<div class="comment"><p>このイベントを発生させた<a href="#TextEditorSelectionChangeKind">種別の変更</a>。
`undefined &#39;にすることができます。</p>
</div>
</div>



<a name="TextEditorSelectionChangeEvent.selections"></a><span class="ts" id=196 data-target="#details-196" data-toggle="collapse"><span class="ident">selections</span><span>: </span><a class="type-ref" href="#Selection">Selection</a>[]</span>
<div class="details collapse" id="details-196">
<div class="comment"><p>[テキストエディタの選択]の新しい値(#TextEditor.selections)。</p>
</div>
</div>



<a name="TextEditorSelectionChangeEvent.textEditor"></a><span class="ts" id=195 data-target="#details-195" data-toggle="collapse"><span class="ident">textEditor</span><span>: </span><a class="type-ref" href="#TextEditor">TextEditor</a></span>
<div class="details collapse" id="details-195">
<div class="comment"><p>選択が変更された<a href="#TextEditor">テキストエディタ</a>。</p>
</div>
</div>

### <a name="TextEditorSelectionChangeKind"></a><span class="code-item" id=190>TextEditorSelectionChangeKind</span>



<div class="comment"><p><a href="#window.onDidChangeTextEditorSelection">select change events</a>を引き起こす可能性があるソースを表します。</p>
</div>

#### Enumeration members



<a name="TextEditorSelectionChangeKind.Command"></a><span class="ts" id=193 data-target="#details-193" data-toggle="collapse"><span class="ident">Command</span></span>
<div class="details collapse" id="details-193">
<em>3</em>
</div>



<a name="TextEditorSelectionChangeKind.Keyboard"></a><span class="ts" id=191 data-target="#details-191" data-toggle="collapse"><span class="ident">Keyboard</span></span>
<div class="details collapse" id="details-191">
<em>1</em>
</div>



<a name="TextEditorSelectionChangeKind.Mouse"></a><span class="ts" id=192 data-target="#details-192" data-toggle="collapse"><span class="ident">Mouse</span></span>
<div class="details collapse" id="details-192">
<em>2</em>
</div>

### <a name="TextEditorViewColumnChangeEvent"></a><span class="code-item" id=201>TextEditorViewColumnChangeEvent</span>



<div class="comment"><p><a href="#TextEditor.viewColumn">テキストエディタのビュー列</a>の変更を説明するイベントを表します。</p>
</div>

#### Properties



<a name="TextEditorViewColumnChangeEvent.textEditor"></a><span class="ts" id=202 data-target="#details-202" data-toggle="collapse"><span class="ident">textEditor</span><span>: </span><a class="type-ref" href="#TextEditor">TextEditor</a></span>
<div class="details collapse" id="details-202">
<div class="comment"><p>オプションが変更された<a href="#TextEditor">テキストエディタ</a>。</p>
</div>
</div>



<a name="TextEditorViewColumnChangeEvent.viewColumn"></a><span class="ts" id=203 data-target="#details-203" data-toggle="collapse"><span class="ident">viewColumn</span><span>: </span><a class="type-ref" href="#ViewColumn">ViewColumn</a></span>
<div class="details collapse" id="details-203">
<div class="comment"><p><a href="#TextEditor.viewColumn">テキストエディタのビュー列</a>の新しい値。</p>
</div>
</div>

### <a name="TextLine"></a><span class="code-item" id=31>TextLine</span>



<div class="comment"><p>ソースコードなどのテキスト行を表します。</p>
<p>TextLineオブジェクトは<strong>immutable</strong>です。
<a href="#TextDocument">document</a> が変更されると、以前に取得された行は最新の状態を表しません。</p>
</div>

#### Properties



<a name="TextLine.firstNonWhitespaceCharacterIndex"></a><span class="ts" id=36 data-target="#details-36" data-toggle="collapse"><span class="ident">firstNonWhitespaceCharacterIndex</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-36">
<div class="comment"><p><code>/\s/</code> で定義された空白文字ではない最初の文字のオフセット。
<strong>注</strong> 行がすべて空白の場合、行の長さが返されます。</p>
</div>
</div>



<a name="TextLine.isEmptyOrWhitespace"></a><span class="ts" id=37 data-target="#details-37" data-toggle="collapse"><span class="ident">isEmptyOrWhitespace</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-37">
<div class="comment"><p>この行が空白であるかどうかは、 <a href="#TextLine.firstNonWhitespaceCharacterIndex">TextLine.firstNonWhitespaceCharacterIndex</a> === <a href="#TextLine.text">TextLine.text.length</a> の省略形です。</p>
</div>
</div>



<a name="TextLine.lineNumber"></a><span class="ts" id=32 data-target="#details-32" data-toggle="collapse"><span class="ident">lineNumber</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-32">
<div class="comment"><p>0から始まる行番号。</p>
</div>
</div>



<a name="TextLine.range"></a><span class="ts" id=34 data-target="#details-34" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-34">
<div class="comment"><p>この行は、行区切り文字なしの範囲です。</p>
</div>
</div>



<a name="TextLine.rangeIncludingLineBreak"></a><span class="ts" id=35 data-target="#details-35" data-toggle="collapse"><span class="ident">rangeIncludingLineBreak</span><span>: </span><a class="type-ref" href="#Range">Range</a></span>
<div class="details collapse" id="details-35">
<div class="comment"><p>この行の範囲は行区切り文字でカバーされます。</p>
</div>
</div>



<a name="TextLine.text"></a><span class="ts" id=33 data-target="#details-33" data-toggle="collapse"><span class="ident">text</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-33">
<div class="comment"><p>行区切り文字のないこの行のテキスト。</p>
</div>
</div>

### <a name="ThemableDecorationAttachmentRenderOptions"></a><span class="code-item" id=268>ThemableDecorationAttachmentRenderOptions</span>



<div class="comment"></div>

#### Properties



<a name="ThemableDecorationAttachmentRenderOptions.backgroundColor"></a><span class="ts" id=275 data-target="#details-275" data-toggle="collapse"><span class="ident">backgroundColor</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-275">
<div class="comment"><p>デコレーション添付ファイルに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationAttachmentRenderOptions.border"></a><span class="ts" id=271 data-target="#details-271" data-toggle="collapse"><span class="ident">border</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-271">
<div class="comment"><p>デコレーション添付ファイルに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationAttachmentRenderOptions.borderColor"></a><span class="ts" id=272 data-target="#details-272" data-toggle="collapse"><span class="ident">borderColor</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-272">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationAttachmentRenderOptions.color"></a><span class="ts" id=274 data-target="#details-274" data-toggle="collapse"><span class="ident">color</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-274">
<div class="comment"><p>デコレーション添付ファイルに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationAttachmentRenderOptions.contentIconPath"></a><span class="ts" id=270 data-target="#details-270" data-toggle="collapse"><span class="ident">contentIconPath</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-270">
<div class="comment"><p>絶対パス**または添付ファイルにレンダリングされる画像のURI。
アイコンまたはテキストのいずれかを表示できますが、両方を表示することはできません。</p>
</div>
</div>



<a name="ThemableDecorationAttachmentRenderOptions.contentText"></a><span class="ts" id=269 data-target="#details-269" data-toggle="collapse"><span class="ident">contentText</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-269">
<div class="comment"><p>添付ファイルに表示されるテキストコンテンツを定義します。
アイコンまたはテキストのいずれかを表示できますが、両方を表示することはできません。</p>
</div>
</div>



<a name="ThemableDecorationAttachmentRenderOptions.height"></a><span class="ts" id=278 data-target="#details-278" data-toggle="collapse"><span class="ident">height</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-278">
<div class="comment"><p>デコレーション添付ファイルに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationAttachmentRenderOptions.margin"></a><span class="ts" id=276 data-target="#details-276" data-toggle="collapse"><span class="ident">margin</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-276">
<div class="comment"><p>デコレーション添付ファイルに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationAttachmentRenderOptions.textDecoration"></a><span class="ts" id=273 data-target="#details-273" data-toggle="collapse"><span class="ident">textDecoration</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-273">
<div class="comment"><p>デコレーション添付ファイルに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationAttachmentRenderOptions.width"></a><span class="ts" id=277 data-target="#details-277" data-toggle="collapse"><span class="ident">width</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-277">
<div class="comment"><p>デコレーション添付ファイルに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>

### <a name="ThemableDecorationInstanceRenderOptions"></a><span class="code-item" id=309>ThemableDecorationInstanceRenderOptions</span>



<div class="comment"></div>

#### Properties



<a name="ThemableDecorationInstanceRenderOptions.after"></a><span class="ts" id=311 data-target="#details-311" data-toggle="collapse"><span class="ident">after</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationAttachmentRenderOptions">ThemableDecorationAttachmentRenderOptions</a></span>
<div class="details collapse" id="details-311">
<div class="comment"><p>装飾されたテキストの後に挿入される添付ファイルのレンダリングオプションを定義します</p>
</div>
</div>



<a name="ThemableDecorationInstanceRenderOptions.before"></a><span class="ts" id=310 data-target="#details-310" data-toggle="collapse"><span class="ident">before</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationAttachmentRenderOptions">ThemableDecorationAttachmentRenderOptions</a></span>
<div class="details collapse" id="details-310">
<div class="comment"><p>装飾されたテキストの前に挿入される添付ファイルのレンダリングオプションを定義します</p>
</div>
</div>

### <a name="ThemableDecorationRenderOptions"></a><span class="code-item" id=247>ThemableDecorationRenderOptions</span>



<div class="comment"><p><a href="#TextEditorDecorationType">テキストエディタの装飾</a>のテーマ固有のレンダリングスタイルを表します。</p>
</div>

#### Properties



<a name="ThemableDecorationRenderOptions.after"></a><span class="ts" id=267 data-target="#details-267" data-toggle="collapse"><span class="ident">after</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationAttachmentRenderOptions">ThemableDecorationAttachmentRenderOptions</a></span>
<div class="details collapse" id="details-267">
<div class="comment"><p>装飾されたテキストの後に挿入される添付ファイルのレンダリングオプションを定義します</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.backgroundColor"></a><span class="ts" id=248 data-target="#details-248" data-toggle="collapse"><span class="ident">backgroundColor</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-248">
<div class="comment"><p>装飾の背景色。
rgba()を使用し、透明な背景色を定義して他の装飾とうまくやります。
代替的に、カラーレジストリの色が参照されます(#ColorIdentifier)。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.before"></a><span class="ts" id=266 data-target="#details-266" data-toggle="collapse"><span class="ident">before</span><span>?</span><span>: </span><a class="type-ref" href="#ThemableDecorationAttachmentRenderOptions">ThemableDecorationAttachmentRenderOptions</a></span>
<div class="details collapse" id="details-266">
<div class="comment"><p>装飾されたテキストの前に挿入される添付ファイルのレンダリングオプションを定義します</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.border"></a><span class="ts" id=253 data-target="#details-253" data-toggle="collapse"><span class="ident">border</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-253">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.borderColor"></a><span class="ts" id=254 data-target="#details-254" data-toggle="collapse"><span class="ident">borderColor</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-254">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々の境界線のプロパティを設定するために、「境界線」を使用する方が効果的です。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.borderRadius"></a><span class="ts" id=255 data-target="#details-255" data-toggle="collapse"><span class="ident">borderRadius</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-255">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々の境界線のプロパティを設定するために、「境界線」を使用する方が効果的です。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.borderSpacing"></a><span class="ts" id=256 data-target="#details-256" data-toggle="collapse"><span class="ident">borderSpacing</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-256">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々の境界線のプロパティを設定するために、「境界線」を使用する方が効果的です。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.borderStyle"></a><span class="ts" id=257 data-target="#details-257" data-toggle="collapse"><span class="ident">borderStyle</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-257">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々の境界線のプロパティを設定するために、「境界線」を使用する方が効果的です。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.borderWidth"></a><span class="ts" id=258 data-target="#details-258" data-toggle="collapse"><span class="ident">borderWidth</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-258">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々の境界線のプロパティを設定するために、「境界線」を使用する方が効果的です。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.color"></a><span class="ts" id=261 data-target="#details-261" data-toggle="collapse"><span class="ident">color</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-261">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.cursor"></a><span class="ts" id=260 data-target="#details-260" data-toggle="collapse"><span class="ident">cursor</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-260">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.gutterIconPath"></a><span class="ts" id=263 data-target="#details-263" data-toggle="collapse"><span class="ident">gutterIconPath</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-263">
<div class="comment"><p><strong>絶対パス</strong>またはガターにレンダリングされる画像へのURI。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.gutterIconSize"></a><span class="ts" id=264 data-target="#details-264" data-toggle="collapse"><span class="ident">gutterIconSize</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-264">
<div class="comment"><p>ガターアイコンのサイズを指定します。
使用可能な値は &#39;auto&#39;、 &#39;contains&#39;、 &#39;cover&#39;および任意のパーセント値です。
詳細は<a href="https://msdn.microsoft.com/en-us/library/jj127316(v=vs.85).aspxを参照してください。">https://msdn.microsoft.com/en-us/library/jj127316(v=vs.85).aspxを参照してください。</a></p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.letterSpacing"></a><span class="ts" id=262 data-target="#details-262" data-toggle="collapse"><span class="ident">letterSpacing</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-262">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.outline"></a><span class="ts" id=249 data-target="#details-249" data-toggle="collapse"><span class="ident">outline</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-249">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.outlineColor"></a><span class="ts" id=250 data-target="#details-250" data-toggle="collapse"><span class="ident">outlineColor</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-250">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々のアウトラインプロパティを設定する場合は、「アウトライン」を使用する方が効果的です。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.outlineStyle"></a><span class="ts" id=251 data-target="#details-251" data-toggle="collapse"><span class="ident">outlineStyle</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-251">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々のアウトラインプロパティを設定する場合は、「アウトライン」を使用する方が効果的です。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.outlineWidth"></a><span class="ts" id=252 data-target="#details-252" data-toggle="collapse"><span class="ident">outlineWidth</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-252">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。
1つ以上の個々のアウトラインプロパティを設定する場合は、「アウトライン」を使用する方が効果的です。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.overviewRulerColor"></a><span class="ts" id=265 data-target="#details-265" data-toggle="collapse"><span class="ident">overviewRulerColor</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-265">
<div class="comment"><p>概観ルーラーの装飾の色。
rgba()を使用し、透明な色を定義して他の装飾とうまく合わせます。</p>
</div>
</div>



<a name="ThemableDecorationRenderOptions.textDecoration"></a><span class="ts" id=259 data-target="#details-259" data-toggle="collapse"><span class="ident">textDecoration</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-259">
<div class="comment"><p>デコレーションで囲まれたテキストに適用されるCSSスタイリングプロパティ。</p>
</div>
</div>

### <a name="ThemeColor"></a><span class="code-item" id=243>ThemeColor</span>



<div class="comment"><p><a href="https://code.visualstudio.com/docs/getstarted/theme-color-referenceに定義されているワークベンチ色のいずれかへの参照。">https://code.visualstudio.com/docs/getstarted/theme-color-referenceに定義されているワークベンチ色のいずれかへの参照。</a>
テーマの色を使用することは、テーマの作者とユーザーに色を変更する可能性があるため、カスタム色よりも優先されます。</p>
</div>

#### Constructors



<a name="ThemeColor.new ThemeColor"></a><span class="ts" id=245 data-target="#details-245" data-toggle="collapse"><span class="ident">new ThemeColor</span><span>(</span><span class="ident">id</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#ThemeColor">ThemeColor</a></span>
<div class="details collapse" id="details-245">
<div class="comment"><p>テーマカラーへの参照を作成します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="id"></a><span class="ts" id=246 data-target="#details-246" data-toggle="collapse"><span class="ident">id</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ThemeColor">ThemeColor</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="TreeDataProvider"></a><span class="code-item" id=1063>TreeDataProvider&lt;T&gt;</span>



<div class="comment"><p>ツリーデータを提供するデータプロバイダ</p>
</div>

#### Events



<a name="TreeDataProvider.onDidChangeTreeData"></a><span class="ts" id=1065 data-target="#details-1065" data-toggle="collapse"><span class="ident">onDidChangeTreeData</span><span>?</span><span>: </span><a class="type-ref" href="#Event">Event</a>&lt;<a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a> &#124; <a class="type-instrinct">null</a>&gt;</span>
<div class="details collapse" id="details-1065">
<div class="comment"><p>要素またはルートが変更されたことを通知するオプションのイベント。
ルートが変更されたことを通知するには、引数を渡さないか、 <code>undefined</code> または <code>null</code> を渡してください。</p>
</div>
</div>

#### Methods



<a name="TreeDataProvider.getChildren"></a><span class="ts" id=1070 data-target="#details-1070" data-toggle="collapse"><span class="ident">getChildren</span><span>(</span><span class="ident">element</span><span>?</span><span>: </span><a class="type-instrinct">T</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-1070">
<div class="comment"><p>要素が渡されない場合、 <code>element</code> の子を取得するか、ルートを取得します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="element"></a><span class="ts" id=1071 data-target="#details-1071" data-toggle="collapse"><span class="ident">element</span><span>?</span><span>: </span><a class="type-instrinct">T</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>要素が渡されない場合、 <code>element</code> の子要素またはルート。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="TreeDataProvider.getTreeItem"></a><span class="ts" id=1067 data-target="#details-1067" data-toggle="collapse"><span class="ident">getTreeItem</span><span>(</span><span class="ident">element</span><span>: </span><a class="type-instrinct">T</a><span>)</span><span>: </span><a class="type-ref" href="#TreeItem">TreeItem</a> &#124; <a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TreeItem">TreeItem</a>&gt;</span>
<div class="details collapse" id="details-1067">
<div class="comment"><p>[要素]の<a href="#TreeItem">TreeItem</a>表現を取得する</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="element"></a><span class="ts" id=1068 data-target="#details-1068" data-toggle="collapse"><span class="ident">element</span><span>: </span><a class="type-instrinct">T</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#TreeItem">TreeItem</a> &#124; <a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-ref" href="#TreeItem">TreeItem</a>&gt;</span></td><td><div class="comment"><p>(#TreeItem)要素の表現</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="TreeItem"></a><span class="code-item" id=1072>TreeItem</span>



<div class="comment"></div>

#### Constructors



<a name="TreeItem.new TreeItem"></a><span class="ts" id=1082 data-target="#details-1082" data-toggle="collapse"><span class="ident">new TreeItem</span><span>(</span><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">collapsibleState</span><span>?</span><span>: </span><a class="type-ref" href="#TreeItemCollapsibleState">TreeItemCollapsibleState</a><span>)</span><span>: </span><a class="type-ref" href="#TreeItem">TreeItem</a></span>
<div class="details collapse" id="details-1082">
<div class="comment"></div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="label"></a><span class="ts" id=1083 data-target="#details-1083" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="collapsibleState"></a><span class="ts" id=1084 data-target="#details-1084" data-toggle="collapse"><span class="ident">collapsibleState</span><span>?</span><span>: </span><a class="type-ref" href="#TreeItemCollapsibleState">TreeItemCollapsibleState</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#TreeItem">TreeItem</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="TreeItem.collapsibleState"></a><span class="ts" id=1079 data-target="#details-1079" data-toggle="collapse"><span class="ident">collapsibleState</span><span>?</span><span>: </span><a class="type-ref" href="#TreeItemCollapsibleState">TreeItemCollapsibleState</a></span>
<div class="details collapse" id="details-1079">
<div class="comment"><p>ツリーアイテムの<a href="#TreeItemCollapsibleState">TreeItemCollapsibleState</a>。</p>
</div>
</div>



<a name="TreeItem.command"></a><span class="ts" id=1078 data-target="#details-1078" data-toggle="collapse"><span class="ident">command</span><span>?</span><span>: </span><a class="type-ref" href="#Command">Command</a></span>
<div class="details collapse" id="details-1078">
<div class="comment"><p>ツリー項目が選択されたときに実行される<a href="#コマンド">command</a>。</p>
</div>
</div>



<a name="TreeItem.contextValue"></a><span class="ts" id=1080 data-target="#details-1080" data-toggle="collapse"><span class="ident">contextValue</span><span>?</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1080">
<div class="comment"><p>ツリー項目のコンテキスト値。
これは、ツリー内のアイテム固有のアクションに貢献するために使用できます。
例えば、ツリー項目には <code>folder</code> というコンテキスト値が与えられます。</p>
<p><code>view / item / context</code> にアクションを提供するとき
<code>menus</code> 拡張ポイントを使うと <code>viewItem == folder</code> のような <code>when</code> 式のキー <code>viewItem</code> のコンテキスト値を指定することができます。</p>

<pre><code><span class="hljs-string">"貢献する"</span>：{
<span class="hljs-string">"メニュー"</span>：{
<span class="hljs-string">"ビュー/アイテム/コンテキスト"</span>：[
{
<span class="hljs-string">"command"</span>： <span class="hljs-string">"extension.deleteFolder"</span>、
<span class="hljs-string">"when"</span>： <span class="hljs-string">"viewItem == folder"</span>
}
]
}
}
</code></pre><p>これは <code>contextValue</code> が <code>folder</code> であるアイテムに対してのみ <code>extension.deleteFolder</code> アクションを表示します。</p>
</div>
</div>



<a name="TreeItem.iconPath"></a><span class="ts" id=1074 data-target="#details-1074" data-toggle="collapse"><span class="ident">iconPath</span><span>?</span><span>: </span><a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#Uri">Uri</a> &#124; {dark: <a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#Uri">Uri</a>, light: <a class="type-instrinct">string</a> &#124; <a class="type-ref" href="#Uri">Uri</a>}</span>
<div class="details collapse" id="details-1074">
<div class="comment"><p>ツリー項目のアイコンパス</p>
</div>
</div>



<a name="TreeItem.label"></a><span class="ts" id=1073 data-target="#details-1073" data-toggle="collapse"><span class="ident">label</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-1073">
<div class="comment"><p>この項目を説明する人間が読める文字列</p>
</div>
</div>

### <a name="TreeItemCollapsibleState"></a><span class="code-item" id=1085>TreeItemCollapsibleState</span>



<div class="comment"><p>ツリー項目の折りたたみ可能な状態</p>
</div>

#### Enumeration members



<a name="TreeItemCollapsibleState.Collapsed"></a><span class="ts" id=1087 data-target="#details-1087" data-toggle="collapse"><span class="ident">Collapsed</span></span>
<div class="details collapse" id="details-1087">
<em>1</em>
</div>



<a name="TreeItemCollapsibleState.Expanded"></a><span class="ts" id=1088 data-target="#details-1088" data-toggle="collapse"><span class="ident">Expanded</span></span>
<div class="details collapse" id="details-1088">
<em>2</em>
</div>



<a name="TreeItemCollapsibleState.None"></a><span class="ts" id=1086 data-target="#details-1086" data-toggle="collapse"><span class="ident">None</span></span>
<div class="details collapse" id="details-1086">
<em>0</em>
</div>

### <a name="TypeDefinitionProvider"></a><span class="code-item" id=534>TypeDefinitionProvider</span>



<div class="comment"><p>型定義プロバイダは、拡張と型定義機能への移動の間のコントラクトを定義します。</p>
</div>

#### Methods



<a name="TypeDefinitionProvider.provideTypeDefinition"></a><span class="ts" id=536 data-target="#details-536" data-toggle="collapse"><span class="ident">provideTypeDefinition</span><span>(</span><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a>, <span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-536">
<div class="comment"><p>指定された位置とドキュメントでシンボルの型定義を提供する。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="document"></a><span class="ts" id=537 data-target="#details-537" data-toggle="collapse"><span class="ident">document</span><span>: </span><a class="type-ref" href="#TextDocument">TextDocument</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="position"></a><span class="ts" id=538 data-target="#details-538" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=539 data-target="#details-539" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>このように解決される定義または変換可能なテーブル。
結果の不足は、 <code>undefined</code> または <code>null</code> を返すことで通知できます。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="Uri"></a><span class="code-item" id=372>Uri</span>



<div class="comment"><p>ディスク上のファイルまたは無題リソースのような別のリソースを表すユニバーサルリソース識別子。</p>
</div>

#### Static



<a name="Uri.file"></a><span class="ts" id=374 data-target="#details-374" data-toggle="collapse"><span class="ident">file</span><span>(</span><span class="ident">path</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-374">
<div class="comment"><p>ファイルシステムパスからURIを作成します。
<a href="#Uri.scheme">スキーム</a> は <code>file</code> になります。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="path"></a><span class="ts" id=375 data-target="#details-375" data-toggle="collapse"><span class="ident">path</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"><p>新しいUriインスタンス。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Uri.parse"></a><span class="ts" id=377 data-target="#details-377" data-toggle="collapse"><span class="ident">parse</span><span>(</span><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-377">
<div class="comment"><p>文字列からURIを作成する。与えられた値がそうでない場合にスローします。
有効です。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="value"></a><span class="ts" id=378 data-target="#details-378" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"><p>Uriの文字列値。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"><p>新しいUriインスタンス。</p>
</div></td></tr>
</table>
</div>
</div>

#### Properties



<a name="Uri.authority"></a><span class="ts" id=380 data-target="#details-380" data-toggle="collapse"><span class="ident">authority</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-380">
<div class="comment"><p>権限は <code>http：//www.msft.com/some/path？query#fragment</code> の <code>www.msft.com</code> の部分です。
最初の二重スラッシュと次のスラッシュの間の部分。</p>
</div>
</div>



<a name="Uri.fragment"></a><span class="ts" id=383 data-target="#details-383" data-toggle="collapse"><span class="ident">fragment</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-383">
<div class="comment"><p>Fragmentは <code>http：//www.msft.com/some/path？query#fragment</code> の <code>fragment</code> 部分です。</p>
</div>
</div>



<a name="Uri.fsPath"></a><span class="ts" id=384 data-target="#details-384" data-toggle="collapse"><span class="ident">fsPath</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-384">
<div class="comment"><p>このUriの対応するファイルシステムパスを表す文字列。</p>
<p>UNCパスを処理し、Windowsのドライブ文字を小文字に正規化します。
プラットフォーム固有のパス区切り文字も使用します。
無効な文字とセマンティクスのパスを検証しません。
このウリの計画を見ない<em> </em>。</p>
</div>
</div>



<a name="Uri.path"></a><span class="ts" id=381 data-target="#details-381" data-toggle="collapse"><span class="ident">path</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-381">
<div class="comment"><p>Pathは <code>http：//www.msft.com/some/path？query#fragment</code> の <code>/ some / path</code> 部分です。</p>
</div>
</div>



<a name="Uri.query"></a><span class="ts" id=382 data-target="#details-382" data-toggle="collapse"><span class="ident">query</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-382">
<div class="comment"><p>クエリは <code>http：//www.msft.com/some/path？query#fragment</code> の <code>query</code> 部分です。</p>
</div>
</div>



<a name="Uri.scheme"></a><span class="ts" id=379 data-target="#details-379" data-toggle="collapse"><span class="ident">scheme</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-379">
<div class="comment"><p>Schemeは <code>http://www.msft.com/some/path?query#fragment</code> の <code>http</code> 部分です。
最初のコロンの前の部分。</p>
</div>
</div>

#### Methods



<a name="Uri.toJSON"></a><span class="ts" id=398 data-target="#details-398" data-toggle="collapse"><span class="ident">toJSON</span><span>(</span><span>)</span><span>: </span><a class="type-instrinct">any</a></span>
<div class="details collapse" id="details-398">
<div class="comment"><p>このUriのJSON表現を返します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">any</a></span></td><td><div class="comment"><p>オブジェクトです。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Uri.toString"></a><span class="ts" id=395 data-target="#details-395" data-toggle="collapse"><span class="ident">toString</span><span>(</span><span class="ident">skipEncoding</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a><span>)</span><span>: </span><a class="type-instrinct">string</a></span>
<div class="details collapse" id="details-395">
<div class="comment"><p>このUriの文字列表現を返します。
URIの表現と正規化はスキームに依存します。
結果の文字列は、
<a href="#Uri.parse">Uri.parse</a>。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="skipEncoding"></a><span class="ts" id=396 data-target="#details-396" data-toggle="collapse"><span class="ident">skipEncoding</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">string</a></span></td><td><div class="comment"><p>このUriの文字列表現。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="Uri.with"></a><span class="ts" id=386 data-target="#details-386" data-toggle="collapse"><span class="ident">with</span><span>(</span><span class="ident">change</span><span>: </span>{authority: <a class="type-instrinct">string</a>, fragment: <a class="type-instrinct">string</a>, path: <a class="type-instrinct">string</a>, query: <a class="type-instrinct">string</a>, scheme: <a class="type-instrinct">string</a>}<span>)</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span>
<div class="details collapse" id="details-386">
<div class="comment"><p>このUri から新しい Uri を得る。</p>

<pre><code class="lang-ts"><span class="hljs-keyword">let</span> file = Uri.parse(<span class="hljs-string">'before:some/file/path'</span>);
<span class="hljs-keyword">let</span> other = file.with({ scheme: <span class="hljs-string">'after'</span> });
assert.ok(other.toString() === <span class="hljs-string">'after:some/file/path'</span>);
</code></pre>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="change"></a><span class="ts" id=387 data-target="#details-387" data-toggle="collapse"><span class="ident">change</span><span>: </span>{authority: <a class="type-instrinct">string</a>, fragment: <a class="type-instrinct">string</a>, path: <a class="type-instrinct">string</a>, query: <a class="type-instrinct">string</a>, scheme: <a class="type-instrinct">string</a>}</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"><p>指定された変更を反映する新しいUri。
変更があれば <code>this</code> を返す 何も変えていない。</p>
</div></td></tr>
</table>
</div>
</div>

### <a name="ViewColumn"></a><span class="code-item" id=970>ViewColumn</span>



<div class="comment"><p>はエディタウィンドウの列を示します。
列は、エディタを並べて表示するために使用されます。</p>
</div>

#### Enumeration members



<a name="ViewColumn.One"></a><span class="ts" id=971 data-target="#details-971" data-toggle="collapse"><span class="ident">One</span></span>
<div class="details collapse" id="details-971">
<em>1</em>
</div>



<a name="ViewColumn.Three"></a><span class="ts" id=973 data-target="#details-973" data-toggle="collapse"><span class="ident">Three</span></span>
<div class="details collapse" id="details-973">
<em>3</em>
</div>



<a name="ViewColumn.Two"></a><span class="ts" id=972 data-target="#details-972" data-toggle="collapse"><span class="ident">Two</span></span>
<div class="details collapse" id="details-972">
<em>2</em>
</div>

### <a name="WorkspaceConfiguration"></a><span class="code-item" id=889>WorkspaceConfiguration</span>



<div class="comment"><p>ワークスペース構成を表します。</p>
<p>ワークスペースの設定はマージされたビューです：現在の<a href="#workspace.rootPath">workspace</a>の設定 (利用可能な場合)、 <code>launch.json</code> のようなファイル、およびインストール全体の設定です。
ワークスペース固有の値はインストール全体の値をシャドウします。</p>
<p><em>注：</em>現在の<a href="#workspace.rootPath">workspace</a>のマージされた設定は、 には <code>launch.json</code> や <code>tasks.json</code> のようなファイルの設定も含まれています。
それらのベース名はセクション識別子の一部になります。
以下のスニペットは <code>launch.json</code> からすべての設定を取得する方法を示しています：</p>
<p>```ts</p>
</div>

#### Methods



<a name="WorkspaceConfiguration.get"></a><span class="ts" id=891 data-target="#details-891" data-toggle="collapse"><span class="ident">get</span><span>&lt;</span>T<span>&gt;</span><span>(</span><span class="ident">section</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-891">
<div class="comment"><p>この設定から値を返します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="section"></a><span class="ts" id=893 data-target="#details-893" data-toggle="collapse"><span class="ident">section</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">T</a> &#124; <a class="type-instrinct">undefined</a></span></td><td><div class="comment"><p>値 <code>section</code> は <code>undefined</code> を表します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="WorkspaceConfiguration.get"></a><span class="ts" id=894 data-target="#details-894" data-toggle="collapse"><span class="ident">get</span><span>&lt;</span>T<span>&gt;</span><span>(</span><span class="ident">section</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">defaultValue</span><span>: </span><a class="type-instrinct">T</a><span>)</span><span>: </span><a class="type-instrinct">T</a></span>
<div class="details collapse" id="details-894">
<div class="comment"><p>この設定から値を返します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="section"></a><span class="ts" id=896 data-target="#details-896" data-toggle="collapse"><span class="ident">section</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="defaultValue"></a><span class="ts" id=897 data-target="#details-897" data-toggle="collapse"><span class="ident">defaultValue</span><span>: </span><a class="type-instrinct">T</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">T</a></span></td><td><div class="comment"><p>値 <code>section</code> は、デフォルトまたはデフォルトを示します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="WorkspaceConfiguration.has"></a><span class="ts" id=899 data-target="#details-899" data-toggle="collapse"><span class="ident">has</span><span>(</span><span class="ident">section</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-899">
<div class="comment"><p>この設定に一定の値があるかどうか確認してください。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="section"></a><span class="ts" id=900 data-target="#details-900" data-toggle="collapse"><span class="ident">section</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>セクションが <code>undefined</code> に解決されない場合はtrueを返します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="WorkspaceConfiguration.inspect"></a><span class="ts" id=902 data-target="#details-902" data-toggle="collapse"><span class="ident">inspect</span><span>&lt;</span>T<span>&gt;</span><span>(</span><span class="ident">section</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span>{defaultValue: <a class="type-instrinct">T</a>, globalValue: <a class="type-instrinct">T</a>, key: <a class="type-instrinct">string</a>, workspaceValue: <a class="type-instrinct">T</a>} &#124; <a class="type-instrinct">undefined</a></span>
<div class="details collapse" id="details-902">
<div class="comment"><p>構成設定に関するすべての情報を取得します。
構成値は、<em>デフォルト</em>値、グローバルまたはインストール全体の値、および作業領域固有の値で構成されることがよくあります。
有効な値(<a href="#WorkspaceConfiguration.get"><code>get</code></a>によって返される)は、 <code>globalValue</code> によって上書きされる <code>defaultValue</code> のように計算されます。</p>
<p><code>globalValue</code> は <code>workspaceValue</code> によって上書きされます。</p>
<p><em>注：</em>設定名は設定ツリーの葉を示さなければなりません( <code>editor.fontSize</code> と <code>editor</code> )。そうでなければ結果は返されません。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="section"></a><span class="ts" id=904 data-target="#details-904" data-toggle="collapse"><span class="ident">section</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts">{defaultValue: <a class="type-instrinct">T</a>, globalValue: <a class="type-instrinct">T</a>, key: <a class="type-instrinct">string</a>, workspaceValue: <a class="type-instrinct">T</a>} &#124; <a class="type-instrinct">undefined</a></span></td><td><div class="comment"><p>構成設定または `未定義 &#39;に関する情報。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="WorkspaceConfiguration.update"></a><span class="ts" id=911 data-target="#details-911" data-toggle="collapse"><span class="ident">update</span><span>(</span><span class="ident">section</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">value</span><span>: </span><a class="type-instrinct">any</a>, <span class="ident">global</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a><span>)</span><span>: </span><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">void</a>&gt;</span>
<div class="details collapse" id="details-911">
<div class="comment"><p>設定値を更新する。
現在の値を変更することができます
<a href="#workspace.rootPath">workspace</a>のみ、またはエディタのすべてのインスタンスに対してグローバルに適用されます。
更新された設定値は保持されます。</p>
<p><em>注1：</em>特定のワークスペース値の存在下でインストール全体の値( <code>global：true</code> )を設定すると、そのワークスペースでは観測可能な効果はありません。</p>
<p>注2：*設定値を削除するには <code>undefined</code> を使います： <code>config.update( &#39;somekey&#39;、undefined)</code></p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="section"></a><span class="ts" id=912 data-target="#details-912" data-toggle="collapse"><span class="ident">section</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="value"></a><span class="ts" id=913 data-target="#details-913" data-toggle="collapse"><span class="ident">value</span><span>: </span><a class="type-instrinct">any</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="global"></a><span class="ts" id=914 data-target="#details-914" data-toggle="collapse"><span class="ident">global</span><span>?</span><span>: </span><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p><code>true</code> はエディタのすべてのインスタンスの設定値を変更します。</p>
</div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#Thenable">Thenable</a>&lt;<a class="type-instrinct">void</a>&gt;</span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="WorkspaceEdit"></a><span class="code-item" id=659>WorkspaceEdit</span>



<div class="comment"><p>ワークスペースの編集は、多くの文書のテキストの変更を表します。</p>
</div>

#### Properties



<a name="WorkspaceEdit.size"></a><span class="ts" id=660 data-target="#details-660" data-toggle="collapse"><span class="ident">size</span><span>: </span><a class="type-instrinct">number</a></span>
<div class="details collapse" id="details-660">
<div class="comment"><p>影響を受けるリソースの数。</p>
</div>
</div>

#### Methods



<a name="WorkspaceEdit.delete"></a><span class="ts" id=672 data-target="#details-672" data-toggle="collapse"><span class="ident">delete</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a>, <span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-672">
<div class="comment"><p>指定された範囲のテキストを削除します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=673 data-target="#details-673" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="range"></a><span class="ts" id=674 data-target="#details-674" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="WorkspaceEdit.entries"></a><span class="ts" id=686 data-target="#details-686" data-toggle="collapse"><span class="ident">entries</span><span>(</span><span>)</span><span>: </span>[<a class="type-ref" href="#Uri">Uri</a>, <a class="type-ref" href="#TextEdit">TextEdit</a>[]][]</span>
<div class="details collapse" id="details-686">
<div class="comment"><p>すべてのテキスト編集をリソース別にグループ化します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts">[<a class="type-ref" href="#Uri">Uri</a>, <a class="type-ref" href="#TextEdit">TextEdit</a>[]][]</span></td><td><div class="comment"><p><code>[Uri、TextEdit []]</code> - の組の配列です。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="WorkspaceEdit.get"></a><span class="ts" id=683 data-target="#details-683" data-toggle="collapse"><span class="ident">get</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a><span>)</span><span>: </span><a class="type-ref" href="#TextEdit">TextEdit</a>[]</span>
<div class="details collapse" id="details-683">
<div class="comment"><p>リソースのテキスト編集を取得します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=684 data-target="#details-684" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#TextEdit">TextEdit</a>[]</span></td><td><div class="comment"><p>テキスト編集の配列。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="WorkspaceEdit.has"></a><span class="ts" id=676 data-target="#details-676" data-toggle="collapse"><span class="ident">has</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a><span>)</span><span>: </span><a class="type-instrinct">boolean</a></span>
<div class="details collapse" id="details-676">
<div class="comment"><p>この編集が指定されたリソースに影響するかどうかを確認します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=677 data-target="#details-677" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">boolean</a></span></td><td><div class="comment"><p>指定されたリソースにこの編集が適用される場合はtrueを返します。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="WorkspaceEdit.insert"></a><span class="ts" id=667 data-target="#details-667" data-toggle="collapse"><span class="ident">insert</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a>, <span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a>, <span class="ident">newText</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-667">
<div class="comment"><p>与えられたテキストを指定された位置に挿入します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=668 data-target="#details-668" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="position"></a><span class="ts" id=669 data-target="#details-669" data-toggle="collapse"><span class="ident">position</span><span>: </span><a class="type-ref" href="#Position">Position</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="newText"></a><span class="ts" id=670 data-target="#details-670" data-toggle="collapse"><span class="ident">newText</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="WorkspaceEdit.replace"></a><span class="ts" id=662 data-target="#details-662" data-toggle="collapse"><span class="ident">replace</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a>, <span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a>, <span class="ident">newText</span><span>: </span><a class="type-instrinct">string</a><span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-662">
<div class="comment"><p>指定された範囲を、指定されたリソースのテキストで置き換えます。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=663 data-target="#details-663" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="range"></a><span class="ts" id=664 data-target="#details-664" data-toggle="collapse"><span class="ident">range</span><span>: </span><a class="type-ref" href="#Range">Range</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="newText"></a><span class="ts" id=665 data-target="#details-665" data-toggle="collapse"><span class="ident">newText</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>



<a name="WorkspaceEdit.set"></a><span class="ts" id=679 data-target="#details-679" data-toggle="collapse"><span class="ident">set</span><span>(</span><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a>, <span class="ident">edits</span><span>: </span><a class="type-ref" href="#TextEdit">TextEdit</a>[]<span>)</span><span>: </span><a class="type-instrinct">void</a></span>
<div class="details collapse" id="details-679">
<div class="comment"><p>リソースのテキスト編集を設定(および置き換え)します。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="uri"></a><span class="ts" id=680 data-target="#details-680" data-toggle="collapse"><span class="ident">uri</span><span>: </span><a class="type-ref" href="#Uri">Uri</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="edits"></a><span class="ts" id=681 data-target="#details-681" data-toggle="collapse"><span class="ident">edits</span><span>: </span><a class="type-ref" href="#TextEdit">TextEdit</a>[]</span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-instrinct">void</a></span></td><td><div class="comment"></div></td></tr>
</table>
</div>
</div>

### <a name="WorkspaceSymbolProvider"></a><span class="code-item" id=619>WorkspaceSymbolProvider</span>



<div class="comment"><p>ワークスペースシンボルプロバイダインタフェースは、拡張機能と<a href="https://code.visualstudio.com/docs/editor/editingevolved#_open-symbol-by-name">シンボル検索</a> - 機能の間の契約を定義します。</p>
</div>

#### Methods



<a name="WorkspaceSymbolProvider.provideWorkspaceSymbols"></a><span class="ts" id=621 data-target="#details-621" data-toggle="collapse"><span class="ident">provideWorkspaceSymbols</span><span>(</span><span class="ident">query</span><span>: </span><a class="type-instrinct">string</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-621">
<div class="comment"><p>指定されたクエリ文字列に一致するシンボルのプロジェクト全体の検索。
サブストリング、indexOfなどのように、クエリ文字列を検索する方法はプロバイダに依存します。
パフォーマンスの実装者を改善するために、シンボルの<a href="#SymbolInformation.location">location</a>をスキップして、それを行うために <code>resolveWorkspaceSymbol</code> を実装することができます
後で。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="query"></a><span class="ts" id=622 data-target="#details-622" data-toggle="collapse"><span class="ident">query</span><span>: </span><a class="type-instrinct">string</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=623 data-target="#details-623" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>ドキュメントハイライトの配列またはそのように解釈されるネーブル。
結果の欠如は、 <code>undefined</code> 、 <code>null</code> 、または空の配列を返すことによって通知できます。</p>
</div></td></tr>
</table>
</div>
</div>



<a name="WorkspaceSymbolProvider.resolveWorkspaceSymbol"></a><span class="ts" id=625 data-target="#details-625" data-toggle="collapse"><span class="ident">resolveWorkspaceSymbol</span><span>(</span><span class="ident">symbol</span><span>: </span><a class="type-ref" href="#SymbolInformation">SymbolInformation</a>, <span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a><span>)</span><span>: </span><a class="type-ref" href="#ProviderResult">ProviderResult</a></span>
<div class="details collapse" id="details-625">
<div class="comment"><p><a href="#SymbolInformation.location">location</a>にシンボルを記入してください。
このメソッドは、UIでシンボルが選択されるたびに呼び出されます。
プロバイダはこのメソッドを実装し、不完全なシンボルを返すことができます
<a href="#WorkspaceSymbolProvider.provideWorkspaceSymbols"><code>provideWorkspaceSymbols</code></a>改善に役立つことが多い
パフォーマンス。</p>
</div>
<div class="signature">
<table class="table table-bordered">
<tr><th>Parameter</th><th>Description</th></tr>
<tr><td><a name="symbol"></a><span class="ts" id=626 data-target="#details-626" data-toggle="collapse"><span class="ident">symbol</span><span>: </span><a class="type-ref" href="#SymbolInformation">SymbolInformation</a></span></td><td><div class="comment"></div></td></tr>
<tr><td><a name="token"></a><span class="ts" id=627 data-target="#details-627" data-toggle="collapse"><span class="ident">token</span><span>: </span><a class="type-ref" href="#CancellationToken">CancellationToken</a></span></td><td><div class="comment"></div></td></tr>
<tr><th>Returns</th><th>Description</th></tr>
<tr><td><span class="ts"><a class="type-ref" href="#ProviderResult">ProviderResult</a></span></td><td><div class="comment"><p>解決されたシンボルまたはそれを解決するネーブル。
結果が返ってこないときは、与えられた <code>symbol</code> が使われます。</p>
</div></td></tr>
</table>
</div>
</div>

