#アプリケーション名  
chatroom-37607  
#アプリケーション概要  
スマホのチャットによって部署と社員間の連絡を取りやすくすることで必要な情報を共有しやすくする。  
#URL  
https://chatroom-37607.herokuapp.com/  
#テスト用アカウント  
Basic認証パスワード : 2222  
パスワードID : admin  
メールアドレス1 : aa@go  
パスワード1 : 111111  
メールアドレス2 : bb@go  
パスワード2 : 222222  
#利用方法  
チャット投稿  
1.一覧ページの左上よりユーザー新規登録を行う。  
2.ルーム作成ボタンよりルーム作成画面に遷移してルーム名を記入してチャットしたいユーザーを選ぶ。  
3.ルーム画面でフォームに文字を記入して投稿ボタンを選択する。  
画像投稿  
1.チャット投稿の2まで行い、ルーム画面の画像ボタンを押して投稿したい画像を選択する。  
ルームの切り替えヘッドバーのプルダウンの中より確認したいルームを選ぶ  
#アプリケーションを制作した背景  
前職では社員間または部署間の連絡は基本的に電話で行われていた。この方法だと着信音に気づかなかった場合折り返し電話をしないと内容が分からず時間がかかってしまう問題があった。その解決策として自分のLINEアカウントを使用していた部長がいたがアカウントに内容は自由にしたかったので極一部の人とのやりとりに使用していた。このことから会社内のみで使えるチャットアプリがあると便利だと思い開発することにした。
#洗い出した要件  
要件定義シート(https://docs.google.com/spreadsheets/d/1eqeS6C0okQ6ibNkkoKuDWfUo0wUQq-aE6QxdJRUjGCM/edit#gid=982722306)  
#実装した機能について  
ユーザー管理機能  
チャット管理機能  
#実装予定の機能  
単体テストの実装  
写真を保存して共有できる機能  
#データベース設計  
[![Image from Gyazo](https://i.gyazo.com/5328865fb8919ed6c03a5733a15a8b23.png)](https://gyazo.com/5328865fb8919ed6c03a5733a15a8b23)
#画面遷移図
[![Image from Gyazo](https://i.gyazo.com/39530735815fc367745b0fea55a934eb.png)](https://gyazo.com/39530735815fc367745b0fea55a934eb)
#開発環境  
・フロントエンド  
・バックエンド  
・インフラ  
・テキストエディタ  
・タスク管理  
#ローカルでの動作方法  
以下のコマンドを順に実行  
％ git clone https://github.com/aki2314/chatroom  
％ cd chatroom  
％bundle install  
％ yarn install  

#工夫したポイント  
スマホ用を目的としているので画面が小さいことを想定してなるべく各要素を小さくしてチャット機能の範囲を広くしました。
その中でもルームの選択画面をプルダウン方式にする部分が一番試行錯誤した箇所です。

















# テーブル設計

## users テーブル

| Column             | Type   | Options     |
| ------------------ | ------ | ------------|
| group              | string | null: false |
| encrypted_password | string | null: false |
| nickname           | string | null: false |

### Association

- has_many :messages
- has_many :rooms, through: :room_users

## rooms テーブル

| Column | Type   | Options     |
| ------ | ------ | ----------- |
| name   | string | null: false |


### Association

- has_many :messages
- has_many :users, through: :room_users

## room_users テーブル

| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| user   | references | null: false, foreign_key: true |
| room   | references | null: false, foreign_key: true |

### Association

- belongs_to :room
- belongs_to :user

## messages テーブル

| Column  | Type       | Options                        |
| ------- | ---------- | ------------------------------ |
| content | string     |                                |
| user    | references | null: false, foreign_key: true |
| room    | references | null: false, foreign_key: true |

### Association

- belongs_to :room
- belongs_to :user