# GetYouTubeTranscript plugin for Claude

Read YouTube from Claude. Paste a video link and ask for a summary, notes, quotes with timestamps or a translation, or ask Claude to find videos on a topic and work through a channel or playlist.

The plugin connects Claude to the [GetYouTubeTranscript](https://getyoutubetranscript.com) remote MCP server and adds two skills that teach Claude when and how to use its tools.

## What's included

| Part | What it does |
| --- | --- |
| MCP server `getyoutubetranscript` | Remote server at `https://getyoutubetranscript.com/api/mcp` with 13 read-only tools: transcripts, caption languages, YouTube search, channel uploads, Shorts, live streams, playlists, community posts, related videos, channel banners, dislike estimates and your credit balance |
| Skill `youtube-transcript` | Fetches a video's transcript and answers from it: summaries, notes, timestamped quotes, translations |
| Skill `youtube-research` | Finds videos and channels, browses channels and playlists, and hands the right videos to the transcript skill |

## Install

In Claude Code, install it straight from this repository:

```
/plugin install getyoutubetranscript --marketplace tubeagentkit/getyoutubetranscript-claude-plugin
```

Or load a local clone for one session:

```
claude --plugin-dir ./getyoutubetranscript-claude-plugin
```

Then sign in: in Claude Code run `/mcp`, pick `getyoutubetranscript` and finish the GetYouTubeTranscript sign-in in your browser (OAuth). No API key is stored in the plugin or in your settings.

## Try it

- "Summarize https://www.youtube.com/watch?v=jNQXAC9IVRw in five bullet points"
- "Find where the speaker talks about pricing in this video and quote it with timestamps: <link>"
- "What has @mkbhd posted about foldable phones this year?"
- "List every video in this playlist and summarize the three most recent: <link>"
- "Translate this video's transcript into Spanish: <link>"

## Pricing

GetYouTubeTranscript is a paid service. New accounts get 100 credits on sign-up, no card needed. Each transcript, search or channel page costs 1 credit, checking your balance costs nothing, and failed calls are never charged. Monthly plans are listed at [getyoutubetranscript.com/pricing](https://getyoutubetranscript.com/pricing).

## What the plugin sends and where

- **To getyoutubetranscript.com:** the video links, video IDs, search queries, channel handles and playlist links that Claude passes to the tools, plus your sign-in token. Nothing else from your conversation or files is sent.
- **What the server does with them:** fetches the public captions, search results and channel pages from YouTube; for dislike counts it queries Return YouTube Dislike; for the `translate` option it machine-translates the captions. Results go back to Claude.
- **What it stores:** usage records for billing (which tool ran, when, and the credit charged) and a cache of public transcripts. See the [privacy policy](https://getyoutubetranscript.com/privacy-policy).

The plugin contains no scripts, hooks or local code. It is two Markdown skills and one MCP server URL.

## Transcripts are untrusted text

A transcript is whatever the video's uploader said or captioned. The skills tell Claude to treat it as data to summarize and quote, never as instructions.

## Support

- Docs: [getyoutubetranscript.com/docs](https://getyoutubetranscript.com/docs)
- Contact: [getyoutubetranscript.com/contact](https://getyoutubetranscript.com/contact)
- Issues: [GitHub issues](https://github.com/tubeagentkit/getyoutubetranscript-claude-plugin/issues)

## License

MIT
