<div align="center">

![AI Image Generator](workflow.png)

# 🤖 AI Image Generator

**A production-ready n8n workflow that automatically generates AI images from text prompts**

[![n8n](https://img.shields.io/badge/n8n-Workflow%20Automation-blue.svg)](https://n8n.io)
[![AI](https://img.shields.io/badge/AI-Powered-purple.svg)](https://github.com/topics/ai-automation)
[![Telegram](https://img.shields.io/badge/Telegram-Bot-26A5E4?style=flat&logo=telegram)](https://telegram.org)

</div>

---

## 📖 Overview

The **AI Image Generator** is a powerful n8n workflow that transforms text descriptions into stunning AI-generated images. It supports multiple input methods including Telegram bot commands and n8n's built-in chat interface.

Simply send a text prompt, and the workflow will:
1. Optimize your prompt using AI
2. Generate a high-quality image
3. Return the image directly to you

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 📱 **Telegram Trigger** | Start generation via Telegram messages |
| 💬 **n8n Chat Trigger** | Use n8n's built-in chat interface |
| 🧠 **AI Prompt Optimization** | Automatically enhance your prompts for better results |
| 🎨 **Multiple Image Models** | Support for various image generation models |
| 📐 **Customizable Dimensions** | Configure image width and height |
| 🔄 **Automatic Processing** | End-to-end automated pipeline |
| 💾 **Save to Disk** | Optional local storage of generated images |
| 🚀 **Production Ready** | Battle-tested and reliable |

---

## 🏗️ Workflow Architecture

The workflow consists of the following nodes working in sequence:

```
┌─────────────────┐
│ Telegram Trigger │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Fields - Set    │
│ Values          │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ AI Agent -      │
│ Create Image    │
│ From Prompt     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Code - Clean    │
│ Json            │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Code - Get      │
│ Prompt          │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Code - Set      │
│ Filename        │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ HTTP Request -  │
│ Create Image    │
└────────┬────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌────────┐ ┌──────────┐
│ Save   │ │ Telegram │
│ Image  │ │ Response │
└────────┘ └──────────┘
```

### Node Descriptions

| # | Node | Purpose |
|---|------|---------|
| 1 | **Telegram Trigger** | Listens for incoming Telegram messages to trigger the workflow |
| 2 | **Fields - Set Values** | Sets default values for image model, width, and height |
| 3 | **AI Agent - Create Image From Prompt** | Uses AI to optimize and enhance the user's text prompt |
| 4 | **Code - Clean Json** | Parses and cleans the AI agent's JSON response |
| 5 | **Code - Get Prompt** | Extracts the optimized prompt for image generation |
| 6 | **Code - Set Filename** | Generates unique filenames for saved images |
| 7 | **HTTP Request - Create Image** | Calls the Pollinations API to generate the image |
| 8 | **Save Image To Disk** | Saves the generated image to local storage |
| 9 | **Telegram Response** | Sends the generated image back to the user via Telegram |

---

## 📋 Requirements

| Requirement | Required | Description |
|-------------|----------|-------------|
| [n8n](https://n8n.io) | ✅ Yes | Self-hosted or cloud instance |
| [Pollinations API](https://pollinations.ai) | ✅ Yes | Free API for image generation |
| [Telegram Bot](https://telegram.org) | 🔶 Optional | For Telegram trigger functionality |
| [OpenRouter API](https://openrouter.ai) | 🔶 Optional | For AI prompt optimization |

---

## 📥 Installation

### Step 1: Download

Download the `workflow.json` file from this directory.

### Step 2: Import into n8n

1. Open your n8n instance
2. Click **Add Workflow** → **Import from File**
3. Select the downloaded `workflow.json`

### Step 3: Configure Credentials

Set up the required credentials in each node:

- **Telegram Trigger**: Add your Telegram Bot API credentials
- **AI Agent**: Configure your OpenRouter API credentials
- **Telegram Response**: Link your Telegram Bot credentials

### Step 4: Update Settings

Modify the `Fields - Set Values` node to customize:

- **model**: Image generation model (default: `flux`)
- **width**: Image width in pixels (default: `1080`)
- **height**: Image height in pixels (default: `1920`)

### Step 5: Activate

Click the **Active** toggle to enable the workflow.

### Step 6: Test

Send a message to your Telegram bot or use n8n's chat to test the workflow.

---

## 📂 Folder Contents

| File | Description |
|------|-------------|
| `workflow.json` | n8n workflow definition — import directly into n8n |
| `workflow.png` | Visual screenshot of the workflow |
| `README.md` | This documentation file |

---

## 🔧 Customization

### Image Size

Modify the `Fields - Set Values` node:

```json
{
  "width": "1080",
  "height": "1920"
}
```

### Image Model

Change the model in `Fields - Set Values`:

```json
{
  "model": "flux"
}
```

Available models via Pollinations:
- `flux` (default)
- `flux-realism`
- `flux-anime`
- `turbo`

### Prompt Optimization

The AI Agent uses a comprehensive system prompt for image generation. You can customize it in the **AI Agent** node's `systemMessage` field.

### Save Location

Modify the `Save Image To Disk` node to change where images are stored:

```
/files/{{ fileName }}
```

### AI Provider

Replace the **OpenRouter Chat Model** node with any n8n-supported language model:
- OpenAI
- Google Gemini
- Anthropic
- Local models

---

## 📸 Screenshot

The workflow screenshot is available at:

```
workflow.png
```

![Workflow Screenshot](workflow.png)

---

## 📄 License

This workflow is licensed under the MIT License — see the [LICENSE](../../LICENSE) file for details.

---

## 🔗 Links

- [GitHub Repository](https://github.com/MazenHaroun/workflows)
- [n8n Documentation](https://docs.n8n.io)
- [Pollinations API](https://pollinations.ai)

---

<div align="center">

**Made with ❤️ by [Mazen Haroun](https://github.com/MazenHaroun)**

</div>
