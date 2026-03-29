# Gemini API Key Setup Guide

## 1. Get Your Gemini API Key

1. Go to https://aistudio.google.com/app/apikeys
2. Click **"Create API key"**
3. Select your Google AI project (or create a new one)
4. Copy the API key (looks like: `AIza...`)

## 2. Add Key to `.env`

Open `.env` in the project root and replace:
```
GEMINI_API_KEY="YOUR_ACTUAL_GEMINI_API_KEY_HERE"
```

With your actual key:
```
GEMINI_API_KEY="AIzaXxxx..."
```

## 3. Restart Dev Server

After saving `.env`, restart your dev server:
```bash
npm run dev
```

## 4. Verify API Key is Loaded

Open **Browser Console** (F12 → Console tab) and look for:

✅ **Success Messages** (you should see these):
```
🎮 Imposter Game - API Key present: true
API Key present: true
🤖 Calling Gemini API for word pair in category: ხელი
✅ Word pair generated: ვაშლი vs მსხალი
```

❌ **Error Messages** (if you see these, fix the key):
```
⚠️  GEMINI_API_KEY is not set. Add it to your .env file
❌ Gemini API failed. Error: 401 Unauthorized
```

## 5. What Each Log Means

| Log | Meaning |
|-----|---------|
| `🎮 Imposter Game - API Key present: true` | API key loaded from .env successfully |
| `🤖 Calling Gemini API...` | Game is requesting word pair from Gemini |
| `✅ Word pair generated: X vs Y` | Gemini returned words successfully |
| `📌 Fallback: X vs Y` | API failed, using backup words instead |
| `❌ Gemini API failed` | API error (check key is correct) |

## 6. Test the Integration

1. Start the game: `http://localhost:3000`
2. Navigate to **Games → Imposter → Create Room**
3. Watch the console - you should see the word pair generation logs
4. The game should show real words (not fallback) in the description phase

## Troubleshooting

### "API Key not set" error
- Make sure `.env` file exists in project root
- Make sure `GEMINI_API_KEY="..."` is on its own line
- Make sure the key is not empty or contains quotes incorrectly

### "401 Unauthorized" error
- Your API key is invalid or expired
- Get a new key from https://aistudio.google.com/app/apikeys
- Make sure you copied the full key (it should start with `AIza`)

### Dev server not picking up changes
- Stop dev server (Ctrl+C)
- Make sure `.env` is saved
- Restart: `npm run dev`

### Still seeing fallback words?
- Check browser console for error messages
- Verify API key one more time
- Check that you successfully restarted dev server after adding key
