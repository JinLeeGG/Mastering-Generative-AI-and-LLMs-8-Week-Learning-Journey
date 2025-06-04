# Web Summarizer

A Python tool that extracts content from websites and generates AI-powered summaries using the Ollama API with the Llama 3.2 model.

## Features

- Web scraping with proper user-agent headers
- Content extraction and cleaning (removes scripts, styles, images, and form inputs)
- AI-powered summarization using local Ollama instance
- Markdown-formatted output
- Handles websites with anti-bot protection

## Prerequisites

- Python 3.6+
- Ollama installed and running locally on port 11434
- Llama 3.2 model downloaded in Ollama

## Installation

1. Install required Python packages:
```bash
pip install requests beautifulsoup4
```

2. Install and set up Ollama:
   - Download Ollama from [ollama.ai](https://ollama.ai)
   - Pull the Llama 3.2 model:
   ```bash
   ollama pull llama3.2
   ```

3. Ensure Ollama is running:
```bash
ollama serve
```

## Usage

### Basic Usage

```python
from web_summarizer import summarize

# Summarize a website
summarize("https://example.com")
```

### Custom Implementation

```python
from web_summarizer import Website, messages_for
import requests

# Create a Website object
website = Website("https://example.com")

# Access website properties
print(f"Title: {website.title}")
print(f"Content length: {len(website.text)}")

# Generate messages for AI model
messages = messages_for(website)
```

## Configuration

### Ollama Settings
- **API Endpoint**: `http://localhost:11434/api/chat`
- **Model**: `llama3.2`
- **Streaming**: Disabled (set to `False`)

### Customization Options

1. **Change AI Model**: Modify the `MODEL` variable to use different Ollama models
2. **Custom System Prompt**: Edit the `system_prompt` variable to change AI behavior
3. **Different Output Language**: Modify system prompt (e.g., "Respond in markdown in Spanish")

## Code Structure

### Classes

#### `Website`
Represents a webpage with extracted content.

**Attributes:**
- `url`: The original URL
- `title`: Extracted page title
- `text`: Clean text content (scripts, styles, images removed)

### Functions

#### `user_prompt_for(website)`
Generates a user prompt for the AI model based on website content.

#### `messages_for(website)`
Creates the complete message structure for the Ollama API.

#### `summarize(url)`
Main function that processes a URL and returns an AI-generated summary.

## Error Handling

The tool includes basic error handling for:
- Missing page titles (defaults to "No title found")
- Network requests with proper headers to avoid blocking

## Example Output

When summarizing a website, the tool outputs a markdown-formatted summary that includes:
- Brief overview of the website's purpose
- Key content highlights
- News or announcements (if present)
- Navigation-related text is ignored

## Limitations

- Requires local Ollama installation
- Limited to websites that allow scraping
- Content extraction may vary depending on website structure
- Summary quality depends on the underlying AI model

## Contributing

Feel free to submit issues or pull requests to improve the tool's functionality.

## License

This project is open source. Please check the repository for specific license terms.
