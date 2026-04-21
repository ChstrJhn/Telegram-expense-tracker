# 🤖 Telegram Expense Tracker Bot

An AI-powered Telegram bot that logs your daily expenses to Google Sheets using **n8n**, **Gemini AI**, and the **Telegram Bot API**.

## Features
- Accepts **text, voice, and photo** (receipt) inputs via Telegram
- Uses Gemini AI to extract: category, item, quantity, price, payment method, and date
- Supports **multiple expenses in one message**
- Sends a **confirmation message** before saving
- Appends structured rows to Google Sheets automatically

## Tech Stack
- [n8n](https://n8n.io) — workflow automation (self-hosted on Pikapods)
- [Gemini AI](https://ai.google.dev) — text parsing, audio transcription, receipt OCR
- [Telegram Bot API](https://core.telegram.org/bots/api) — messaging interface
- [Google Sheets API](https://developers.google.com/sheets) — data storage

## How It Works

1. You send an expense message to your Telegram bot (text, voice, or photo)
2. Gemini extracts structured data from your message
3. The bot replies with a confirmation summary
4. You reply ✅ to save or ❌ to discard
5. The expense is appended as a row in Google Sheets

## Workflow Overview

![Workdlow Overview](/tg-expense-tracker-workflow.png)

## Setup

### Prerequisites
- n8n instance (self-hosted or cloud)
- Gemini API key (free at [Google AI Studio](https://aistudio.google.com))
- Telegram Bot Token (from [@BotFather](https://t.me/botfather))
- Google Sheets OAuth2 credentials

### Installation
1. Import `workflows/workflow-expense-tracker.json` into your n8n instance
2. Add your credentials (Telegram Bot, Google Gemini API key, Google Sheets OAuth2)
3. Create a Google Sheet with columns: Date, Category, Item, Quantity, Total Price, Payment Method, Raw Input — plus a `Pending` tab with columns: chat_id, resume_url, timestamp
4. Activate the workflow
5. Send your bot a message to test

## Example

**Input (text):** `"Nasi lemak RM8 cash, kopi RM3 TnG"`

**Bot reply:**
📋 Here's what I captured:

🍽️ Nasi lemak x1 — RM8.00 · Cash · 21/04/2026
☕ Kopi x1 — RM3.00 · Touch n' Go · 21/04/2026

Reply ✅ to save all, ❌ to discard, or type a correction.
