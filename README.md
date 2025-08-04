```mermaid

graph TD
    A[案件評価完了] --> B{"IF: Rule 3の条件に合致？<br>特定ユーザー/業種/資本金<br>+ 商材:Easier<br>+ アウトレット:3 or 5"};
    B -- YES --> C["Rule 3 適用プロセス"];
    C --> C1{"HS: REQ-01-M01, M02<br>検出されたか？"};
    C1 -- YES / NO --> C2["アクション: 除外<br>→ 無視する (詰め直し不要)"];
    
    C2 --> C3{"Add: REQ-01-P02<br>検出されなかったか？"};
    C3 -- YES / NO --> C4["アクション: 追加しない<br>→ 無視する (詰め直し不要)"];

    C4 --> C5{"Deduct: REQ-04-M01など<br>検出されたか？"};
    C5 -- YES --> F_Rework["詰め直し指示を生成"];
    C5 -- NO --> G_Pass["詰め直し指示を生成しない"];

    B -- NO --> D["Rule 2 適用プロセス"];
    D --> D1{"IF: Rule 2の条件に合致？<br>商材:Easier<br>+ アウトレット:3 or 5"};
    D1 -- YES --> E["Rule 2 アクション評価開始"];
    E --> E1{"HS: REQ-01-M01<br>検出されたか？"};
    E1 -- YES / NO --> E2["アクション: 除外<br>→ 無視する (詰め直し不要)"];

    E2 --> E3{"Add: REQ-01-P02<br>検出されなかったか？"};
    E3 -- YES --> F_Rework;

    E3 -- NO --> E4{"Deduct: REQ-04-M01など<br>検出されたか？"};
    E4 -- YES --> F_Rework;
    E4 -- NO --> G_Pass;
    
    D1 -- NO --> H["標準ルール(Rule 1)へ<br>(この図ではスコープ外)"];

    subgraph "優先度1: Rule 3"
        C
        C1
        C2
        C3
        C4
        C5
    end

    subgraph "優先度2: Rule 2"
        D
        D1
        E
        E1
        E2
        E3
        E4
    end

    %% --- スタイル定義 ---
    style F_Rework fill:#d9534f,color:#fff,stroke:#333
    style G_Pass fill:#5cb85c,color:#fff,stroke:#333
    style C fill:#e6f3ff,stroke:#333
    style D fill:#fff3e6,stroke:#333
