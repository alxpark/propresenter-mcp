# propresenter-mcp

A comprehensive Model Context Protocol (MCP) server that provides complete control over ProPresenter presentations via the ProPresenter API. This server implements the full ProPresenter API specification with **231 endpoints** organized into **27 API groups** and exposed through modular client classes.

## Official MCP Registry
- https://registry.modelcontextprotocol.io/?q=alxpark%2Fpropresenter-mcp

## Features

This MCP server provides complete coverage of the ProPresenter API across all major control surfaces:

### 📊 Status & System
- Get ProPresenter version and build information (/version)
- Get/set audience and stage screen status (/v1/status)
- Get layer status information
- Get slide/cue information
- Aggregate status updates from multiple endpoints

### 🎬 Presentation Controls
- **31 endpoints** for complete presentation control
- Get focused/active presentations
- Get current slide index and chord charts
- Focus and trigger presentations
- Navigate through slides (next, previous, by index)
- Timeline operations (play, pause, rewind)
- Group-based triggering
- Thumbnail generation for any slide

### 📢 Announcement Controls
- **9 endpoints** for announcement management
- Get active announcements and slide index
- Focus and trigger announcements
- Navigate through announcement cues
- Timeline operations for announcements

### 🎵 Audio & Media Playlists
- **21 audio endpoints** + **22 media endpoints**
- List and manage playlists
- Get playlist contents with pagination
- Focus playlists (next, previous, specific, active)
- Trigger playlists and individual items
- Real-time playlist updates
- Navigate through playlist items

### 📋 Presentation Playlists
- **30 endpoints** for playlist management
- Complete CRUD operations for playlists
- Focus management (active, focused, next, previous)
- Separate presentation/announcement destinations
- Trigger items by index
- Thumbnail generation
- Real-time playlist change updates

### 📹 Capture Controls
- **4 endpoints** for recording control
- Get capture status and time
- Start/stop capture operations
- Get capture settings
- Get available capture encodings (disk, RTMP, Resi)

### 🧹 Clear Controls
- **9 endpoints** for clearing layers
- Clear specific layers (audio, props, messages, announcements, slide, media, video_input)
- Full CRUD operations for clear groups
- Custom group icons
- Trigger clear groups

### 📚 Library Controls
- **4 endpoints** for library access
- List all configured libraries
- Get library contents
- Trigger presentations from libraries
- Trigger specific cues in library presentations

### 👁️ Looks
- **8 endpoints** for audience screen control
- List all configured looks
- Get/set current live look
- Full CRUD operations for looks
- Trigger looks to make them live

### ⚙️ Macros
- **12 endpoints** for macro automation
- List all configured macros
- Full CRUD for macros and macro collections
- Custom macro icons
- Trigger macros

### 🎭 Props
- **14 endpoints** for prop management
- Full CRUD for props and prop collections
- Trigger and clear props
- Auto-clear timer control (pause/resume)
- Prop thumbnails

### 📱 Stage Displays
- **11 endpoints** for stage screen control
- Show/hide stage messages
- Get/set stage layout maps
- Manage stage screens and layouts
- Layout thumbnails

### 💬 Messages
- **7 endpoints** for message control
- Full CRUD operations for messages
- Show/hide messages with token support
- Clear all messages

### ⏱️ Timers
- **12 endpoints** for timer management
- Full CRUD operations for timers
- Start/stop/reset operations
- Get system time and video countdown
- Increment timer values
- Get all timer states

### 🎨 Themes
- **5 endpoints** for theme management
- List all themes and theme slides
- Get/set theme slide details
- Theme slide thumbnails

### 🎭 Masks
- **3 endpoints** for mask control
- List all configured masks
- Get mask details
- Mask thumbnails

### 🎮 Transport Controls
- **10 endpoints** for media transport
- Play/pause controls for presentation, announcement, and audio layers
- Skip forward/backward by time
- Get/set playback time
- Go to end
- Auto-advance control

### 🔧 Global Groups
- **1 endpoint** for global group management
- List all configured global groups

### 🎯 Trigger Controls
- **6 endpoints** for quick triggering
- Trigger next/previous for audio and media
- Universal next/previous for active content

### 📹 Video Inputs
- **2 endpoints** for video input control
- List video inputs playlist
- Trigger video inputs

Each module follows a consistent three-layer architecture:
- **Clients**: API call wrappers with type-safe methods
- **Tools**: MCP tool definitions with JSON schemas
- **Handlers**: Request processors that map tool calls to client methods

All client modules include comment headers referencing API group numbers for easy cross-reference with `api/api.md`.

## Prerequisites

- Node.js 18 or higher
- ProPresenter 7 with API enabled
- ProPresenter running and accessible on your network

## Installation

1. Clone this repository or download the source code

2. Install dependencies:
```bash
npm install
```

3. Build the project:
```bash
npm run build
```

## Configuration

The server connects to ProPresenter using environment variables:

- `PROPRESENTER_URL` - The URL of your ProPresenter instance (default: `http://localhost:50000`)
- `PROPRESENTER_PASSWORD` - The API password (if configured in ProPresenter)

### ProPresenter Setup

1. Open ProPresenter preferences
2. Go to the Network tab
3. Enable "Network" and note the port number (default: 50000)
4. Optionally set a password for API access

## Usage

### With Claude Desktop

Add this to your Claude Desktop configuration file:

**macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`

**Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "propresenter": {
      "command": "node",
      "args": ["/absolute/path/to/propresenter-mcp/build/index.js"],
      "env": {
        "PROPRESENTER_URL": "http://localhost:50000",
        "PROPRESENTER_PASSWORD": "your-password-if-needed"
      }
    }
  }
}
```

Replace `/absolute/path/to/propresenter-mcp` with the actual path to this project.

### With VS Code

This server can be debugged directly in VS Code using the included MCP configuration.

1. Open this project in VS Code
2. The server is automatically configured for debugging via `.vscode/mcp.json`
3. Use the MCP extension to test and debug the server

## Example Commands

Once connected, you can ask Claude to control ProPresenter:

**Status & Information:**
- "What version of ProPresenter is running?"
- "Show me the status of all screens"
- "What's the status of audience screens?"
- "Get the current slide information"

**Presentations:**
- "What presentation is currently active?"
- "Trigger the presentation with UUID [uuid]"
- "Go to the next slide"
- "Go to slide number 5"
- "Play the presentation timeline"
- "Show me the chord chart"
- "Get a thumbnail of slide 3"

**Announcements:**
- "What announcement is currently active?"
- "Trigger the next announcement cue"
- "Show me the announcement timeline status"
- "Go to announcement cue 2"

**Audio & Media:**
- "List all audio playlists"
- "Show me the contents of audio playlist [id]"
- "Play the next song in the active playlist"
- "Trigger the focused audio playlist"
- "List all media playlists"
- "Trigger media item [id] in playlist [playlist_id]"

**Playlists:**
- "List all presentation playlists"
- "Show me the active playlist"
- "Focus the next playlist"
- "Trigger the first item in the focused playlist"
- "Create a new playlist called 'Sunday Service'"

**Capture:**
- "What's the current capture status?"
- "Start recording"
- "Stop the capture"
- "Show me available capture encodings for RTMP"

**Clear:**
- "Clear the announcements layer"
- "Show me all clear groups"
- "Trigger the clear group [id]"
- "Create a new clear group"

**Library:**
- "List all my libraries"
- "Show presentations in library [id]"
- "Trigger presentation [id] from library [library_id]"

**Looks:**
- "Show me all configured looks"
- "What look is currently live?"
- "Switch to look [id]"
- "Create a new look"

**Macros:**
- "List all macros"
- "Trigger macro [id]"
- "Show me all macro collections"
- "Create a new macro"

**Props:**
- "List all props"
- "Trigger prop [id]"
- "Clear prop [id]"
- "Pause auto-clear for prop [id]"
- "List all prop collections"

**Stage:**
- "Show me the current stage message"
- "Display stage message [message]"
- "Hide the stage message"
- "List all stage layouts"
- "Set stage layout [layout_id] for screen [screen_id]"

**Messages:**
- "Show me all messages"
- "Display message [id]"
- "Hide message [id]"
- "Create a new message"

**Timers:**
- "List all timers"
- "Start timer [id]"
- "Stop timer [id]"
- "Reset the sermon timer"
- "Create a countdown timer"
- "Get the current system time"

**Themes:**
- "List all themes"
- "Show me details of theme [id]"
- "Get theme slide [slide_id] from theme [theme_id]"

**Transport:**
- "Play the presentation layer"
- "Pause the audio layer"
- "Skip forward 30 seconds on the announcement layer"
- "Go to the end of the presentation"
- "Get the current playback time"

**Masks:**
- "List all masks"
- "Show me details of mask [id]"

**Triggers:**
- "Trigger the next cue"
- "Trigger the previous media item"

## Development

### Build
```bash
npm run build
```

### Watch Mode
```bash
npm run watch
```

## API Reference

This server implements the complete ProPresenter API documented at https://openapi.propresenter.com/

### API Coverage

- **Total Endpoints**: 231 REST API endpoints
- **API Groups**: 27 functional groups
- **Client Modules**: 18 TypeScript client classes
- **Tool Definitions**: 18 MCP tool modules
- **Handler Modules**: 18 request handler modules
- **HTTP Methods**: Full support for GET, POST, PUT, DELETE operations
- **Architecture**: Complete three-layer implementation (clients → tools → handlers)

See `api/api.md` for complete API documentation with all 231 endpoints organized by group.

### API Groups Reference

| Group | Path | Client Module | Endpoints |
|-------|------|---------------|-----------|
| 1 | /v1/announcement | AnnouncementClient | 9 |
| 2 | /v1/audio | AudioClient | 21 |
| 3 | /v1/capture | CaptureClient | 4 |
| 4 | /v1/clear | ClearClient | 9 |
| 6 | /v1/group | GlobalGroupsClient | 1 |
| 7 | /v1/library | LibraryClient | 4 |
| 8 | /v1/look | LooksClient | 8 |
| 9-11 | /v1/macro* | MacrosClient | 12 |
| 12 | /v1/mask | MasksClient | 3 |
| 14 | /v1/message | MessagesClient | 7 |
| 15 | /v1/playlist | PlaylistsClient | 30 |
| 16 | /v1/presentation | PresentationClient | 31 |
| 17-19 | /v1/prop* | PropsClient | 14 |
| 20 | /v1/stage | StageClient | 11 |
| 21 | /v1/status | StatusClient | 8 |
| 22 | /v1/theme | ThemesClient | 5 |
| 23 | /v1/timer | TimersClient | 12 |
| 24 | /v1/transport | TransportClient | 10 |
| 27 | /version | StatusClient | 1 |

*Groups 9-11 include /v1/macro, /v1/macro_collection, and /v1/macros  
*Groups 17-19 include /v1/prop, /v1/prop_collection, and /v1/props

## Troubleshooting

**Connection Issues:**
- Verify ProPresenter is running and the API is enabled
- Check that the URL and port are correct
- Ensure no firewall is blocking the connection
- Verify the password if authentication is enabled

**Server Not Starting:**
- Make sure you've built the project with `npm run build`
- Check that Node.js 18+ is installed
- Verify all dependencies are installed with `npm install`

## License

MIT
