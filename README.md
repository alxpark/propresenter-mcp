# propresenter-mcp

A comprehensive Model Context Protocol (MCP) server that provides complete control over ProPresenter presentations via the ProPresenter API. This server implements the full ProPresenter API specification with **231 endpoints** organized into **27 API groups** and exposed through modular client classes.

## Official MCP Registry
- https://registry.modelcontextprotocol.io/?q=alxpark%2Fpropresenter-mcp

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