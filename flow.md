```mermaid

flowchart TD
  S[Start: 電話番号] --> SR[検索結果 1〜3ページのURL収集]
  SR --> NORM[URL正規化・重複排除・既訪問除外]
  NORM --> CLASS[各URLを HP / MediaMaster に分類（同時評価）]
  CLASS --> HPQ{HP候補はあるか?}
