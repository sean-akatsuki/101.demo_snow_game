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
- 一般ユーザ/app_user--ロールをグループapp_userに紐づく
- レビュアー/app_adm--ロールをグループapp_admに紐づく

## 4. UI  
### 4.1 Module/モジュール  

![app1 module](https://github.com/sean-akatsuki/101.demo_snow_game/assets/18321490/462410ef-3e79-4361-a436-b0441b60e95b)

### 4.2 Form  
Game/ゲームビュー  
![app1 form](https://github.com/sean-akatsuki/101.demo_snow_game/assets/18321490/8fdd8948-36e2-4342-800e-38a7dd63819b)

GameReview/レビュービュー
![app1 reviewform](https://github.com/sean-akatsuki/101.demo_snow_game/assets/18321490/ed12cbe6-12e9-4b1d-8940-d95eb405c938)

### 4.3 Client-Side制御
**Game/ゲーム**  
- 一般ユーザーはレコードを作成できる。入力必須提示がある
- 一般ユーザは自分作ったレコードを更新できるが、一部の項目の更新が可能、更新可能以外の項目を編集できないにする、ボタンUpdateを表示する。
- 一般ユーザは他人のレコードを更新できない、ボタンUpdateを表示しない、画面項目を編集できないにする
- 一般ユーザはレコードを削除できない、ボタンDeleteを表示しない。
- レビュアーはレコードを作成・更新・削除できる
- 更新の際、入力したリリース日付を当時日付と比べて、リリース済みフラグを設定する

**GameReview/ゲームレビュー**  
- 一般ユーザーはレコードを作成できる。入力必須提示がある、ステータス=Waiting
- 一般ユーザは自分作ったレコードを更新できるが、一部の項目の更新が可能、更新可能以外の項目を編集できないにする、ボタンUpdateを表示する。
- 一般ユーザは他人のレコードを更新できない、ボタンUpdateを表示しない、画面項目を編集できないにする。
- レビュアーはレコードを更新できるが、一部の項目の更新が可能、更新可能以外の項目を編集できないにする、ボタンUpdateを表示する。
- レビュアーはステータスを更新する時、選択したステータスによって、入力必須の項目・提示メッセージが違う
- 一般ユーザ・レビュアーはレコードを削除できない、ボタンDeleteを表示しない。
- システム管理者はレコードを削除できる

## 5. Notification/通知メール
- レビューレコードが新規作成された後、レビュアーグループにメール通知を送信
- レビューレコードのステータスが変更されたとき、レコード作成者にメール通知を送信

## 6. workspace/レポート
  ![app1 workspace](https://github.com/sean-akatsuki/101.demo_snow_game/assets/18321490/00ec6d55-f64f-479b-a12d-989eab868917)
