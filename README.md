# B-READY Methodology Chatbot

A web-based chatbot that answers questions about the World Bank's Business Ready (B-READY) methodology using the Methodology Handbook (Second Edition).

![B-READY Chatbot](https://img.shields.io/badge/B--READY-Methodology%20Assistant-002244)

## Features

- 💬 **Conversational Interface**: Ask questions in natural language
- 📚 **Comprehensive Knowledge**: Trained on the full B-READY Methodology Handbook
- 🔍 **Smart Search**: Automatically finds relevant handbook sections
- 📱 **Responsive Design**: Works on desktop and mobile
- ⚡ **Fast Responses**: Powered by Claude AI

## Quick Deploy to Netlify

### Option 1: One-Click Deploy (Recommended)

1. Click the button below:
   
   [![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start)

2. Connect your GitHub account and create a new repository

3. After deployment, go to **Site Settings** → **Environment Variables**

4. Add your API key:
   - **Key**: `ANTHROPIC_API_KEY`
   - **Value**: Your Claude API key from [console.anthropic.com](https://console.anthropic.com)

5. Redeploy the site (Deploys → Trigger deploy)

### Option 2: Manual Deploy via Netlify CLI

1. **Install Netlify CLI**:
   ```bash
   npm install -g netlify-cli
   ```

2. **Login to Netlify**:
   ```bash
   netlify login
   ```

3. **Navigate to project folder** and deploy:
   ```bash
   cd bready-chatbot
   netlify deploy --prod
   ```

4. **Set environment variable** (via Netlify dashboard or CLI):
   ```bash
   netlify env:set ANTHROPIC_API_KEY your_api_key_here
   ```

### Option 3: Manual Deploy via Netlify Dashboard

1. Go to [app.netlify.com](https://app.netlify.com)
2. Click "Add new site" → "Deploy manually"
3. Drag and drop the entire `bready-chatbot` folder
4. Go to **Site Settings** → **Environment Variables**
5. Add `ANTHROPIC_API_KEY` with your Claude API key
6. Trigger a redeploy

## Project Structure

```
bready-chatbot/
├── index.html                    # Main chat interface
├── netlify.toml                  # Netlify configuration
├── netlify/
│   └── functions/
│       └── chat.js              # Serverless function (calls Claude API)
├── data/
│   ├── handbook-chunks.json     # Processed handbook content (1483 chunks)
│   └── search-index.json        # Search index for quick lookup
└── README.md
```

## How It Works

1. **User asks a question** in the chat interface
2. **Keyword search** finds relevant sections from the handbook
3. **Claude API** generates an answer using the relevant context
4. **Response** is displayed in the chat with proper formatting

## Getting Your Claude API Key

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign in or create an account
3. Navigate to "API Keys"
4. Click "Create Key"
5. Copy the key (starts with `sk-ant-`)

**Important**: Keep your API key secret. Never commit it to version control.

## Customization

### Changing the Appearance

Edit the CSS in `index.html` to match your branding. Key variables:

```css
:root {
    --wb-blue: #002244;        /* Primary color */
    --wb-gold: #F4A100;        /* Accent color */
    --bg-light: #f8f9fa;       /* Background */
}
```

### Adjusting the AI Behavior

Modify the `systemPrompt` in `netlify/functions/chat.js` to change how Claude responds.

### Adding More Context

The handbook is split into ~1500 searchable chunks. To update:
1. Replace the PDF
2. Re-run the chunking script
3. Redeploy

## Estimated Costs

- **Netlify**: Free tier includes 125K function requests/month
- **Claude API**: ~$0.003 per 1K input tokens, ~$0.015 per 1K output tokens
- **Typical query**: ~$0.01-0.03 per question

## Troubleshooting

**"API key not configured"**: Make sure `ANTHROPIC_API_KEY` is set in Netlify environment variables and you've redeployed.

**"Failed to process request"**: Check the function logs in Netlify dashboard (Functions → chat → Recent invocations).

**Slow responses**: The first request after inactivity may be slow due to cold starts. Subsequent requests are faster.

## Support

For questions about:
- **B-READY Methodology**: [worldbank.org/b-ready](https://www.worldbank.org/en/programs/business-ready)
- **This Chatbot**: Open an issue on GitHub
- **Claude API**: [docs.anthropic.com](https://docs.anthropic.com)

## License

This chatbot is provided for educational and informational purposes. The B-READY Methodology Handbook content is © World Bank Group.

---

Built with ❤️ for the B-READY team
