# Project Proposal: Browser-Based Game Engine

---
## **3. Objectives/Goals**
The goal of this project is to develop a fully browser-based game engine with the following features:

- **Simplicity & Accessibility**: The engine should be intuitive and easy to use for users of all ages.  
- **Platform Independence**: Games should run on any modern web browser without requiring installation or specialized hardware.
- **Mobile Devices as Controllers/Game Pads**: Smartphone and tablets can be registered as input devices since they are widely available and accessible to most users.
- **Flexible Display Options**: Any internet-capable screen with a browser (e.g.smartTvs, laptops, tablets, phones) can be used as a display for the game.
- **Optimization for Multiplayer Scenarios**: The engine will support different game modes:
  
  - **Couch Co-op**: Multiplayer, people in the same room play together.
  - **Distant Multiplayer**: Players connect over the internet.
  - **Multi-Screen**: Players can view different content on separate displays for innovative gameplay mechanics. e.g. active player, common area, opponent player.
  
- **Technical Aspects and Expandability**:
  
  - Initial focus on **Android + Chromium** for a quick development of a working prototype.
  - Maybe later expansion to **iOS + Safari** to reach broader user-base.
  - Use of modern web technologies to provide real-time interaction and synchronization.
  
- **Latency Minimization through Turn-Based Gameplay**: Since browser-based technologies inherently introduce some delays, the focus will be on turn-based games to ensure a fluid gaming experience.
  
---

## **1. Initial Situation:**

### **Problem**

Currently, NO existing game engine that is fully browser-based meeting the following criteria:

1. **No Local Installation Required**: Many engines rely on installable software or require special hardware.
2. **Flexible Use of Controllers and Displays**:
   - Standard PC games require keyboard/mouse combo or gamepads
   - Consoles rely on dedicated controllers, which are included when buying a new console, but very expensive when replacing them.
   - Browser-based games rarely use smartphones as controllers or support multiple screens simultaneously.

3. **Multiplayer Optimization**:
   - Existing browser-based games are often limited to very simple concepts, mainly found in the gambling industry.
   - Latency issues prevent real-time interaction in more complex game genres.

### **Solution & Challenges**

- Web-based game services like **Google Stadia/Xbox Cloud Gaming** do exist, but are **mainly streaming services** that require powerful servers.
- Technologies like **WebSockets and WebRTC** enable real-time communication, but no unified platform has been developed specifically for browser-based multiplayer games.
- Most established game engines like Unity, Unreal or Godot are designed for native applications/games and require additional plugins/addons for web compatibility.

---

## **4. General Conditions and Constraints:**

### **Technical Frameworks**

- **Technology Stack**:
  - Frontend: HTML5, CSS and JavaScript including Libraries and Frameworks. **>>TO BE REPLACED<<**
  - Real-time communication: WebSockets / WebRTC for synchronization between controllers and screens
  - Backend: Node.js with Express / WebSocket server for session and turn management. **>>TO BE REPLACED<<**
  - Storage: Minimal data requirements (e.g. for high scores and game states) => Optional integration of NOSQL databases like MongoDB or Firebase.
  - Compatibility: Initial version Android & Chromium, later expansion to iOS.
  
### **Gameplay Mechanics and Use Cases**

- **Game Types**: Limited to turn-based or non-time-sensitive games because of the fact of latency issues, e.g. educational games, turn-based strategy a.s.o.
- **Connection Methods**:
  - Devices identify themselves via QR codes or short links for easy user-friendly registration in the game.
  - No app required - everything runs in te browser!
  
### **Limitations and Challenges**

- **Latency Issues**: Real-time games require fast reaction times. This is not our target group.
- **Platform Differences**: iOS and Safari have different restrictions for WebSockets and WebRTC!
- **Privacy & Security**:
  - Minimization of personal data collection, the least possible data overhead.
  - Secure session management
  - No third-party cloud services needed unless necessary for data protection.

### **Conclusion**

This game engine presents an innovative solution for making multiplayer games easily accessible through the browser on any device. It allows smartphones to be used as controllers and any screen as a display, without requiring specialized hardware or software installation. The implementation focuses on turn-based games to avoid latency issues and provides a platform for couch co-op, distant multiplayer, and multi-screen gameplay experiences.
