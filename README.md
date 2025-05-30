# TulgaTTS
**TulgaTTS is an AI-based text-to-speech (TTS) library that generates speech using various voices popular in Kazakhstan. It leverages Character AI technology to synthesize natural-sounding speech from text.**

## Installation

```bash
# Via pip (in the future)
pip install tulgatts
# For audio playback (optional):
pip install -e .[audio]
```

## Getting Started

1.  **Obtain your token:**
    *   ⚠️ **DO NOT SHARE YOUR TOKEN!** It is required to send requests from your account.
    *   Open link https://character.ai/chat/2WPyJRflV_4nTx6_-tuNrhkiiqhDyOsn9O25BR1sDO8
    *   Open **Developer Tools** in your browser (usually F12).
    *   Go to the **Network** tab.
    *   Refresh the page or send a message to any character.
    *   In the list of network requests, click on any request (for example, to `/settings`).
    ![How to find the Authorization Token](https://github.com/dauitsuragan002/tulgatts/raw/main/img/asset.jpg)
    *   Go to the **Headers** section.
    *   Find the **Authorization** header. It will look like:
        ```
        Authorization: Token <your_token_here>
        ```
    *   Copy only the token part (after `Token `).
    *   Set the `CHARACTER_AI_TOKEN` environment variable or create a `.env` file in the project root and add `CHARACTER_AI_TOKEN=your_copied_token`.
    **Authorization easy (use for mobile) script**  
    If you want to easily obtain your CharacterAI token using your email, you can use the provided `auth.py` script:

    ```sh
    pip install characterai
    python auth.py
    ```
    - Enter your email address.
    - Open the sign-in link sent to your email (you can do this on your mobile).
    - Paste the link back into the script prompt.
    - The script will save your token to `user_token.txt` in the format required for `.env`.

    This makes it easy to get your token without using browser developer tools.

2.  Use the library.

## Usage Examples
You can use the library in several ways. For simple scripts, use the synchronous method; for async applications, use the `async`/`await` method.
### 1. The simplest usage

```python
from tulgatts import TulgaTTS

# Create a client (default voice – Tokaev)
client = TulgaTTS(api_token="CHARACTER_AI_TOKEN", voice="Tokaev")

# 1. Speak with the default voice and save to file
client.say("This is an example created with this class")
```

### 2. Synchronous usage

```python
import os
from tulgatts import TulgaTTS
from dotenv import load_dotenv

# Load token from .env
load_dotenv()
api_token = os.getenv("CHARACTER_AI_TOKEN")
def sync_say_usage():
    if not api_token:
        print("❌ No token!")
        return
    try:
        tts_client = TulgaTTS(api_token=api_token, voice='Tokaev')
        print(f"✅ Client ready with voice '{tts_client.voice}'.")
        tts_client.say("Synchronous example.", output_file="sync_example.mp3")
        print("🎧 File ready: sync_example.mp3")
    except Exception as e:
        print(f"⚠️ Error occurred: {e}")

if __name__ == "__main__":
    print("2. Synchronous example...")
    sync_say_usage()
    print("-" * 20)
```

### 3. Asynchronous usage
```python
import os, asyncio
from tulgatts import TulgaTTS
from dotenv import load_dotenv

# Load token from .env
load_dotenv()
api_token = os.getenv("CHARACTER_AI_TOKEN")

async def advanced_async_say():
    if not api_token: return print("No token!")
    try:
        tts_client = TulgaTTS(api_token=api_token)
        print(f"Client ready with voice '{tts_client.voice}'.")
        await tts_client.say_async("Third example, part one.", voice="Tokaev", output_file="advanced_async1.mp3", play_audio=True)
    except Exception as e: print(f"Error: {e}")

if __name__ == "__main__":
    print("\n3. More advanced async example...")
    asyncio.run(advanced_async_say())
    print("All examples completed.")
```

## Available Voices
The library comes with the following pre-configured voices:
*   Nursultan Nazarbaev
*   Tokaev
*   Pavel Durov
*   Nurlan Saburov
*   Putin
*   Skriptonit
*   Elon Musk
*   Albert E
*   Yandex Alica
*   J.A.R.V.I.S
*   Tony Stark

Note: Sometimes TulgaTTS may not synthesize your expected text. This issue is being worked on.
Special thanks to [PyCharacterAI](https://github.com/Xtr4F/PyCharacterAI) for enabling TTS with Character AI voices. And special thanks to [CharacterAI](https://github.com/kramcat/CharacterAI) for the authentication script.

## Authors
- David Suragan (TulgaTTS)
- Gemini AI

## License
MIT
