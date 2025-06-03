# 🚀 MCP Study Project - Text Processing Tools

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![Gradio](https://img.shields.io/badge/Gradio-Latest-orange.svg)](https://gradio.app)
[![MCP](https://img.shields.io/badge/MCP-Model%20Context%20Protocol-green.svg)](https://modelcontextprotocol.io)

A hands-on exploration of the **Model Context Protocol (MCP)** through interactive text processing tools built with Gradio. This project demonstrates how to create applications that work both as web interfaces and MCP servers.

## 🎯 What is MCP?

The **Model Context Protocol** is a universal standard that enables AI assistants to securely connect to data sources and tools. It allows applications to expose their functionality to AI models in a standardized way, enabling seamless integration and enhanced capabilities.

## ✨ Features

- 🔤 **Letter Counter**: Count occurrences of specific letters in text
- 🌐 **Dual Interface**: Web UI + MCP Server in one application
- 🔧 **Tool Exposure**: Automatically converts Gradio functions to MCP tools
- 📡 **Real-time Communication**: JSON-RPC over HTTP+SSE protocol
- 🎨 **Clean UI**: Modern Gradio interface for easy interaction

## 🏗️ Project Structure

```
 mcp/
├── letter_counter.py    # Main application with Gradio + MCP server
├── agent.json         # Remote MCP agent configuration
├── README.md          # This file
```

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- Node.js (for Playwright MCP if using agent.json)

### Installation

1. **Clone and navigate to the project:**

   ```bash
   cd mcp
   ```
2. **Set up virtual environment:**

   ```bash
   uv venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```
3. **Install dependencies:**

   ```bash
   uv pip install gradio
   ```

### Running the Application

```bash
python letter_counter.py
```

The application will start and provide:

- **Web Interface**: `http://127.0.0.1:7861`
- **MCP Server**: `http://127.0.0.1:7861/gradio_api/mcp/sse`

## 🔧 How It Works

### The Magic of `mcp_server=True`

When you set `mcp_server=True` in the Gradio `launch()` method, several powerful things happen:

```python
demo.launch(mcp_server=True)
```

1. **🔄 Automatic Tool Conversion**: Gradio functions become MCP Tools
2. **📋 Schema Mapping**: Input components map to tool argument schemas
3. **📤 Response Format**: Output components determine the response structure
4. **🌐 Dual Protocol**: Server handles both HTTP requests and MCP protocol messages
5. **🔗 Communication Setup**: JSON-RPC over HTTP+SSE enables real-time client-server interaction

### Example Function as MCP Tool

```python
def letter_counter(word: str, letter: str) -> int:
    """
    Count the number of occurrences of a letter in a word or text.
  
    This function is automatically exposed as an MCP tool!
    """
    return word.lower().count(letter.lower())
```

## 🎮 Usage Examples

### Web Interface

1. Open `http://127.0.0.1:7861` in your browser
2. Enter text in the first textbox
3. Enter the letter you want to count in the second textbox
4. See the count result instantly

### MCP Client Integration

The MCP server endpoint can be integrated with AI assistants and other MCP-compatible clients to provide text processing capabilities programmatically.

## 📁 Configuration Files

### `agent.json` - Tiny-Agents Web Browser Configuration

The `agent.json` file configures a **web-browsing agent** using the `tiny-agents` framework. This demonstrates MCP in action by connecting an AI model to browser automation capabilities:

```json
{
    "model": "Qwen/Qwen2.5-72B-Instruct",
    "provider": "nebius",
    "servers": [
        {
            "type": "stdio",
            "config": {
                "command": "npx",
                "args": ["@playwright/mcp@latest"]
            }
        }
    ]
}
```

**What this configuration does:**

- 🤖 **AI Model**: Uses Qwen/Qwen2.5-72B-Instruct via Nebius inference provider
- 🌐 **Browser Control**: Integrates `@playwright/mcp` server for web automation
- 🔧 **MCP Server**: Playwright MCP server provides browser control tools to the AI
- 📡 **Communication**: Uses stdio for MCP protocol communication

**Running the Web-Browsing Agent:**

```bash
tiny-agents run agent.json
```

**Example Capabilities:**
The agent can perform complex web tasks like:

- Opening new browser tabs
- Performing web searches (e.g., on Brave Search)
- Navigating websites and extracting information
- Interacting with web elements

**Example Prompt:**

```
"Give me  5 user reviews from any top-rated restaurants on TripAdvisor"
```

This showcases how MCP enables AI models to use external tools (browser automation) seamlessly, demonstrating the protocol's power for creating AI agents with real-world capabilities.

## 🔮 Learning Outcomes

This project helps understand:

- **MCP Protocol Basics**: How applications expose functionality to AI models
- **Gradio Integration**: Building dual-purpose applications (UI + Server)
- **Tool Schema Design**: How function signatures become tool specifications
- **Real-time Communication**: JSON-RPC and Server-Sent Events implementation
- **AI Assistant Integration**: Connecting tools to language models

## 📚 Resources

- [Model Context Protocol Documentation](https://modelcontextprotocol.io)
- [Gradio Documentation](https://gradio.app/docs)
- [MCP Specification](https://spec.modelcontextprotocol.io)
