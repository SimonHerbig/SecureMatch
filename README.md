# SecureMatch
The Challenge: Traditional cybersecurity training often struggles with low user engagement.

The Solution: A Privacy-First, Gamified Interaction Loop. "Secure Match" is a Public Security User Interface (PSUI) [prototype designed to solve this](https://www.figma.com/proto/fkKpp87tJ7glGrov6AkjdH/SecureMatch-Prototype?node-id=1-2&starting-point-node-id=1%3A2&t=PpDtmNnlRbMUkY4J-1). It creates an engaging, multi-stage experience that encourages active participation while protecting user privacy.

Core Concept: Gesture-Voting, Balanced Grouping & AI-Assisted Chat

The core innovation is its unique, three-stage interaction model:

1. Gesture-Based Voting: Users are presented with security scenarios as simple Yes/No questions (e.g., "Is this email a phishing attempt?"). They vote in real-time using intuitive, privacy-preserving gestures: nodding for "Yes" or shaking their head for "No".

2. Balanced Grouping (via Public Display): After voting, the system forms balanced discussion groups composed of users who gave different answers. This is designed to foster debate and peer-to-peer learning. These groups are visualized on a central public display.

3. QR-Code Transfer & AI Chat: To continue the discussion privately, users can scan a QR code from the display, transferring the chat to their personal devices. Within this chat, messages that begin with @ai will summon an automated assistant powered by DeepSeek to provide more information about the current topic. These answers also include suggested follow-up questions to keep the discussion going.

This loop (Vote -> Group -> Transfer) maximizes engagement by encouraging active discussion between users with opposing viewpoints, all while maintaining privacy.

## Getting Started

1. Install dependencies:
   ```sh
   npm install
   ```
2. Start the WebSocket server:
   ```sh
   # DEEPSEEK_API_KEY is optional but required for the @ai assistant
   DEEPSEEK_API_KEY=your_key npm run server
   ```
   This starts a Socket.IO server on <http://localhost:3001>.

3. Start the development server:
   ```sh
   npm run dev
   ```
   The app runs on <http://localhost:8080> by default.
   You can view aggregated session statistics at <http://localhost:8080/stats> while the server is running.
4. Build for production:
   ```sh
   npm run build
   ```
   The production files will be output to the `dist` directory.

## Code Overview

- **src/pages/Index.tsx** – main page that rotates through questions, collects votes and shows charts.
- **src/components/WebcamFeed.tsx** – handles MediaPipe face detection and interprets head gestures.
- **src/components/VoteChart.tsx** – displays the yes/no vote counts.
- **src/components/ChatInterface.tsx** – modal chat window that connects to a Socket.IO chat server and can generate a QR code for joining from another device.
- **src/services/dataService.ts** – stores session data and lightweight analytics in `localStorage`.
- **src/services/websocketService.ts** – WebSocket client wrapper used by the chat interface.
- **src/pages/Stats.tsx** – visualizes anonymous event logs and vote data.

Voting runs entirely in the browser. A small Node.js server handles real-time chat messages.

## Technologies

- React + TypeScript
- Vite
- Tailwind CSS and shadcn-ui components
- MediaPipe for facial gesture detection

## Deployment

After building the project, serve the contents of the `dist` folder with any static hosting provider.
