
# CORS
オリジンサーバのドメインとXHRによるアクセス先のドメインが異なる場合は、ブラウザ側で自動的にOriginフィールドを付加してくれる。
CORSによるリクエストヘッダには、このフィールドが付加されている必要がある。

リクエストヘッダにOriginフィールドの値が設定されているか、さらに、このOriginフィールドのドメインがクロスドメインアクセスを許可する対象であるかを判定し、受け入れの判断をする。

下記２点に該当する場合、preflightリクエストを受け取ったとして処理することになる。
・HTTPメソッドがOPTIONSであるか
・リクエストヘッダにAccess-Control-Request-Methodフィールドが付加されているか

HTTPメソッドはアクセスを許可しているものであるか
ここまでチェックし終えると、リクエストに対してリソースのアクセスを許可するという判断となります。

CORSのリクエストが成立した場合、リクエストがアクセスを求めてきたリソースをレスポンスで返す際に、必ずレスポンスヘッダのAccess-Control-Allow-Originフィールドにクロスドメインアクセスが許可されるサイトのドメイン名を付加する。レスポンスヘッダにこのフィールドがない場合、ブラウザはクロスドメインアクセスに失敗したと判断してエラーを発生させる。

場合によってはいくつかCORSのレスポンスヘッダを付加する事になる。
まず、CORSによるリクエストがサーバーにおいてクライアントに対して使用可能なリクエストヘッダを公開するよう設定されている場合、Access-Control-Expose-Headersフィールドに使用可能なリクエストヘッダのホワイトリストを付加する。
もう一点、リクエストにCookieの情報が付加されており、なおかつサーバー側の設定でCookieの利用が許可されている場合はレスポンスヘッダのAccess-Control-Allow-Credentialsフィールドにtrueをセットする。

[CORS](https://www.ey-office.com/blog_archive/2022/03/03/learned-the-proxy-setting-of-create-react-app/)