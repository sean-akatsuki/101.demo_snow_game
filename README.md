# 101.demo_snow_game:a servicenow  demonstration project/SNOW練習プロジェクト  
## 1. Requirements/要件概要  
- ユーザがゲームレコードを作成する
- 作成したゲームレコードに基づいて、ユーザがゲームのレビューをリクエストする
- レビュアーグループのメンバーがリクエストされたゲームレビューを評価してApprove/Rejectする

## 2. Data Modeling/データモデリング
### 2.1 テーブル設計
**テーブル-Game/ゲーム**  
|カラム|タイプ|ラベル|
| :---        |    :----   |          :---- |
|Game_id|String|ゲームID|
|Title|String|ゲーム名|
|Developer|String|開発者|
|Esrb_rating|Choice|ESRBレイティング|
|Genre|Choice|ジャンル/体裁|
|release_date|Date|リリース日付|
|released|boolean|リリース済みフラグ|
|reviewed|boolean|レビュー提出済みフラグ|

**テーブル-GameReview/ゲームレビュー**  
|カラム|タイプ|ラベル|
| :---        |    :----   |          :---- |
|review_id|String|レビューID|
|game|reference|ゲーム|
|reviewer|reference|レビュアー|
|Stars|Choice|オススメ|
|review_date|date|レビュー日付|
|status|Choice|レビューステータス|
|comment_his|Journal|コメント履歴|
### 2.2 テーブル実装
source file:
dictionary/x_1058161_game_rev_game.xml  
dictionary/x_1058161_game_rev_game_review.xml    

## 3. Role/アプリロール
- 一般ユーザ/app_user
- レビュー/app_adm

