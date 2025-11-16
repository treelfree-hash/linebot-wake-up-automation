# Line BOT Wake-Up Automation

Automated tool to keep your Line BOT alive using GitHub Actions. Instead of relying on periodic Ping requests, this solution sends real text messages to your bot, ensuring it stays active 24/7 without server interruptions.

## Problem

When hosting a Line BOT on free hosting services, the server often enters sleep mode after a period of inactivity. While periodic Ping requests can help, they may not be sufficient to keep the bot fully active. This solution sends actual text messages to trigger the bot's functionality regularly.

## Solution

This repository uses **GitHub Actions** to run a scheduled workflow that sends real text messages to your Line BOT at regular intervals, keeping it awake and functional.

## Features

- ✨ **No Server Required**: Uses GitHub Actions for free automation
- 📨 **Real Messages**: Sends actual text messages instead of just pings
- ⏰ **Configurable Schedule**: Customize the interval between messages
- 🔐 **Secure**: Uses environment variables to store sensitive credentials
- 🤖 **Easy Setup**: Simple configuration process

## Prerequisites

1. A Line BOT with a Channel Access Token
2. Line Bot's User ID or Group ID (where messages should be sent)
3. GitHub account

## Setup Instructions

### Step 1: Fork or Clone This Repository

```bash
git clone https://github.com/CYENCHUANG/linebot-wake-up-automation.git
cd linebot-wake-up-automation
```

### Step 2: Configure Secrets

Add the following secrets to your GitHub repository:

1. Go to **Settings > Secrets and variables > Actions**
2. Click **New repository secret**
3. Add these secrets:
   - **LINE_CHANNEL_ACCESS_TOKEN**: Your Line Channel Access Token
   - **LINE_USER_ID**: The User ID where messages will be sent (your Line ID)
   - **MESSAGE_CONTENT**: The message to send (default: "Keep alive ping!")

### Step 3: Enable GitHub Actions

1. Go to **Actions** tab
2. Click **I understand my workflows, go ahead and enable them**

### Step 4: Adjust Schedule (Optional)

Edit `.github/workflows/linebot-wakeup.yml` to change the schedule:

```yaml
on:
  schedule:
    - cron: '0 */6 * * *'  # Every 6 hours
```

Common cron expressions:
- `0 */6 * * *` - Every 6 hours
- `0 */4 * * *` - Every 4 hours
- `0 * * * *` - Every hour
- `0 0 * * *` - Daily at midnight

## Configuration

### How to Get Your Line Channel Access Token

1. Go to [Line Developers Console](https://developers.line.biz/)
2. Select your bot channel
3. Go to **Messaging API settings**
4. Copy the **Channel access token**

### How to Get Your Line User ID

1. Add your bot to your Line account
2. Send a message to your bot
3. Your User ID will be displayed in the webhook event

Alternatively, use a temporary webhook handler to capture your ID.

## How It Works

1. GitHub Actions runs the workflow on the specified schedule
2. The workflow uses Line Messaging API to send a message
3. Your bot receives the message and responds (if configured)
4. Server stays active due to regular API calls

## File Structure

```
.
├── .github/
│   └── workflows/
│       └── linebot-wakeup.yml    # Main workflow file
├── README.md
└── config.example.json    # Example configuration
```

## Troubleshooting

### Workflow not running
- Check if GitHub Actions are enabled
- Verify secrets are correctly set
- Check workflow syntax in `.github/workflows/linebot-wakeup.yml`

### Messages not being received
- Verify Line Channel Access Token is correct
- Ensure User ID is correct and bot is added to your account
- Check GitHub Actions logs for error messages

### How to check logs
- Go to **Actions** tab
- Click on the workflow run
- Check the job logs

## Security Note

**Never** commit your Line Channel Access Token or User ID directly to the repository. Always use GitHub Secrets.

## License

MIT License - Feel free to use and modify this project

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Support

If you encounter issues or have suggestions, please open an issue on GitHub.
