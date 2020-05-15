
# トレーニング・食事管理アプリ（仮）
### 目的
ボディメイクの「続ける」をサポートすることで「目標達成」へ導く

### 要件
- 基礎代謝を算出する
  - 性別・年齢・身長・体重を入力すると基礎代謝が算出される
  - ユーザー登録不要
- 消費カロリーを算出する
  - 運動強度を選択すると消費カロリーが算出される
  - ユーザー登録不要
- 目標体重・期限をもとに1日の摂取カロリーを算出する
  - 目標体重・期限を指定すると摂取カロリーとPFCバランスが算出される
   - ユーザー登録不要
- マイページ 
  - ユーザー登録すると使用可能
  - カレンダー
  - トレーニング管理
  - 食事管理
  - アイテム購入
- スケジュール管理
  - トレーニングメニュー・食事内容をカレンダーで管理できる
- トレーニング管理（Record）
  - トレーニングメニュー（種目・重量・REP数・セット数）を登録できる
  - カレンダー機能と連携している
- 食事管理
  - 食品マスタが用意されている
  - 自分で食事メニューを登録できる
  - 食品マスタからメニューを選択すると、カロリー、PFCバランスを自動計算
  - スケジュールと連携し日毎の消費カロリー、PFCバランスを管
  - メニューは検索できる
- アイテム購入
  - プロテインやトレーニンググッズなどを特別価格で購入できる
- SNS連携（Commitment,Share）
  - 今日のトレーニング内容、摂取目標カロリーを自動投稿（コミットメント）
  - トレーニングの実績を自動投稿（シェア）

#### 追加要件
- ユーザー間コラボレーション
  - 電子会議室
  - ダイレクトメッセージ
  - いいね、フレンド登録
- プロフィール

### 設計

#### 画面遷移
- トップページ⇨ログインページ⇨マイページ⇨各種機能

#### ビュー
- トップページ
- サインアップページ
- ログインページ
- マイページ
- カレンダー
- 食事管理
- アイテム購入
- ログアウト

### DB設計
#### usersテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, unique:true|
|mail|string|null: false, unique:true|
|password|string|null: false|
|tall|integer|null: false|
|weight|integer|null: false|
|target_weight|integer|null: false|
|exercise_intensity|integer|null: false|
|deadline|date|null: false|

##### Association
- has_many :lift_managements
- has_many :food_managements

#### liftsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, unique:true|
|part|string|null: false, unique:true|
|detail|text|null: false|

##### Association
- has_many :lift_managements

#### foodsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, unique:true|
|size|string|null: false, unique:true|
|calorie|string|null: false|
|protein|integer|null: false|
|fat|integer|null: false|
|carbohydrate|integer|null: false|

##### Association
- has_many :food_managements

#### food_managementsテーブル
|Column|Type|Options|
|------|----|-------|
|user|integer|null: false|
|food|integer|null: false|
|date|date|null: false|

##### Association
- belongs_to :user
- belongs_to :food

#### lift_managementsテーブル
|Column|Type|Options|
|------|----|-------|
|user|integer|null: false|
|lifts|integer|null: false|
|weight|integer|null: false|
|set|integer|null: false|
|rep|integer|null: false|

##### Association
- belongs_to :user
- belongs_to :lift
