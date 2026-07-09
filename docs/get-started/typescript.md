import os
import speech_recognition as sr
import pyttsx3
import webbrowser
import datetime

engine = pyttsx3.init()

def speak(text):
    print("Deeva:", text)
    engine.say(text)
    engine.runAndWait()

def listen():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        audio = r.listen(source)

    try:
        command = r.recognize_google(audio).lower()
        print("You:", command)
        return command
    except:
        return ""

speak("Hello! I am Deeva. How can I help you?")

while True:
    command = listen()

    if "hello" in command:
        speak("Hello Anil!")

    elif "time" in command:
        speak("Current time is " + datetime.datetime.now().strftime("%I:%M %p"))

    elif "youtube" in command:
        webbrowser.open("https://youtube.com")
        speak("Opening YouTube")

    elif "google" in command:
        webbrowser.open("https://google.com")
        speak("Opening Google")

    elif "exit" in command:
        speak("Goodbye!")
        break  description: 'Tells the current time in a specified city.',
  instruction: `You are a helpful assistant that tells the current time in a city.
                Use the 'getCurrentTime' tool for this purpose.`,
  tools: [getCurrentTime],
});
```

### Set your API key

This project uses the Gemini API, which requires an API key. If you
don't already have Gemini API key, create a key in Google AI Studio on the
[API Keys](https://aistudio.google.com/app/apikey) page.

In a terminal window, write your API key into your `.env` file of your project
to set environment variables:

=== "MacOS / Linux"

    ```bash title="Update: my-agent/.env"
    echo 'GEMINI_API_KEY="YOUR_API_KEY"' > .env
    ```

=== "Windows PowerShell"

    ```console title="Update: my-agent/.env"
    echo 'GEMINI_API_KEY="YOUR_API_KEY"' > .env
    ```

=== "Windows Command Prompt"

    ```console title="Update: my-agent/.env"
    echo GEMINI_API_KEY="YOUR_API_KEY" > .env
    ```

??? tip "Using other AI models with ADK"
    ADK supports the use of many generative AI models. For more
    information on configuring other models in ADK agents, see
    [Models & Authentication](/agents/models).

## Run your agent

You can run your ADK agent with the `@google/adk-devtools` library as an
interactive command-line interface using the `run` command or the ADK web user
interface using the `web` command. Both these options allow you to test and
interact with your agent.

### Run with command-line interface

Run your agent with the ADK TypeScript command-line interface tool
using the following command:

```console
npx adk run agent.ts
```

![adk-run.png](/assets/adk-run.png)

### Run with web interface

Run your agent with the ADK web interface using the following command:

```console
npx adk web
```

This command starts a web server with a chat interface for your agent. You can
access the web interface at `http://localhost:8000`. Select your agent at the
upper right corner and type a request.
