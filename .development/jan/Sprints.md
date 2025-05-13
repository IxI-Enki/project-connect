# Backlog-Punkt: WebSocket - Connection
### Titel: WebSocket - Connection  

- **Beschreibung**: Als Benutzer möchte ich mein Gerät über WebSockets mit einer gemeinsamen Sitzung verbinden, um Echtzeit-Updates (wie Hintergrundfarbänderungen) zu sehen, die von anderen verbundenen Geräten ausgelöst werden.  

- **Akzeptanzkriterien**:  
  - Mehrere Geräte können sich über WebSockets in derselben Sitzung im selben Netzwerk verbinden.  
  - Eine Aktion (z. B. ein Button-Klick) auf einem verbundenen Gerät löst eine sichtbare Änderung (z. B. Hintergrundfarbänderung) auf allen anderen verbundenen Geräten in nahezu Echtzeit aus.

- Priorität: 3  
- Geschätzter Aufwand: 3 Stunden 🙈
 
<!--
```mermaid
kanban
    title Kanban-Board: WebSocket - Connection Sprint
    section To Do
        task Recherche und Planung
            subtask Untersuchung der WebSocket-Technologie
            subtask Integration in die bestehende Architektur planen
            subtask Anforderungen für die Sitzungsverwaltung festlegen
        task Backend-Entwicklung
            subtask WebSocket-Server einrichten
            subtask Logik für Nachrichtenverarbeitung implementieren
            subtask Ereignisverarbeitung für Button-Klicks hinzufügen
        task Frontend-Entwicklung
            subtask WebSocket-Client in die Benutzeroberfläche integrieren
            subtask Funktionalität für das Senden von Nachrichten implementieren
            subtask Empfangene Nachrichten verarbeiten und anzeigen
        task Testen
            subtask Unit-Tests für die WebSocket-Verbindung schreiben
            subtask Integrationstests für mehrere Geräte durchführen
            subtask Echtzeit-Kommunikation testen
        task Dokumentation
            subtask Implementierungsdokumentation erstellen
            subtask Nutzungsdokumentation für die WebSocket-Funktion schreiben
    section In Progress
        task Recherche und Planung
            subtask Untersuchung der WebSocket-Technologie :done
            subtask Integration in die bestehende Architektur planen
            subtask Anforderungen für die Sitzungsverwaltung festlegen
    section Review
        task Backend-Entwicklung
            subtask WebSocket-Server einrichten :done
            subtask Logik für Nachrichtenverarbeitung implementieren :inprogress
            subtask Ereignisverarbeitung für Button-Klicks hinzufügen
    section Done
        task Frontend-Entwicklung
            subtask WebSocket-Client in die Benutzeroberfläche integrieren :done
            subtask Funktionalität für das Senden von Nachrichten implementieren :done
            subtask Empfangene Nachrichten verarbeiten und anzeigen :done
``` -->

---

## Sprint-Planung für „WebSocket - Connection“
<!--Um diesen Backlog-Punkt rückwirkend in einen Sprint zu integrieren, gehen wir Schritt für Schritt vor. Das Ziel ist es, eine realistische Sprint-Struktur zu erstellen, die du zum Üben nutzen kannst.-->
- ### Schritt 1: Sprint-Ziel definieren
<!-- Das Sprint-Ziel beschreibt, was am Ende des Sprints erreicht sein soll. Für diesen Backlog-Punkt lautet es:-->  
  - **Sprint-Ziel**: Implementierung der WebSocket-Verbindung, um Echtzeit-Kommunikation zwischen Geräten in einer Sitzung zu ermöglichen.

- ### Schritt 2: Sprint-Backlog erstellen
<!-- Das Sprint-Backlog besteht aus den Aufgaben, die notwendig sind, um das Sprint-Ziel zu erreichen. Basierend auf dem Backlog-Punkt und dem Projektkontext (z. B. Nutzung von WebSockets für die „Connect“-Plattform) könnten die Aufgaben wie folgt aussehen:-->
  - Recherche und Planung (4 Stunden)  
    - Untersuchung der WebSocket-Technologie und deren Integration in die bestehende Architektur (Blazor/AvaloniaUI Frontend, ASP.NET Backend).  
    - Festlegung der Anforderungen für die Sitzungsverwaltung (z. B. Verbindung im selben Netzwerk).

  - Backend-Entwicklung (8 Stunden)  
    - Einrichtung eines WebSocket-Servers zur Verwaltung von Verbindungen zwischen Geräten.  
    - Implementierung der Logik, um Nachrichten und Ereignisse (z. B. Button-Klicks) zu verarbeiten und an alle verbundenen Geräte zu senden.

  - Frontend-Entwicklung (6 Stunden)  
    - Integration eines WebSocket-Clients in die Benutzeroberfläche.  
    - Implementierung der Funktionalität, um Nachrichten zu senden (z. B. Button-Klick) und zu empfangen (z. B. Hintergrundfarbänderung anzeigen).

  - Testen (4 Stunden)  
    - Unit-Tests für die WebSocket-Verbindung (z. B. erfolgreiche Verbindungsherstellung).  
    - Integrationstests, um sicherzustellen, dass mehrere Geräte korrekt verbunden sind und Ereignisse in Echtzeit austauschen.

  - Dokumentation (2 Stunden)  
    - Erstellung einer kurzen Dokumentation zur Implementierung und Nutzung der WebSocket-Funktion.

  - **Gesamtaufwand**: 24 Stunden 
    > (Hinweis: Der ursprüngliche Aufwand von 3 Stunden war eine grobe Schätzung. In der Praxis zeigt die Aufgabenaufteilung, dass der tatsächliche Aufwand höher ist.)

- ### Schritt 3: Sprint-Dauer festlegen
  <!-- Obwohl der ursprüngliche Aufwand mit 3 Stunden angegeben wurde, ist es realistischer, einen Sprint von einer Woche (5 Arbeitstagen) anzunehmen. Dies bietet genug Zeit, um die Aufgaben zu erledigen und zusätzliche Puffer für unerwartete Probleme oder Teamabstimmungen einzuplanen. Für ein kleines Team (z. B. Imre und Jan) könnte der Sprint so organisiert werden, dass die 24 Stunden Arbeit über die Woche verteilt werden.-->
  - Sprint-Dauer: 1 Woche (z. B. Montag bis Freitag).

- ### Schritt 4: Sprint-Planung
  <!-- In einer kurzen Planungssitzung (z. B. 30 Minuten) würde das Team:-->
  - Die Aufgaben im Sprint-Backlog besprechen.  
  - Verantwortlichkeiten zuweisen (z. B. Imre übernimmt Frontend, Jan übernimmt Backend).  
  - Sicherstellen, dass alle Ressourcen (z. B. Entwicklungsumgebung, Testgeräte) verfügbar sind.

---
- realistischer Aufwand
```mermaid
gantt
    title Gantt Chart: WebSocket - Connection Sprint
    dateFormat  YYYY-MM-DD
    axisFormat  %m-%d
    section Tasks
    Recherche und Planung    :a1, 2025-05-19, 0.5d
    Backend-Entwicklung     :a2, after a1, 1d
    Frontend-Entwicklung    :a3, after a1, 0.75d
    Testen                  :a4, after a2, 0.5d
    Dokumentation           :a5, after a4, 0.25d
    section Reviews
    Sprint Review           :a6, 2025-05-23, 1h
    Sprint Retrospektive    :a7, after a6, 0.5h
```
---

- ### Schritt 5: Durchführung des Sprints
  <!-- Während der Woche arbeitet das Team an den Aufgaben: -->
  **Tägliche Stand-ups (15 Minuten täglich)**: Fortschritt besprechen, Hindernisse identifizieren (z. B. Probleme mit der WebSocket-Konfiguration).  

  - #### Verteilung:  
    - **Montag**: Recherche und Planung abschließen.  
    - **Dienstag-Mittwoch**: Backend- und Frontend-Entwicklung.  
    - **Donnerstag**: Testen.  
    - **Freitag**: Dokumentation und Abschluss.

- ### Schritt 6: Sprint-Review
  > Am Ende der Woche (z. B. Freitag) wird ein Sprint-Review abgehalten:  
  > Dauer: 1 Stunde.  

  - **Inhalt**: Demonstration der WebSocket-Verbindung (z. B. zwei Geräte verbinden, Button klicken, Hintergrundfarbe ändert sich auf beiden).  
  - **Ergebnis**: Überprüfung der Akzeptanzkriterien – funktioniert die Echtzeit-Kommunikation wie gewünscht?

- ### Schritt 7: Sprint-Retrospektive
  > Nach dem Review reflektiert das Team:  
  > Dauer: 30 Minuten.  

  - **Fragen**:  
    - Was lief gut? (z. B. schnelle Implementierung des WebSocket-Servers)  
    - Was kann verbessert werden? (z. B. bessere Aufwandsschätzung)

  - **Ergebnis**: Erkenntnisse für zukünftige Sprints dokumentieren.

  - #### **Zusammenfassung des Sprints**
    - **Sprint-Dauer**: 1 Woche  
    - **Sprint-Ziel**: Implementierung der WebSocket-Verbindung für Echtzeit-Kommunikation.  

  - #### **Sprint-Backlog**:  
    - Recherche und Planung (4 Stunden)  
    - Backend-Entwicklung (8 Stunden)  
    - Frontend-Entwicklung (6 Stunden)  
    - Testen (4 Stunden)  
    - Dokumentation (2 Stunden)
    - **Team**: Imre Obermüller (Frontend), Jan Ritt (Backend)  
    - **Ergebnis**: Eine funktionsfähige WebSocket-Verbindung, die es mehreren Geräten ermöglicht, sich zu verbinden und Echtzeit-Updates (z. B. Hintergrundfarbänderungen) auszutauschen.

