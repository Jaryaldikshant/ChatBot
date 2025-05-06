# BitNet 

This project demonstrates how to deploy **BitNet (b1.58-2b-4t)**, a lightweight 1-bit quantized LLM, as a **sidecar container** alongside a **Flask API** using **Azure App Service for Linux**. It enables running chat completions on **CPU** only — no GPU required.

---

## 🚀 Project Overview

- Flask app exposes a `/chat` endpoint
- BitNet runs in a sidecar container using `llama.cpp` engine
- Flask app communicates with BitNet via `http://localhost:11434`

---



## 🔧 How to Deploy on Azure

### 1. Create Azure App Service (Linux)
- In Azure Portal: **Create Resource > Web App**
- Choose:
  - **Publish**: Code
  - **Runtime Stack**: Python 3.x
  - **Operating System**: Linux

### 2. Deploy Flask App
- Use GitHub, VS Code, or Zip deploy to upload your Flask project.

### 3. Add BitNet as a Sidecar Container
- Go to your App Service → **Deployment Center > Sidecar Containers**
- Add the following sidecar:

  - **Image**:  
    ```
    mcr.microsoft.com/appsvc/docs/sidecars/sample-experiment:bitnet-b1.58-2b-4t-gguf
    ```
  - **Port**: `11434`

- Save and **restart** your App Service.

---

## 🧠 Chat Endpoint (`/chat`)

Your Flask app exposes the following endpoint:

- **URL**: `/chat`
- **Method**: `POST`
- **Request Body (JSON)**:
  ```json
  {
    "message": "Hello, who are you?"
  }
  
---

## 📁 Project Structure

```plaintext
/bitnet-flask-app
├── templates/
│   └── chat.html         # Template for the chat UI
├── app.py                # Flask application with chat endpoint
├── requirements.txt      # Python dependencies
└── README.md             # Project documentation

