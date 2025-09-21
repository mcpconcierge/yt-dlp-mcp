# yt-dlp-mcp

An MCP server implementation that integrates with yt-dlp, providing video and audio content download capabilities (e.g. YouTube, Facebook, Tiktok, etc.) for LLMs.

## Features

* **Video Metadata**: Extract comprehensive video information without downloading content
* **Subtitles**: Download subtitles in SRT format for LLMs to read
* **Video Download**: Save videos to your Downloads folder with resolution control
* **Audio Download**: Save audios to your Downloads folder
* **Video Search**: Search for videos on YouTube using keywords
* **Privacy-Focused**: Direct download without tracking
* **MCP Integration**: Works with Dive and other MCP-compatible LLMs

## Installation

### Prerequisites

Install `yt-dlp` based on your operating system:

```bash
# Windows
winget install yt-dlp

# macOS
brew install yt-dlp

# Linux
pip install yt-dlp
```

### With [Dive Desktop](https://github.com/OpenAgentPlatform/Dive)

1. Click "+ Add MCP Server" in Dive Desktop
2. Copy and paste this configuration:

```json
{
  "mcpServers": {
    "yt-dlp": {
      "command": "npx",
      "args": [
        "-y",
        "@kevinwatt/yt-dlp-mcp"
      ]
    }
  }
}
```
3. Click "Save" to install the MCP server

## Tool Documentation

* **search_videos**
  * Search for videos on YouTube using keywords
  * Inputs:
    * `query` (string, required): Search keywords or phrase
    * `maxResults` (number, optional): Maximum number of results to return (1-50, default: 10)

* **list_subtitle_languages**
  * List all available subtitle languages and their formats for a video (including auto-generated captions)
  * Inputs:
    * `url` (string, required): URL of the video

* **download_video_subtitles**
  * Download video subtitles in any available format. Supports both regular and auto-generated subtitles
  * Inputs:
    * `url` (string, required): URL of the video
    * `language` (string, optional): Language code (e.g., 'en', 'zh-Hant', 'ja'). Defaults to 'en'

* **download_video**
  * Download video to user's Downloads folder
  * Inputs:
    * `url` (string, required): URL of the video
    * `resolution` (string, optional): Video resolution ('480p', '720p', '1080p', 'best'). Defaults to '720p'
    * `startTime` (string, optional): Start time for trimming (format: HH:MM:SS[.ms]) - e.g., '00:01:30' or '00:01:30.500'
    * `endTime` (string, optional): End time for trimming (format: HH:MM:SS[.ms]) - e.g., '00:02:45' or '00:02:45.500'

* **download_audio**
  * Download audio in best available quality (usually m4a/mp3 format) to user's Downloads folder
  * Inputs:
    * `url` (string, required): URL of the video

* **download_transcript**
  * Download and clean video subtitles to produce a plain text transcript without timestamps or formatting
  * Inputs:
    * `url` (string, required): URL of the video
    * `language` (string, optional): Language code (e.g., 'en', 'zh-Hant', 'ja'). Defaults to 'en'

* **get_video_metadata**
  * Extract comprehensive video metadata without downloading the content
  * Returns detailed information including title, description, channel, timestamps, view counts, and more
  * Inputs:
    * `url` (string, required): URL of the video
    * `fields` (array, optional): Specific metadata fields to extract (e.g., ['id', 'title', 'description', 'channel']). If not provided, returns all available metadata

* **get_video_metadata_summary**
  * Get a human-readable summary of key video metadata
  * Returns formatted text with title, channel, duration, views, upload date, and description preview
  * Inputs:
    * `url` (string, required): URL of the video

## Usage Examples

Ask your LLM to:
```
"Search for Python tutorial videos"
"Find JavaScript courses and show me the top 5 results"
"Search for machine learning tutorials with 15 results"
"List available subtitles for this video: https://youtube.com/watch?v=..."
"Download a video from facebook: https://facebook.com/..."
"Download Chinese subtitles from this video: https://youtube.com/watch?v=..."
"Download this video in 1080p: https://youtube.com/watch?v=..."
"Download audio from this YouTube video: https://youtube.com/watch?v=..."
"Get a clean transcript of this video: https://youtube.com/watch?v=..."
"Download Spanish transcript from this video: https://youtube.com/watch?v=..."
"Get metadata for this video: https://youtube.com/watch?v=..."
"Show me the title, description, and channel info for this video: https://youtube.com/watch?v=..."
"Get a summary of this video's metadata: https://youtube.com/watch?v=..."
"Extract just the id, title, and view count from this video: https://youtube.com/watch?v=..."
```

## Manual Local Install - Windows

If needed, start the server manually:
```bash
git clone https://github.com/mcpconcierge/yt-dlp-mcp
cd yt-dlp-mcp
npm install
```

### Add to Claude Desktop Config file 
```
C:\Users\{WINDOWS_USER}\AppData\Roaming\Claude\claude_desktop_config.json
```
Open Editor and add following json 
```
{
  "mcpServers": {
    "yt-dlp": {
      "command": "node",
      "args": [
        "C:/path/to/yt-dlp-mcp/lib/index.mjs"
      ],
      "env": {
        "PATH": "C:/path/to/YT-Dlp;%PATH%"
      }
    }
  }
}

```

## Install on Linux or Mac 

make samll change in package.json
Ln:29
replace :
```
"prepare": "tsc --skipLibCheck && npx shx chmod +x ./lib/index.mjs",
```
with 
```
"prepare": "tsc --skipLibCheck && chmod +x ./lib/index.mjs",
``` 

and run 
```
npm install
```

## Requirements

* Node.js 20+
* `yt-dlp` in system PATH
* MCP-compatible LLM service


## Documentation

- [API Reference](./docs/api.md)
- [Configuration](./docs/configuration.md)
- [Error Handling](./docs/error-handling.md)
- [Contributing](./docs/contributing.md)


## License

MIT

## Author

Dewei Yen


