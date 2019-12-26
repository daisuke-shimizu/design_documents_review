# テーブル定義書1
## 全体
- PKのカラム名はすべて「〇〇_id」ではなく「id」
- テーブル名の先頭の文字が大文字になっている
- created_atが全てユーザ登録日時になっている
- updated_atが全てユーザ更新日時になっている

## Admin
- テーブル名が単数形になっている
- 「admin_id(正しくはid)」のPK,AUTO INCREMENt,INDEXに◯が入っていない

## Users
- カラム名に「user_」という接頭辞がついているが接頭辞は必要ない
- 「user_f_name」,「user_f_kana」の NOT NULLに◯が入っていない
- 「user_tel」などでカラム名に略語を使ってるが、略語は使うべきでない
- 「zip_code」がinteger型になっている
- 「member_status」のデータ型がstringになっているが,正しくはboolean
- 「member_status」というカラム名では会員の何のステータスを表しているか分からない
- 配送先を複数登録することを考慮してない

## Products
- カラム名に「product_」という接頭辞がついているが接頭辞は必要ない
- 「disc_id」,「genre_id」,「label_id」,「artist_id」はFK
- 「cd_image」はrefileを使うなら「cd_image_id」とする必要がある。またデータ型はstringのほうが好ましい
- 「stock_status」のデータ型はintegerにして、enumで管理したほうがいい
- 在庫数はカラムで管理するべきでない

## Discs
- 「disc_id(正しくはid)」のINDEXに◯がない
- FKが「products_id」となっていますが、「product_id」にすべき

## Songs,Labels,Genre,Cart item
- PKである「id」が抜けている

## Songs
- 曲名をもつカラムを「song」としているが、「name」などにすべき
- 「song」のデータ型がintegerになっているが,正しくはstring

## Labels
- FK「product_id」は必要ない
- レーベル名をもつカラムを「label」としているが、「name」などにすべき

## Artists
- FK「product_id」は必要ない
- 「artist」のデータ型がintegerになってるが、正しくはstring
- アーティスト名をもつカラムを「artist」としているが、「name」などにすべき
- FKはAUTO INCREMENtではない,INDEXにする必要もない

## Genre
- FK「product_id」は必要ない
- テーブル名が単数形になっている
- FKはAUTO INCREMENtではない,INDEXにする必要もない
- 「genre」のデータ型がintegerになってるが、正しくはstring
- ジャンル名をもつカラムを「genre」としているが、「name」などにすべき

## Cart item
- テーブル名が単数形になっている。_で区切ってcart_itemとするのが正しい
- FKが「products_id」となっていますが、「product_id」にすべき
- FKはAUTO INCREMENtではない,INDEXにする必要もない
- 「buy num」となっているが「buy_num」とする必要がある
- 「subtotal」は必要ない

## Buy details
- テーブル名が「受注詳細」の意味になっていないので「order_details」などにするべき
- [Buy details]が多で[Buy]が1なので、FKとして「buy_id」が必要
- 「buy num」が何を表しているかわかりにくい&スネークケースになっていない。「qunantity」などにするべき

## Buy
- テーブル名が「受注」の意味になっていないので「orders」などにするべき
- Buy detailsで述べたとおり、[Buy details]が多で[Buy]が1なのでFK「buy_details_Id」は必要ない
- 「pay」のデータ型はintegerにして、enumで管理したほうがいい
- 「pay」が何を意味しているかわかりにくいので、「payment_method」などにすべき
- 「buy_at」はcreated_atと同じなので、必要ない
- 「stock」が何を表しているかわからないので、「total_price」などにすべき
- 送付先住所はあるが、郵便番号と住所がない

**研修担当レビュー**
<font color="Red">再提出の際はこのレビューを残しておいてください。</font>

## 全体
- created_atが全てユーザ登録日時になっていますが、問題ありませんか。
- updated_atが全てユーザ更新日時になっていますが、問題ありませんか。
## Users
- user_という接頭辞がついているカラムがある点は問題ありませんか。
- "「user_tel」のデータ型がstringになっているが,正しくはinteger "という抽出がありますが電話番号のカラムは、計算に使う必要がなく、先頭のゼロに意味があることからstring型で作るのが望ましいです。
- "user_tel"などでカラム名に略語を使っていますが、問題ありませんか。
- 郵便番号がinteger型になっていますが、問題ありませんか。
- カラムの命名規則として、「カラム名だけで何を表しているか分かること」があります。
	- member_statusが会員の何のステータスを表しているか分かりますか。
- 配送先を複数登録することを考慮してない

## Products
- カラム名にproduct_という接頭辞がついていますが、問題ありませんか。
- 在庫数をカラムで管理していますが問題ありませんか。

## Discs
- FKがproducts_idとなっていますが、product_idにすべきです

## Songs
- 曲名をもつカラムがsongになっていますが、問題ありませんか。

## Labels
- product_idがありますが、問題ありませんか。
- レーベル名をlabelカラムで持っていますが、問題ありませんか。

## Artists
- product_idがありますが、問題ありませんか。
- アーティスト名をartistカラムで持っていますが、問題ありませんか。

## Genre
- product_idがありますが、問題ありませんか。
- ジャンル名をgenreカラムで持っていますが、問題ありませんか。

## Cart item
- products_idではなく、product_idにすべき。
- buy numの_(アンダースコア)がない。
- 小計金額は不要。
	- 数量と商品の価格から算出可能.
## Buy
- テーブルbuyだと「受注」の意味になっていません。
	- orderなどにするべき。
- payが何を意味しているか不明。
	- payment_methodなどにするべき。
- 支払合計がstockになっていて意味不明。
	- total_priceなどにするべき。
- 送付先住所はあるが、郵便番号と住所がない。
## Buy details
- buy detailsだと受注詳細の意味になっていません。
	- order_details などのするべき。
- buy numは意味不明。スネークケースになってない。
	- qunantityなどにするべき。
	

# フィードバック2回目
[add]→付け加えなければいけないところ
[fix]→修正が必要なところ
[comment]→その他コメント（修正ではないけど、確認して欲しいポイントです）

## 全体
[add]→カラムにテーブル名と同じワードを入れない
[add]→命名に略語を使わない。user_l_nameのlってなんですか？ってこと。全体で指摘した上で、各各のテーブルで指摘するのがベター。

## Users
- 「user_tel」などでカラム名に略語を使ってるが、略語は使うべきでない
[fix]→更に、データ型がおかしい。
- 「member_status」のデータ型がstringになっているが,正しくはboolean
[fix]→enumを使う場合はbool型でも構わないので、boolが正しいと言い切ってしまうのは不適。要するにデータ型はstringでdefaultがfalseになっており、矛盾していることが間違っているということ。
- 「member_status」というカラム名では会員の何のステータスを表しているか分からない
[fix]→更に、データ型がおかしい。

## Products
[add]→子テーブルのidを持っている

## Discs
[add]→ディスク番号はどのように管理するか
