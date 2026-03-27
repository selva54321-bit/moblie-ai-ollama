# 🤖 MajaAI

MajaAI is a sleek, completely private React Native chat application that runs a large language model (LLM) locally on your own machine. It features a premium, animated dark-mode UI and connects to a localized AI backend using [Ollama](https://ollama.com/).

Because the AI runs locally on your device/computer, **no data is sent to the cloud**, making it fast, private, and free to use!

---

## 🛠️ Prerequisites

Before you start, make sure you have the following installed:
1. **Node.js**: (v18+ recommended)
2. **React Native Environment**: [Setup guide for Android/iOS](https://reactnative.dev/docs/environment-setup) (Android Studio for Android, Xcode for iOS)
3. **Ollama**: Download from [ollama.com](https://ollama.com/)

---

## 🧠 Step 1: Setting up the Local AI (Ollama)

You have two options for hosting the AI: running it on your computer, or running it directly on your Android phone!

### Option A: Host on your Computer
This app uses the lightweight `qwen2.5:0.5b` model by default so it runs smoothly even on older laptops.
1. **Install Ollama** on your computer.
2. **Open your computer's terminal** and run the following command to download and start the AI model:
   ```bash
   ollama run qwen2.5:0.5b
   ```
3. Ensure the Ollama server is running in the background. It typically listens on `http://127.0.0.1:11434`.

### Option B: Host directly on your Phone (via Termux)
If you want the AI to live completely on your Android device:
1. Download and install **Termux** (from F-Droid).
2. Install Ollama inside your Termux environment.
3. Pull a tiny model to play with directly on your phone:
   ```bash
   ollama run qwen2.5:0.5b
   ```
*(Note: Because the React Native app makes a fetch request to `127.0.0.1`, it will seamlessly connect to the Ollama backend running inside Termux on your actual device!)*

---

## 📱 Step 2: Running the Mobile App

1. **Navigate to the app directory:**
   ```bash
   cd majaai
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Link Localhost for Android (Crucial)**
   By default, the Android emulator uses `10.0.2.2` to access your computer's localhost. Because our app points to `127.0.0.1`, you need to set up a port forward via ADB so the emulator can talk to Ollama:
   ```bash
   adb reverse tcp:11434 tcp:11434
   ```
   *(Note: The app is already configured with `android:usesCleartextTraffic="true"` to allow local HTTP requests).*

4. **Start the Metro Bundler:**
   ```bash
   npm start
   ```

5. **Run the App:**
   With the Metro Bundler running, press **`a`** to open the app on your Android emulator or connected device, or press **`i`** to run on the iOS simulator.
   
   Alternatively, open a new terminal and run:
   * **Android:** `npm run android`
   * **iOS:** `npm run ios` (Make sure to run `cd ios && pod install && cd ..` first on Mac)

---

## 🎨 Features
* **Completely Private:** All conversation data stays local.
* **Premium Animations:** Messages smoothly slide and fade in.
* **Spring Physics:** Interactive buttons utilizing React Native's Native Driver.
* **Keyboard Avoiding:** Automatically handles user keyboard popping up and down seamlessly.
* **Dark Mode Theme:** Beautiful, eye-friendly layout.

## ⚙️ Changing the AI Model
If your computer is powerful and you want to use a smarter model (like `llama3` or `qwen2.5:7b`), simply download it via Ollama (`ollama run llama3`) and update the model name in `App.tsx`:

```javascript
// App.tsx
body: JSON.stringify({
  model: 'llama3', // <-- change this to your preferred local model
  messages: updatedMessages,
  stream: false 
}),
```