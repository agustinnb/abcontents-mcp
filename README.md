# ABContents MCP server

Let an AI agent make narrated videos. Send a brief, documents (PDF, Word, Excel, PowerPoint, CSV, text, photos)
or a public website, and get back an MP4 with an AI-written script, AI voice, word-by-word captions and music.
Vertical 9:16 for Reels, TikTok and Shorts by default, also 4:5, 1:1 and 16:9. 30 seconds to 5 minutes.
English and Spanish. 30 styles (2D and 3D), including 10 animated explainer looks with characters and drawings; no avatars.

No account and no subscription: an API key is a prepaid wallet. Pay per video, from USD 3.

- Endpoint: `https://abcontents.com/api/mcp` (Streamable HTTP)
- Website: https://abcontents.com
- Agent reference: https://abcontents.com/llms.txt
- Get an API key: https://abcontents.com/api-access

<!-- mcp-name: io.github.agustinnb/abcontents -->

## Tools

| Tool | What it does | Cost |
|---|---|---|
| `list_styles` | The 30 video styles (id, name, 2D/3D) | Free |
| `list_voices` | Narrators for a language, with a sample mp3 each | Free |
| `list_music` | Background music choices with previews | Free |
| `get_quote` | Price in tokens and estimated wait, queue included | Free |
| `get_video` | Status, step, progress, seconds left and the download URL | Free |
| `create_video` | Make a video from a brief, files and/or a website | Tokens from your key |
| `get_balance` | Tokens left on your key | Needs a key |

The free tools work without a key, so an agent can browse styles and quote a video before anyone pays.

## Connect

**Claude Code**

```sh
claude mcp add --transport http abcontents https://abcontents.com/api/mcp \
  --header "Authorization: Bearer YOUR_API_KEY"
```

**Cursor, Windsurf, VS Code and other clients that take a JSON config**

```json
{
  "mcpServers": {
    "abcontents": {
      "url": "https://abcontents.com/api/mcp",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" }
    }
  }
}
```

Leave out the `Authorization` header to use only the free tools.

## Example

> "Make a 60-second vertical video in English from this product sheet, kinetic-type style."

The agent calls `get_quote` (`{"style": "kinetic-type", "duration_seconds": 60}` → 3 tokens, about 3 minutes),
then `create_video` with the file as base64, then polls `get_video` until it returns `downloadUrl`.

## Pricing

1 token = USD 1. A video costs 1 token + 2 tokens per minute (2D styles) or 3 per minute (3D styles), minimum 3.
API packs: 25 tokens USD 25, 100 tokens USD 90, 500 tokens USD 400. Tokens do not expire.
A failed video is retried once and then refunded automatically.

## REST

The same features are available as a plain REST API: see https://abcontents.com/llms.txt.

## About

ABContents is operated by MenuNode LLC. Contact: hola@abcontents.com.
This repository holds the public listing files for the MCP server (the server itself runs at the endpoint above).
