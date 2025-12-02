# 🎲 Slack Random Emoji Reactor

A Python Jupyter notebook that fetches available emoji from Slack and adds random emoji reactions to messages, with support for skin-tone modifiers.

## 📸 Bot in Action

![Bot Reaction in Slack](Bot_Reaction_in_Slack.png)

*Example of the bot successfully adding a random emoji reaction to a Slack message*

## 📋 Features

- 🔍 **Fetch Emoji**: Retrieves all available emoji from your Slack workspace
- 🎲 **Random Selection**: Picks random emoji from valid candidates  
- 🎨 **Skin-Tone Support**: Optionally adds skin-tone modifiers to compatible emoji
- ➕ **Add Reactions**: Automatically adds emoji reactions to specified messages
- 🔄 **Retry Logic**: Handles rate limits and transient errors with exponential backoff
- 📊 **Comprehensive Logging**: Detailed output for debugging and monitoring
- 💾 **Debug Files**: Saves emoji data and analysis to JSON files

## 🚀 Quick Start

### Prerequisites

- Python 3.10+ 
- Slack Bot Token with required permissions
- Access to target Slack workspace and channel

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/VikrantSingh01/vik_reaction_sample.git
   cd vik_reaction_sample
   ```

2. **Install dependencies**
   ```bash
   pip install python-dotenv requests jupyter
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the project root:
   ```env
   SLACK_BOT_TOKEN=xoxb-your-bot-token-here
   SLACK_CHANNEL_ID=C1234567890
   SLACK_MESSAGE_TS=1234567890.123456
   ```

4. **Run the notebook**
   ```bash
   jupyter notebook SlackReactionTest.ipynb
   ```

## 🔧 Configuration

### Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `SLACK_BOT_TOKEN` | Your Slack Bot User OAuth Token | `xoxb-1234-5678-abcd` |
| `SLACK_CHANNEL_ID` | Target channel ID | `C02ABCDEFGH` |
| `SLACK_MESSAGE_TS` | Message timestamp to react to | `1697542800.123456` |

### Finding Channel ID and Message Timestamp

1. **Right-click** on any message in Slack
2. Select **"Copy link"** from the context menu
3. Extract from URL: `https://workspace.slack.com/archives/CHANNEL_ID/pTIMESTAMP`
4. Convert timestamp: `p1234567890123456` → `1234567890.123456`

## 🎨 Skin-Tone Support

The notebook includes advanced skin-tone modifier support:

- **Available tones**: `skin-tone-2` through `skin-tone-6` (light to dark)
- **Compatible emoji**: Automatically detects emoji that support skin-tones
- **Format**: `base_emoji::skin-tone-X`
- **Examples**: `+1::skin-tone-3`, `wave::skin-tone-5`

## 📁 Project Structure

```
VS_SLACK_BOTREACTION/
├── SlackReactionTest.ipynb     # Main Jupyter notebook
├── .env                        # Environment configuration
├── emoji_list_raw.json         # Complete API response from emoji.list
├── emoji_candidates.json       # Filtered list of usable emoji names
├── skin_tone_reference.json    # Skin-tone modifier reference guide
└── README.md                   # This file
```

## 🛠 API Permissions

Your Slack bot requires these OAuth scopes:

- **`emoji:read`** - To fetch emoji list from workspace
- **`reactions:write`** - To add emoji reactions to messages

## 📖 Notebook Structure

The Jupyter notebook is organized into clear sections:

1. **📘 Introduction** - Overview and setup requirements
2. **⚙️ Install & Imports** - Dependencies and helper functions
3. **🔐 Load Environment** - Configuration and validation
4. **🧰 HTTP Helpers** - API request functions with retry logic
5. **📥 Fetch Emoji List** - Retrieve and filter emoji from Slack
6. **🎲 Pick Random Emoji** - Select emoji with optional skin-tone support
7. **➕ Add Reaction** - Add emoji reaction to target message
8. **🧪 Try-Again Cell** - Convenience function for multiple attempts
9. **🎨 Skin-Tone Analysis** - Extract and analyze skin-tone data
10. **📝 Notes & Troubleshooting** - Common issues and solutions

## 🚨 Error Handling

The notebook handles common Slack API errors:

| Error | Cause | Solution |
|-------|-------|----------|
| `invalid_name` | Emoji doesn't exist | Check emoji name spelling |
| `already_reacted` | Duplicate reaction | Try different emoji |
| `not_in_channel` | Bot not in channel | Invite bot to channel |
| `missing_scope` | Insufficient permissions | Add required OAuth scopes |
| `rate_limited` | Too many requests | Automatic retry with backoff |

## 🔄 Rate Limiting

- **Automatic retries** on HTTP 429 responses
- **Exponential backoff** for server errors (5xx)
- **Respects `Retry-After`** headers from Slack
- **Maximum retry attempts**: 5 (configurable)

## 🧪 Testing

Run individual notebook cells to test specific functionality:

```python
# Test emoji fetching
emoji_candidates = fetch_emoji_list()

# Test emoji selection with skin-tones
selected_emoji = pick_random_emoji(emoji_candidates, include_skin_tone=True)

# Test reaction adding
add_emoji_reaction(SLACK_CHANNEL_ID, SLACK_MESSAGE_TS, selected_emoji)

# Deleting reaction

```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🆘 Support

- **Issues**: Report bugs or request features via [GitHub Issues](https://github.com/VikrantSingh01/vik_reaction_sample/issues)
- **Documentation**: Full API documentation in the notebook
- **Slack API**: [Official Slack API Documentation](https://api.slack.com/methods)

## 🙏 Acknowledgments

- [Slack API](https://api.slack.com/) for emoji and reactions endpoints
- [python-dotenv](https://github.com/theskumar/python-dotenv) for environment management
- [requests](https://requests.readthedocs.io/) for HTTP client functionality

---

**Made with ❤️ by [VikrantSingh01](https://github.com/VikrantSingh01)**
