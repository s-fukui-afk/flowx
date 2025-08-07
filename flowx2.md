```mermaid

sequenceDiagram
    participant Operator as オペレーター
    participant FlowX as WEBアプリケーション (FlowX)
    participant AndroidApp as Android通話アプリ
    participant CallLogServer as 通話ログ管理サーバー
    participant Carrier as キャリア網
    participant STTServer as Speech to Text

    Operator->>FlowX: 通話終了ボタンをクリック
    FlowX->>AndroidApp: 通話終了指示
    AndroidApp->>Carrier: 通話切断
    AndroidApp->>CallLogServer: 通話終了ログを送信
    FlowX->>CallLogServer: 架電結果登録画面を表示
    
    Note over CallLogServer,Carrier: 別途
    CallLogServer->>Carrier: 通話ファイル取得要求
    Carrier-->>CallLogServer: 通話ファイルを送信
    CallLogServer->>STTServer: 通話ファイルを送信
    STTServer-->>CallLogServer: テキストデータを受信
    
    Note over CallLogServer,Operator: 人手とは別に
    CallLogServer->>CallLogServer: テキストデータから情報を解析
    CallLogServer->>CallLogServer: アポイント日時・通話概要を登録
    
    Operator->>FlowX: 架電結果情報を入力
    FlowX->>CallLogServer: 架電結果登録
