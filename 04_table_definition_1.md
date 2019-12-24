# テーブル定義書1
## 全体
- 自分以外の住所(配送先住所)を格納する場所がない
- PKは table_id とするべきか、単に id とするべきか (わかりやすいようにあえてそう書いているのか？)(ex: book.book_id ではなく book.idとアクセスするため)
- ↑ この通りであれば全てのテーブル名を table_id → id

## Users
- user_f_name, user_f_kanaにNOT NULLがかかっていない
- 名前(性) → 名前(姓)
- DEFAULTがFALSEになっているのでデータ型は string → boolean(またはintegerにして、備考欄にenumで管理を追加)

## Buy
- 購入日カラムが不要
- テーブル名をBuy → Buys
- 配送ステータスがない
- 支払い方法カラムはenumで管理した方が楽(データ型をstring → integer)

## Buy details
- テーブル名をBuy details → Buy_details

## Cart item
- テーブル名をCart item → Cart_items
- カラム名をbuy num → buy_number
- PKがない

## Genre
- PKがない
- テーブル名をGenre → Genres
- genreカラムのカラム名をnameやgenre_nameに変更
- ジャンル名のデータ型を integer → string

## Aritists
- PKがない
- artistカラムのカラム名をnameやartist_nameに変更
- アーティスト名のデータ型を integer → string

## Labels
- PKがない
- labelカラムのカラム名をnameやlabel_nameに変更

## Admin
- テーブル名をAdmin → Admins
- PKがない

## Products
- カラム名をnotax_price → no_tax_price(税は購入時に追加するので単にpriceでも良い)
- disc_idカラムが不要
- genre_id, label_id, artist_idのFKに○を追加
- 在庫数カラムを削除して、入荷数カラムを追加
- 在庫ステータスカラムが不要
- ジャケット画像のNOT NULLが空なのはジャケット画像が入手しにくい状況が想定されるからなのか？(そのためのDEFAULT="画像準備中")

## Discs
- track_num → disc_num にカラム名を変更

## Songs
- PKがない
- songカラムのカラム名をnameやsong_nameに変更
- 曲名のデータ型を integer → string

# 注意
* マークダウン形式で記入してください。
* 全体を通しての指摘事項の場合、テーブル名の部分を「全体」「共通」などとしてください。


# フィードバック
【フィードバックは消さないこと】
[add]→付け加えなければいけないところ
[fix]→修正が必要なところ
[comment]→その他コメント

## 全体
- ↑ この通りであれば全てのテーブル名を table_id → id
[comment]→その通り！
[add]→　created_atとupdated_atの「カラム説明」が全て「ユーザ」を対象とすることになっている。
[add]→　全体的にテーブルとカラムの命名について見直すべき。命名規則は「管理者側での視点」「小文字、アンダーバーで単語を連結させる」「複数、単数形に注意」


## Users
- 名前(性) → 名前(姓)
[comment]→俺も初めて誤字に気がついたw
- DEFAULTがFALSEになっているのでデータ型は string → boolean(またはintegerにして、備考欄にenumで管理を追加)
[fix]→ member_statusという命名だと、何の情報を表しているか、不明確。
[add]→　「電話番号」や「郵便番号」のデータ型はintegerにしてしまうと、0始まりの数列の場合、頭の0が取れるからstringで。　

## Buy
- テーブル名をBuy → Buys
[fix]→ そもそも、命名規則的にテーブル名に動詞を使うことは不適。名詞にする。また、「管理者側での視点」で命名することを心かける。この場合、購入された商品は管理者側からは「注文」or「受注」と言った表現が適切。
- 支払い方法カラムはenumで管理した方が楽(データ型をstring → integer)
[fix]→ payという命名は不適。
[add]→子テーブル（buy_details）のidをFKとして持っている
[add]→送付先住所はあるが、郵便番号と住所がないのはなぜか？
[add]→stockカラム、命名が不適


## Buy details
- テーブル名をBuy details → Buy_details
[fix]→ buyテーブルと同じ理由で「注文」or「受注」と言った表現に変更する。
[add]→　スネークケース（アンダーバーで単語を連結すること）が使われていないカラムがある


## Cart item
- テーブル名をCart item → Cart_items
[fix]→ いや、cart_items。小文字っす
[add]→products_idではなく、product_idにすべき
[add]→小計金額は不要。小計はただの掛け算ですぐ求まる値のため。わざわざデータベースに格納する必要はない。

## Genre
- genreカラムのカラム名をnameやgenre_nameに変更
[fix]→ テーブル名とカラム名に同じ言葉を含めるのはnot good。
[add]→product_idは不要

## Aritists
- artistカラムのカラム名をnameやartist_nameに変更
[fix]→ テーブル名とカラム名に同じ言葉を含めるのはnot good。
[add]→product_idは不要

## Labels
- labelカラムのカラム名をnameやlabel_nameに変更
[fix]→ テーブル名とカラム名に同じ言葉を含めるのはnot good。
[add]→product_idは不要


## Products
[add]→cd_titleはtitleで十分。
[add]→FKの記載がない。
[add]→product_という接頭辞はいらない。idで十分。

## Discs
[add]→disc_という接頭辞はいらない。idで十分。
[add]→products_idではなく、product_idにすべき。

## Songs
- songカラムのカラム名をnameやsong_nameに変更
[fix]→ テーブル名とカラム名に同じ言葉を含めるのはnot good。

# 注意
* マークダウン形式で記入してください。
* 全体を通しての指摘事項の場合、テーブル名の部分を「全体」「共通」などとしてください。
