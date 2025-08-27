[![Run Tests](https://github.com/pygreece/discord/actions/workflows/test.yml/badge.svg)](https://github.com/pygreece/discord/actions/workflows/test.yml)
[![codecov](https://codecov.io/github/pygreece/discord/graph/badge.svg?token=TRIHAIZE7D)](https://codecov.io/github/pygreece/discord)

# PyGreece Discord Bot 🤖

A Discord bot for the PyGreece online community that handles member onboarding through a Code of Conduct acceptance flow.

## ✨ Features

- 👋 Automatically sends welcome messages to new members
- 📜 Implements a Code of Conduct acceptance workflow
- 🏷️ Assigns roles when members react to the Code of Conduct message
- 🗄️ Tracks member status in a database

## 🔧 Requirements

- 🐍 Python 3.12+
- 🐘 PostgreSQL database (for production)
- 🔑 Discord Bot Token

## 🚀 Setup

### Discord Application

1. Go to the [Discord Developer Portal](https://discord.com/developers/applications)
2. Create a new application
3. Go to the "Bot" tab and create a bot
4. Enable the "Server Members Intent" and "Message Content Intent" under Privileged Gateway Intents
5. Save the bot token for configuration
6. Go to the "Installation" tab and choose the "bot" option on the applications.commands dropdown for Guild Install
7. Select "Manage Channels", "Manage Messages", "Manage Roles", "Manage Threads", "Send Messages", "Send Messages in Threads", from permissions
8. Copy and paste the install link into your browser and invite the bot to your server
9. Ensure the bot role is above the organizers and members roles in the role hierarchy

> This bot is used as a public bot in a Guild Install, private bot mode and user install will need testing

### Environment Configuration

Copy `.env.sample` to a new file called `.env` and update the placeholder values:
   ```dosini
DISCORD_TOKEN=<your-discord-bot-token>
DISCORD_GUILD=<your-discord-server-name>
ORGANIZER_ROLE_NAME=organizers
DATABASE_URL=postgresql+asyncpg://<username>:<password>@postgres/<db>
SPAM_COOLDOWN=<spam-cooldown-time-in-seconds>

MEMBER_ROLE_NAME=members
COC_MESSAGE_LINK=<message-link-of-code-of-conduct>
COC_THREAD_PREFIX=welcome

TICKET_HOLDER_ROLE_NAME=ticketholders
TICKET_MESSAGE_LINK=<message-link-of-ticket-message>
TICKET_THREAD_PREFIX=ticket
BOT_INTERACTIONS_CHANNEL_ID=<bot-interactions-channel-id>
   ```

> Use `compose.yml` to set DB credentials

### Local Development

1. Clone the repository
   ```bash
   git clone https://github.com/pygreece/discord.git
   cd discord
   ```

2. Install dependencies with `uv`
   ```bash
   uv venv
   source .venv/bin/activate  # On Windows use: .venv\Scripts\activate
   uv sync
   ```

### Docker Deployment 🐳

The project includes Docker configuration for easy local deployment:

```bash
docker-compose up -d
```

## 📁 Project Structure

- `bot/`: Main bot code
  - `__main__.py`: Entry point
  - `modals/`: UI input forms
    - `ticket_modal.py`: Ticket verification UI input form
  - `services/`: Database insert logic
    - `ticket_services.py`: Ticket db insert logic
  - `validations/`: Validations checks
    - `ticket_validation.py`: Ticket validation check
  - `views/`: UI views
    - `base_view.py`: Base UI view with boilerplate logic
    - `ticket_view.py`: Ticket validation UI view
  - `config.py`: Configuration handling
  - `db.py`: Database connection management
  - `exceptions.py`: Custom exceptions
  - `messages.py`: Messages sent to members based on interactions
  - `models.py`: Database models
  - `roles.py`: Role related functions
  - `sanitizers.py`: String sanitizers
  - `senders.py`: Sends dms, creates private categories and channels if dms are closed
  - `ticket_cog.py`: Ticket verification system
  - `utility_cog.py`: Administration commands - main cog
  - `utility_tasks.py`: Background tasks
  - `welcome_and_coc_cog.py`: Actions related to new members joining
- `tests/`: Test suite
- `alembic/`: Database migrations

## 🧪 Testing

Run the test suite:

```bash
uv run pytest
```

Run with coverage:

```bash
uv run pytest --cov
```

## 👥 Contributing

1. Fork the repository
2. Create a feature branch
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Make your changes
4. Run tests and make sure they pass ✅
5. Push your branch and create a pull request

## 💬 Code of Conduct

This project follows the [PyGreece code of conduct](https://pygreece.org/code-of-conduct/).
Please be respectful and inclusive when contributing to this project.
