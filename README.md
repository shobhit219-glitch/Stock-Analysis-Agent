# 📈 AI Stock Analysis Agent

An intelligent n8n automation workflow that analyzes any stock ticker using AI and delivers professional analysis reports directly to your email inbox.

![n8n](https://img.shields.io/badge/n8n-Workflow-FF6D5A?style=for-the-badge&logo=n8n&logoColor=white)
![Google Gemini](https://img.shields.io/badge/Google%20Gemini-AI%20Powered-4285F4?style=for-the-badge&logo=google&logoColor=white)
![Gmail](https://img.shields.io/badge/Gmail-Integration-EA4335?style=for-the-badge&logo=gmail&logoColor=white)

---

## 🎯 Overview

This AI-powered stock analysis agent transforms investment research into a seamless, automated experience. Simply input any stock ticker symbol, and receive a comprehensive analysis covering technical indicators, fundamental metrics, and actionable recommendations — delivered straight to your inbox.

**Perfect for:**
- Financial advisors & analysts
- Investment newsletter operators
- Personal portfolio monitoring
- Retail investors seeking quick insights

---

## ✨ Features

- **🤖 AI-Powered Analysis** — Leverages Google Gemini for intelligent stock evaluation
- **📊 Technical Analysis** — Price trends, support/resistance levels, moving averages, volume signals
- **📈 Fundamental Insights** — P/E ratios, earnings trends, debt metrics, competitive positioning
- **🎯 Clear Recommendations** — BUY / HOLD / SELL actions with confidence levels
- **📧 Automated Email Delivery** — Reports sent directly to specified recipients
- **⚡ Real-Time Processing** — Instant analysis on any stock ticker input

---

## 🏗️ Workflow Architecture

```
┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│                     │     │                     │     │                     │
│   Chat Trigger      │────▶│     AI Agent        │────▶│   Gmail Node        │
│   (User Input)      │     │  (Stock Analysis)   │     │  (Email Delivery)   │
│                     │     │                     │     │                     │
└─────────────────────┘     └──────────┬──────────┘     └─────────────────────┘
                                       │
                                       │
                            ┌──────────▼──────────┐
                            │                     │
                            │   Google Gemini     │
                            │   (LLM Model)       │
                            │                     │
                            └─────────────────────┘
```

---

## 📋 Prerequisites

Before setting up this workflow, ensure you have:

- [n8n](https://n8n.io/) installed (self-hosted or cloud)
- Google Cloud account with Gemini API access
- Gmail account with OAuth2 configured
- Basic understanding of n8n workflows

---

## 🔧 Node Breakdown

| Node | Type | Purpose |
|------|------|---------|
| **When chat message received** | Chat Trigger | Captures user input (stock ticker symbol) |
| **AI Agent** | LangChain Agent | Processes the analysis prompt with user input |
| **Google Gemini Chat Model** | LLM | Powers the AI analysis engine |
| **Send a message** | Gmail | Delivers the formatted report via email |

---

## 🚀 Installation

### Step 1: Import the Workflow

1. Open your n8n instance
2. Navigate to **Workflows** → **Import from File**
3. Upload the `stock-analysis-agent.json` file
4. Click **Import**

### Step 2: Configure Google Gemini API

1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Create a new API key
3. In n8n, click on the **Google Gemini Chat Model** node
4. Add new credentials with your API key

### Step 3: Configure Gmail OAuth2

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create OAuth2 credentials for Gmail API
3. In n8n, click on the **Send a message** node
4. Configure Gmail OAuth2 credentials
5. Update the `sendTo` field with your recipient email

### Step 4: Activate the Workflow

1. Toggle the workflow to **Active**
2. Copy the webhook/chat URL for triggering

---

## 📝 Usage

### Via Chat Interface

1. Open the n8n chat trigger URL
2. Enter a stock ticker symbol (e.g., `AAPL`, `TSLA`, `RELIANCE`)
3. Wait for processing
4. Check your email for the analysis report

### Sample Input

```
AAPL
```

### Sample Output

```
══════════════════════════════════════
STOCK ANALYSIS: AAPL
══════════════════════════════════════

CURRENT CONTEXT:
Apple continues to demonstrate resilience in the tech sector amid 
mixed market conditions, with services revenue showing strong growth.

──────────────────────────────────────
TECHNICAL ANALYSIS:
──────────────────────────────────────
- Price Trend: Bullish
- Support Levels: $178-180
- Resistance Levels: $195-200
- Moving Averages: Trading above 50-day and 200-day MA
- Volume: Moderate with accumulation patterns

──────────────────────────────────────
FUNDAMENTAL HIGHLIGHTS:
──────────────────────────────────────
- Earnings/Revenue: Steady growth in services segment
- P/E Ratio: 28.5 (slightly above industry average)
- Debt Position: Healthy balance sheet with strong cash reserves
- Industry Position: Market leader in premium smartphones
- Recent News: Positive reception for new product launches

──────────────────────────────────────
RECOMMENDATION:
──────────────────────────────────────
Action: HOLD
Confidence: Medium
Price Target: $200
Stop Loss: $175
Time Horizon: Medium-term (3-12 months)

──────────────────────────────────────
KEY RISKS:
──────────────────────────────────────
1. China market exposure and regulatory concerns
2. Smartphone market saturation
3. Currency headwinds affecting international revenue

──────────────────────────────────────
RATIONALE:
──────────────────────────────────────
Apple's strong ecosystem and services growth provide stability, 
but current valuation suggests limited near-term upside. 
Hold for long-term value with services expansion.

══════════════════════════════════════
```

---

## ⚙️ Customization

### Change Email Recipient

In the **Send a message** node, modify the `sendTo` parameter:

```
sendTo: "your-email@example.com"
```

### Modify Analysis Prompt

Edit the prompt in the **AI Agent** node to customize:
- Analysis depth
- Output format
- Specific metrics to include
- Recommendation criteria

### Switch LLM Provider

Replace the Google Gemini node with:
- OpenAI GPT-4
- Anthropic Claude
- Local LLMs via Ollama

---

## 🔒 Security Notes

- **API Keys**: Never commit API keys to version control
- **OAuth Tokens**: Stored securely in n8n credentials
- **Email**: Consider using environment variables for recipient addresses
- **Rate Limits**: Be mindful of API rate limits on Gemini and Gmail

---

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| `\n` showing as text in emails | Use HTML email format or add a Code node to replace `\\n` with `<br>` |
| Gemini API errors | Verify API key and check quota limits |
| Gmail authentication failed | Re-authenticate OAuth2 credentials |
| Empty analysis output | Check if ticker symbol is valid and recognized |

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📬 Contact

For questions or support, please open an issue in this repository.

---

## ⭐ Show Your Support

If this project helped you, give it a ⭐ on GitHub!

---

**Disclaimer:** This tool provides AI-generated analysis for informational purposes only. It does not constitute financial advice. Always conduct your own research and consult with a qualified financial advisor before making investment decisions.
