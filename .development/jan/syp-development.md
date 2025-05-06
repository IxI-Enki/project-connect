```mermaid
classDiagram
   direction LR
namespace AceIsHigh{


    class Card {
        +Guid Id
        +String[16] Suit
        +String[16] Rank
        +Guid? PlayerId
        +Guid? DeckId
    }

    class Deck {
        +Guid Id
        +Guid SessionId
        +List~Card~ Cards
    }

    class Game {
        +Guid Id
        +Guid SessionId
        +Int CurrentTurn
        +Guid? WinnerId
        +Boolean IsFinished
    }

    class Player {
        +Guid Id
        +String[64] Name
        +Guid SessionId
        +List~Card~ Hand
        +Boolean IsReady
        +Boolean IsHost
    }

    class Session {
        +Guid Id
        +String[64] SessionCode
        +List~Player~ Players
        +Boolean IsGameStarted
        +DateTime CreatedAt
        +Guid? HostPlayerId
    }
}
```

---
```mermaid
erDiagram
    SESSION ||--o{ PLAYER : contains
    SESSION ||--o{ DECK : has
    SESSION ||--o{ GAME : has
    PLAYER ||--o{ CARD : holds
    DECK ||--o{ CARD : contains
    GAME ||--o{ PLAYER : winner
    SESSION {
        Guid Id PK
        String SessionCode
        Boolean IsGameStarted
        DateTime CreatedAt
        Guid HostPlayerId FK
    }
    PLAYER {
        Guid Id PK
        String Name
        Guid SessionId FK
        Boolean IsReady
        Boolean IsHost
    }
    CARD {
        Guid Id PK
        String Suit
        String Rank
        Guid PlayerId FK
        Guid DeckId FK
    }
    DECK {
        Guid Id PK
        Guid SessionId FK
    }
    GAME {
        Guid Id PK
        Guid SessionId FK
        Int CurrentTurn
        Guid WinnerId FK
        Boolean IsFinished
    }
```
---
```mermaid
erDiagram
    SESSION ||--o{ PLAYER : contains
    SESSION ||--o| PLAYER : hosted_by
    SESSION {
        Guid Id PK
        String SessionCode
        Boolean IsGameStarted
        DateTime CreatedAt
        Guid HostPlayerId FK
    }
    PLAYER {
        Guid Id PK
        String Name
        Guid SessionId FK
        Boolean IsReady
        Boolean IsHost
    }
```
---
```mermaid
erDiagram
    SESSION ||--o{ DECK : has
    DECK ||--o{ CARD : contains
    PLAYER ||--o{ CARD : holds
    DECK {
        Guid Id PK
        Guid SessionId FK
    }
    CARD {
        Guid Id PK
        String Suit
        String Rank
        Guid PlayerId FK
        Guid DeckId FK
    }
    SESSION {
        Guid Id PK
    }
    PLAYER {
        Guid Id PK
    }
```
---
```mermaid
erDiagram
    SESSION ||--o{ GAME : has
    GAME ||--o| PLAYER : winner
    SESSION {
        Guid Id PK
    }
    GAME {
        Guid Id PK
        Guid SessionId FK
        Int CurrentTurn
        Guid WinnerId FK
        Boolean IsFinished
    }
    PLAYER {
        Guid Id PK
    }
```

---
# <p align="center"> Ace is High - Sequenzdiagramme </p>
---

## 1. Starten einer Session
```mermaid
graph LR
    A[User klickt 'Start Session'] --> B[Frontend sendet CreateSessionRequest an WebSocket-Server]
    B --> C{Server prüft Anfrage}
    C -->|Gültig| D[Erstelle neue Session mit SessionCode]
    D --> E[Erstelle Host-Player mit IsHost=true]
    E --> F[Füge Player zur Session hinzu]
    F --> G[Generiere Session-Link]
    G --> H[Sende SessionCode an Frontend]
    H --> I[Frontend zeigt Session-Link]
    C -->|Ungültig| J[Sende Fehlermeldung an Frontend]
    J --> K[Frontend zeigt Fehler]
```
---
```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant WebSocketServer
    participant Session
    participant Player

    User->>Frontend: Klickt "Start Session"
    Frontend->>WebSocketServer: CreateSessionRequest
    WebSocketServer->>Session: Create()
    Session-->>WebSocketServer: Session {Id, SessionCode}
    WebSocketServer->>Player: Create(Name, IsHost=true)
    Player-->>WebSocketServer: Player {Id, Name}
    WebSocketServer->>Session: AddPlayer(Player)
    Session-->>WebSocketServer: Updated Session
    WebSocketServer->>Frontend: SessionCode, Redirect to Session
    Frontend->>User: Zeigt Session-Link
```
---

## 2. Beitreten einer Session
```mermaid
graph LR
    A[User klickt 'Join Session'] --> B[Frontend zeigt Eingabefeld für SessionCode]
    B --> C[User gibt SessionCode ein]
    C --> D[Frontend sendet JoinSessionRequest an WebSocket-Server]
    D --> E{Server prüft SessionCode}
    E -->|Gültig| F[Erstelle neuen Player mit IsHost=false]
    F --> G{Spieler bereits in Session?}
    G -->|Nein| H[Füge Player zur Session hinzu]
    H --> I[Benachrichtige Host über neuen Spieler]
    I --> J[Sende Join Success an Frontend]
    J --> K[Frontend leitet zu Session weiter]
    E -->|Ungültig| L[Sende Fehlermeldung an Frontend]
    L --> M[Frontend zeigt Fehler]
    G -->|Ja| L
```
---
```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant WebSocketServer
    participant Session
    participant Player

    User->>Frontend: Klickt "Join Session", gibt SessionCode ein
    Frontend->>WebSocketServer: JoinSessionRequest(SessionCode, Name)
    WebSocketServer->>Session: FindBySessionCode(SessionCode)
    alt Session existiert
        Session-->>WebSocketServer: Session
        WebSocketServer->>Player: Create(Name, IsHost=false)
        Player-->>WebSocketServer: Player {Id, Name}
        WebSocketServer->>Session: AddPlayer(Player)
        Session-->>WebSocketServer: Updated Session
        WebSocketServer->>Frontend: Join Success, Redirect to Session
        WebSocketServer->>Frontend: Notify Host (New Player Joined)
        Frontend->>User: Zeigt Session
    else Session existiert nicht
        WebSocketServer->>Frontend: Error (Invalid SessionCode)
        Frontend->>User: Zeigt Fehlermeldung
    end
```
---

## 3. Spielstart
```mermaid
graph LR
    A[User klickt 'Start Game'] --> B[Frontend sendet SetReadyRequest an WebSocket-Server]
    B --> C[Server setzt Player.IsReady=true]
    C --> D{Server prüft: Alle Spieler bereit?}
    D -->|Ja| E[Setze Session.IsGameStarted=true]
    E --> F[Erstelle neues Game-Objekt]
    F --> G[Erstelle neues Deck mit gemischten Karten]
    G --> H[Benachrichtige alle Spieler: Spiel gestartet]
    H --> I[Frontend zeigt Spieloberfläche]
    D -->|Nein| J[Benachrichtige alle Spieler: Warten auf Spieler]
    J --> K[Frontend zeigt Wartebildschirm]
```
---
```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant WebSocketServer
    participant Session
    participant Player
    participant Game
    participant Deck

    User->>Frontend: Klickt "Start Game"
    Frontend->>WebSocketServer: SetReadyRequest(PlayerId)
    WebSocketServer->>Player: Set IsReady=true
    Player-->>WebSocketServer: Updated Player
    WebSocketServer->>Session: CheckAllPlayersReady()
    alt Alle Spieler bereit
        Session-->>WebSocketServer: IsGameStarted=true
        WebSocketServer->>Game: Create(SessionId)
        Game-->>WebSocketServer: Game {Id, SessionId}
        WebSocketServer->>Deck: Create(SessionId)
        Deck-->>WebSocketServer: Deck {Id, Cards}
        WebSocketServer->>Frontend: Notify All (Game Started)
        Frontend->>User: Zeigt Spieloberfläche
    else Nicht alle bereit
        WebSocketServer->>Frontend: Notify All (Waiting for Players)
        Frontend->>User: Zeigt Wartebildschirm
    end
```
---

## 4. Kartenziehen und Rundenablauf
```mermaid
graph LR
    A[Spiel gestartet] --> B{Für jeden Spieler}
    B --> C[Deck: Ziehe Karte]
    C --> D[Player: Füge Karte zu Hand hinzu]
    D --> E[Benachrichtige Spieler: Neue Karte]
    E --> F{Nächster Spieler?}
    F -->|Ja| C
    F -->|Nein| G[Starte Rundenablauf]
    G --> H{Für jede Runde}
    H --> I[Game: Bestimme aktuellen Spieler]
    I --> J[Benachrichtige Spieler: Dein Zug]
    J --> K[Spieler wählt Karte]
    K --> L[Frontend sendet PlayCard an Server]
    L --> M[Player: Entferne Karte aus Hand]
    M --> N[Game: Speichere gespielte Karte]
    N --> O[Game: Nächster Zug]
    O --> P[Benachrichtige alle: Karte gespielt]
    P --> Q{Nächste Runde?}
    Q -->|Ja| H
    Q -->|Nein| R[Gehe zu Gewinnerermittlung]
```
---
```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant WebSocketServer
    participant Game
    participant Deck
    participant Player
    participant Card

    loop Für jeden Spieler
        WebSocketServer->>Deck: DrawCard()
        Deck-->>Card: Card {Id, Suit, Rank}
        WebSocketServer->>Player: AddCardToHand(Card)
        Player-->>WebSocketServer: Updated Hand
        WebSocketServer->>Frontend: Notify Player (New Card)
        Frontend->>User: Zeigt Karte
    end
    loop Jede Runde
        WebSocketServer->>Game: GetCurrentTurnPlayer()
        Game-->>WebSocketServer: PlayerId
        WebSocketServer->>Frontend: Notify Current Player (Your Turn)
        User->>Frontend: Spielt Karte
        Frontend->>WebSocketServer: PlayCard(PlayerId, CardId)
        WebSocketServer->>Player: RemoveCardFromHand(CardId)
        Player-->>WebSocketServer: Updated Hand
        WebSocketServer->>Game: RecordPlayedCard(Card)
        Game-->>WebSocketServer: Next Turn
        WebSocketServer->>Frontend: Notify All (Card Played, Next Turn)
        Frontend->>User: Aktualisiert Spielstatus
    end
```
---

## 5. Gewinnerermittlung
```mermaid
graph LR
    A[Runden beendet] --> B[Game: Prüfe Gewinnbedingung]
    B --> C{Gewinner gefunden?}
    C -->|Ja| D[Game: Setze WinnerId, IsFinished=true]
    D --> E[Benachrichtige alle Spieler: Spielende, Gewinner]
    E --> F[Frontend zeigt Gewinner]
    C -->|Nein| G[Benachrichtige alle: Spiel läuft weiter]
    G --> H[Frontend zeigt aktuellen Spielstatus]
```
---
```mermaid
sequenceDiagram
    actor User
    participant Frontend
    participant WebSocketServer
    participant Game
    participant Player

    WebSocketServer->>Game: CheckWinCondition()
    alt Gewinner gefunden
        Game-->>WebSocketServer: WinnerId, IsFinished=true
        WebSocketServer->>Player: Set Winner
        Player-->>WebSocketServer: Winner
        WebSocketServer->>Frontend: Notify All (Game Ended, Winner)
        Frontend->>User: Zeigt Gew 内
    else Spiel läuft weiter
        WebSocketServer->>Frontend: Notify All (Continue Game)
        Frontend->>User: Zeigt Spielstatus
    end
```
---