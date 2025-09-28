# Handling Errors

In addition to state changes, it's important to handle errors that may occur during a session. In real-time conversations, inference API failures can disrupt the flow, potentially leaving the agent unable to continue.

For STT, LLM, and TTS, the Agents framework includes a FallbackAdapter that can fall back to secondary providers if the primary one fails.

When in use, FallbackAdapter would:
- automatically resubmit the failed request to backup providers when the primary provider fails
- mark the failed provider as unhealthy and stop sending requests to it
- continue to use the backup providers until the primary provider recovers
- periodically checks the primary provider’s status in the background

```py
from livekit.agents import llm, stt, tts
from livekit.plugins import assemblyai, deepgram, elevenlabs, openai, groq

session = AgentSession(
    stt=stt.FallbackAdapter(
        [
            assemblyai.STT(),
            deepgram.STT(),
        ]
    ),
    llm=llm.FallbackAdapter(
        [
            openai.LLM(model="gpt-4o"),
            openai.LLM.with_azure(model="gpt-4o", ...),
        ]
    ),
    tts=tts.FallbackAdapter(
        [
            elevenlabs.TTS(...),
            groq.TTS(...),
        ]
    ),
)
```