# MCP Chat

MCP Chat is a command-line interface application that enables interactive chat capabilities with AI models through the Anthropic API. The application supports document retrieval, command-based prompts, and extensible tool integrations via the MCP (Model Context Protocol) architecture.

## Prerequisites

- Python 3.10+
- Anthropic API Key

## Setup

### Step 1: Configure the environment variables

1. Create or edit the `.env` file in the project root and verify that the following variables are set correctly:

```
ANTHROPIC_API_KEY=""  # Enter your Anthropic API secret key
```

### Step 2: Install dependencies

#### Option 1: Setup with uv (Recommended)

[uv](https://github.com/astral-sh/uv) is a fast Python package installer and resolver.

1. Install uv, if not already installed:

```bash
pip install uv
```

2. Create and activate a virtual environment:

On macOS/Linux:

```bash
uv venv
source .venv/bin/activate
```

On Windows PowerShell:

```powershell
uv venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation scripts, allow them for the current terminal session, then activate:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

On Windows Command Prompt:

```bat
uv venv
.\.venv\Scripts\activate.bat
```

3. Install dependencies:

```bash
uv pip install -e .
```

4. Run the project

```bash
uv run main.py
```

#### Option 2: Setup without uv

1. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

2. Install dependencies, and set `USE_UV=0` in the `.env` file:

```bash
pip install "anthropic<1" python-dotenv prompt-toolkit "mcp[cli]>=1.8.0,<2"
```

3. Run the project

```bash
python main.py
```

## Usage

### Basic Interaction

Simply type your message and press Enter to chat with the model.

### Document Retrieval

Use the @ symbol followed by a document ID to include document content in your query:

```
> Tell me about @deposition.md
```

### Commands

Use the / prefix to execute commands defined in the MCP server:

```
> /summarize deposition.md
```

Commands will auto-complete when you press Tab.

## Development

### Adding New Documents

Edit the `mcp_server.py` file to add new documents to the `docs` dictionary.

### Linting and Typing Check

There are no lint or type checks implemented.

## MCP Server Inspector

When building MCP servers, you need a way to test your functionality without connecting to a full application. The Python MCP SDK includes a built-in browser-based inspector that lets you debug and test your server in real-time.

### Starting the MCP Inspector

First, make sure your Python environment is activated. Then run the inspector with:

```bash
mcp dev mcp_server.py
```

This starts a development server and gives you a local URL, typically something like http://127.0.0.1:6274. Open this URL in your browser to access the MCP Inspector.

### Using the MCP Inspector Interface

1. Toggle the button to connect to the MCP server.
2. Once connected, you'd see "Servers", "Tools", "Prompts" and "Resources" tabs at the top the screen.

### Testing Your Tools

Navigate to the "Tools" tab to see all available tools from your server. When you select a tool, the right panel shows its details and input fields.

For example, to test a document reading tool:
1. Select the read_doc_contents tool.
2. Enter a document ID (like "deposition.md").
3. Click "Execute Tool" button.
4. Check the results for success and expected output.

Similarly, you can also test "Prompts" and "Resources" in the MCP Server Inspector.