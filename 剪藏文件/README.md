# Batch WeChat Article Reader & Summarizer

This tool allows you to batch read WeChat Official Account articles from a list of URLs, summarize them using DeepSeek, save them as Markdown files, and send a notification via Feishu.

## Setup

1.  **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

2.  **Configuration**:
    *   Copy `.env.example` to `.env`:
        ```bash
        cp .env.example .env
        ```
    *   Edit `.env` and add your API keys:
        *   `DEEPSEEK_API_KEY`: Your DeepSeek API key.
        *   `FEISHU_WEBHOOK_URL`: Your Feishu Webhook URL (optional).

3.  **Add URLs**:
    *   Add WeChat article URLs to `urls.txt`, one per line.

## Usage

Run the script:

```bash
python batch_reader.py
```

## Output

*   **Markdown Files**: Saved in the current directory with the format `YYYY-MM-DD-Title.md`.
*   **Notification**: Sent to Feishu upon completion.
