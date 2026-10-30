---
name: youtube-research
description: Use when the user wants to find YouTube videos or channels on a topic, browse a channel's uploads, playlists, Shorts, live streams or community posts, list the videos in a playlist, or research what a creator or topic covers across several videos. Uses the getyoutubetranscript MCP tools.
---

# YouTube research

Find the right videos first, then read them. This skill finds and lists; the `youtube-transcript` skill reads.

## Tools

Every tool below costs 1 credit per call or page. Paged tools return a `continuation` token: pass it back unchanged to get the next page, and never build one yourself.

| Goal | Tool | Main inputs |
| --- | --- | --- |
| Search YouTube for videos or channels | `search_youtube` | `query`, `search_type` (`video` default, or `channel`) |
| A channel's newest uploads | `get_channel_latest_videos` | `channel` (@handle, URL or UC... id) |
| Search inside one channel | `search_channel_videos` | `channel`, `query` |
| Browse a channel's full uploads | `list_channel_videos` | `channel`, `tab` (`videos`, `shorts`, `streams`), `sort` (`latest`, `popular`, `oldest`) |
| A channel's playlists | `list_channel_playlists` | `channel` |
| A channel's community posts | `list_channel_posts` | `channel` |
| Every video in a playlist | `list_playlist_videos` | `playlist` (URL or id) |
| Videos related to one video | `get_related_videos` | `video_url` |
| Channel banner image | `get_channel_banner` | `channel` |
| Like and dislike estimate for a video | `get_video_dislikes` | `video_url` |
| Credits left (free) | `get_credits` | none |

## How to work

1. Pick the narrowest tool for the request. "What has @channel posted about X" is `search_channel_videos`, not a general search plus filtering.
2. Show the user the list you found (title, channel, date, link) before fetching many transcripts, unless they already asked for the full workflow.
3. Page with `continuation` only as far as the request needs. Say how many pages you read.
4. For "summarize the last N videos" or "what does this playlist cover", fetch transcripts with the `youtube-transcript` skill, checking `get_credits` first for more than about 10 videos.
5. Keep every claim tied to the video it came from, with its link.

## Limits

- Search results and view counts change over time; give the date you looked when it matters.
- `get_video_dislikes` returns estimates from Return YouTube Dislike, because YouTube no longer publishes dislikes. Say they are estimates when you report them.
- If a tool reports the account is out of credits, stop and tell the user. Plans are at https://getyoutubetranscript.com/pricing.
