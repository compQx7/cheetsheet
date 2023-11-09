# DB設計
* 各DBMSマニュアルが示す構文図は仕組みがよく分かる。
* トランザクション管理、排他制御、障害回復、レプリケーション

## 概念設計
* [DB設計におけるエンティティやER図] 始めは難しいが経験を積めば自然とできる。普段からエンティティ関係図をイメージするようにしよう。
* [PKが備えるべき特性] 必ず何らかの値を持つ非null性、 他と重複しない一意性、値が変化することはない不変性。項目一覧から候補キーを探すときは一意に識別できるかを考えるのがポイント。

## 論理設計
* [正規形] すべての行のすべての列に1つずつ値が入っているべきであり、セルの重複のような形をなくす。ある列Aの値が決まれば、自ずとBの値も決まる関係を関数従属と言い、すべての非キー列は主キーにきれいに関数従属すべきである。複合主キーの場合は、複合主キー全体に対して関数従属となるべき。また、主キーに関数従属になっている列に対して、さらに関数従属になっている列は切り出す。
* 第1正規形は行内に重複がない状態、第2正規形は主キーが決まれば他の値が決まる状態、第3正規形は主キー以外の値によって決まる値がない状態。
* [正規化しないケース] データ更新を行わないもの（ログやデータハウス、データ履歴などの追記するだけのもの）、性能を最重視するもの。

## 物理設計
* 列名の決定、型の決定、制約やデフォルト値、インデックス、その他ビューなど。

## NOT NULL
* アプリコードに頼らず、データベースで一貫した制約を強制することがてきる。
* NULLがアプリのポリシー違反に反するケースや、列においてNULLが意味をなさない場合はつけるべき。

## 権限
* ユーザーとロールに権限を付与できる。ロール自体はユーザーに付与する。
* ユーザーに付与した権限とロールに付与した権限で、最も包括的な権限が付与される。

# トランザクション
* トランザクション内の処理は、すべて更新してコミットするか、すべて取り消すかのどちらかしかなく、途中かけにはならない仕組み。
* トランザクション内処理を取り消すことをロールバック。
* ディスク障害などでDBが壊れてしまった場合などに、バックアップから復元し、更新後ジャーナルから更新情報を取得して、故障直前まで戻すことをロールフォワード。

# 排他制御、ロック
* 共有ロックは、他者が読むことは許され、書き込みは許されない。専有ロックはどちらも許されない。

# インデックス
DBでインデックスを貼る時はカーディナリティを意識する。どんなデータがどんな分布で入るのかを想定して設計する。

# 3値論理
* Trueかどうかを判定するように考えれば分かりやすい。その中でFalseと断定できなければNull。
* True and Null はNullがどちらか分からないのでNull
* Null and False はすでにFalseが確定しているからFalse
* Null or True はTrueが確定しているからTrve

# others
* DBの排他制御では防げない部分は楽観ロックなどの考え方で対処する必要がある。ロックキーとしてはバージョンが推奨される。


# Oracle
## tnsnames.oraファイルの内容がうまく読み取られない
スペースでインデントを付けてみる。
その後読み取るようになってから、再度スペースを消してもきちんと読み取ったため、正確に原因は不明。