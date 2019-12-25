# テーブル定義書1
## 全体
- 指摘事項

## テーブル名
- 指摘事項

# 注意
* マークダウン形式で記入してください。
* 全体を通しての指摘事項の場合、テーブル名の部分を「全体」「共通」などとしてください。


## 全体
- idカラムが無い。
- テーブル名の最初の文字が大文字になっている。
- モデル名の記載がない。

## admins
- テーブル名はadmins
- 管理者IDのカラム名は「admin_id」ではなく「id」。

## users
- ユーザIDのカラム名は「user_id」ではなく「id」。
- 「user_f_name、user_f_kana」が空欄で登録されてしまう。
- 名前で検索できるようにするなら「user_f_name、user_l_name、user_f_kana、user_l_kana」にindexを付けるべき。
- 退会ステータスのtrueとfalseがどっちが退会を意味しているかわかりづらいので備考に書くべき。
- 配送先住所カラムと住所カラムの使い分けがわからない。配送先を複数登録したい場合もあるので配送先住所テーブルを作るべき。

## products
- 商品IDのカラム名は「product_id」ではなく「id」。
- 商品画像、refile使うのだったらカラム名は「cd_image_id」でデータ型はinteger。
- 発売日カラムが必要
- genre_id、artist_id、label_idはFK。

## discs
- ディスクナンバーを記録したいので、カラム名の「track_num」は不適切。

## songs
- disc_idのautoincrementは◯では無い。

## labels
- products_idカラムは必要ない。

## artists
- products_idカラムは必要ない。

## genres
- テーブル名はgenres
- products_idカラムは必要ない。

## cart_items
- テーブル名はcart_items
- user_idのautoincrementは◯では無い。
- products_idのデータ型が書かれていない。
- buy numではなくbuy_num
- subtotalカラムは必要ない。

## buy_details
- テーブル名はbuy_details
- buy_details_idではなくid
- buy numではなくbuy_num

## buys
- テーブル名はbuys
- buy_idではなくid
- 購入日は時間は必要ないのでデータ型はdateが適切。




# フィードバック1回目
[add]→付け加えなければいけないところ
[fix]→修正が必要なところ
[comment]→その他コメント（修正ではないけど、確認して欲しいポイントです）

## 全体
- idカラムが無い。
- テーブル名の最初の文字が大文字になっている。
- モデル名の記載がない。
[fix]→テーブル名のみを書き出せばいいので、モデル名は必要のないように思われ。
[add]→テーブル名と同じワードを含む、カラムは改名する必要がある。
[add]→user_l_nameのlのような略語は使わない。この場合、きちんとlastと書くことを指摘。


## admins
- テーブル名はadmins
- 管理者IDのカラム名は「admin_id」ではなく「id」。
[add]→PKにまるがついてないことも指摘。

## users
- ユーザIDのカラム名は「user_id」ではなく「id」。
- 「user_f_name、user_f_kana」が空欄で登録されてしまう。
- 名前で検索できるようにするなら「user_f_name、user_l_name、user_f_kana、user_l_kana」にindexを付けるべき。
- 退会ステータスのtrueとfalseがどっちが退会を意味しているかわかりづらいので備考に書くべき。
[fix]→かつ、データ型がstringになってしまっている。
[add]→電話番号や郵便番号がintegerになっている。0始まりの数列が正しく認識されなくなる


## products
- 商品IDのカラム名は「product_id」ではなく「id」。
- 商品画像、refile使うのだったらカラム名は「cd_image_id」でデータ型はinteger。
- 発売日カラムが必要
- genre_id、artist_id、label_idはFK。
[add]→在庫数が分かれば、在庫状況はわかる為、不要。
[add]→在庫数は計算された値なので、廃止。（入荷数）ー（購買数）で計算できるため。

## discs
- ディスクナンバーを記録したいので、カラム名の「track_num」は不適切。
[add]→ディスクの順番はどのように管理するか
[add]→複数枚組を考慮してない。

## songs
- disc_idのautoincrementは◯では無い。
[add]→songカラムが曲名をもつならば命名はnameなどとするべき。
[add]→songカラムが曲名をもたせるのに、integerとなってる。

## labels
- products_idカラムは必要ない。
[add]→labelカラムがレーベル名をもつならばnameなどとするべき

## artists
- products_idカラムは必要ない。
[add]→artistカラムがアーティスト名をもつならばnameなどとするべき
[add]→artistカラムが曲名をもたせるのに、integerとなってる。


## genres
- テーブル名はgenres
- products_idカラムは必要ない。
[add]→genreカラムがジャンル名をもつならばnameなどとするべき
[add]→genreカラムが曲名をもたせるのに、integerとなってる。

## cart_items
- テーブル名はcart_items
- user_idのautoincrementは◯では無い。
- products_idのデータ型が書かれていない。
- buy numではなくbuy_num
- subtotalカラムは必要ない。

## buy_details
- テーブル名はbuy_details
- buy_details_idではなくid
- buy numではなくbuy_num
[fix]→そもそもbuy_numだと、意味が通らず、命名に問題あり。
[add]→buy_detailsだと受注詳細の意味じゃない。命名は「管理者の立場で行う」「動詞は不適。名詞にする。」そもそも「買う」では意味が通らない。「受注」「注文」と言った言葉に変更。


## buys
- テーブル名はbuys
- buy_idではなくid
- 購入日は時間は必要ないのでデータ型はdateが適切。
[add]→buyだと受注の意味じゃない。命名は「管理者の立場で行う」「動詞は不適。名詞にする。」そもそも「買う」では意味が通らない。「受注」「注文」と言った言葉に変更。
[add]→送付先住所はあるが、郵便番号と住所がない
[add]→支払い方法がstringになっており、enumを考慮してない。また、カラム名の命名も不適。
[add]→stock =　「支払い合計」？命名がおかしい。
