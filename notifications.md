# Notifications

Send CI/CD notifications, files, and formatted messages to **Discord** and **Telegram**.

---

## Discord (`appleboy/discord-action`)
Docker-based (Linux runners). Supports webhook URL or ID+token, custom username/avatar, embed color, and file attachments.

**Key Inputs**: `webhook_url` (or `webhook_id` + `webhook_token`), `message`, `file`, `color`, `username`, `avatar_url`, `debug`

### Custom message
```yaml
- name: Send Discord message
  uses: appleboy/discord-action@v1.2.0
  with:
    webhook_url: ${{ secrets.WEBHOOK_URL }}
    message: The ${{ github.event_name }} event triggered this build.
```

### Custom color, username & file attachment
```yaml
- name: Send Discord message with file
  uses: appleboy/discord-action@v1.2.0
  with:
    webhook_id: ${{ secrets.WEBHOOK_ID }}
    webhook_token: ${{ secrets.WEBHOOK_TOKEN }}
    color: "#48f442"
    username: "GitHub Bot"
    file: "./images/message.png"
    message: "Build artifact attached."
```

---

## Discord (`Ilshidur/action-discord`)
Docker-based (Linux runners). Supports template interpolation (`{{ GITHUB_ACTION }}`, `{{ EVENT_PAYLOAD... }}`), embeds, and allowed mentions via `env`.

**Key Env**: `DISCORD_WEBHOOK` *(required, do not append `/github`)*, `DISCORD_USERNAME`, `DISCORD_AVATAR`, `DISCORD_EMBEDS`, `DISCORD_MENTIONS`

```yaml
- name: Discord notification
  uses: Ilshidur/action-discord@0.4.0
  env:
    DISCORD_WEBHOOK: ${{ secrets.DISCORD_WEBHOOK }}
  with:
    args: 'The project {{ EVENT_PAYLOAD.repository.full_name }} has been deployed.'
```

---

## Telegram (`appleboy/telegram-action`)
Send text, markdown/HTML, photos, documents, audio/video/stickers, or location to one or multiple Telegram chats/channels/forum topics.

**Key Inputs**: `to` *(required, numeric chat ID(s), comma-separated)*, `token` *(required, from `@BotFather`)*, `message`, `message_file`, `message_thread_id`, `format` (`markdown` or `html`), `photo`, `document`, `sticker`, `audio`, `voice`, `video`, `location`, `venue`, `disable_notification`, `socks5`

### Send message
```yaml
- name: Send Telegram message
  uses: appleboy/telegram-action@v1
  with:
    to: ${{ secrets.TELEGRAM_TO }}
    token: ${{ secrets.TELEGRAM_TOKEN }}
    message: |
      ${{ github.actor }} pushed to ${{ github.repository }}
      https://github.com/${{ github.repository }}/commit/${{ github.sha }}
```

### Send photo & document (requires `actions/checkout`)
```yaml
- uses: actions/checkout@v4
- name: Send Telegram photo & doc
  uses: appleboy/telegram-action@v1
  with:
    to: ${{ secrets.TELEGRAM_TO }}
    token: ${{ secrets.TELEGRAM_TOKEN }}
    message: Build outputs
    photo: tests/github.png
    document: tests/gophercolor.png
```

### Send from file or via proxy
```yaml
- name: Send Telegram message from file
  uses: appleboy/telegram-action@v1
  with:
    to: "65382999,-1001234567890"
    token: ${{ secrets.TELEGRAM_TOKEN }}
    message_file: tests/message.txt
    socks5: "socks5://127.0.0.1:1080"
```
