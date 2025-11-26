```mermaid
flowchart TD

    A([Start]) --> B[Detect Flashdrive]

    B -->|Removable Drive Found| C[Set usbPath + tokenFilePath]
    B -->|No Drive Found| B

    C --> D{tokens.txt exists?}
    D -->|Yes| E[Load tokens]
    D -->|No| F[Create tokens.txt with 0 tokens] --> E

    E --> G{Main Menu}

    G -->|1 View Tokens| H[Display token count] --> G
    G -->|2 Add Tokens| I[Ask user for amount] --> J[Add and Save Tokens] --> G
    G -->|3 Play Blackjack| K{Enough Tokens?}

    K -->|No| L[Display 'Not Enough Tokens'] --> G
    K -->|Yes| M[Deduct 3 Tokens and Save] --> N[Run Blackjack Game] --> G

    G -->|4 Play Detective Riley| O{Enough Tokens?}
    O -->|No| L2[Display 'Not Enough Tokens'] --> G
    O -->|Yes| P[Deduct 2 Tokens and Save] --> Q[Run Detective Riley Game] --> G

    G -->|5 Play Tic Tac Toe| R{Enough Tokens?}
    R -->|No| L3[Display 'Not Enough Tokens'] --> G
    R -->|Yes| S[Deduct 1 Token and Save] --> T[Run TicTacToe Game] --> G

    G -->|6 Exit| U[Save Tokens] --> V([End])

    %% Blackjack Logic
    N --> N1[3 Rounds]
    N1 --> N2{Hit or Stand?}
    N2 -->|Hit| N3[Draw card, Update total]
    N2 -->|Stand| N4[Dealer plays]
    N3 --> N5{Player bust?}
    N5 -->|Yes| N6[Dealer Wins] --> N1
    N5 -->|No| N2
    N4 --> N7[Compare totals] --> N1
    N1 -->|After 3 Rounds| N8[Display final winner] --> Ndone([Return to Menu])

    %% Detective Riley Logic
    Q --> Q1[Input-based branching story]
    Q1 --> Q2{Correct choices?}
    Q2 -->|Yes| Q3[Gain clues, Continue Story]
    Q2 -->|No| Q4[Game Over]
    Q3 --> Q1
    Q1 -->|Clues enough & correct final choice| Q5[Case Solved]
    Q5 --> Qdone([Return to Menu])
    Q4 --> Qdone

    %% Tic Tac Toe Logic
    T --> T1[Initialize 3x3 board]
    T1 --> T2{Board Full or Win?}
    T2 -->|No| T3[Player Move]
    T3 --> T4[AI Move]
    T4 --> T2
    T2 -->|Yes| T5[Display Winner or Draw] --> Tdone([Return to Menu])


