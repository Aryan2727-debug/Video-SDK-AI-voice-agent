# VideoSDK AI Voice Agent — Telephony Demo

An AI-powered voice agent that handles inbound and outbound phone calls using [VideoSDK's Telephony feature](https://docs.videosdk.live/telephony/introduction) and Google's Gemini model for real-time voice interaction.

## Overview

This project demonstrates how to build an AI telephony agent that can:

- **Receive inbound calls** — Callers dial a Twilio phone number, which routes to the agent via VideoSDK's Inbound Gateway.
- **Make outbound calls** — The agent can dial out to external phone numbers via VideoSDK's Outbound Gateway.
- **Converse in real-time** — Uses Google Gemini's native audio model for natural, low-latency voice conversations.

### How It Works

1. A phone number purchased from **Twilio** is configured as a SIP trunk connected to VideoSDK.
2. When a call comes in, VideoSDK's **Inbound Gateway** validates and routes it to a meeting room.
3. The AI agent (registered as `MyTelephonyAgent`) picks up the job, joins the room, and starts a real-time voice session.
4. **Gemini 2.5 Flash** (native audio preview) powers the conversational AI, responding directly with audio.
5. The SIP-to-WebRTC bridge allows seamless communication between the phone caller and the AI agent.

### Architecture

```
Caller (Phone) → Twilio SIP Trunk → VideoSDK Inbound Gateway → VideoSDK Meeting Room ← AI Agent (this project)
```

## Prerequisites

- Python 3.10+
- A [VideoSDK](https://app.videosdk.live/) account with a valid auth token
- A [Google AI](https://aistudio.google.com/) API key (for Gemini)
- A [Twilio](https://www.twilio.com/) phone number configured with VideoSDK's SIP integration

## Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/<your-username>/Video-SDK-AI-voice-agent.git
   cd Video-SDK-AI-voice-agent
   ```

2. **Create and activate a virtual environment**

   ```bash
   python -m venv .venv

   # Windows
   .venv\Scripts\activate

   # macOS/Linux
   source .venv/bin/activate
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**

   Create a `.env` file in the project root:

   ```env
   VIDEOSDK_AUTH_TOKEN=<your-videosdk-auth-token>
   GOOGLE_API_KEY=<your-google-api-key>
   ```

5. **Run the agent**

   ```bash
   python main.py
   ```

   The agent will register with VideoSDK and start listening for incoming call assignments on port `8081`.

## Project Structure

```
├── main.py              # Agent entry point and configuration
├── requirements.txt     # Python dependencies
├── .env                 # Environment variables (not committed)
└── README.md
```

## Configuration

Key settings in `main.py`:

| Parameter | Description |
|---|---|
| `agent_id` | Unique identifier for routing calls to this agent (`MyTelephonyAgent`) |
| `register` | Registers the agent with VideoSDK's backend for telephony |
| `max_processes` | Maximum number of concurrent calls to handle |
| `model` | Gemini model used for voice AI (`gemini-2.5-flash-native-audio-preview-12-2025`) |
| `voice` | Gemini voice persona (`Leda`) |

## Dependencies

- **videosdk-agents** — VideoSDK's agent framework for managing sessions, rooms, and telephony
- **videosdk-plugins-google** — Google Gemini integration for real-time voice AI
- **python-dotenv** — Loads environment variables from `.env`

## Resources

- [VideoSDK Telephony Docs](https://docs.videosdk.live/telephony/introduction)
- [VideoSDK AI Telephony Agent Quick Start](https://docs.videosdk.live/telephony/ai-telephony-agent-quick-start)
- [VideoSDK Dashboard](https://app.videosdk.live/)
- [Google AI Studio](https://aistudio.google.com/)