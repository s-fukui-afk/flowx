```mermaid

flowchart TD
  S[Start: 電話番号] --> SR[検索結果 1〜3ページのURL収集]
  SR --> NORM[URL正規化・重複排除・（既訪問除外：追加検索時）]
  NORM --> CLASS[各URLを HP / MediaMaster に分類（同時評価）]
  CLASS --> HPQ{HP候補はあるか?}

  HPQ -- Yes --> HPX[HP抽出/正規化（屋号・住所・電話・代表）]
  HPX --> SAVE[HP情報をDB保存（正）]
  SAVE --> HPM[法人番号 名寄せ（HP）]
  HPM --> HPS{名寄せ成功?}

  HPQ -- No --> MMDIFF{MMに「HPと異なる 会社名+住所」あり?}
  HPS -- No --> MMDIFF
  HPS -- Yes --> HQ[HQ 本社確定]

  MMDIFF -- Yes --> MMX[MM抽出/正規化（会社名・住所・電話・代表）]
  MMDIFF -- No --> ADD[追加検索: 新クエリ/未訪問URL追加]
  MMX --> MMM[法人番号 名寄せ（MM）]
  MMM --> MMS{名寄せ成功?}
  MMS -- Yes --> HQ
  MMS -- No --> ADD

  ADD --> LOOP{最大イテレーション未満?}
  LOOP -- Yes --> SR
  LOOP -- No --> UNRES[未判定で終了]

  HQ --> BRCHK{同一法人番号の他拠点か?}
  BRCHK -- Yes --> BRLABEL{拠点種別表記あり?}
  BRCHK -- No --> ENDHQ[終了]
  BRLABEL -- Yes --> BR[BR 支社確定]
  BRLABEL -- No --> UK[UNKNOWN 未分類拠点]
