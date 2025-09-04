```mermaid

flowchart TD
  HPQ{HP候補はあるか?}
  HPQ -- Yes --> HPX[HPから 屋号・住所・電話・代表 を抽出/正規化]
  HPX --> SAVE[HP情報をDB保存（正）]
  SAVE --> HPM[法人番号 名寄せ（HP）]
  HPM --> HPS{名寄せ成功?}
  HPS -- Yes --> HQ[HQ 本社確定]
  HPS -- No --> MMDIFF{MMに「HPと異なる 会社名+住所」あり?}
  HPQ -- No --> MMDIFF
