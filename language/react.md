
# 基本
HTMLとJavasscriptをセットにしてコンポーネントとして定義する。
仮想DOMという仕組みで、実際のDOMと比較して差分のHTMLだけを更新する。
コンポーネントはクラスとしての表現方法と関数としての表現方法がある。（現在は主に関数コンポーネント）
コンポーネントは見た目と機能を持ったUI部品
1コンポーネント1ファイルにして分ける
子コンポーネントでexportすることで、親コンポーネントでimportできるようになる。
親から子に引数として渡す値がprops
コンポーネントを責務を明確にして分けることで、再利用しやすく、修正しやすく管理できる。

ツールチェインを使わない create react app という方法がある。Babel,Webpackなど
npx create-react-app

Reactコンポーネントが再描画されるきっかけは、state,propsが変更されたとき。

* 関数コンポーネントはその性質上、状態や副作用を持てない。その欠点を補う形でHooksがある。

## マウント・アンマウント
コンポーネントがDOMに追加されることをマウント、削除されることをアンマウントという。

## props
親コンポーネントから受け取る属性（値）
親のstateを変更する必要があるなら、propsで子にイベントハンドラを渡す。

## state
コンポーネント内部で管理する状態（値）
フックによってstateが変更されると再レンダーされる。

コンポーネント単位に保持する状態変数。これがReactの仕組みにより更新された時、再レンダーが行われる。

## 画面設計
最初に画面を設計し、どんなコンポーネントで構成するか、何（値、状態など）をどのコンポーネントで持つか考える。誰がハンドラーを定義して誰が実行するか。

## アプリケーション構造
各.tsx -> App.tsx -> index.tsx -> index.html

# hooks
## useEffect
実行タイミングの制御のためのフック。DOMレンダリング後に実行される。主に副作用（UI構築以外の処理）を実行する。
コールバック関数から返されるクリーンアップ関数はアンマウント時に実行される。

処理の実行タイミングをレンダリング後まで遅らせるhook。

## useContext
Reactコンポーネントのツリーに対して「グローバル」とみなすデータについて利用するように設計されている。コンポーネントの再利用を難しくするため慎重に使う必要がある。

## HTMLとの違い
* class -> className
* タグの属性に代入するときは { }で囲う。（Javascript形式）

# react 公式doc
## JSX
マークアップとロジックを分離（技術の分離）するのではなく、コンポーネントの単位で関心の分離を行う。
JSXは式である。コンパイルの後、JSの関数呼び出しに変換され、JSオブジェクトへと評価される。
JSXでJSの値は{}で渡す。JSオブジェクトを渡す場合はオブジェクトを{}でラップする。（{{}}となる）

DOMを値として考えて仮想DOMで操作する。レンダリング時にDOMとの差分を抽出する。

JSXの実体は、CreateElementによって生成されたReact要素。

## レンダーされた要素の更新
React要素はイミュータブル。一度作成すると子要素や属性は変更できない。特定のある時点のUI。

## コンポーネントとprops
propsはタグのクラスやIDみたいなもの。この値によってコンポーネントをカスタマイズできる。
概念的にはコンポーネントはJSの関数に似ている。propsという任意の入力を受け取り、画面上に表示すべきものを記述するReact要素を返す。

関数コンポーネント（コンポーネントを定義するシンプルな方法：JSの関数）（こちらが主流？）
function Welcom(props) {
    return <h1>hello, {props.name}</h1>;
}
クラスコンポーネント
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

コンポーネントは最初は大文字推奨
コンポーネントが使用される文脈ではなく、コンポーネント自身からの観点でpropsの名前を付ける。
UIの一部（ボタンなど）が複数回使われている場合や、そのUI自体が複雑な場合は別コンポーネントとして抽出する価値は大きい。

全ての React コンポーネントは、自己の props に対して純関数のように振る舞わねばなりません。自分自身のpropsは変更してはいけない。

## propsとstate
原則として、propsはコンポーネントのレンダリングを設定する際に使い、stateは時間経過で変化するようなデータ（状態）を追跡する際に使う。

## stateとライフサイクル
ライフサイクルメソッド
多くのコンポーネントを有するアプリケーションでは、コンポーネントが破棄された場合にそのコンポーネントが占有していたリソースを解放することが重要。componentDidMount、componentWillUnmountなどのライフサイクルメソッドを活用する。
renderメソッドは更新が発生するたびに呼ばれる。これによりReactは何を表示すべきかを知る。その後ReactはDOMをレンダー出力と一致するように更新する。
componentDidMountメソッドは出力がDOMにレンダーされた後に実行される処理。
constructor > render > （出力がDOMに挿入されると）componentDidMount

stateは直接変更せず、setStateを利用する。（直接更新できるのはコンストラクタ内のみ）
this.propsとthis.stateは非同期に更新される。そのためお互いの値に依存するべきではない。
stateはコンポーネント自身以外からはアクセスできない。ローカル、カプセル化されている。
コンポーネントは子コンポーネントにpropsとして自身のstateを渡すことはできる。つまりstateはそのコンポーネントよりも下にのみ影響する。任意の場所で追加で合流してくる水源のようなもの。

## others
Viewタグ、Textタグはそれぞれdivタグ、pタグのようなもの。
ほとんどのCoreComponentsはpropsによってカスタマイズ可能。（Imageコンポーネントのsourceなど）


# hooks

## useState
stateとstate更新関数を返すフック。
stateは画面に表示するデータやUIの状態。アプリケーションが保持している情報。
state管理では、stateの保持とstateの更新を行う。
stateの変更により再レンダーを行う。
複数のstateをひとつのオブジェクトでまとめることもできる。

## useEffect
コンポーネントに副作用（Reactから生成されたDOMの変更、API通信、非同期処理など）を追加する。
コンポーネントのレンダー後やアンマウント（コンポーネント廃棄）後に副作用を実行する。
引数の渡し方によって、毎回実行したり、一度だけ実行させたり、特定の値が変更された時だけ実行てきる。

## useRef
DOMの参照や値の保持をする。useStateとは異なり、useRefで生成した値を更新しても再レンダーされない。レンダーに関係ないstateを扱いたい時に利用。

## React.memo
コンポーネントのレンダー結果をメモ化する。
レンダーコストの高いコンポーネントや、頻繁に再レンダーされるコンポーネント内の子コンポーネントの再レンダーをスキップしてパフォーマンスを上げる。
propsの等価性をチェックして再レンダーを判断する。
useCallback、useMemo と併せて使う。
パフォーマンス向上が必要になった際に利用を検討すれば良い？

## useReducer
stateとdispatch（actionを送信する関数）を返すフック。
複雑なstate更新を行う時に使うと良い？

## useContext

## カスタムフック
コンポーネントから切り出したロジックを定義した関数。
カスタムフックは、ロジックの再利用や関心の分離を実現するためにReactで利用されます。以下は、カスタムフックを使用する典型的な場面の一部です：

1. **ロジックの再利用**:
   複数のコンポーネントで共通のロジックを使用する場合、そのロジックをカスタムフックとして切り出し、再利用することができます。

2. **外部データの取得**:
   API呼び出しやWebSocketの接続など、外部データの取得とその状態管理をカスタムフック内で行うことがよくあります。

3. **イベントリスナの管理**:
   ウィンドウのリサイズやキープレスなど、特定のイベントリスナを設定・削除するロジックをカスタムフックでまとめることができます。

4. **フォームの管理**:
   フォームの入力状態管理やバリデーションのロジックをカスタムフックで一元化することができます。

5. **サードパーティのライブラリとの統合**:
   特定のサードパーティのライブラリをReactのコンポーネントで使用する際のロジックをカスタムフック内でカプセル化することがよくあります。

6. **アニメーションやトランジション**:
   アニメーションの状態や進行を制御するロジックをカスタムフックとして切り出すことができます。

7. **グローバルな状態の購読**:
   グローバルな状態（例: ReduxやMobXのような状態管理ライブラリ）を購読し、その状態をコンポーネントで利用しやすくするためのカスタムフックを作成することができます。

8. **副作用の管理**:
   一貫した副作用の実行やクリーンアップのロジックをカスタムフックで管理することができます。

これらの場面では、カスタムフックを使用することで、コードの再利用性、読みやすさ、メンテナンス性が向上します。また、カスタムフックは関数ベースのコンポーネントとの相性が良く、Hooksの導入以降、Reactの開発スタイルとして一般的になっています。


# クラスコンポーネント
* reactモジュールのComponentクラスを継承
* renderメソッドで描画内容（React要素）を返す
* ライフサイクルを理解するために知っておくとよい。

# Export

## `export` (名前付きエクスポート)

- **名前付きエクスポート**：この方法を使用すると、複数の値やコンポーネントを同一ファイルからエクスポートできます。
- **インポート方法**：インポートする際は、エクスポートされた名前を`{}`内に記載してインポートします。例：`import { MyComponent } from './MyComponent';`
- **柔軟性**：一つのファイルから複数の関数やコンポーネントをエクスポートし、必要なものだけを選んでインポートできるため、柔軟性があります。

## `export default` (デフォルトエクスポート)

- **デフォルトエクスポート**：各ファイルには一つの`export default`が存在できます。これはそのファイルの「主要な」エクスポートと見なされます。
- **インポート方法**：デフォルトエクスポートされた値は、`{}`なしで直接インポートできます。また、インポートする際に任意の名前を与えることができます。例：`import MyComponent from './MyComponent';`
- **簡潔さ**：通常は、ファイルごとに一つの主要なコンポーネントや機能がある場合に使われ、インポートが簡単になります。

### 使用例

以下の例では、一つのファイルから複数の関数やコンポーネントをエクスポートしています。

```javascript
// MyComponent.js

export const MyFunction = () => {
  // 何かの関数
};

export const AnotherFunction = () => {
  // 別の関数
};

const MyComponent = () => {
  // コンポーネントの定義
};

export default MyComponent;
```

これらをインポートするには：

```javascript
import MyComponent, { MyFunction, AnotherFunction } from './MyComponent';
```

# ライフサイクル
ライフサイクルはコンポーネントが生成されてから削除されるまでの一連の流れ
内部のstateが更新された時、もしくは親コンポーネントから新しいpropsが渡された際にコンポーネントの更新処理が起きる。

mounting
コンポーネントが配置される期間
初期化→レンダリング→マウント後処理

updating
コンポーネントが変更される期間
レンダリング→更新後処理

unmounting
コンポーネントが破棄される期間
破棄前の処理

Reactの再レンダリングの流れは、以下のようになります：

1. **State/Propsの変更**:
   Reactのコンポーネントは、stateやpropsが変更されたときに再レンダリングされることが多いです。

2. **仮想DOMの生成**:
   コンポーネントが再レンダリングされると、Reactは新しい仮想DOMを生成します。これは実際のDOMとは異なり、メモリ上でのみ存在する軽量の表現です。

3. **差分検出（Diffing）**:
   Reactは新しい仮想DOMと前回の仮想DOMを比較して、どの部分が変更されたかを特定します。

4. **再描画（Reconciliation）**:
   差分をもとに、実際のDOMに必要な変更を適用します。このステップにより、DOMの更新が最適化され、必要最小限の変更のみが行われます。

5. **コンポーネントのライフサイクルメソッド**:
   一部のライフサイクルメソッド（例: `componentDidUpdate`）がこの再レンダリングの過程で呼び出されることもあります。

注意点:
- `shouldComponentUpdate`やReact.memoなどのオプティマイゼーション技術を利用することで、不要な再レンダリングを回避することができます。
- Hooksを使用している場合、`useEffect`や`useMemo`などのフックも再レンダリングの制御に影響することがあります。

Reactの再レンダリングの流れを理解することは、パフォーマンスの最適化やバグのトラブルシューティングに役立ちます。

もちろん、Reactのコンポーネントライフサイクルは、特定のフェーズにおいて何が起こっているのかを理解するためのキーです。クラスベースのコンポーネントに特有のものですが、Reactの進化と共にHooksが導入されたことで、関数ベースのコンポーネントでも同様のライフサイクル処理を模倣することができるようになりました。

クラスベースのコンポーネントにおける主なライフサイクルメソッドは以下のとおりです：

1. **マウント（Mounting）**:
   - `constructor()`: コンポーネントの初期化とstateの設定を行います。
   - `static getDerivedStateFromProps()`: propsからstateへの値のセットを行う場合に使います。
   - `render()`: コンポーネントを描画します。
   - `componentDidMount()`: コンポーネントがDOMにマウントされた後に実行される。API呼び出しやDOM操作、イベントリスナの追加などをここで行うことが多いです。

2. **更新（Updating）**:
   - `static getDerivedStateFromProps()`: 新しいpropsを受け取ったときに呼び出されます。
   - `shouldComponentUpdate()`: パフォーマンス最適化のために、再レンダリングをするべきかどうかを決めることができます。
   - `render()`: 再レンダリングを行います。
   - `getSnapshotBeforeUpdate()`: 更新前のDOMの状態や情報をキャッチするために使います。
   - `componentDidUpdate()`: コンポーネントが更新された後に呼び出される。新しいpropsやstateをもとに何らかの操作を行うことが多いです。

3. **アンマウント（Unmounting）**:
   - `componentWillUnmount()`: コンポーネントがDOMから削除される直前に実行される。イベントリスナの削除やクリーンアップ作業をここで行うことが多いです。

4. **エラーハンドリング**:
   - `static getDerivedStateFromError()`: 子コンポーネントでエラーが発生した場合に、エラー情報をもとにstateを更新するために使います。
   - `componentDidCatch()`: エラーロギングや特定のUIを表示するために使用します。

関数ベースのコンポーネントでは、`useEffect` フックを使って同様のライフサイクルイベントを模倣することができます。たとえば、`componentDidMount` と `componentWillUnmount` は `useEffect` でそれぞれの処理を書くことで再現できます。


# 再レンダリング
Reactのコンポーネントにおける状態遷移は主に、コンポーネントの内部状態（`state`）や外部から渡されるデータ（`props`）の変更を指します。この変更は、コンポーネントの再レンダリングを引き起こします。

以下に、Reactコンポーネントの状態遷移の概要とそのステップを説明します。

1. **初期化**:
   - コンポーネントのインスタンスが生成される際、`constructor`内で`state`の初期化が行われます。
   - コンポーネントは初めてのレンダリングを行い、画面に表示されます。

2. **propsの変更**:
   - 親コンポーネントから新しい`props`が渡されると、子コンポーネントの再レンダリングが引き起こされることがあります。
   - `getDerivedStateFromProps`が存在する場合、新しい`props`を元に`state`の更新を行うことができます。

3. **stateの変更**:
   - コンポーネント内部で`setState`メソッドや`useState`フックのセッター関数が呼び出されると、`state`が更新されます。
   - `state`の変更は再レンダリングを引き起こします。

4. **ユーザーインタラクション**:
   - ユーザーがボタンをクリックしたり、フォームの入力を行ったりすると、イベントハンドラがトリガーされます。
   - このイベントハンドラ内で`state`の変更や親コンポーネントへのコールバックの実行など、状態遷移の起点となるアクションが行われることが多いです。

5. **外部データの取得**:
   - API呼び出しの結果やWebSocketのメッセージなど、外部からのデータの受け取りが状態遷移の起点となることもあります。

6. **アンマウント**:
   - コンポーネントがDOMから削除される際、関連するリソースやイベントリスナのクリーンアップを行う必要があります。

これらの遷移は、Reactのコンポーネントライフサイクルやフックを使用して管理されます。適切なライフサイクルメソッドやフック内で状態遷移を制御することで、効率的でバグの少ないアプリケーションを実現することができます。


はい、`state`や`props`の変更以外にも、コンポーネントが再レンダリングされるケースはいくつか存在します。以下はその主なケースです：

1. **親コンポーネントの再レンダリング**:
   親コンポーネントが再レンダリングされると、子コンポーネントもデフォルトで再レンダリングされます。これは、子コンポーネントが`props`の変更を受け取らなくても発生します。

2. **`forceUpdate`メソッドの使用**:
   クラスコンポーネントには`forceUpdate`というメソッドが存在し、これを呼び出すと、コンポーネントは強制的に再レンダリングされます。

3. **コンテクストの変更**:
   `Context.Provider`の`value`が変更されたとき、そのコンテクストを購読しているコンポーネントは再レンダリングされます。

4. **不純なコンポーネント**:
   Reactはデフォルトではコンポーネントが純粋（pure）でないと仮定します。したがって、再レンダリングが頻繁に発生する可能性があります。`PureComponent`や`React.memo`を使用することで、この再レンダリングを最適化することができます。

5. **Hooksの状態更新**:
   `useState`や`useReducer`などのHooksの状態更新関数を呼び出すと、関数コンポーネントは再レンダリングされます。

これらのケースを理解しておくことは、パフォーマンスの最適化や不要な再レンダリングを避けるために重要です。適切な最適化手段を適用することで、アプリケーションの効率を高めることができます。


4番の「不純なコンポーネント」に関する再レンダリングの説明は、コンポーネントが純粋であるか否かという概念に基づいています。ここでの「純粋」とは、同じpropsとstateが与えられた場合、常に同じ出力（レンダリング結果）を返すコンポーネントを指します。

Reactのデフォルトの動作は、コンポーネントが純粋でないと仮定するため、再レンダリングが頻繁に発生します。これは、Reactが`props`や`state`の浅い比較を行わないためです。

4番のケースでの再レンダリングが発生する主な理由は以下の通りです：

1. **新しいオブジェクトや配列の生成**:
   コンポーネントの`render`メソッド内や関数コンポーネントの本体内で新しいオブジェクトや配列を生成すると、そのオブジェクトや配列は毎回新しい参照として生成されます。そのため、親コンポーネントから子コンポーネントへこれを`props`として渡すと、子コンポーネントは再レンダリングされる可能性が高まります。

2. **関数の新しいインスタンスの生成**:
   同様に、コンポーネント内で新しい関数のインスタンスを生成すると、その関数は新しい参照として扱われます。これも不要な再レンダリングを引き起こす要因となります。

3. **親コンポーネントの再レンダリング**:
   親コンポーネントが再レンダリングされると、その子コンポーネントも再レンダリングされる可能性があります。ただし、子コンポーネントが純粋であると明示的に示されている場合（`React.PureComponent`や`React.memo`を使用している場合）は、この動作は最適化されます。

これらの不要な再レンダリングを避けるためには、コンポーネントの最適化や`React.memo`、`useMemo`、`useCallback`などのツールを使用して、参照の安定性を保つなどの対策を取ることが推奨されます。

はい、Reactでは親コンポーネントが再レンダリングされても、特定の条件下で子コンポーネントが再レンダリングされないケースが存在します。以下はそのケースをいくつか挙げます：

1. **PureComponentまたはReact.memoを使用する**: 子コンポーネントが`React.PureComponent`を継承しているか、または`React.memo`でラップされている場合、propsとstateが前のレンダリングと同じであれば、子コンポーネントは再レンダリングされません。

2. **stateとpropsが変更されていない**: 親コンポーネントが再レンダリングされたとしても、子コンポーネントに渡されるpropsやstateが変更されていない場合、子コンポーネントの再レンダリングは発生しない可能性があります。

3. **shouldComponentUpdateを使用する**: 子コンポーネントで`shouldComponentUpdate`ライフサイクルメソッドを使用し、そのメソッドが`false`を返す場合、子コンポーネントは再レンダリングされません。

これらの方法を使用して、不要な子コンポーネントの再レンダリングを防ぐことで、アプリケーションのパフォーマンスを向上させることができます。ただし、これらの方法を過度に使用すると、アプリケーションの動作に予期しない問題が生じる可能性があるため、注意が必要です。


`onClick`でカスタムフックを使用するボタンコンポーネントが押下時に再レンダリングされるかどうかは、そのカスタムフックの中身やボタンコンポーネントの他のプロパティやステートに依存します。

以下は考慮すべきシナリオです：

1. **カスタムフックが内部でステートを更新する**: カスタムフックが内部でuseStateやuseReducerなどのステートを更新するロジックを持っている場合、そのステートが変更されると、ボタンコンポーネントは再レンダリングされます。

2. **親コンポーネントのステート/プロップスが変わる**: ボタンコンポーネントが親コンポーネントからのプロップスに依存している場合、それらのプロップスが変わるとボタンも再レンダリングされる可能性があります。

3. **カスタムフックが新しい関数/オブジェクトを返す**: カスタムフックが常に新しい関数やオブジェクトを返す場合、ボタンコンポーネントはそれによって再レンダリングがトリガーされる可能性があります。これを防ぐためには、`useCallback`や`useMemo`をカスタムフック内で使用すると良いでしょう。

4. **ボタン自体のステートが変更されない**: もしボタンコンポーネントの内部ステートや受け取るプロップスが変更されない場合、ボタンは再レンダリングされないかもしれません。

結論として、`onClick`でカスタムフックを使用するだけでは、ボタンが再レンダリングされるとは限りません。カスタムフックの動作や、ボタンのステートやプロップスの変更によって再レンダリングが決まります。


カスタムフック内に`useState`が含まれており、そのフックの処理内で必ずステートが更新される場合、そのステートを使用しているコンポーネントは再レンダリングされるはずです。

しかし、以下のような特殊な状況や理由で再レンダリングが発生しない場合も考えられます：

1. **新しいステートの値が前のステートの値と同じ**: Reactの`useState`は参照の同一性ではなく、シャロー比較を行います。したがって、新しいステートの値が前回と同じであれば、再レンダリングはトリガーされません。

2. **子コンポーネントの再レンダリングをブロック**: 子コンポーネントに`React.memo`や`shouldComponentUpdate`を使用している場合、再レンダリングがブロックされることがあります。

3. **Reactのバッチ処理による更新のマージ**: 連続して多数のステート更新が行われる場合、Reactはこれらの更新をバッチ処理し、1回の再レンダリングでこれらの変更を適用することがあります。

4. **エラーや例外**: カスタムフックやコンポーネント内で何らかのエラーや例外が発生し、それにより更新が完了しない場合が考えられます。

通常、ステートの更新があると再レンダリングがトリガーされるのですが、上記のような特定の条件下では再レンダリングが発生しないことが考えられます。

# state
Reactで`state`に設定するものは、コンポーネント内部でのデータの動的な変化や状態を表現するものです。以下は、`state`に設定される典型的な例をいくつか挙げます：

1. **ユーザー入力**: フォームのテキスト入力、選択ボックスの選択、チェックボックスの状態など、ユーザーからの入力に基づくデータ。

   ```javascript
   const [inputValue, setInputValue] = useState('');
   ```

2. **表示・非表示のフラグ**: モーダルやドロップダウンメニュー、トースト通知などの表示状態。

   ```javascript
   const [isModalOpen, setModalOpen] = useState(false);
   ```

3. **データの取得結果**: APIからのデータ取得やデータベースのクエリ結果。

   ```javascript
   const [userData, setUserData] = useState(null);
   ```

4. **ページネーション**: 現在のページ番号や表示するアイテムの数。

   ```javascript
   const [currentPage, setCurrentPage] = useState(1);
   ```

5. **アニメーション**: アニメーションの進行状態や完了フラグ。

   ```javascript
   const [animationProgress, setAnimationProgress] = useState(0);
   ```

6. **カウンターやタイマー**: 値が時間経過やユーザー操作によって増減する数字。

   ```javascript
   const [counter, setCounter] = useState(0);
   ```

7. **エラーや通知メッセージ**: API呼び出しのエラー情報やユーザーへの通知メッセージ。

   ```javascript
   const [errorMessage, setErrorMessage] = useState('');
   ```

8. **ユーザーのインタラクション**: タブの選択、スライダーの位置、ドラッグ&ドロップの状態など。

   ```javascript
   const [selectedTab, setSelectedTab] = useState('overview');
   ```

これらは一部の例に過ぎません。実際には、アプリケーションの要件や動作に合わせて、さまざまなデータや状態を`state`として管理することがあります。

