```mermaid
sequenceDiagram
    participant Operator as オペレーター
    participant FlowX as WEBアプリケーション (FlowX)
    participant AndroidApp as Android通話アプリ
    participant CallLogServer as 通話ログ管理サーバー
    participant Carrier as キャリア網

    Operator->>FlowX: 発信ボタンをクリック
    FlowX->>AndroidApp: 発信指示 + 通話先情報
    AndroidApp->>Carrier: 発信
    Carrier-->>AndroidApp: 接続確立
    AndroidApp->>CallLogServer: 通話開始ログを送信
    CallLogServer-->>FlowX: 通話開始を通知
    Note over AndroidApp,Carrier: 通話開始
