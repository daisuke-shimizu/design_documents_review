# テーブル定義書1
## 全体
- 主キーは~idという命名規則ではなくid
- テーブル名が全部大文字、スネークケースで書かれていない
- カラム命名規則(adminテーブルのadmin_emailカラムではなくadminテーブルのemaiカラム)
- 複数単語のカラムがスネークケースで書かれていない(スペースまたは１単語扱いで書かれている)
<!-- 追記-->
- created_at, updated_atカラムの説明が全て「ユーザー登録日時」, 「ユーザー更新日時」となっている
- 在庫数は実際の在庫と入荷の数量が同一に格納される恐れがあるので入荷用の情報を管理できるテーブルを作成すると良い

<!-- 追記-->
## Admin
- テーブル名は複数形
- admin_idがPKになっていない

## user
- l_name,f_name等意味合いを省略して書くとカラムの役割がわかりづらい
- 郵便番号電話番号はintegerではなく、string型
- メンバーステータスの命名規則、ユーザー情報なのに急にメンバーになるのはおかしい
- メンバーステータスのデータ種類は限られているのでintegerでenumとかで管理すべき
- ship_addressでは他住所を1ユーザーにつき1つしか登録できない

## products
- disc_idがある(ディスクが親テーブルとなっている)
- genre_id,label_id,artist_idにFKがない
- CD画像カラム、refileを使用するなら後ろにidをつけて型をintegerにする(carrierwaveならこれで可能)
- notax_priceカラムはno_tax_priceにすると良い、というかここは単純にpriceでいいと思う
<!-- 追記-->
- stock_statusは在庫数がわかればわかるので不要。
- stockは（入荷数-購買数）で計算できるので不要。

## discs
- productのidがあること自体はあっているがそうなるとproductにdisc_idがあるのでおかしくなる
- products_idではなくproduct_id
- track_numの命名がわかりづらい

## songs
- 曲順を識別するカラムがない
- songカラムをnameに

## labels
- レーベルは商品を複数所持している関係性のためproduct_idは必要ない
- products_idではなくproduct_id
- labelカラムをnameに

## artists
- アーティストは商品を複数所持している関係性のためproduct_idは必要ない
- products_idではなくproduct_id
- artistカラムをnameに
- artistカラムがinteger型になっている

## genres
- ジャンルは商品を複数所持している関係性のためproduct_idは必要ない
- products_idではなくproduct_id
- genreカラムをnameに
- genreカラムがinteger型になっている
- テーブル名は複数形、スネークケース小文字

## cart_item
- products_idではなくproduct_id、データ型無し
- 小計はCD情報から引っ張れるのでいらない
- buy numの命名がわかりづらい
- テーブル名は複数形、スネークケース小文字

## buy_details
- 管理者目線なのでテーブル名が不適切
- buy numの命名がわかりづらい
- CDと紐づいてない

## buy
- 管理者目線なのでテーブル名が不適切
- buy_detailと関係性が逆
- payの命名がわかりづらい、データ型はenumを使って切り替えるのならinteger
- stockの命名がわかりづらい
- buy_atの命名がわかりづらい
- 郵便番号を格納するカラムがない


**研修担当レビュー**
<font color="Red">再提出の際はこのレビューを残しておいてください。</font>

## 全体
- created_at, updated_atカラムの説明が全て「ユーザー登録日時」, 「ユーザー更新日時」となっていますが、問題ありませんか？

## Admin
- テーブル名は複数形でなくてはいけません
- PKが○のカラムがありません

## Products
- 在庫数カラムがありますが問題ありませんか？
- 在庫ステータスカラムがありますが問題ありませんか？

## Songs
- songというカラムがありますがこの命名は問題ありませんか？

## Labels
- product_idは必要でしょうか？

## Artists
- product_idは必要でしょうか？
- `artist`というカラムがinteger型になっていますが問題ありませんか？

## Genres
- product_idは必要でしょうか？
- テーブル名は複数形でなくてはいけません
- `genre`というカラムがinteger型になっていますが問題ありませんか？

# フィードバック2回目

## 全体
　- PKがそもそもないテーブルに対して指摘する

## products
　- refileを用いてimage_idを保存するときのデータ型って実は、integerは推奨されてないです。画像のurlをしまうので。何が適切でしょう？
 
## songs
 - 曲名をしまうカラムのデータ型がintegerになってしまっていますね。
 
## buy_details
　- このテーブルにしまう情報は、注文された商品１つずつ。subtotalカラムは適さない。「購入時点での」商品価格情報をログとして保存するためのカラムを作りましょう。
 
## buy
　- buy_atカラムとcreate_atカラムには同じ情報が入力されると思います。そのため、buy_atは不要ですね。
　- 消費税データを入力するカラムがあったほうがいいです。

