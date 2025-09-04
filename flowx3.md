```mermaid

flowchart TD
  MMDIFF{MMに「HPと異なる 会社名+住所」あり?}
  MMDIFF -- Yes --> MMX[MMから 会社名・住所・電話・代表 を抽出/正規化]
  MMX --> MMM[法人番号 名寄せ（MM）]
  MMM --> MMS{名寄せ成功?}
  MMS -- Yes --> HQ[HQ 本社確定]
  MMS -- No --> ADD[追加検索へ]
  MMDIFF -- No --> ADD
