# Slack XBlock for Open edX

An XBlock that integrates Slack channels directly into Open edX courses, enabling seamless communication between course content and discussions.

## Features

- 🚀 Easy integration with existing Slack workspaces
- 🎯 Auto-generated channel names based on course context
- 🎨 Responsive, modern UI design
- ⚙️ Studio-configurable settings
- 📊 Optional analytics and tracking
- 🔧 Flexible channel management

## Installation

### Development

```bash
git clone git@github.com:3N61N33R/slack-xblock.git
cd slack-xblock
pip install -e .
```

### Production

```bash
pip install slack-xblock
```

## Configuration

This XBlock requires setting the Slack variables inside the Open edX common settings.  
The recommended way (when using Tutor) is to create a simple plugin such as `slack-xblock` (or any name you prefer) and set these variables using the Tutor hooks.

Create a plugin file and add the following:

```python
from tutor import hooks

hooks.Filters.ENV_PATCHES.add_items(
    [
        (
            "openedx-common-settings",
            """
INSTALLED_APPS += ['slack_xblock']
FEATURES['ENABLE_SLACK_XBLOCK'] = True

SLACK_BOT_TOKEN = "your-bot-token"
SLACK_SIGNING_SECRET = "your-signing-secret"
AUTO_CREATE_CHANNELS = True
CHANNEL_PREFIX = "course-"            (optional)
CHANNEL_SUFFIX = "-discussion"        (optional)
DEFAULT_WORKSPACE_URL = "https://your-workspace.slack.com"
WORKSPACE_INVITE_URL = "https://your-invite-link"
"""
        )
    ]
)


```
Replace the placeholder values with your actual Slack workspace data.
After enabling the Tutor plugin and rebuilding/restarting LMS and CMS, the Slack XBlock will read these settings from Django.

- SLACK_BOT_TOKEN: Your Slack app's Bot User OAuth Token (starts with xoxb-).

- SLACK_SIGNING_SECRET: The signing secret from your Slack app's "Basic Information" page.

- AUTO_CREATE_CHANNELS: A boolean (True/False) to enable or disable automatic channel creation.

- CHANNEL_PREFIX & CHANNEL_SUFFIX: The prefix and suffix for automatically generated channel names. For example, course- and -discussion would create a channel like course-cs101-discussion.

- DEFAULT_WORKSPACE_URL: The base URL for your Slack workspace.

- WORKSPACE_INVITE_URL: The public invite link for users to join the workspace.

## Open edX Settings

1. Add to Open edX settings:

```python
INSTALLED_APPS += ['slack_xblock']
FEATURES['ENABLE_SLACK_XBLOCK'] = True
```

2. Configure in Studio:

- Add "slack_xblock" inside the advanced settings module lists.
- Add Slack component to course units
- Set workspace URL and channel settings
- Customize display options

## License

---
