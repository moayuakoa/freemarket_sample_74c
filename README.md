## ER図
[![Image from Gyazo](https://i.gyazo.com/907ad06f26dca32fbcd159a8c7c32bcf.png)](https://gyazo.com/907ad06f26dca32fbcd159a8c7c32bcf)
# freemarket_sample_74c

# フリマアプリのクローンサイト。
![c215521bb708fd14f5ce31b646ad830c](https://github.com/suzukisabataro/freemarket_sample_74c/blob/master/public/image/c215521bb708fd14f5ce31b646ad830c.gif)

# フリマアプリ訪問
URL: http://46.51.232.119//

ID: teamb

Pass: bbbb

 購入用アカウント: sell@gmail.com

 パスワード： 1234567

 出品用アカウント: buy@gmail.com

 パスワード: 1234567

# 機能一覧
 ・ユーザ登録(session と devise を用いたページ遷移あり),ログイン機能全般

 ・facebook/googele での omniauth 認証(ローカル環境のみ)

 ・商品出品機能

 ・多階層カテゴリー(ancestry)

 ・画像のプレビュー機能(jquery) 

 ・複数画像アップロード(carrierwave)

 ・商品購入機能(payjp)

 ・検索機能(ransack)

 ・自動デプロイ(capistrano)
 
 # 主に携わった開発⬇︎
 開発担当箇所（担当箇所一覧）

・DB設計(テーブル設計)

・本番環境デプロイ

・トップページ(フロントエンド/サーバーサイド)

・マイページ（フロントエンド）

・購入完了ページ（フロントエンド）

・商品カテゴリー機能(フロントエンド/サーバーサイド)

・パンくず(フロントエンド/サーバーサイド)

・イメージ画像スライド実装

・各担当箇所の詳細⬇︎

# DB設計

概要

   　▪︎　必要なテーブル、カラムの選定とアソシエーションの関係

実施内容

    ▪︎　Lucidchartのツールを使ってER図の作成

    ▪︎　READMEにテーブルとアソシエーションを記述


# トップページ

概要

   　▪︎　トップページのマークアップと商品の一覧表示

実施内容

    ▪︎　サービス内容がわかるビューの表示

    ▪︎　商品出品されたアイテムとカテゴリー別のデータの紐付け

    ▪︎　カテゴリー別と新着アイテムの一覧表示

    ▪︎　swiperAPIを使ってスライド画像実装

# カテゴリ機能

概要

   　▪︎　カテゴリー一覧画面の作成各カテゴリに属する商品の表示

   　▪︎　ドロッ プダウンメニューの作成中

実施内容

   　▪︎　ancestryのgemを使った経路列挙型テーブルの作成

   　▪︎　各カテゴリページの作成

   　▪︎  各カテゴリに属する商品の取得及び表示

   　▪︎　カテゴリーのドロップダウン 表示作成

# ユーザーマイページ

概要

   　▪︎　ユーザーが編集やログアウトできるページ

実施内容

   　▪︎　マイページのビューとログアウトできるページを作成



# パンくずリスト

概要

   　▪︎　gretelのgemでページの視覚化

実施内容

   　▪︎　パンくずリストのルート作成及び設置

# 購入完了ページ

概要

   　　▪︎　ユーザーが商品購入を確認できるページ

実施内容

   　　▪︎　商品購入完了ページ作成


## Usersテーブル
|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false|
|password|string|null: false|
|image|string||
|family_name|string|null: false|
|first_name|string|null: false|
|family_name_kana|string|null: false|
|first_name_kana|string|null: false|
|birth_day_yy|integer|null: false|
|birth_day_mm|integer|null: false|
|birth_day_dd|integer|null: false|
|introduuction|text||
|phone_number|integer|null: false|

### Association
- belongs_to_active_hash :birth_day_yy
- belongs_to_active_hash :birth_day_mm
- belongs_to_active_hash :birth_day_dd
- belongs_to_active_hash :prefecture
- has_many :items
- has_many :comments
- has_one :credit_card, (pay.ja使用)
- has_one :address

## Addressテーブル
|Column|Type|Options|
|------|----|-------|
|postal_code|intager|null: false|
|prefecture|integer|null: false|
|city|string|null: false|
|address1（番地）|string|null: false|
|building_name|string|
|user_id|refarences|null: false, foreign_key: true|
### Association
- belongs_to :user

## Credit_cardsテーブル(pay.ja使用)
|Column|Type|Options|
|------|----|-------|
|costomer_id|intager|null: false|
|cord_id|intager|null: false|
|user_id|refarences|null: false, foreign_key: true|
### Association
- belongs_to :user

## Commentsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|refarences|null: false, foreign_key: true|
|items_id|refarences|null: false, foreign_key: true|
|commtnt|text|null: false|

### Association
- belongs_to :user
- belongs_to :item

## Likesテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|refarences|null: false, foreign_key: true|
|item_id|refarences|null: false, foreign_key: true|
### Association
- belongs_to :user
- belongs_to :item

## Itemsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|description|text|null: false|
|price|integer|null: false|
|brand_id|refarences|foreign_key: true|
|item_condition_id(商品状態)|reference|null: false, foreign_key: true|
|size_id|refarences|null: false|
|delivery_charge|references|null: false, foreign_key: true|
|delivery_day_id|references|null: false, foreign_key: true|
|delivery_way_id|references|null: false, foreign_key: true|
|prefecture_id|references|null: false, foreign_key: true|
|category_id|references|null: false, foreign_key: true|
|user_id|references|null: false, foreign_key: true|

### Association
- belongs_to_active_hash :item_condition
- belongs_to_active_hash :delivery_charge
- belongs_to_active_hash :delivery_day
- belongs_to_active_hash :delivery_way
- belongs_to_active_hash :delivery_way
- belongs_to_active_hash :prefecture
- belongs_to_active_hash :size
- belongs_to :categories
- belongs_to : brand
- has_many :images
- belongs_to :user
- add_index :items, :name

## Brandsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
### Association
- has_many :items

## categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|ancestry|null: false|
### Association
- has_many :items
- has_ancestry

## Item_imagesテーブル
|Column|Type|Options|
|------|----|-------|
|item_id|references|null: false, foreign_key: true|
|item_images|string|null: false|
### Association
- belongs_to :item
