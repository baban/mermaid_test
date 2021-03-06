
```mermaid
sequenceDiagram
    rect rgb(235, 235, 235)
    note right of U: 既存機能のエリア
    actor U as User
    participant B as Browser
    participant S as Server
    participant M as Mailer
    participant Slack
    activate B
    B->>+S: フォームページをリクエスト(/sell/entry_inquiry/)
    deactivate B
    S-->>-B: フォームページを返す
    activate B
    B->>+U: フォームのページ
    U->>U: 物件情報とユーザーの連絡先を登録
    U-->>-B: 送信
    B->>+U: 確認ページをレンダリング
    U->>U: 送信確認画面を確認
    U-->>-B: 送信
    B->>+S: フォームで入力された項目を送信
    S->>S: ユーザーとアカウントを作成
    S->>M: 登録完了メール
    activate M
    M-->>M: パスワード設定メール送信
    deactivate M
    end
    S-->>-B: 返信
    B->>+U: 完了ページ#9829;
    U->>U:面談予約フォームをフォームに送信する
    U-->>-B: 面談予約時間を送信
    B->>+S: POST 面談時間
    S->>S:  面談時間をDBに保存
    S->>M: メール配信
    S->>Slack: Slackへ配信
    S -->>- B: 登録結果
    B ->> U: 面談登録結果を表示
    deactivate B
```