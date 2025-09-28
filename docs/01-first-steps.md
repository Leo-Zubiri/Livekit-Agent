# First steps

## Environment

We need to get all Keys to set the environment, create `.env.local`

From Livekit Cloud or the Self hosted livekit server get:

```env
LIVEKIT_URL=
LIVEKIT_API_KEY=
LIVEKIT_API_SECRET=
```

Get keys for STT (Speech to Text), TTS (Text To Speech) and the LLM (Large Language Model)

```env
OPENAI_API_KEY=
DEEPGRAM_API_KEY=
CARTESIA_API_KEY=
```

## Sync Packages

It's neccesary to have `UV` package manager. `pip install uv`

```ps
uv sync
```

Before the first run it's necessary to download some models

```uv
uv run python src/agent.py download-files
```

Next, run this command to speak to your agent directly in your terminal:

```console
uv run python src/agent.py console
```

To run the agent for use with a frontend or telephony, use the `dev` command:

```console
uv run python src/agent.py dev
```

In production, use the `start` command:

```console
uv run python src/agent.py start
```