# proverbed/actions

Reusable GitHub Actions for proverbed repos.

## Actions

### `notify-deploy`

Sends a Telegram message on production deploy — success or failure.

**Prerequisites (set once at org level):**
- `TELEGRAM_BOT_TOKEN` — from @BotFather
- `TELEGRAM_CHAT_ID` — your personal chat or private channel ID

**Usage — add to the end of any production job:**

```yaml
- uses: proverbed/actions/notify-deploy@main
  if: always()
  with:
    token: ${{ secrets.TELEGRAM_BOT_TOKEN }}
    chat_id: ${{ secrets.TELEGRAM_CHAT_ID }}
    status: ${{ job.status }}
    label: Cloud Functions   # optional — defaults to job name
```

**Inputs:**

| Input | Required | Description |
|-------|----------|-------------|
| `token` | yes | Telegram bot token |
| `chat_id` | yes | Telegram chat/channel ID |
| `status` | yes | Pass `${{ job.status }}` |
| `label` | no | Human-readable deploy label (defaults to job name) |

**Message format:**

```
✅ proverbed/trapify
Deploy: Cloud Functions
Ref: `v1.2.3`
By: dmitrid-zebra
https://github.com/proverbed/trapify/actions/runs/123456
```
