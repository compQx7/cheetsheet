
# モジュール機能
# イベント
* イベントターゲット（ボタンタグなど）、イベント（クリックなど）、イベントリスナー（ボタンタグでイベントが発生した時の処理など）を関連付けるのがaddEbentListenee。

# スクリプト実行タイミング
* html解析完了
* defer属性を指定したタグののスクリプト
* DOMContentLoadedイベントのスクリプト
* 全リソースの読み込み完了
* loadイベントのスクリプト

# ページ遷移
* location.hrefで、a要素のクリックではないタイミングで遷移できる。このプロパティを読み込んだ場合は現在のURLを取得でき、このプロパティにURLを書き込んだタイミングで遷移できる。

## クライアントJSでできること概要
* HTML内の情報を取得・変更・削除できる
	* 要素、属性、テキスト
	* 読み込むファイルを変える
	* クラスを変えて読み込むスタイルを変える
	* コントロールを動的に動かす、表現を変える
* 要素にイベントを追加できる
	* ボタンクリックや画面タッチを検知してイベント発火
* ブラウザの情報を取得できる、ブラウザ、デバイスの操作を検知できる
* 外部と通信できる
	* データを取得してHTMLに反映できる
	* 外部DBに対してデータを登録更新削除できる 
* SVGやキャンバスを使ったグラフィックス
* クライアントのブラウザ上でデータを保存させることができる


# JavaScriptのthis
* 通常の関数内でのthisは、関数が定義された場所によって決まる。
* アロー関数内のthisは、関数が実行された場所で決まる。