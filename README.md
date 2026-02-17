🤖 Local Gemini Nano Chat
A Private, Offline AI Interface for Chrome
This project is a lightweight, single-file HTML interface that allows you to chat with Gemini Nano, the large language model built directly into Google Chrome.

Unlike traditional AI tools, this doesn't use an API key, doesn't cost money, and never sends your data to the cloud. It runs 100% locally on your computer's GPU/CPU. (Really, turn off your WiFi and try it!)

✨ Features
Total Privacy: Your conversations stay on your hard drive.

Multi-Chat Sidebar: Manage multiple threads like a pro.

Persistent Memory: Uses browser Local Storage to remember multiple chat sessions.

Smart Summarization: Automatically condenses long conversations to stay within the model's token limits.

Session Sidebar: Create, name, and switch between different chat threads.

Download & Delete: Export transcripts to .txt or wipe individual chats and total history with one click.

Zero Latency: No server wait times—if your GPU is fast, the AI is fast. On the other side of tht coin, if your GPU is slow, so is this.

🚀 Setup Instructions (Chrome 144+)
Since window.ai is part of Chrome's AI Mode ecosystem, you must manually enable it and download the "brain" (on-device model).

1. Enable Chrome Flags
Paste these into your address bar and set them to Enabled:

chrome://flags/#prompt-api-for-gemini-nano

chrome://flags/#optimization-guide-on-device-model (Set to Enabled BypassPrefRequirement)

Relaunch Chrome after changing these. chrome://restart

2. Force the Model Download
Chrome needs to download the 2GB–4GB model file.

Go to chrome://components

Find Optimization Guide On Device Model.

Click Check for update.

Wait for the status to reach "Component already up to date." (If it's at 0.0.0.0, it is still downloading—give it a few minutes).

3. Run the Chat
Simply download the html files from this repo and open them with Chrome. minimi.html is a single window chat example and local_AI_with_sidebar.html is a full-featured multi-chat setup with that has persistent memory (using Chrome's local history) and the ability to export chats.

🧠 How it Works 
Local LLMs are "stateless"-they forget everything as soon as the session ends. This project fixes that using two tricks: To give the AI "memory," the script:

1. Local Handshake: Every prompt sends the last few messages from localStorage back to the AI so it "remembers" the current thread.

2. Recursive Summarization: When a chat exceeds 10 turns, the script silently asks the AI to summarize the conversation. It then replaces the "messy" history with a single Context Capsule summary, saving thousands of tokens and preventing the "Quadratic Slowdown."

This technique shrinks the history when it gets too long, ensuring the AI never exceeds its hardware-defined context window.

🛠️ Customization: Changing the AI's Personality
You can change how the AI behaves by modifying the systemPrompt in the init() function within html files.

Look for this block:

JavaScript
session = await LanguageModel.create({
    systemPrompt: "Your name is Gemini Nano. You are a local AI assistant...",
});


Try these custom prompts:

"You are an expert Senior Software Engineer. Provide concise, high-quality code snippets and architectural advice."

"You are a whimsical storyteller. Use vivid imagery and a touch of wit in all your responses."
"You are a concise engineering assistant who loves Python.",

"You are a minimalist assistant. Provide the shortest possible answer that is still accurate."

📂 Managing the Model Data
Storage: The model takes up ~4GB in your Chrome user profile. If you delete it, simply "Check for update" in chrome://components to redownload it.Chrome typically stores these models in your User Data folder under OptimizationGuidePredictionModels
RAM Limits: Local storage for chats is limited to ~5MB per site. If you have hundreds of massive chats, use the Export feature to save them as .txt and use the Clear All History button to stay lean.

Deleting/Resetting: If you delete this folder, Chrome will simply show the component as "Not Started" or "Version 0.0.0.0" in chrome://components. You can re-trigger the download by clicking Check for update.

Power Management: On laptops, Chrome may disable the local model if Battery Saver is active. Plug in your device if the model fails to initialize.


📜 License
MIT - Use it, break it, build something cool. Let me know what you build with it.